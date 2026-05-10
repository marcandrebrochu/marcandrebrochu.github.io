+++
title = "Galois connections"
date = "2025-02-06"
toc = true
+++

Let @X@ and @Y@ be two partially ordered sets (posets). Two functions @f : X \to Y@ and @g : Y \to X@ are said to form a *Galois connection* when the following is true for all @a \in X@ and all @b \in Y@:
\begin{equation*}f(a) \leq b \iff a \leq g(b).\tag{C}\end{equation*}
We say that @f@ is the lower (or left) adjoint, and @g@ is the upper (or right) adjoint. Oftentimes the lower adjoint is marked with a lower-star @f_*@ and the upper adjoint with an upper-star @f^*@. We will see for instance that the direct and inverse image form such a connection, and this hopefully explains the usual notation for these concepts. The shorthand I'm going to use for saying two functions are in Galois connection is @f_* \dashv f^*@.

In some sense, this says @f(a)@ is the best approximation of @a@ from above using objects of @Y@ with respect to @g@, and @g(b)@ is the best approximation of @b@ from below using objects of @X@ with respect to @f@. Don't worry if this is unclear (it is I'm sure).

## Some examples

### Three-way connection: direct image, inverse image, image in fibers

Let @f : X \to Y@ be any set function.
The *direct image* is the function @f_* : 2^X \to 2^Y@ defined as
@@f_*(A) = \{ y \in Y \mid \exists x \in A, f(x) = y \}.@@
The *inverse image* is the function @f^* : 2^Y \to 2^X@ defined as
@@f^*(B) = \{ x \in X \mid f(x) \in B \}.@@
These functions form a Galois connection @f_* \dashv f^*@. The direct image is left adjoint to the inverse image, and reciprocally the inverse image is the right adjoint to the direct image. The use of "the" in the previous sentence will be explained below, where I show that the left or right adjoint, if it exists, is uniquely determined.

Here's a more interesting example! We now construct a *right* adjoint to the inverse image. That's not something you see often! Given a set function @f : X \to Y@, we define the *image in fibers* to be the function @f_! : 2^X \to 2^Y@ with the equation
@@f_!(A) = \{ y \in Y \mid f^{-1}(y) \subseteq A \}.@@
It's the set of points such that their fiber is contained in @A@. It's an interesting construction. Notice for instance that any point that is not in the image of @f@ has an empty fiber, hence is an element of @f_!(A)@. Let's prove that there is a connection @f^* \dashv f_!@. First, suppose @f^*(B) \subseteq A@. In this context we want to show that @B \subseteq f_!(A)@, so pick any element @b \in B@. We just have to show @f^{-1}(b) \subseteq A@, which is the case because our hypothesis says *every* element of @B@ has its preimage contained in @A@, so we're done. Second, suppose @B \subseteq f_!(A)@, and let's show that as a consequence @f^*(B) \subseteq A@. Pick any element @a \in f^*(B)@, so @f(a) \in B@. Hence @f(a) \in f_!(A)@ by hypothesis. This means @f^{-1}(f(a)) \subseteq A@, and since @a@ is an element of @f^{-1}(f(a))@ we are done.

### Linear algebra: span

Let @V@ be some vector space. Given a collection @\mathcal{V}@ of vectors of @V@, their *span* is the smallest vector space which contains all vectors in @\mathcal{V}@. It is denoted by @\langle \mathcal{V} \rangle@. That's a well-defined operation that produces a function @\langle{-}\rangle : 2^V \to \text{Sub}(V)@, where @\text{Sub}(V)@ is the set of subspaces of @V@, partially ordered by inclusion. There's also a "forgetful" function @U@ that goes the other way and produces the set of vectors underlying a given subspace of @V@. These two functions are in Galois connection, with the span being left adjoint to the forgetful function.

### Algebraic geometry: the vanishing set

