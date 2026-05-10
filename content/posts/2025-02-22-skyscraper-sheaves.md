+++
title = "Skyscraper sheaves"
date = "2025-02-22T00:00:00"
+++

Let @X@ be a topological space, let @p@ be a point of @X@, and let @S@ be any set. In the notation of Vakil, define the **skyscraper sheaf** supported at @p@ by the formula
@@
(i_{p,*}S)(U) =
\begin{cases}
S & \text{if $p \in U$;} \\
1 & \text{otherwise.}
\end{cases}
@@
Here @1@ is the singleton set. We can also define such a sheaf in other categories (abelian groups, rings, etc.), replacing the singleton set by the appropriate terminal object.

If @V \subseteq U@ is a containement of open sets, then the restriction @\rho_{U,V}@ is given as follows:

 * if @p \in V@, then @\rho_{U,V}@ is the identity on @S@;
 * otherwise, @\rho_{U,V}@ is the unique map to @1@.
 
For @W \subseteq V \subseteq U@, we have @\rho_{U,W} = \rho_{V,W} \circ \rho_{U,V}@, because if @p \notin W@ both sides are the unique map to @1@, and otherwise both sides are the identity map on @S@. Therefore we have a presheaf of sets on @X@ (and this could also be a presheaf of other objects as well, as long as there is a terminal object).

Suppose @\{U_i\}_{i \in I}@ is an open cover of some open set @U@ in @X@, and suppose @\{s_i \in (i_{p,*}S)(U_i)\}_{i \in I}@ is a collection of sections such that, for any @i,j \in I@, we have @s_i|_{U_i \cap U_j} = s_j|_{U_i \cap U_j}@. If @p \notin U@, then the unique element of @(i_{p,*}S)(U)@ is evidently the unique gluing of the sections. If @p \in U@, then there is some @i_0 \in I@ such that @p \in U_i@; let @s=s_{i_0}@ be the gluing of the sections. Because restriction to @U_{i_0}@ is the identity, the gluing is clearly unique. We want to show that for any @i \in I@, we have @s|_{U_i} = s_i@. If @p \notin U_i@, then it's obviously true. If @p \in U_i@, then @p \in U_i \cap U_{i_0}@, and since @s_i|_{U_i \cap U_{i_0}} = s_{i_0}|_{U_i \cap U_{i_0}}@ with these restrictions being the identity, we find @s_i = s_{i_0} = s = s|_{U_i}@, as required. This was a lot of words to say a simple thing: we have a sheaf.

The "skyscraper" in the name is explained by the following fact:

> The stalk of @i_{p,*}S@ at a point @q \in X@ is @S@ if @q@ is in the closure of @p@, and is the singleton set @1@ otherwise.

That's not very hard to show. Suppose that @q@ is not in the closure of @p@. Then there exists some open set around @q@ that does not contain @p@. Hence any germ in the stalk at @q@ can be represented by an element in the singleton set @1@, which means all germs are equal and the stalk may be identified with @1@. On the other hand, suppose that @q@ is in the closure of @p@. This means all open sets which contain @q@ *also* contain @p@. The stalk is a colimit, and now we're saying it's a colimit over a constant diagram (every object in the diagram is @S@). Therefore, the colimit is @S@.

Note that we can argue more abstractly for the first case, when @q@ is not in the closure, in a way that shows the stalk is the terminal object @1@ in other categories (abelian groups, rings, etc). The stalk is a direct limit which is computed over the directed set of all opens containing @p@, ordered by reverse inclusion. Recall that a directed set is a poset @(A, \leq)@ in which every pair of elements has an upper bound. A subset @(B,\leq)@ of a poset is said to be **cofinal** in @A@ if, for every @a \in A@, it is possible to find some @b \in B@ such that @a \leq b@. For instance, when @q@ is not contained in the closure of @p@, the set of open neighborhoods of @q@ that do not contain @p@ is cofinal in the directed set of all open neighborhoods of @q@, ordered by reverse inclusion. Note that any cofinal set in a directed set is also directed. One can show that the direct limit computed over a directed set is equal (or more precisely, isomorphic up to a unique canonical isomorphism) to the direct limit computed over the "smaller" cofinal set. In our example, this means the stalk at @q@ is @1@ in any category with such a terminal object, because the direct limit can be computed over the cofinal set of neighborhoods not containing @p@, and that's a constant diagram with all objects equal to @1@.

