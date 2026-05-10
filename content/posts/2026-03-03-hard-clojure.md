+++
title = "Closing in closure in Clojure"
date = "2026-03-03"
Toc = true
+++

Learning Clojure is a lot of fun. For one, the community is great.[^1]
On top of that, there's many exercises available; that's excellent for people like me, who learn by doing.
For instance, [rich4clojure](https://github.com/PEZ/rich4clojure) is a great resource.
It works out-of-the-box with Visual Studio Code, which is nice when you just want to start working
on problems asap and you'll just "setup the tools later".

Tonight, I'm solving [problem 84](https://github.com/PEZ/rich4clojure/blob/main/src/rich4clojure/hard/problem_084.clj) from that set.
I thought, maybe you'd like to follow along with me. Here it goes:

```clojure
;; Write a function which generates the transitive closure
;; of a binary relation. The relation will be represented
;; as a set of 2 item vectors.
```

As a reminder, the transitive closure of a relation is the smallest transitive relation that contains the original one as a subset.
In other words, if originally @a@ and @b@ are in relation, and @b@ and @c@ are in relation, then @a@ and @c@ are in transitive relation
and the pair @(a,c)@ will appear in the transitive closure.

For instance, if we have a relation @R@ on the set @A=\{\text{cat},\text{man},\text{snake},\text{spider}\}@ given by
@@R = \{(\text{cat},\text{man}), (\text{man},\text{snake}),(\text{spider},\text{cat})\},@@
then its transitive closure would be
@@\overline{R} = R \cup \{(\text{cat},\text{snake}),(\text{spider},\text{man}),(\text{spider},\text{snake})\}.@@

In the given code, we have a test for that (obviously it currently fails since we haven't written any code yet):
```clojure
(tests
 [more-legs
  #{["cat" "man"] ["man" "snake"] ["spider" "cat"]}] :=
 (= (transitive-closure more-legs)
    #{["cat" "man"] ["cat" "snake"] ["man" "snake"]
      ["spider" "cat"] ["spider" "man"] ["spider" "snake"]}))
```

Here the `transitive-closure` function is what we have to write.

In fact, I couldn't make the test work (even before writing any code) because Clojure complains that `more-legs` isn't defined.
I'm not sure how the testing library used in those exercises work, so I just replaced this test (and all the other ones, too) with:
```clojure
(tests
 (= (transitive-closure #{[4 8] [3 9] [2 4] [9 27]}) #{[4 2] [8 4] [8 2] [9 3] [27 9] [27 3]})
 (= (transitive-closure #{["cat" "man"] ["man" "snake"] ["spider" "cat"]})
    #{["cat" "man"] ["cat" "snake"] ["man" "snake"] ["spider" "cat"] ["spider" "man"] ["spider" "snake"]})
 (= (transitive-closure #{["father" "son"] ["uncle" "cousin"] ["son" "grandson"]})
    #{["father" "son"] ["father" "grandson"] ["uncle" "cousin"] ["son" "grandson"]}))
```

## Algorithm: An Idea

The first idea I had is naive (because it's still new), but maybe it'll work.
Suppose we have some set @R \subseteq A^2@, where as above @A@ is the "underlying set" of our relation @R@.
What we're going to do is, set the "first level" @R_1 = R@. Imagine the pairs in @R@ as "atomic paths", or "paths of length 1".
The idea is to make an algorithm that will produce @R_2@, the "paths of length 2", then @R_3@, then @R_4@, ... ad infinitum.
As @n@ tends to infinity, the set @R_n@ should tend to the transitive closure of @R@ (notation @\overline{R}@).
In our case, since @R@ is a finite set, we won't even have to get to infinity: there should exist some natural number @N@ such that @R_N = \overline{R}@.
Hopefully, @N@ is small enough, and computing @R_n@ given @R@ is quick enough.

In any case, the first step should be to convince ourselves that
@@\overline{R} = \bigcup_{n=1}^\infty R_n.@@

**Proof**. To avoid writing that big cup everywhere, let @S = \bigcup_{n=1}^\infty R_n@.
By definition, @S@ contains @R@.
Also, @S@ is a transitive relation on @A@. To see this, suppose that @a S b@ and @b S c@.
Hence, there exists two natural numbers @k,\ell \geq 1@ such that @(a,b)\in R_k@ and @(b,c)\in R_\ell@.
This means there is a "path" of length @k@ from @a@ to @b@ in @A@, and a "path" of length @\ell@ from @b@ to @c@ in @A@.
By "concatenating" those paths, we get a path of length @k+\ell@ from @a@ to @c@ in @A@.
Hence, by defintion @(a,c) \in R_{k+\ell}@, so that @aSc@ as we wanted.

We showed @S@ is a transitive relation which contains @R@. We still need to show it's the smallest.
Let @T \subseteq A^2@ be any other transitive relation on @A@ which contains @R@.
Any @(a,b) \in S@ is proof that there is a path @\pi@ from @a@ to @b@ in @A@, of a certain finite length.
Because @T@ contains @R@, all of the "atomic paths" or "paths of length 1" that make up @\pi@ are contained in @T@.
Since @T@ is transitive, that means there must be an atomic path from @a@ to @b@ in @T@, i.e. @aTb@.
Thus @S \subseteq T@, which shows @S@ is the smallest transitive relation containing @R@, as we wanted. @\blacksquare@

## Algorithm: Implementation

First, let's define a constant that's going to be our relation (let say it's a relation on @\text{String}@):
```clojure
(comment
  (def demo-rel #{["cat" "man"] ["man" "snake"] ["spider" "cat"]})
  ,)
```

By the way, this comma before the last parenthesis in a rich comment is a trick to control autoformatting that I learned in some YouTube video.

Anyways, suppose we already have some @R_n@ and we want to construct @R_{n+1}@.
Given a pair such as `["spider", "man"]` in @R_n@, we'll want to find all atomic paths in @R@ that *begin* with `"man"`.
```clojure
(filter (fn [p] (= "man" (first p))) demo-rel) ;=> (["man" "snake"])

; now package that into a shiny function
(defn find-steps [genset apath]
  (filter (fn [p] (= (second apath) (first p))) genset))

(find-steps demo-rel ["cat" "man"]) ;=> (["man" "snake"])
(find-steps demo-rel ["man" "snake"]) ;=> ()
(find-steps demo-rel ["spider" "cat"]) ;=> (["cat" "man"])
```
What I call `genset` in the code is what've called @R@ in this article.
The function is named `find-steps` because I felt like atomic paths in @R@ are like a "small step" that you take when you've reached the end of the path, to increase it.

Now, we'll "concatenate" those "steps" with the given paths to obtain longer (@n+1@) paths that all start with `"spider"`.
```clojure
(map (fn [p] ["cat" (second p)])
     (find-steps demo-rel ["cat" "man"])) ;=> (["cat" "snake"])

; package into shiney function again
(defn concat-steps [genset apath]
  (map (fn [p] [(first apath) (second p)])
       (find-steps genset apath)))
  
(concat-steps demo-rel ["spider" "cat"]) ;=> (["spider" "man"])
```

As we do that for each element in the finite set @R_n@ and collect the results, we will obtain @R_{n+1}@.
Indeed, any path of length @n+1@ must start with path of length @n@ (i.e. an element of @R_n@), to which is concatenated an atomic path of @R@.
```clojure
(map (fn [p] (concat-steps demo-rel p)) demo-rel) ;=> (() (["cat" "snake"]) (["spider" "man"]))
; previous evaluation: would like to reduce the list,
; interpreting the internal lists as sets to union together
; So:
(map (fn [p] (set (concat-steps demo-rel p))) demo-rel)
;=> (#{} #{["cat" "snake"]} #{["spider" "man"]})
```
Now to get the ability to correctly work with sets, we import `[clojure.set :as set]` in our namespace. Then,
```clojure
(reduce (fn [u s] (set/union u s))
        (map (fn [p] (set (concat-steps demo-rel p))) demo-rel))
;=> #{["spider" "man"] ["cat" "snake"]}
```
We bundle this into a function as before (note that two first evaluations are for the internal forms in the defs):
```clojure
(defn step [genset curset]
  (reduce (fn [u s] (set/union u s))
          (map (fn [p] (set (concat-steps genset p))) curset)))

(def r2 (step demo-rel demo-rel)) ;=> #{["spider" "man"] ["cat" "snake"]}
(def r3 (step demo-rel r2)) ;=> #{["spider" "snake"]}
(step demo-rel r3) ;=> #{}
```
Interestingly, this ends with @R_3@ being the empty set.
I wonder if that always happen for all starting relations @R@, when @R@ is finite...
But let's not get carried away. This is marked here for future investigation; let's finish the algorithm like we planned.

We'll use the lazy list facilities that Clojure provides for us:
```clojure
(take 4 (iterate (fn [curset] (step demo-rel curset)) demo-rel))
;=> (#{["man" "snake"] ["cat" "man"] ["spider" "cat"]} #{["spider" "man"] ["cat" "snake"]} #{["spider" "snake"]} #{})
```
This is essentially (if we remove the top-level `take` call) our infinite tower of @R_n@'s that we called @S@ above.
Let's encapsulate that in a function.
```clojure
(defn tower [genset]
  (reductions (fn [u s] (set/union u s))
              (iterate (fn [curset] (step genset curset)) genset)))
```

We want to reduce the list using union but we want each intermediate result, to detect when the tower stabilize.
The function to use in this case seems to be `reductions`.
```clojure
(take 4 (reductions (fn [u s] (set/union u s))
                    (iterate (fn [curset] (step demo-rel curset)) demo-rel)))
;=> (#{["man" "snake"] ["cat" "man"] ["spider" "cat"]}
;    #{["man" "snake"] ["spider" "man"] ["cat" "man"] ["cat" "snake"] ["spider" "cat"]}
;    #{["man" "snake"] ["spider" "man"] ["cat" "man"] ["cat" "snake"] ["spider" "snake"] ["spider" "cat"]}
;    #{["man" "snake"] ["spider" "man"] ["cat" "man"] ["cat" "snake"] ["spider" "snake"] ["spider" "cat"]})
```
We can see the stabilization phenomenon at work just above. I believe the following function should do the trick.
It expects an infinite list, and as soon as it detects that two consecutive elements in the list have the same value,
it returns that value.
```clojure
(defn zip [l1 l2] (map vector l1 l2))
(take 4 (zip (cons nil (iterate inc 0)) (iterate inc 0)))
;=> ([nil 0] [0 1] [1 2] [2 3])

(defn stabilized [inf-list]
  (let [zipped (zip (cons nil inf-list) inf-list)]
    (first (first (drop-while (fn [p] (not= (first p) (second p))) zipped)))))

(stabilized (tower demo-rel))
;=> #{["man" "snake"] ["spider" "man"] ["cat" "man"] ["cat" "snake"] ["spider" "snake"] ["spider" "cat"]}
```

Hey! That does seem to be what we want. Let's wrap this up in a function and see if it passes the tests.
```clojure
(defn transitive-closure [genset]
  (stabilized (tower genset)))
```

Looks like this is *almost* working...
```clojure
(tests
 (= (transitive-closure #{[4 8] [3 9] [2 4] [9 27]}) #{[4 2] [8 4] [8 2] [9 3] [27 9] [27 3]})
 ;=> false
 (= (transitive-closure #{["cat" "man"] ["man" "snake"] ["spider" "cat"]})
    #{["cat" "man"] ["cat" "snake"] ["man" "snake"] ["spider" "cat"] ["spider" "man"] ["spider" "snake"]})
 ;=> true
 (= (transitive-closure #{["father" "son"] ["uncle" "cousin"] ["son" "grandson"]})
    #{["father" "son"] ["father" "grandson"] ["uncle" "cousin"] ["son" "grandson"]}))
 ;=> true
```

The first case doesn't pass. This is supposed to be a "divides" relation on the natural numbers.
Oh, my, I see the problem. Looks like the problem is actually with the test itself. In the right-hand side
of the equality, I wrote the relation backwards. The smaller number should come first in each vector.
```clojure
(= (transitive-closure #{[4 8] [3 9] [2 4] [9 27]}) #{[2 4] [4 8] [2 8] [3 9] [9 27] [3 27]})
;=> true
```

Now this evaluates to `true`, as it should. Welp, those three tests convince me. We're done here!
I hope you enjoyed my write up of how I think about these problems.
Of course this is a simple problem overall, and I probably solved it once or twice in my early university years and forgotten about it.
Nonetheless, it's a great problem to try and work out some Clojure skills, and work with the REPL!

Here's the full solution, in its 22-lines glory/gory:
```clojure
(defn find-steps [genset apath]
  (filter (fn [p] (= (second apath) (first p))) genset))

(defn concat-steps [genset apath]
  (map (fn [p] [(first apath) (second p)])
       (find-steps genset apath)))

(defn step [genset curset]
  (reduce (fn [u s] (set/union u s))
          (map (fn [p] (set (concat-steps genset p))) curset)))

(defn tower [genset]
  (reductions (fn [u s] (set/union u s))
              (iterate (fn [curset] (step genset curset)) genset)))

(defn zip [l1 l2] (map vector l1 l2))

(defn stabilized [inf-list]
  (let [zipped (zip (cons nil inf-list) inf-list)]
    (first (first (drop-while (fn [p] (not= (first p) (second p))) zipped)))))

(defn transitive-closure [genset]
  (stabilized (tower genset)))
```

Even though this is probably the worst code you've seen today/this week/this millenia, it's quite impressive to think Clojure allows
you to express such a solution in so few lines.

[^1]: Although a bit culty about BDFL Rich Hickey.