Here's another example which is close to my heart. Consider @\mathbb{C}[x,y]@ the ring of polynomials in the variables @x@ and @y@, with coefficients in @\mathbb{C}@. Of course we could generalize the base field and the number of variables, but I bet you'll be thankful I'm to lazy to do it. Anyways, for @S \subseteq \mathbb{C}[x,y]@ a set of polynomial, we define their *vanishing set* @V(S)@ to be the subset of points of @\mathbb{C}^2@ where they all vanish:
@@V(S) = \{ (x,y) \in \mathbb{C}^2 \mid \forall p \in S, p(x,y) = 0\}.@@
Reciprocally, given a subset @V \subseteq \mathbb{C}^2@, we define the set @I(V)@ consisting of the polynomials that vanish at all points of @V@:
@@I(V) = \{ p \in \mathbb{C}[x,y] \mid \forall (x,y) \in V, p(x,y) = 0\}.@@
If we order the subsets of @\mathbb{C}[x,y]@ by "reverse containement", we obtain a connection @I \dashv V@, which formally expresses the idea that being "algebraically small" is the same as being "geometrically big", and vice-versa. In other words, the smaller a geometric place is, the more constraints (that's the algebra part) are needed to specify it.

### Closure in topology

Now for a purely topological example. Consider @X@ a topological space, and partially order its closed subsets by containement. Name the set of closed subsets @\mathcal{C}@. The closure is the function that sends any subset @A@ of @X@ to @\overline{A}@, the smallest closed subset that contains @A@. There's also a "forgetful" function @U : \mathcal{C} \to 2^X@ that sends a closed subset to itself. The claim here is that the closure is left adjoint to the forgetful function.

Do you see the similarity between this example and the one about the span in vector spaces? It's this kind of abstract correspondence that a Galois connection expresses.

## More theory

The composite @g\circ f : X \to X@ is called the *closure operator*, and composition the other way around @f \circ g : Y \to Y@ is called the *kernel operator*. A connection is called a *Galois insertion* if the kernel operator is the identity map. Consider the last example where we used the closure of a set in a topological space. Here the closure operator is literally the closure, while the kernel operator is the identity, so we have a Galois insertion. The span example is also a Galois insertion.

Because we always have @g(b) \leq g(b)@, the condition (C) says we always have @f(g(b)) \leq b@ (just set @a = g(b)@). Similarily, we always have @a \leq g(f(a))@. Also notice that if @f@ and @g@ are in connection, then @f@ and @g@ are necessarily monotone. For instance, take @a_1@ and @a_2@ two elements of @X@ with @a_1 \leq a_2@. Then @a_1 \leq a_2 \leq g(f(a_2))@, hence @f(a_1) \leq f(a_2)@. For instance, this gives us for free that the direct and inverse image constructions are monotone, and we always have:

* @A \subseteq f^*(f_*(A))@ for any @A \subseteq X@
* @f_*(f^*(B)) \subseteq B@ for any @B \subseteq Y@

But also:

* @B \subseteq f_!(f^*(B))@ for any @B \subseteq Y@
* @A \subseteq f^*(f_!(A))@ for any @A \subseteq X@
* @\mathcal{V} \subseteq \langle \mathcal{V} \rangle@ for any @\mathcal{V} \subseteq V@ (that's actually part of the definition of the span)
* @Y \subseteq V(I(Y))@ for any @Y \subseteq \mathbb{C}^2@
* @I(V(S)) \subseteq S@ for any @S \subseteq \mathbb{C}[x,y]@

While we're at it, notice what happens if we replace @a@ by @f^*(b)@ in the equation @a \leq f^*(f_*(a))@. (Here @f_*@ and @f^*@ are two general functions in connection, not necessarily the direct/inverse image pair). We get @f^*(b) \leq f^*(f_*(f^*(b)))@, and that's true for every @b \in Y@. On the other hand, it's also true for every @b@ that @f_*(f^*(b)) \leq b@, by what we said above. Because @f^*@ is monotone, we obtain @f^*(f_*(f^*(b))) \leq f^*(b)@. From antisymmetry of our order relation, we conclude
@@f^*(b) = f^*(f_*(f^*(b))).@@
In other words, for every @b \in Y@ the element @f^*(b) \in X@ is a fixed point for the closure operator. Similarily, for every @a \in X@ the element @f_*(a) \in Y@ is a fixed point for the kernel operator.

## Even more theory

If you stare long enough at condition (C) above, after a while you'll understand suddenly and all at once that it is *precisely* the data of two equations. First, it gives a definition of the upper adjoint in terms of the lower adjoint:
@@g(b) = \max\{ a \in X \mid f(a) \leq b \}.@@
Second, it gives a definition of the lower adjoint in terms of the upper adjoint:
@@f(a) = \min\{ b \in Y \mid a \leq g(b) \}.@@

A striking consequence of the previous equations is that two functions in connection mutually define each other. Hence an adjoint to some given function, if it exists, is unique. Another sizeable consequence: if a function @f : X \to Y@ is such that, for some @b \in Y@, the set @\{ a \in X \mid f(a) \leq b\}@ does *not* have a maximum element, then @f@ *cannot* have a right adjoint. A similar remark applies to a function @g : Y \to X@, which would then have no left adjoint if no minimum exists for a given @a \in X@.

When we considered the direct image @f_*@ of a set function @f : X \to Y@, we explicitely built a right adjoint for it: it was the inverse image @f^*@. Now we can give a new characterization of the inverse image in terms of the direct image, using the previous formulas: for any @B \subseteq Y@,
@@f^*(B) = \max\{ A \subseteq X \mid f_*(A) \subseteq B\}.@@
In other words, *the inverse image of a set @B@ is the biggest subset of @X@ such that its image is contained in @B@*. That's really nice. We can also play the same game and characterize the direct image in terms of the inverse image: *the direct image of a set @A@ is the smallest subset of @Y@ such that its inverse image contains @A@*. Hence it seems lower adjoints can be thought of as supremums, approximating from above, while upper adjoints behave as infimums, approximating from below.

Since we have a three-way connection @f_* \dashv f^* \dashv f_!@, one could reasonably ask if it's possible to extend it further. Let's ask the first obvious question: is there a left adjoint to @f_*@? It would necessarily be given, for each @B \subseteq Y@, by the minimum of the set @\{ A \subseteq X \mid B \subseteq f_*(A) \}@. Suppose @f@ is not surjective. Then there is some point @y_0 \in Y@ which is not contained in the image of @f@. For a left adjoint to @f_*@ to be defined, it would have to spit out, when evaluated at @B=\{y_0\}@, the minimum of @\{A \subseteq X \mid y_0 \in f_*(A)\}@, but this set is empty since @y_0@ is not in the image of @f@. Therefore the left adjoint cannot exist when @f@ is not surjective. Well, what if @f@ *is* surjective? After thinking about this for a while, I realized we need another disjunction here. Suppose @f@ is not injective. Take two distincts elements @x_1@ and @x_2@ in @X@ with @y = f(x_1) = f(x_2)@. Set @B = \{y\}@. If a left adjoint to @f_*@ were to exist, it would have to be defined at @B@ as the minimum of the set @\{A \subseteq X \mid y \in f_*(A) \}@. Clearly both @\{x_1\}@ and @\{x_2\}@ are elements of this set; hence, if there was a minimum element, it would have to be contained in both @\{x_1\}@ and @\{x_2\}@, which would make it the empty set. However, the empty set fails to verify @B \subseteq f_*(\varnothing)@. So the left adjoint cannot exist in this case either. Since it trivially exists when @f@ is bijective (it's @f^*@), we conclude: the direct image @f_*@ admits a left adjoint if and only if @f@ is bijective.

The next obvious question on this matter is: does the image in fibers @f_!@ admit a right adjoint? From the previous paragraph our expectations are: if and only if @f@ is bijective. Let's see if that's really the case. In fact, when @f@ is bijective we have @f_! = f_*@, so by unicity of right adjoints we already know that the right adjoint of @f_!@, if it exists, has got to be @f^*@, which it is. So imagine @f@ is not bijective. First case: suppose it is not surjective. Then @f_!(A)@ contains all @y \in Y@ which are not contained in the image of @f@, since their fibers are all empty. Hence by taking @B@ to be any subset of @Y@ completely contained in the image of @f@, we find that the set @\{A \subseteq X \mid f_!(A) \subseteq B\}@ is empty; in particular it has no maximum element, so the right adjoint does not exist. Second case: suppose @f@ is not injective. Without loss of generality we may suppose @f@ is surjective, so that the fiber of any point in @Y@ is never empty. Pick some point @y \in Y@ with at least two distinct preimages and partition @f^{-1}(y)@ into two disjoint non-empty subsets: @f^{-1}(y) = A_1 \cup A_2@. If the right adjoint were to exist, its value at the empty set would have to be the maximum element of the set @\{A \subseteq X \mid f_!(A) = \varnothing\}@. Quick scribling on napkin paper is able to show that both @A_1@ and @A_2@ are contained in this set, but their union is not. Hence it is necessary that @f@ be bijective for @f_!@ to admit a right adjoint.

We have seen that the inverse image is quite special because it is the only one having both a left and a right adjoint in general. This is reflected in the nice properties the inverse image admits, for instance it preserves unions and intersections of subsets. We will see momentarily that this fact is an instance of a general fact about Galois connections (and even more generally about adjunctions).

## When will this theory ever end?

I want to end on the general note that left adjoints preserve joins and right adjoints preserve meets. This is a special case of a more general theorem that left adjoints (in a more general sense) preserve colimits while right adjoints preserve limits.

Suppose @f_* \dashv f^*@ are functions in Galois connection, with @f_* : X \to Y@. Suppose also that @X@ and @Y@ are not only posets but also lattices (i.e. every pair of elements has an infimum and a supremum). Fix @a_1@ and @a_2@ two elements of @X@. Because @f_*@ is necessarily monotone, we must have @f_*(a_1) \leq f_*(a_1 \vee a_2)@ and @f_*(a_2) \leq f_*(a_1 \vee a_2)@. Hence @f_*(a_1 \vee a_2)@ is an upper bound for the pair @f_*(a_1)@, @f_*(a_2)@. Now we show that this is not only an upper bound, it's actually the least upper bound. Let @b@ be any other upper bound, that is, @f_*(a_1) \leq b@ and @f_*(a_2) \leq b@. By the Galois connection condition we must have @a_1 \leq f^*(b)@ and @a_2 \leq f^*(b)@. Then @f^*(b)@ is an upper bound for the pair @a_1@, @a_2@ whence @a_1 \vee a_2 \leq f^*(b)@. But now by the connection condition again, we must have @f_*(a_1 \vee a_2) \leq b@, which is what we wanted. Therefore @f_*(a_1 \vee a_2) = f_*(a_1) \vee f_*(a_2)@. A dual argument shows that @f^*(b_1 \wedge b_2) = f^*(b_1) \wedge f^*(b_2)@ for any pair of elements @b_1@, @b_2@ in @Y@.

Let's return to our example of three-way connection between the direct image, the inverse image and the image in fibers for any set function @f : X \to Y@. What we can conclude from the previous paragraph is: the inverse image is very special, for it preserves both unions and intersections, being a right and left adjoint at the same time. The direct image only preserves unions in general, while the image in fibers only preserves intersections.