From the previous discussion, skyscraper sheaves look like a skyscraper towering above a point, and this mental picture is accurate when the point @p@ is closed. When a point is not closed (such a situation happens frequently in algebraic geometry), there are some points "nearby" over which the stalk is also @S@, so it looks like a city's downtown more than a single skyscraper.

## What About the Weird Notation?

The notation @i_{p,*}S@ is weird, but it makes sense in light of the following construction. Let @f : X \to Y@ be a (continuous) map of topological spaces, and let @\mathscr{F}@ be a sheaf on @X@. We define the **pushforward** of @\mathscr{F}@ along @f@ to be the sheaf defined by the equation
@@(f_*\mathscr{F})(U) = \mathscr{F}(f^*U),@@
where @f^*@ denotes the inverse image (or preimage) of @f@ (it's more often written as @f^{-1}@ but I prefer the notation with a star). Because @f@ is continuous, the inverse image of an open set is an open set, so the previous equation makes sense. Given @V \subseteq U@ an inclusion of open sets in @Y@, the restriction from @U@ to @V@ is defined by the equation
@@\rho_{U,V}^{f_*\mathscr{F}} = \rho_{f^*U, f^*V}^{\mathscr{F}}.@@
This defines a presheaf, simply because @\mathscr{F}@ itself is a presheaf: clearly the restriction from an open set to itself is the identity, and
@@
\begin{align*}
\rho_{V,W}^{f_*\mathscr{F}} \circ \rho_{U,V}^{f_*\mathscr{F}} &= \rho_{f^*V,f^*W}^{\mathscr{F}} \circ \rho_{f^*U,f^*V}^{\mathscr{F}} \\
&= \rho_{f^*U,f^*W}^{\mathscr{F}} \\
&= \rho_{U,W}^{f_*\mathscr{F}}.
\end{align*}
@@

The fact @\mathscr{F}@ is a sheaf is also sufficient to make its pushforward a sheaf as well. Suppose @U@ is an open set in @Y@, and @\{U_i\}_{i \in I}@ is an open cover of @U@. For each @i \in I@, let @s_i \in f_*\mathscr{F}(U_i)@ and suppose further that, for any @i, j \in I@, we have @s_i|_{U_i \cap U_j} = s_j|_{U_i \cap U_j}@. We want to show the existence of a unique section @s \in f_*\mathscr{F}(U)@ such that @s|_{U_i} = s_i@ for each @i \in I@. Each section @s_i@ is an element of @\mathscr{F}(f^*U_i)@, and the fact these sections all agree on overlaps @U_i \cap U_j@ together with the fact @f^*(U_i \cap U_j) = f^*U_i \cap f^*U_j@ means there exists a unique @s \in \mathscr{F}(f^*U)@ with the desired property. Notice that a key part of why the pushforward is a sheaf, is the fact the inverse image preserves both arbitrary unions and intersections (union is because we need the collection @\{f^*U_i\}_{i \in I}@ to be an open cover of @f^*U@).

To make sense of the notation for skyscraper sheaves, we also need to talk about the **constant sheaf**. Let @S@ be any set. The constant sheaf associated to @S@, denoted @\underline{S}@, is defined by labeling each open set @U@ with the set of functions @U \to S@ that are locally constant (i.e. around each point of @U@ there exists some open set contained in @U@ on which the function is constant -- this is the same as requiring the function to be constant on connected components of @U@). Restriction is the usual restriction of maps, which obviously respects the presheaf condition. The sheaf axiom is not hard to check either.

Back to skyscrapers. Let @i_p : 1 \to X@ be the "inclusion map" which points to @p \in X@. We consider @\underline{S}@ as a sheaf over the topological space @1@. Let @U@ be an open set in @X@. If @p \in U@, then @i_p^*U@ is the unique point of @1@, while on the other hand if @p \notin U@ then @i_p^*U@ is the empty set. Hence we see the pushforward @i_{p,*}\underline{S}@ of the constant sheaf @\underline{S}@ is isomorphic in some obvious sense to the skyscraper sheaf @i_{p,*}S@ as defined earlier.