+++
title = "The dominance order on partitions"
date = "2025-02-08T00:00:01"
+++

*TODO: Fix Young diagrams as they just don't show up right now!*

Recall that a *partition* @\lambda@ of some fixed natural number @n \geq 0@ is a list of nonnegative integers @(\lambda_1,\lambda_2,\dots)@ such that @\lambda_1 \geq \lambda_2 \geq \dots \geq 0@ and such that @\lambda_1+\lambda_2+\dots = n@. For the purposes of this post, the actual number of parts in a partition is irrelevant, and since one can always extend a partition with zeroes we may suppose that all partitions have the same fixed number of parts, let's say @\ell@.

We put a relation on the set of all partitions of @n@ by declaring @\lambda \preceq \mu@ if and only if @\lambda_1 \leq \mu_1@, @\lambda_1 + \lambda_2 \leq \mu_1 + \mu_2@, and so on. In other words, for every integer @k@ ranging from @1@ to @\ell@, the sum of the first @k@ parts of @\lambda@ must not be greater than the sum of the first @k@ parts of @\mu@. Let's prove that this is a partial order: it must be reflexive, transitive and antisymmetric.

* Reflexive: this one's pretty easy.
* Transitive: also easy. Suppose @\lambda \preceq \mu@ and @\mu \preceq \nu@. That means for each @k \in \{1,2,\dots, \ell\}@, we have @\sum_{i=1}^k \lambda_i \leq \sum_{i=1}^k \mu_i@ and @\sum_{i=1}^k \lambda_i \leq \sum_{i=1}^k \nu_i@. We conclude by transitivity of the usual order @\leq@.
* Antisymmetric: suppose @\lambda \preceq \mu@ and @\mu \preceq \lambda@. The definition of @\preceq@ says that, in particular at @k=1@, we have @\lambda_1 \leq \mu_1@ and @\mu_1 \leq \lambda_1@, whence @\lambda_1 = \mu_1@ from the antisymmetry of @\leq@. Then at @k=2@ we have @\lambda_1 + \lambda_2 \leq \mu_1 + \mu_2@ and @\mu_1 + \mu_2 \leq \lambda_1 + \lambda_2@, whence @\lambda_2 = \mu_2@ by antisymmetry of @\leq@ and substitution. We can continue in this way (a more rigorous approach would be a proof by induction but I don't care enough to do it).

This order @\preceq@ on the set of partitions of @n@ is called the *dominance order* (French: *ordre de dominance*). When @n \geq 6@, this order has incomparable elements; in fact it's a linear order if and only if @n \leq 5@. For instance, temporarily suppose @n=6@ and pick @\lambda = (3,1,1,1)@ and @\mu = (2,2,2)@. Since @3 \not\leq 2@ we immediately find @\lambda \not\preceq \mu@. On the other hand, @2+2+2@ fails to be smaller than @3+1+1@, so @\mu \not\preceq \lambda@. Hence these two elements are incomparable in this order.

Recall that any partition @\lambda@ represents a Young diagram. For instance, @(3,2,2,1,1,1)@ is a partition of @10@ that may be drawn as
<div style="display:flex;align-items:center;width:100%;margin-bottom:16px;">
<svg style="display:bock;margin:0 auto;" height="163px" version="1.1" viewBox="-.500002 -122.082337 389.542968 122.582339" width="620pxpx">
<g>
<rect fill="currentColor" height="18.027125" width=".468154" x="167.031545" y="-108.396826"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="185.05867" y="-108.396826"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="167.031545" y="-108.630903"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="167.031545" y="-90.603778"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="167.031545" y="-90.369701"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="185.05867" y="-90.369701"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="167.031545" y="-90.603778"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="167.031545" y="-72.576653"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="167.031545" y="-72.342576"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="185.05867" y="-72.342576"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="167.031545" y="-72.576653"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="167.031545" y="-54.549529"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="167.031545" y="-54.315452"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="185.05867" y="-54.315452"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="167.031545" y="-54.549529"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="167.031545" y="-36.522404"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="185.05867" y="-54.315452"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="203.085795" y="-54.315452"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="185.05867" y="-54.549529"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="185.05867" y="-36.522404"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="167.031545" y="-36.288327"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="185.05867" y="-36.288327"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="167.031545" y="-36.522404"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="167.031545" y="-18.495279"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="185.05867" y="-36.288327"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="203.085795" y="-36.288327"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="185.05867" y="-36.522404"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="185.05867" y="-18.495279"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="167.031545" y="-18.261202"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="185.05867" y="-18.261202"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="167.031545" y="-18.495279"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="167.031545" y="-.468154"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="185.05867" y="-18.261202"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="203.085795" y="-18.261202"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="185.05867" y="-18.495279"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="185.05867" y="-.468154"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="203.085795" y="-18.261202"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="221.112919" y="-18.261202"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="203.085795" y="-18.495279"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="203.085795" y="-.468154"></rect>
</g>
</svg>
</div>

The *conjugate* of a partition @\lambda@, written @\lambda^*@, is another partition of @n@ obtained by flipping the Young diagram about its antidiagonal. For our previous example, that would be
<div style="display:flex;align-items:center;width:100%;">
<svg style="display:bock;margin:0 auto;" height="91px" version="1.1" viewBox="-.500002 -68.000963 389.542968 68.500964" width="620px">
<g>
<rect fill="currentColor" height="18.027125" width=".468154" x="139.990858" y="-54.315452"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="158.017982" y="-54.315452"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="139.990858" y="-54.549529"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="139.990858" y="-36.522404"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="139.990858" y="-36.288327"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="158.017982" y="-36.288327"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="139.990858" y="-36.522404"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="139.990858" y="-18.495279"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="158.017982" y="-36.288327"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="176.045107" y="-36.288327"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="158.017982" y="-36.522404"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="158.017982" y="-18.495279"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="176.045107" y="-36.288327"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="194.072232" y="-36.288327"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="176.045107" y="-36.522404"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="176.045107" y="-18.495279"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="139.990858" y="-18.261202"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="158.017982" y="-18.261202"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="139.990858" y="-18.495279"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="139.990858" y="-.468154"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="158.017982" y="-18.261202"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="176.045107" y="-18.261202"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="158.017982" y="-18.495279"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="158.017982" y="-.468154"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="176.045107" y="-18.261202"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="194.072232" y="-18.261202"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="176.045107" y="-18.495279"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="176.045107" y="-.468154"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="194.072232" y="-18.261202"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="212.099357" y="-18.261202"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="194.072232" y="-18.495279"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="194.072232" y="-.468154"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="212.099357" y="-18.261202"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="230.126482" y="-18.261202"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="212.099357" y="-18.495279"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="212.099357" y="-.468154"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="230.126482" y="-18.261202"></rect>
<rect fill="currentColor" height="18.027125" width=".468154" x="248.153607" y="-18.261202"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="230.126482" y="-18.495279"></rect>
<rect fill="currentColor" height=".468154" width="18.495279" x="230.126482" y="-.468154"></rect>
</g>
</svg>
</div>

written textually as @(6,3,1)@.

**TODO** Show that conjugation is an antiautomorphism.

## A new way of seeing things

All these sums are annoying sometimes, so here's an alternative way to see this construction. To any partition @\lambda@ we associate the list @\Sigma \lambda@ defined as
@@\Sigma\lambda = (0,\lambda_1,\lambda_1+\lambda_2,\lambda_1+\lambda_2+\lambda_3,\dots).@@
We call this list the *associated list*. It has length @\ell+1@ and is always (weakly) increasing. Moreover, the last term in the list is always @n@ and the first is always @0@. Finally, the associated list is *concave*: for any @i \in \{2,3,\dots,\ell\}@, we have
@@2(\Sigma\lambda)_i \geq (\Sigma\lambda)_{i-1} + (\Sigma\lambda)_{i+1}.@@
This fact can be proven by noticing @2\lambda_i \geq \lambda_{i}+\lambda_{i+1}@ (easy to see or prove by induction); then
\begin{align*}
(\Sigma\lambda)_{i-1}+(\Sigma\lambda)_{i+1} &= 2(\Sigma\lambda)_{i-1}+\lambda_i+\lambda_{i+1}\\
&\leq 2(\Sigma\lambda)_{i-1}+2\lambda_i\\
&= 2(\Sigma\lambda)_i.
\end{align*}

Having any list @f@ of @\ell+1@ elements with the above three properties (starts with @0@ and ends with @n@, weakly increasing, concave), we can produce another list having @\ell@ elements using the difference operator @\Delta@ defined as
@@\Delta f = (f_2-f_1, f_3-f_2, \dots).@@
Because of concavity, the list @\Delta f@ is weakly decreasing:
@@f_i - f_{i-1} - (f_{i+1} - f_i) = 2 f_i - f_{i-1} - f_{i+1} \geq 0.@@
Also, the list @\Delta f@ only contains nonnegative integers since @f@ is weakly increasing. Finally, the sum of all elements in @\Delta f@ is precisely @n@ because the sum telescopes to be @f_\ell-f_1@, which is @n-0@ by the first property. In other words, @\Delta f@ is actually a partition of @n@. It's not hard to show the operators @\Sigma@ and @\Delta@ are mutual inverses:

> The associated list operator @\Sigma@ furnishes a bijection between the partitions of @n@ and the lists of @\ell+1@ integers which: (i) start with @0@ and end with @n@; (ii) are weakly increasing; and (iii) are concave. The inverse of @\Sigma@ is the difference operator @\Delta@.

Back to order. From the definition of @\Sigma@, we see that @\lambda \preceq \mu@ if and only if @\Sigma\lambda \leq \Sigma\mu@, with the obvious partial order that compares lists "element by element". Therefore @\Sigma@ is an order isomorphism.

Write @A@ for that set of lists which are concave, etc., with which the set of partitions of @n@ is in bijection. For any two @f,g \in A@, set @h@ to be the list defined by: @h_i@ is the minimum between @f_i@ and @g_i@. This list is still weakly increasing, its first element is still @0@ and its last element is still @n@. Moreover, @h_i@ is also concave, so @h \in A@. Because the order on @A@ is comparision element by element, this @h@ is actually the minimum (in the order theory sense) of @f@ and @g@: we can write @f \wedge g = h@. Because @\Sigma@ is an order isomorphism, this gives us a formula for the infimum of two partitions of @n@ in the order @\preceq@:
@@\lambda \wedge \mu = \Delta(\Sigma \lambda \wedge \Sigma \mu).@@
For instance, take @(3,1,1,1)@ and @(2,2,2)@. Recall that these elements are not comparable. We have @\Sigma(3,1,1,1) = (0,3,4,5,6)@ and @\Sigma(2,2,2) = (0,2,4,6)@. Now we compute the minimum in @A@ by taking the minimum componentwise: it's @(0,2,4,5,6)@. Using the difference operator @\Delta@ to move back into partitions of @n@, we obtain
@@(3,1,1,1) \wedge (2,2,2) = (2,2,1,1).@@

We don't have such an easy time applying the same idea to get a supremum, because the maximum componentwise of two lists in @A@ is not necessarily another list in @A@. Indeed, it may not be concave: take for instance the componentwise maximum of @(0,3,4,5,6)@ and @(0,2,4,6,6)@, which is @(0,3,4,6,6)@, and that's not concave at @4@. However we can use the fact that the conjugation is an antiautomorphism, that is, an order isomorphism which reverses the order. Anytime we have something like that, the supremum corresponds to the infimum in the image by the antiautomorphism, so we can set:
@@\lambda \vee \mu = (\lambda^* \wedge \mu^*)^*.@@

As an example, let's compute the supremum of @(3,1,1,1)@ and @(2,2,2)@. We start by computing their conjugates: @(3,1,1,1)^* = (4,1,1)@ and @(2,2,2)^* = (3,3)@. Now to find the infimum of the conjugates, we move into @A@ using the @\Sigma@ operator: @\Sigma(4,1,1) = (0,4,5,6)@ and @\Sigma(3,3) = (0,3,6,6)@. As discussed before, their minimum in @A@ is given by the componentwise minimum, which is @(0,3,5,6)@. We move back into partitions of @n@ using the difference operator, which gives us @(3,2,1)@. Finally we should take the conjugate of this, but in this particular case @(3,2,1)@ is autodual. Hence
@@(3,1,1,1)\vee (2,2,2) = (3,2,1).@@

This shows that the set of partitions of @n@ is not only a partial order, but also a lattice, under the dominance order @\preceq@.

