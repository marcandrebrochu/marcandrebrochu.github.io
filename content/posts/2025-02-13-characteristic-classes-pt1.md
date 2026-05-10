+++
title = "Characteristic classes (Part 1, Cohomology)"
date = "2025-02-13"
toc = true
+++

*TODO: I need to fix the commutative diagrams in this post because they just don't show up right now.*

I'm planning on writing a series of posts that explore the theory and applications of characteristic classes in algebraic topology, following the book from Milnor and Stasheff. Here I start with the appendix A, where homology is discussed and basic theorems are laid out. This post will also serve me well as a quick reminder, since I keep forgetting small details and ideas regarding (singular) (co)homology. Many results and explanations can be found in Hatcher's book.

## Singular homology

The **standard @n@-simplex** is the set @\Delta^n \subseteq \mathbb{R}^{n+1}@ consisting of all @(n+1)@-tuples @(t_0,t_1,\dots,t_n)@ with the following two properties:

* for each @i@, we have @t_i \geq 0@;
* and @\sum t_i = 1@.

The second property says that points in @\Delta^n@ are such that the dot product of the vector @(t_0-1,t_1,\dots,t_n)@ with the vector @n=(1,1,\dots,1)@ is zero, i.e. @\Delta^n@ lies in the @n@-hyperplane with normal @n@, translated by one unit in any direction. Hence each @\Delta^n@ is an affine space of dimension @n@. For instance:

* @\Delta^0@ is a single point @1 \in \mathbb{R}@;
* @\Delta^1@ is the line segment in @\mathbb{R}^2@ going up from @(1,0)@ to @(0,1)@;
* @\Delta^2@ is the (filled) triangle in @\mathbb{R}^3@ having as vertices the three standard basis vectors;
* etc.

As a special case, we also define @\Delta^{-1}@ to be the empty set.

In general each @\Delta^n@ has @(n+1)@ **vertices**, which are the points in @\Delta^n@ corresponding to the standard basis vectors. Another way to talk about the standard @n@-simplex is to say it is the *convex hull* of the standard basis vectors in @\mathbb{R}^{n+1}@. We can label each vertex with an integer @i@, where @i@ is the (zero-based) position of the unique @1@ in the standard basis vector corresponding to that vertex.

For each @0 \leq i \leq n@, we have a way to talk about the **@i@-th side** of a standard @n@-simplex via the function @\phi_i : \Delta^{n-1} \to\Delta^n@, which is defined as
@@\phi_i(t_0,\dots, \widehat{t_i},\dots,t_n) = (t_0,\dots,t_{i-1},0,t_{i+1},\dots,t_n).@@
(As usual the hat over a variable in an enumeration means that variable is actually omitted from the enumeration.) Thus the @i@-th side is the convex hull of all vertices of @\Delta^n@ that are not labelled with @i@. Notice that @\phi_i@ is actually an affine embedding. Moreover, it gives an orientation to each side of a standard simplex: the orientation is positive @i@ is even, and negative otherwise.

Again, as a special case, we define the @0@-th side of @\Delta^0@ to be the unique function
@\phi_0 : \Delta^{-1} \to \Delta^0@
from the empty set (i.e. @\Delta^{-1}@) to the singleton @\{1\}@ (i.e. @\Delta^0@).

Let @X@ be any topological space. A **singular @n@-simplex** in @X@ is a continuous map from @\Delta^n@ to @X@. The idea here is to identify such a map with its image; since there are no restrictions on what this image may look like except that nearby points stay nearby (continuity), there could be collapsing or other weird things happening to @\Delta^n@ when viewed through the map. That's why it's called a *singular* simplex.

For @0 \leq i \leq n@, the **@i@-th face** of a singular @n@-simplex @\sigma : \Delta^n \to X@ is the singular @(n-1)@-simplex given by
@@\sigma \circ \phi_i : \Delta^{n-1} \to X.@@

For each @n\geq 0@, the **singular chain group** @C_n(X;Λ)@ with coefficients in a commutative ring @Λ@ is the free @Λ@-module having one generator for each singular @n@-simplex @\sigma@ in @X@. In other words, @C_n(X;Λ)@ consists of the formal @Λ@-linear combinations of @n@-simplices in @X@:
@@C_n(X;Λ) = \bigoplus_{\sigma : \Delta^n \to X} Λ.@@
Notice that this is a *module*, even though we use the term *group*. Just another fun little opportunity to be confused down the line. When @n<0@, the singular chain group is defined to be the zero module. In the special case @Λ = \mathbb{Z}@, the singular chain group at @n@ is the free abelian group on the singular @n@-simplices.

The singular chain group is the algebraic realization of how "sticking triangles on a space" works. If @Λ = \mathbb{Z}/2\mathbb{Z}@, then glueing two copies of the same simplex one on top of another means they "cancel out", and when only one of their sides are overlapping, these overlapping sides also cancel out; you obtain a square in the space instead of two triangles. Many geometric arguments use the fact that sides on the boundaries cancel out. The precise meaning of this in @C_n(X;Λ)@ is given by the **boundary homomorphism**, which is a @Λ@-linear map @∂: C_n(X;Λ) \to C_{n-1}(X;Λ)@ defined as
@@∂\sigma = \sum_{i=0}^n (-1)^i(\sigma \circ \phi_i).@@
This definition is made for @n \geq 1@; if @n \leq 0@ we simply say @∂= 0@.
The sign in the formula represents the orientation of each side (recall: the @i@-th side has positive orientation when @i@ is even, and negative orientation otherwise). This is done because we need "identical sides" that are "going in opposite directions" to cancel out in many geometrical arguments. For instance, the boundary of a tiling of some region of space by triangles (i.e. a sum in the singular chain group @C_2@) should be the boundary of the region, *not* the sum of the individual boundaries of each triangle (for instance, think about the proof of Stoke's formula).

An important property of the boundary homomorphism is this: @∂^2 = 0@. Intuitively: the boundary of the boundary is empty. Think of @\Delta^2@, which is a (filled) triangle, and think about it as a singular simplex in @\mathbb{R}^2@ (maybe via the projection on the plane in which @\Delta^2@ lies). Its boundary is the formal sum of three line segments. These segments are all perfectly lined up so that the end of the one is the start of the next: they form a cycle. Moreover, the point corresponding to the end of one segment has the opposite orientation to the point corresponding to the start of the next segment, so they cancel out. Since these endpoints are the boundaries of each of the three line segment, and since they all cancel out, the boundary of the boundary is effectively zero.

In fact, the boundary of a singular chain is zero precisely when all of the summands in the chain are arranged so that their boundaries all cancel out, that is, when they form a cycle and "enclose" some region of space. We define the **@n@-cycles** to be the set of all such chains:
@@Z_n(X;Λ) = \ker (∂: C_n(X;Λ) \to C_{n-1}(X;Λ)).@@
The **@n@-boundaries** is the set of all chains that can be expressed as the boundary of some @(n+1)@-dimensional singular chain:
@@B_n(X;Λ) = \operatorname{im} (∂: C_{n+1}(X;Λ) \to C_n(X;Λ)).@@
The identity @∂^2 = 0@ says we have a containment of @Λ@-submodules
@@B_n(X;Λ) \subseteq Z_n(X;Λ).@@
Hence we can consider the **@n@-th singular homology group**
@@H_n(X;Λ) = Z_n(X;Λ)/B_n(X;Λ).@@

The homology group captures in algebra an intuitive spatial fact. We have seen that any cycle "encloses" a region of space, by sticking together simplices of the same dimension along their boundaries until none are "left alone" (each boundary has a matching, opposite, boundary). Now suppose a given cycle is itself the boundary of some higher-dimensional simplex @\Delta@. Now the cycle can "move inside" @\Delta@ without breaking appart, shrinking until it becomes a single point. If a cycle is not a boundary, it means that something about the space @X@ obstructs the construction of a simplex @\Delta@ which would have the cycle as its boundary: there's a hole in @X@. Notice that the condition of continuity on singular simplices is essential here: the hole would basically force any @\Delta@ to be torn appart if it were to have the cycle as a boundary, breaking continuity. In this way, the homology construction detects holes in @X@ and gives useful information about them. This technology could be used to make a precise definition of what a "hole" in a topological space is: a hole is a generator for the homology group.

### Some abstract nonsense

Homology is a functor from the category of topological spaces up to homotopy, to the category of @Λ@-modules. The source category's objects are topological spaces, and the arrows are equivalence classes of continuous maps, where two maps are considered to be the same when they are homotopic. Since I always forget the details of what this means, here they are: consider two continuous maps @f,g : X \to Y@ between topological spaces. We say they are **homotopic** when there exists another continuous map @H : X \times [0,1] \to Y@ (called an **homotopy**) such that @H({-},0)=f@ and @H({-},1)=g@. In the source category we're interested in, an arrow is a actually a set of continous maps, all homotopic to each other.

Functoriality gives us the following for free: if two spaces are homotopic, then they have isomorphic homology groups. In particular, since @\mathbb{R}^n@ is contractible (i.e. homotopy equivalent to a point) for any @n \geq 0@, we have a concrete homology computation: for any @i \geq 1@,
\begin{equation*}
H_i(\mathbb{R}^n;Λ) \cong H_i(\{p\};Λ) = 0.
\end{equation*}
(It's easy to compute homology of a point: all singular simplices are the same!) When @i=0@, things are a bit weird, and fixing weird things is the purpose of the next section.

### Reduced homology

There's a technical point to address here. Consider what happens when we take the space @X@ to be a single point @p@ and we compute the @0@-th homology group. Since singular @1@-simplices are continuous maps @\Delta^1 \to \{p\}@, all @1@-simplices are actually the same. Hence they are all cycles, so by definition their boundaries are zero: @B_0(\{p\};Λ) = 0@. Therefore @H_0(\{p\};Λ) \cong Z_0(\{p\};Λ)@. However, we set @∂@ to be the zero map for all @n\leq 0@ earlier, so @H_0(\{p\};Λ)@ is @C_0(\{p\};Λ)@, the free module generated by all @0@-simplices. Since they are all the same, there's actually only one generator, so @H_0(\{p\};Λ) \cong Λ@. For technical reasons, it's better for the zeroth homology of a point to be the zero module; also, it makes sense intuitively, since we expect the homology to measure holes in a space, and we feel a point doesn't have holes.

There's an easy fix to this. Instead of having @∂= 0@ at degree zero, we set @C_{-1}(X;Λ)@ to be @Λ@ (recall: we made a special case above, where the only singular @(-1)@-simplex is the unique function from the empty set @\Delta^{-1}@ to @X@; then the chain group of degree @-1@ has to be the free @Λ@-module generated by that single @(-1)@-simplex), and now we may define @∂@ at degree zero with the same formula we used for positive degrees. For any singular @0@-simplex @\sigma : \Delta^0 \to X@, we now have
@@∂\sigma = \sigma \circ \phi_0,@@
which is the unique function from the empty set to @X@, and which is identified with @1 \in Λ@. Therefore @∂@ corresponds to the identity map on @Λ@. This means @Z_0(\{p\};Λ)@ is trivial, and so is this modified homology at degree zero.

This modified homology is called **reduced singular homology** and its homology groups are denoted with a tilde:
@@\widetilde{H}_i(X;Λ).@@
Since the only modification happens at degree zero, we have
@@\widetilde{H}_i(X;Λ)=H_i(X;Λ)@@
for each @i \geq 1@. In general, we see that for any @0@-chain @a_1\sigma_1+\dots+a_k\sigma_k@ (these are just formal linear combinations of points in @X@) we have
@@∂_0(a_1\sigma_1+\dots+a_k\sigma_k) = \sum_{i=1}^k a_i \in Λ.@@

There is an easy way to get from unreduced homology to reduced homology: at all positive dimensions the groups are the same, and at dimension zero we have the equation
@@H_0(X;Λ) \cong \widetilde{H}_0(X;Λ) \oplus Λ.@@
(Hint: think about what happens if @X@ is path-connected, and which @0@-chains are boundaries.)

### Mayer-Vietoris sequence

A great tool for computing with homology. It works for "unreduced" and reduced homology (just replace @H@ with @\widetilde{H}@ everywhere). Let @A@ and @B@ be two subsets of @X@ such that their interior cover @X@ (and for reduced homology, we also want their intersection to be nonempty). Then there is a long exact sequence in homology
<div style="display:flex;align-items:center;width:100%;margin-bottom:12px;">
<svg style="display:bock;margin:0 auto;" height="46.35343733333333px" style="vertical-align:-0.6691693333333333px;" version="1.1" viewBox="-.500002 -34.265076 389.542968 34.765078" width="519.3906239999999px" xmlns="http://www.w3.org/2000/svg">
<defs>
<path d="M8.631631-2.988792C8.631631-5.188543 6.838356-6.969863 4.65056-6.969863C2.426899-6.969863 .657534-5.164633 .657534-2.988792C.657534-.789041 2.450809 .992279 4.638605 .992279C6.862267 .992279 8.631631-.812951 8.631631-2.988792ZM.956413-3.144209C1.075965-5.152677 2.630137-6.575342 4.495143-6.670984V-3.144209H.956413ZM4.794022-6.670984C6.670984-6.575342 8.2132-5.140722 8.332752-3.144209H4.794022V-6.670984ZM4.495143 .6934C2.642092 .597758 1.075965-.800996 .956413-2.84533H4.495143V.6934ZM8.332752-2.84533C8.2132-.800996 6.635118 .597758 4.794022 .6934V-2.84533H8.332752Z" id="g3-8-drasiojs"></path>
<path d="M7.304608-4.542964C7.304608-6.360149 5.475467-7.149191 3.981071-7.149191C2.426899-7.149191 .657534-6.312329 .657534-4.554919V-.167372C.657534 .047821 .657534 .263014 .896638 .263014S1.135741 .047821 1.135741-.167372V-4.495143C1.135741-6.288418 3.084433-6.670984 3.981071-6.670984C4.519054-6.670984 5.272229-6.563387 5.905853-6.156912C6.826401-5.571108 6.826401-4.805978 6.826401-4.483188V-.167372C6.826401 .047821 6.826401 .263014 7.065504 .263014S7.304608 .047821 7.304608-.167372V-4.542964Z" id="g3-92-drasiojs"></path>
<path d="M3.88543 2.905106C3.88543 2.86924 3.88543 2.84533 3.682192 2.642092C2.486675 1.43462 1.817186-.537983 1.817186-2.976837C1.817186-5.296139 2.379078-7.292653 3.765878-8.703362C3.88543-8.810959 3.88543-8.834869 3.88543-8.870735C3.88543-8.942466 3.825654-8.966376 3.777833-8.966376C3.622416-8.966376 2.642092-8.105604 2.056289-6.933998C1.446575-5.726526 1.171606-4.447323 1.171606-2.976837C1.171606-1.912827 1.338979-.490162 1.960648 .789041C2.666002 2.223661 3.646326 3.000747 3.777833 3.000747C3.825654 3.000747 3.88543 2.976837 3.88543 2.905106Z" id="g8-40-drasiojs"></path>
<path d="M3.371357-2.976837C3.371357-3.88543 3.251806-5.36787 2.582316-6.75467C1.876961-8.18929 .896638-8.966376 .765131-8.966376C.71731-8.966376 .657534-8.942466 .657534-8.870735C.657534-8.834869 .657534-8.810959 .860772-8.607721C2.056289-7.400249 2.725778-5.427646 2.725778-2.988792C2.725778-.669489 2.163885 1.327024 .777086 2.737733C.657534 2.84533 .657534 2.86924 .657534 2.905106C.657534 2.976837 .71731 3.000747 .765131 3.000747C.920548 3.000747 1.900872 2.139975 2.486675 .968369C3.096389-.251059 3.371357-1.542217 3.371357-2.976837Z" id="g8-41-drasiojs"></path>
<path d="M3.474969-1.809215H5.818182C5.929763-1.809215 6.105106-1.809215 6.105106-1.992528S5.929763-2.175841 5.818182-2.175841H3.474969V-4.527024C3.474969-4.638605 3.474969-4.813948 3.291656-4.813948S3.108344-4.638605 3.108344-4.527024V-2.175841H.757161C.645579-2.175841 .470237-2.175841 .470237-1.992528S.645579-1.809215 .757161-1.809215H3.108344V.541968C3.108344 .653549 3.108344 .828892 3.291656 .828892S3.474969 .653549 3.474969 .541968V-1.809215Z" id="g7-43-drasiojs"></path>
<path d="M2.502615-5.076961C2.502615-5.292154 2.486675-5.300125 2.271482-5.300125C1.944707-4.98132 1.522291-4.790037 .765131-4.790037V-4.527024C.980324-4.527024 1.41071-4.527024 1.872976-4.742217V-.653549C1.872976-.358655 1.849066-.263014 1.091905-.263014H.812951V0C1.139726-.02391 1.825156-.02391 2.183811-.02391S3.235866-.02391 3.56264 0V-.263014H3.283686C2.526526-.263014 2.502615-.358655 2.502615-.653549V-5.076961Z" id="g7-49-drasiojs"></path>
<path d="M2.375093-4.97335C2.375093-5.148692 2.247572-5.276214 2.064259-5.276214C1.857036-5.276214 1.625903-5.084932 1.625903-4.845828C1.625903-4.670486 1.753425-4.542964 1.936737-4.542964C2.14396-4.542964 2.375093-4.734247 2.375093-4.97335ZM1.211457-2.048319L.781071-.948443C.74122-.828892 .70137-.73325 .70137-.597758C.70137-.207223 1.004234 .079701 1.42665 .079701C2.199751 .079701 2.526526-1.036115 2.526526-1.139726C2.526526-1.219427 2.462765-1.243337 2.406974-1.243337C2.311333-1.243337 2.295392-1.187547 2.271482-1.107846C2.088169-.470237 1.761395-.143462 1.44259-.143462C1.346949-.143462 1.251308-.183313 1.251308-.398506C1.251308-.589788 1.307098-.73325 1.41071-.980324C1.490411-1.195517 1.570112-1.41071 1.657783-1.625903L1.904857-2.271482C1.976588-2.454795 2.072229-2.701868 2.072229-2.83736C2.072229-3.235866 1.753425-3.514819 1.346949-3.514819C.573848-3.514819 .239103-2.399004 .239103-2.295392C.239103-2.223661 .294894-2.191781 .358655-2.191781C.462267-2.191781 .470237-2.239601 .494147-2.319303C.71731-3.076463 1.083935-3.291656 1.323039-3.291656C1.43462-3.291656 1.514321-3.251806 1.514321-3.028643C1.514321-2.948941 1.506351-2.83736 1.42665-2.598257L1.211457-2.048319Z" id="g5-105-drasiojs"></path>
<path d="M2.199751-.573848C2.199751-.920548 1.912827-1.159651 1.625903-1.159651C1.279203-1.159651 1.0401-.872727 1.0401-.585803C1.0401-.239103 1.327024 0 1.613948 0C1.960648 0 2.199751-.286924 2.199751-.573848Z" id="g6-58-drasiojs"></path>
<path d="M2.032379-1.327024C1.613948-.621669 1.207472-.382565 .633624-.3467C.502117-.334745 .406476-.334745 .406476-.119552C.406476-.047821 .466252 0 .549938 0C.765131 0 1.303113-.02391 1.518306-.02391C1.865006-.02391 2.247572 0 2.582316 0C2.654047 0 2.797509 0 2.797509-.227148C2.797509-.334745 2.701868-.3467 2.630137-.3467C2.355168-.37061 2.12802-.466252 2.12802-.753176C2.12802-.920548 2.199751-1.052055 2.355168-1.315068L3.263761-2.82142H6.312329C6.324284-2.713823 6.324284-2.618182 6.336239-2.510585C6.372105-2.199751 6.515567-.956413 6.515567-.729265C6.515567-.37061 5.905853-.3467 5.71457-.3467C5.583064-.3467 5.451557-.3467 5.451557-.131507C5.451557 0 5.559153 0 5.630884 0C5.834122 0 6.073225-.02391 6.276463-.02391H6.957908C7.687173-.02391 8.2132 0 8.225156 0C8.308842 0 8.440349 0 8.440349-.227148C8.440349-.3467 8.332752-.3467 8.153425-.3467C7.49589-.3467 7.483935-.454296 7.44807-.812951L6.718804-8.272976C6.694894-8.51208 6.647073-8.53599 6.515567-8.53599C6.396015-8.53599 6.324284-8.51208 6.216687-8.332752L2.032379-1.327024ZM3.466999-3.16812L5.869988-7.185056L6.276463-3.16812H3.466999Z" id="g6-65-drasiojs"></path>
<path d="M4.375592-7.352428C4.483188-7.79477 4.531009-7.81868 4.99726-7.81868H6.551432C7.902366-7.81868 7.902366-6.670984 7.902366-6.563387C7.902366-5.595019 6.933998-4.363636 5.355915-4.363636H3.634371L4.375592-7.352428ZM6.396015-4.267995C7.699128-4.507098 8.88269-5.415691 8.88269-6.515567C8.88269-7.44807 8.057783-8.16538 6.706849-8.16538H2.86924C2.642092-8.16538 2.534496-8.16538 2.534496-7.938232C2.534496-7.81868 2.642092-7.81868 2.82142-7.81868C3.550685-7.81868 3.550685-7.723039 3.550685-7.591532C3.550685-7.567621 3.550685-7.49589 3.502864-7.316563L1.888917-.884682C1.78132-.466252 1.75741-.3467 .920548-.3467C.6934-.3467 .573848-.3467 .573848-.131507C.573848 0 .645579 0 .884682 0H4.985305C6.814446 0 8.225156-1.3868 8.225156-2.594271C8.225156-3.574595 7.364384-4.172354 6.396015-4.267995ZM4.698381-.3467H3.084433C2.917061-.3467 2.893151-.3467 2.82142-.358655C2.689913-.37061 2.677958-.394521 2.677958-.490162C2.677958-.573848 2.701868-.645579 2.725778-.753176L3.56264-4.124533H5.810212C7.220922-4.124533 7.220922-2.809465 7.220922-2.713823C7.220922-1.566127 6.180822-.3467 4.698381-.3467Z" id="g6-66-drasiojs"></path>
<path d="M8.942466-7.292653C9.050062-7.699128 9.073973-7.81868 9.92279-7.81868C10.137983-7.81868 10.257534-7.81868 10.257534-8.033873C10.257534-8.16538 10.149938-8.16538 10.078207-8.16538C9.863014-8.16538 9.611955-8.141469 9.384807-8.141469H7.974097C7.746949-8.141469 7.49589-8.16538 7.268742-8.16538C7.185056-8.16538 7.041594-8.16538 7.041594-7.938232C7.041594-7.81868 7.12528-7.81868 7.352428-7.81868C8.069738-7.81868 8.069738-7.723039 8.069738-7.591532C8.069738-7.567621 8.069738-7.49589 8.021918-7.316563L7.292653-4.423412H3.682192L4.399502-7.292653C4.507098-7.699128 4.531009-7.81868 5.379826-7.81868C5.595019-7.81868 5.71457-7.81868 5.71457-8.033873C5.71457-8.16538 5.606974-8.16538 5.535243-8.16538C5.32005-8.16538 5.068991-8.141469 4.841843-8.141469H3.431133C3.203985-8.141469 2.952927-8.16538 2.725778-8.16538C2.642092-8.16538 2.49863-8.16538 2.49863-7.938232C2.49863-7.81868 2.582316-7.81868 2.809465-7.81868C3.526775-7.81868 3.526775-7.723039 3.526775-7.591532C3.526775-7.567621 3.526775-7.49589 3.478954-7.316563L1.865006-.884682C1.75741-.466252 1.733499-.3467 .908593-.3467C.633624-.3467 .549938-.3467 .549938-.119552C.549938 0 .681445 0 .71731 0C.932503 0 1.183562-.02391 1.41071-.02391H2.82142C3.048568-.02391 3.299626 0 3.526775 0C3.622416 0 3.753923 0 3.753923-.227148C3.753923-.3467 3.646326-.3467 3.466999-.3467C2.737733-.3467 2.737733-.442341 2.737733-.561893C2.737733-.573848 2.737733-.657534 2.761644-.753176L3.58655-4.076712H7.208966C7.005729-3.287671 6.396015-.789041 6.372105-.71731C6.240598-.358655 6.049315-.358655 5.34396-.3467C5.200498-.3467 5.092902-.3467 5.092902-.119552C5.092902 0 5.224408 0 5.260274 0C5.475467 0 5.726526-.02391 5.953674-.02391H7.364384C7.591532-.02391 7.84259 0 8.069738 0C8.16538 0 8.296887 0 8.296887-.227148C8.296887-.3467 8.18929-.3467 8.009963-.3467C7.280697-.3467 7.280697-.442341 7.280697-.561893C7.280697-.573848 7.280697-.657534 7.304608-.753176L8.942466-7.292653Z" id="g6-72-drasiojs"></path>
<path d="M5.678705-4.853798L4.554919-7.47198C4.710336-7.758904 5.068991-7.806725 5.212453-7.81868C5.284184-7.81868 5.415691-7.830635 5.415691-8.033873C5.415691-8.16538 5.308095-8.16538 5.236364-8.16538C5.033126-8.16538 4.794022-8.141469 4.590785-8.141469H3.897385C3.16812-8.141469 2.642092-8.16538 2.630137-8.16538C2.534496-8.16538 2.414944-8.16538 2.414944-7.938232C2.414944-7.81868 2.52254-7.81868 2.677958-7.81868C3.371357-7.81868 3.419178-7.699128 3.53873-7.412204L4.961395-4.088667L2.367123-1.315068C1.936737-.848817 1.422665-.394521 .537983-.3467C.394521-.334745 .298879-.334745 .298879-.119552C.298879-.083686 .310834 0 .442341 0C.609714 0 .789041-.02391 .956413-.02391H1.518306C1.900872-.02391 2.319303 0 2.689913 0C2.773599 0 2.917061 0 2.917061-.215193C2.917061-.334745 2.833375-.3467 2.761644-.3467C2.52254-.37061 2.367123-.502117 2.367123-.6934C2.367123-.896638 2.510585-1.0401 2.857285-1.398755L3.921295-2.558406C4.184309-2.833375 4.817933-3.526775 5.080946-3.789788L6.336239-.848817C6.348194-.824907 6.396015-.705355 6.396015-.6934C6.396015-.585803 6.133001-.37061 5.750436-.3467C5.678705-.3467 5.547198-.334745 5.547198-.119552C5.547198 0 5.66675 0 5.726526 0C5.929763 0 6.168867-.02391 6.372105-.02391H7.687173C7.902366-.02391 8.129514 0 8.332752 0C8.416438 0 8.547945 0 8.547945-.227148C8.547945-.3467 8.428394-.3467 8.320797-.3467C7.603487-.358655 7.579577-.418431 7.376339-.860772L5.798257-4.566874L7.316563-6.192777C7.436115-6.312329 7.711083-6.611208 7.81868-6.73076C8.332752-7.268742 8.810959-7.758904 9.779328-7.81868C9.898879-7.830635 10.018431-7.830635 10.018431-8.033873C10.018431-8.16538 9.910834-8.16538 9.863014-8.16538C9.695641-8.16538 9.516314-8.141469 9.348941-8.141469H8.799004C8.416438-8.141469 7.998007-8.16538 7.627397-8.16538C7.543711-8.16538 7.400249-8.16538 7.400249-7.950187C7.400249-7.830635 7.483935-7.81868 7.555666-7.81868C7.746949-7.79477 7.950187-7.699128 7.950187-7.47198L7.938232-7.44807C7.926276-7.364384 7.902366-7.244832 7.770859-7.10137L5.678705-4.853798Z" id="g6-88-drasiojs"></path>
</defs>
<g id="page168-drasiojs">
<g fill="currentColor" transform="matrix(1 0 0 1 -190.3613 2.98883)">
<use href="#g6-58-drasiojs" x="206.288841" y="-10.35287"></use>
<use href="#g6-58-drasiojs" x="211.532999" y="-10.35287"></use>
<use href="#g6-58-drasiojs" x="216.777158" y="-10.35287"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -205.3219 2.98883)">
<use href="#g6-72-drasiojs" x="259.331036" y="-10.35287"></use>
<use href="#g5-105-drasiojs" x="269.030017" y="-8.559607"></use>
<use href="#g7-43-drasiojs" x="271.913156" y="-8.559607"></use>
<use href="#g7-49-drasiojs" x="278.499663" y="-8.559607"></use>
<use href="#g8-40-drasiojs" x="283.231978" y="-10.35287"></use>
<use href="#g6-88-drasiojs" x="287.784304" y="-10.35287"></use>
<use href="#g8-41-drasiojs" x="298.439412" y="-10.35287"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -210.362 2.98883)">
<use href="#g6-72-drasiojs" x="332.373214" y="-10.35287"></use>
<use href="#g5-105-drasiojs" x="342.072194" y="-8.559607"></use>
<use href="#g8-40-drasiojs" x="345.453466" y="-10.35287"></use>
<use href="#g6-65-drasiojs" x="350.005792" y="-10.35287"></use>
<use href="#g3-92-drasiojs" x="361.437802" y="-10.35287"></use>
<use href="#g6-66-drasiojs" x="372.064604" y="-10.35287"></use>
<use href="#g8-41-drasiojs" x="381.560865" y="-10.35287"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -222.118 2.98883)">
<use href="#g6-72-drasiojs" x="422.211659" y="-10.35287"></use>
<use href="#g5-105-drasiojs" x="431.910639" y="-8.559607"></use>
<use href="#g8-40-drasiojs" x="435.291911" y="-10.35287"></use>
<use href="#g6-65-drasiojs" x="439.844236" y="-10.35287"></use>
<use href="#g8-41-drasiojs" x="448.619583" y="-10.35287"></use>
<use href="#g3-8-drasiojs" x="455.828572" y="-10.35287"></use>
<use href="#g6-72-drasiojs" x="467.783733" y="-10.35287"></use>
<use href="#g5-105-drasiojs" x="477.482713" y="-8.559607"></use>
<use href="#g8-40-drasiojs" x="480.863985" y="-10.35287"></use>
<use href="#g6-66-drasiojs" x="485.416311" y="-10.35287"></use>
<use href="#g8-41-drasiojs" x="494.912572" y="-10.35287"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -199.911 2.98883)">
<use href="#g6-72-drasiojs" x="501.600124" y="-10.35287"></use>
<use href="#g5-105-drasiojs" x="511.299105" y="-8.559607"></use>
<use href="#g8-40-drasiojs" x="514.680376" y="-10.35287"></use>
<use href="#g6-88-drasiojs" x="519.232702" y="-10.35287"></use>
<use href="#g8-41-drasiojs" x="529.88781" y="-10.35287"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -190.361 2.98883)">
<use href="#g6-58-drasiojs" x="549.231976" y="-10.35287"></use>
<use href="#g6-58-drasiojs" x="554.476134" y="-10.35287"></use>
<use href="#g6-58-drasiojs" x="559.720293" y="-10.35287"></use>
</g>
<path d="M35.016-10.351563H48.184" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M45.93749-13.22266C46.39062-11.5 47.40234-10.6875 48.421869-10.351563C47.40234-10.019532 46.39062-9.20703 45.93749-7.48438" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M103.0156-10.351563H116.1875" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M113.94128-13.22266C114.39441-11.5 115.40613-10.6875 116.425657-10.351563C115.40613-10.019532 114.39441-9.20703 113.94128-7.48438" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M181.1016-10.351563H194.269535" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M192.0235-13.22266C192.47663-11.5 193.48835-10.6875 194.511785-10.351563C193.48835-10.019532 192.47663-9.20703 192.0235-7.48438" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M282.6953-10.351563H295.867" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M293.62077-13.22266C294.0739-11.5 295.08561-10.6875 296.105146-10.351563C295.08561-10.019532 294.0739-9.20703 293.62077-7.48438" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M339.879-10.351563H353.051" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M350.80087-13.22266C351.2579-11.5 352.26962-10.6875 353.289153-10.351563C352.26962-10.019532 351.2579-9.20703 350.80087-7.48438" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
</g>
</svg>
</div>

We can use this to compute the homology of the @n@-sphere @S^n@. Let @A@ be the "open north cap" and @B@ be the "open south cap", i.e. @A@ and @B@ are contractible open sets in @S^n@ such that their intersection is homotopic to the "equator" @S^{n-1}@. Then the reduced Mayer-Vietoris sequence looks like
<div style="display:flex;align-items:center;width:100%;">
<svg style="display:bock;margin:0 auto;" height="49.79613333333333px" style="vertical-align:-0.6691693333333333px;" version="1.1" viewBox="-.500002 -36.847099 389.542968 37.3471" width="519.3906239999999px" xmlns="http://www.w3.org/2000/svg">
<defs>
<path d="M8.631631-2.988792C8.631631-5.188543 6.838356-6.969863 4.65056-6.969863C2.426899-6.969863 .657534-5.164633 .657534-2.988792C.657534-.789041 2.450809 .992279 4.638605 .992279C6.862267 .992279 8.631631-.812951 8.631631-2.988792ZM.956413-3.144209C1.075965-5.152677 2.630137-6.575342 4.495143-6.670984V-3.144209H.956413ZM4.794022-6.670984C6.670984-6.575342 8.2132-5.140722 8.332752-3.144209H4.794022V-6.670984ZM4.495143 .6934C2.642092 .597758 1.075965-.800996 .956413-2.84533H4.495143V.6934ZM8.332752-2.84533C8.2132-.800996 6.635118 .597758 4.794022 .6934V-2.84533H8.332752Z" id="g3-8-drasiojs"></path>
<path d="M5.571108-1.809215C5.69863-1.809215 5.873973-1.809215 5.873973-1.992528S5.69863-2.175841 5.571108-2.175841H1.004234C.876712-2.175841 .70137-2.175841 .70137-1.992528S.876712-1.809215 1.004234-1.809215H5.571108Z" id="g2-0-drasiojs"></path>
<path d="M3.88543 2.905106C3.88543 2.86924 3.88543 2.84533 3.682192 2.642092C2.486675 1.43462 1.817186-.537983 1.817186-2.976837C1.817186-5.296139 2.379078-7.292653 3.765878-8.703362C3.88543-8.810959 3.88543-8.834869 3.88543-8.870735C3.88543-8.942466 3.825654-8.966376 3.777833-8.966376C3.622416-8.966376 2.642092-8.105604 2.056289-6.933998C1.446575-5.726526 1.171606-4.447323 1.171606-2.976837C1.171606-1.912827 1.338979-.490162 1.960648 .789041C2.666002 2.223661 3.646326 3.000747 3.777833 3.000747C3.825654 3.000747 3.88543 2.976837 3.88543 2.905106Z" id="g8-40-drasiojs"></path>
<path d="M3.371357-2.976837C3.371357-3.88543 3.251806-5.36787 2.582316-6.75467C1.876961-8.18929 .896638-8.966376 .765131-8.966376C.71731-8.966376 .657534-8.942466 .657534-8.870735C.657534-8.834869 .657534-8.810959 .860772-8.607721C2.056289-7.400249 2.725778-5.427646 2.725778-2.988792C2.725778-.669489 2.163885 1.327024 .777086 2.737733C.657534 2.84533 .657534 2.86924 .657534 2.905106C.657534 2.976837 .71731 3.000747 .765131 3.000747C.920548 3.000747 1.900872 2.139975 2.486675 .968369C3.096389-.251059 3.371357-1.542217 3.371357-2.976837Z" id="g8-41-drasiojs"></path>
<path d="M3.474969-1.809215H5.818182C5.929763-1.809215 6.105106-1.809215 6.105106-1.992528S5.929763-2.175841 5.818182-2.175841H3.474969V-4.527024C3.474969-4.638605 3.474969-4.813948 3.291656-4.813948S3.108344-4.638605 3.108344-4.527024V-2.175841H.757161C.645579-2.175841 .470237-2.175841 .470237-1.992528S.645579-1.809215 .757161-1.809215H3.108344V.541968C3.108344 .653549 3.108344 .828892 3.291656 .828892S3.474969 .653549 3.474969 .541968V-1.809215Z" id="g7-43-drasiojs"></path>
<path d="M2.502615-5.076961C2.502615-5.292154 2.486675-5.300125 2.271482-5.300125C1.944707-4.98132 1.522291-4.790037 .765131-4.790037V-4.527024C.980324-4.527024 1.41071-4.527024 1.872976-4.742217V-.653549C1.872976-.358655 1.849066-.263014 1.091905-.263014H.812951V0C1.139726-.02391 1.825156-.02391 2.183811-.02391S3.235866-.02391 3.56264 0V-.263014H3.283686C2.526526-.263014 2.502615-.358655 2.502615-.653549V-5.076961Z" id="g7-49-drasiojs"></path>
<path d="M2.375093-4.97335C2.375093-5.148692 2.247572-5.276214 2.064259-5.276214C1.857036-5.276214 1.625903-5.084932 1.625903-4.845828C1.625903-4.670486 1.753425-4.542964 1.936737-4.542964C2.14396-4.542964 2.375093-4.734247 2.375093-4.97335ZM1.211457-2.048319L.781071-.948443C.74122-.828892 .70137-.73325 .70137-.597758C.70137-.207223 1.004234 .079701 1.42665 .079701C2.199751 .079701 2.526526-1.036115 2.526526-1.139726C2.526526-1.219427 2.462765-1.243337 2.406974-1.243337C2.311333-1.243337 2.295392-1.187547 2.271482-1.107846C2.088169-.470237 1.761395-.143462 1.44259-.143462C1.346949-.143462 1.251308-.183313 1.251308-.398506C1.251308-.589788 1.307098-.73325 1.41071-.980324C1.490411-1.195517 1.570112-1.41071 1.657783-1.625903L1.904857-2.271482C1.976588-2.454795 2.072229-2.701868 2.072229-2.83736C2.072229-3.235866 1.753425-3.514819 1.346949-3.514819C.573848-3.514819 .239103-2.399004 .239103-2.295392C.239103-2.223661 .294894-2.191781 .358655-2.191781C.462267-2.191781 .470237-2.239601 .494147-2.319303C.71731-3.076463 1.083935-3.291656 1.323039-3.291656C1.43462-3.291656 1.514321-3.251806 1.514321-3.028643C1.514321-2.948941 1.506351-2.83736 1.42665-2.598257L1.211457-2.048319Z" id="g5-105-drasiojs"></path>
<path d="M1.594022-1.307098C1.617933-1.42665 1.697634-1.729514 1.721544-1.849066C1.833126-2.279452 1.833126-2.287422 2.016438-2.550436C2.279452-2.940971 2.654047-3.291656 3.188045-3.291656C3.474969-3.291656 3.642341-3.124284 3.642341-2.749689C3.642341-2.311333 3.307597-1.40274 3.156164-1.012204C3.052553-.749191 3.052553-.70137 3.052553-.597758C3.052553-.143462 3.427148 .079701 3.769863 .079701C4.550934 .079701 4.877709-1.036115 4.877709-1.139726C4.877709-1.219427 4.813948-1.243337 4.758157-1.243337C4.662516-1.243337 4.646575-1.187547 4.622665-1.107846C4.431382-.454296 4.096638-.143462 3.793773-.143462C3.666252-.143462 3.602491-.223163 3.602491-.406476S3.666252-.765131 3.745953-.964384C3.865504-1.267248 4.216189-2.183811 4.216189-2.630137C4.216189-3.227895 3.801743-3.514819 3.227895-3.514819C2.582316-3.514819 2.16787-3.124284 1.936737-2.82142C1.880946-3.259776 1.530262-3.514819 1.123786-3.514819C.836862-3.514819 .637609-3.331507 .510087-3.084433C.318804-2.709838 .239103-2.311333 .239103-2.295392C.239103-2.223661 .294894-2.191781 .358655-2.191781C.462267-2.191781 .470237-2.223661 .526027-2.430884C.621669-2.82142 .765131-3.291656 1.099875-3.291656C1.307098-3.291656 1.354919-3.092403 1.354919-2.917061C1.354919-2.773599 1.315068-2.622167 1.251308-2.359153C1.235367-2.295392 1.115816-1.825156 1.083935-1.713574L.789041-.518057C.757161-.398506 .70934-.199253 .70934-.167372C.70934 .01594 .860772 .079701 .964384 .079701C1.107846 .079701 1.227397-.01594 1.283188-.111582C1.307098-.159402 1.370859-.430386 1.41071-.597758L1.594022-1.307098Z" id="g5-110-drasiojs"></path>
<path d="M6.467746-8.631631C5.881943-8.141469 5.248319-7.782814 4.638605-7.782814C4.160399-7.782814 3.813699-7.986052 3.395268-8.225156C3.048568-8.428394 2.677958-8.631631 2.199751-8.631631C1.900872-8.631631 1.590037-8.53599 1.327024-8.416438C1.08792-8.296887 .848817-8.16538 .645579-7.998007L0-7.47198L.167372-7.268742C.753176-7.758904 1.3868-8.117559 1.996513-8.117559C2.47472-8.117559 2.82142-7.914321 3.239851-7.675218C3.58655-7.47198 3.957161-7.268742 4.435367-7.268742C4.734247-7.268742 5.045081-7.364384 5.308095-7.483935C5.547198-7.603487 5.786301-7.734994 5.989539-7.902366L6.635118-8.428394L6.467746-8.631631Z" id="g1-101-drasiojs"></path>
<path d="M2.199751-.573848C2.199751-.920548 1.912827-1.159651 1.625903-1.159651C1.279203-1.159651 1.0401-.872727 1.0401-.585803C1.0401-.239103 1.327024 0 1.613948 0C1.960648 0 2.199751-.286924 2.199751-.573848Z" id="g6-58-drasiojs"></path>
<path d="M2.032379-1.327024C1.613948-.621669 1.207472-.382565 .633624-.3467C.502117-.334745 .406476-.334745 .406476-.119552C.406476-.047821 .466252 0 .549938 0C.765131 0 1.303113-.02391 1.518306-.02391C1.865006-.02391 2.247572 0 2.582316 0C2.654047 0 2.797509 0 2.797509-.227148C2.797509-.334745 2.701868-.3467 2.630137-.3467C2.355168-.37061 2.12802-.466252 2.12802-.753176C2.12802-.920548 2.199751-1.052055 2.355168-1.315068L3.263761-2.82142H6.312329C6.324284-2.713823 6.324284-2.618182 6.336239-2.510585C6.372105-2.199751 6.515567-.956413 6.515567-.729265C6.515567-.37061 5.905853-.3467 5.71457-.3467C5.583064-.3467 5.451557-.3467 5.451557-.131507C5.451557 0 5.559153 0 5.630884 0C5.834122 0 6.073225-.02391 6.276463-.02391H6.957908C7.687173-.02391 8.2132 0 8.225156 0C8.308842 0 8.440349 0 8.440349-.227148C8.440349-.3467 8.332752-.3467 8.153425-.3467C7.49589-.3467 7.483935-.454296 7.44807-.812951L6.718804-8.272976C6.694894-8.51208 6.647073-8.53599 6.515567-8.53599C6.396015-8.53599 6.324284-8.51208 6.216687-8.332752L2.032379-1.327024ZM3.466999-3.16812L5.869988-7.185056L6.276463-3.16812H3.466999Z" id="g6-65-drasiojs"></path>
<path d="M4.375592-7.352428C4.483188-7.79477 4.531009-7.81868 4.99726-7.81868H6.551432C7.902366-7.81868 7.902366-6.670984 7.902366-6.563387C7.902366-5.595019 6.933998-4.363636 5.355915-4.363636H3.634371L4.375592-7.352428ZM6.396015-4.267995C7.699128-4.507098 8.88269-5.415691 8.88269-6.515567C8.88269-7.44807 8.057783-8.16538 6.706849-8.16538H2.86924C2.642092-8.16538 2.534496-8.16538 2.534496-7.938232C2.534496-7.81868 2.642092-7.81868 2.82142-7.81868C3.550685-7.81868 3.550685-7.723039 3.550685-7.591532C3.550685-7.567621 3.550685-7.49589 3.502864-7.316563L1.888917-.884682C1.78132-.466252 1.75741-.3467 .920548-.3467C.6934-.3467 .573848-.3467 .573848-.131507C.573848 0 .645579 0 .884682 0H4.985305C6.814446 0 8.225156-1.3868 8.225156-2.594271C8.225156-3.574595 7.364384-4.172354 6.396015-4.267995ZM4.698381-.3467H3.084433C2.917061-.3467 2.893151-.3467 2.82142-.358655C2.689913-.37061 2.677958-.394521 2.677958-.490162C2.677958-.573848 2.701868-.645579 2.725778-.753176L3.56264-4.124533H5.810212C7.220922-4.124533 7.220922-2.809465 7.220922-2.713823C7.220922-1.566127 6.180822-.3467 4.698381-.3467Z" id="g6-66-drasiojs"></path>
<path d="M8.942466-7.292653C9.050062-7.699128 9.073973-7.81868 9.92279-7.81868C10.137983-7.81868 10.257534-7.81868 10.257534-8.033873C10.257534-8.16538 10.149938-8.16538 10.078207-8.16538C9.863014-8.16538 9.611955-8.141469 9.384807-8.141469H7.974097C7.746949-8.141469 7.49589-8.16538 7.268742-8.16538C7.185056-8.16538 7.041594-8.16538 7.041594-7.938232C7.041594-7.81868 7.12528-7.81868 7.352428-7.81868C8.069738-7.81868 8.069738-7.723039 8.069738-7.591532C8.069738-7.567621 8.069738-7.49589 8.021918-7.316563L7.292653-4.423412H3.682192L4.399502-7.292653C4.507098-7.699128 4.531009-7.81868 5.379826-7.81868C5.595019-7.81868 5.71457-7.81868 5.71457-8.033873C5.71457-8.16538 5.606974-8.16538 5.535243-8.16538C5.32005-8.16538 5.068991-8.141469 4.841843-8.141469H3.431133C3.203985-8.141469 2.952927-8.16538 2.725778-8.16538C2.642092-8.16538 2.49863-8.16538 2.49863-7.938232C2.49863-7.81868 2.582316-7.81868 2.809465-7.81868C3.526775-7.81868 3.526775-7.723039 3.526775-7.591532C3.526775-7.567621 3.526775-7.49589 3.478954-7.316563L1.865006-.884682C1.75741-.466252 1.733499-.3467 .908593-.3467C.633624-.3467 .549938-.3467 .549938-.119552C.549938 0 .681445 0 .71731 0C.932503 0 1.183562-.02391 1.41071-.02391H2.82142C3.048568-.02391 3.299626 0 3.526775 0C3.622416 0 3.753923 0 3.753923-.227148C3.753923-.3467 3.646326-.3467 3.466999-.3467C2.737733-.3467 2.737733-.442341 2.737733-.561893C2.737733-.573848 2.737733-.657534 2.761644-.753176L3.58655-4.076712H7.208966C7.005729-3.287671 6.396015-.789041 6.372105-.71731C6.240598-.358655 6.049315-.358655 5.34396-.3467C5.200498-.3467 5.092902-.3467 5.092902-.119552C5.092902 0 5.224408 0 5.260274 0C5.475467 0 5.726526-.02391 5.953674-.02391H7.364384C7.591532-.02391 7.84259 0 8.069738 0C8.16538 0 8.296887 0 8.296887-.227148C8.296887-.3467 8.18929-.3467 8.009963-.3467C7.280697-.3467 7.280697-.442341 7.280697-.561893C7.280697-.573848 7.280697-.657534 7.304608-.753176L8.942466-7.292653Z" id="g6-72-drasiojs"></path>
<path d="M7.591532-8.308842C7.591532-8.416438 7.507846-8.416438 7.483935-8.416438C7.436115-8.416438 7.424159-8.404483 7.280697-8.225156C7.208966-8.141469 6.718804-7.519801 6.706849-7.507846C6.312329-8.284932 5.523288-8.416438 5.021171-8.416438C3.502864-8.416438 2.12802-7.029639 2.12802-5.678705C2.12802-4.782067 2.666002-4.25604 3.251806-4.052802C3.383313-4.004981 4.088667-3.813699 4.447323-3.730012C5.057036-3.56264 5.212453-3.514819 5.463512-3.251806C5.511333-3.19203 5.750436-2.917061 5.750436-2.355168C5.750436-1.243337 4.722291-.095641 3.526775-.095641C2.546451-.095641 1.458531-.514072 1.458531-1.853051C1.458531-2.080199 1.506351-2.367123 1.542217-2.486675C1.542217-2.52254 1.554172-2.582316 1.554172-2.606227C1.554172-2.654047 1.530262-2.713823 1.43462-2.713823C1.327024-2.713823 1.315068-2.689913 1.267248-2.486675L.657534-.035866C.657534-.02391 .609714 .131507 .609714 .143462C.609714 .251059 .705355 .251059 .729265 .251059C.777086 .251059 .789041 .239103 .932503 .059776L1.482441-.657534C1.769365-.227148 2.391034 .251059 3.502864 .251059C5.045081 .251059 6.455791-1.243337 6.455791-2.737733C6.455791-3.239851 6.336239-3.682192 5.881943-4.124533C5.630884-4.375592 5.415691-4.435367 4.315816-4.722291C3.514819-4.937484 3.407223-4.97335 3.19203-5.164633C2.988792-5.36787 2.833375-5.654795 2.833375-6.06127C2.833375-7.065504 3.849564-8.093649 4.985305-8.093649C6.156912-8.093649 6.706849-7.376339 6.706849-6.240598C6.706849-5.929763 6.647073-5.606974 6.647073-5.559153C6.647073-5.451557 6.742715-5.451557 6.77858-5.451557C6.886177-5.451557 6.898132-5.487422 6.945953-5.678705L7.591532-8.308842Z" id="g6-83-drasiojs"></path>
</defs>
<g id="page177-drasiojs">
<g fill="currentColor" transform="matrix(1 0 0 1 -189.6366 4.3338)">
<use href="#g6-58-drasiojs" x="206.288841" y="-11.697832"></use>
<use href="#g6-58-drasiojs" x="211.532999" y="-11.697832"></use>
<use href="#g6-58-drasiojs" x="216.777158" y="-11.697832"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -206.0354 4.3338)">
<use href="#g1-101-drasiojs" x="263.41007" y="-14.71984"></use>
<use href="#g6-72-drasiojs" x="260.769323" y="-11.697832"></use>
<use href="#g5-105-drasiojs" x="270.468303" y="-9.904569"></use>
<use href="#g7-43-drasiojs" x="273.351443" y="-9.904569"></use>
<use href="#g7-49-drasiojs" x="279.937949" y="-9.904569"></use>
<use href="#g8-40-drasiojs" x="284.670264" y="-11.697832"></use>
<use href="#g6-83-drasiojs" x="289.22259" y="-11.697832"></use>
<use href="#g5-110-drasiojs" x="297.117913" y="-16.036269"></use>
<use href="#g8-41-drasiojs" x="302.754248" y="-11.697832"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -206.035 4.3338)">
<use href="#g1-101-drasiojs" x="334.289186" y="-14.71984"></use>
<use href="#g6-72-drasiojs" x="331.648439" y="-11.697832"></use>
<use href="#g5-105-drasiojs" x="341.347419" y="-9.904569"></use>
<use href="#g8-40-drasiojs" x="344.728691" y="-11.697832"></use>
<use href="#g6-83-drasiojs" x="349.281017" y="-11.697832"></use>
<use href="#g5-110-drasiojs" x="357.17634" y="-16.036269"></use>
<use href="#g2-0-drasiojs" x="362.314542" y="-16.036269"></use>
<use href="#g7-49-drasiojs" x="368.901049" y="-16.036269"></use>
<use href="#g8-41-drasiojs" x="373.633364" y="-11.697832"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -221.394 4.3338)">
<use href="#g1-101-drasiojs" x="420.526283" y="-14.71984"></use>
<use href="#g6-72-drasiojs" x="417.885535" y="-11.697832"></use>
<use href="#g5-105-drasiojs" x="427.584516" y="-9.904569"></use>
<use href="#g8-40-drasiojs" x="430.965787" y="-11.697832"></use>
<use href="#g6-65-drasiojs" x="435.518113" y="-11.697832"></use>
<use href="#g8-41-drasiojs" x="444.29346" y="-11.697832"></use>
<use href="#g3-8-drasiojs" x="451.502449" y="-11.697832"></use>
<use href="#g1-101-drasiojs" x="466.098357" y="-14.71984"></use>
<use href="#g6-72-drasiojs" x="463.45761" y="-11.697832"></use>
<use href="#g5-105-drasiojs" x="473.15659" y="-9.904569"></use>
<use href="#g8-40-drasiojs" x="476.537862" y="-11.697832"></use>
<use href="#g6-66-drasiojs" x="481.090187" y="-11.697832"></use>
<use href="#g8-41-drasiojs" x="490.586448" y="-11.697832"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -200.625 4.3338)">
<use href="#g1-101-drasiojs" x="501.353035" y="-14.71984"></use>
<use href="#g6-72-drasiojs" x="498.712287" y="-11.697832"></use>
<use href="#g5-105-drasiojs" x="508.411268" y="-9.904569"></use>
<use href="#g8-40-drasiojs" x="511.792539" y="-11.697832"></use>
<use href="#g6-83-drasiojs" x="516.344865" y="-11.697832"></use>
<use href="#g5-110-drasiojs" x="524.240188" y="-16.036269"></use>
<use href="#g8-41-drasiojs" x="529.876523" y="-11.697832"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -189.637 4.3338)">
<use href="#g6-58-drasiojs" x="547.782425" y="-11.697832"></use>
<use href="#g6-58-drasiojs" x="553.026584" y="-11.697832"></use>
<use href="#g6-58-drasiojs" x="558.270743" y="-11.697832"></use>
</g>
<path d="M35.738-10.35156H48.91" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M46.66016-13.22263C47.11719-11.49997 48.12891-10.68747 49.148439-10.351533C48.12891-10.019501 47.11719-9.207 46.66016-7.48435" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M106.6172-10.35156H119.7891" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M117.54345-13.22263C117.99658-11.49997 119.00829-10.68747 120.027825-10.351533C119.00829-10.019501 117.99658-9.207 117.54345-7.48435" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M177.5-10.35156H190.66797" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M188.42232-13.22263C188.87545-11.49997 189.88716-10.68747 190.910602-10.351533C189.88716-10.019501 188.87545-9.207 188.42232-7.48435" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M279.0938-10.35156H292.2656" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M290.01959-13.22263C290.47271-11.49997 291.48443-10.68747 292.503962-10.351533C291.48443-10.019501 290.47271-9.207 290.01959-7.48435" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M339.156-10.35156H352.324" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M350.07798-13.22263C350.5311-11.49997 351.54282-10.68747 352.562352-10.351533C351.54282-10.019501 350.5311-9.207 350.07798-7.48435" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
</g>
</svg>
</div>

Because @A@ and @B@ are contractible, the middle term above is zero for all @i \in \mathbb{Z}@, so we have a collection of isomorphisms @\widetilde{H}_i(S^n) \cong \widetilde{H}_{i-1}(S^{i-1})@. Since @\widetilde{H}_0(S^0) = Λ@ and zero otherwise, we find by induction on @n@ the following calculation:
@@
\begin{align*}
\widetilde{H}_i(S^n;Λ) =
\begin{cases}
Λ & \text{if $i = n$} \\
0 & \text{otherwise.}
\end{cases}
\end{align*}
@@

### Relative homology

We now consider pairs @(X,A)@ where @A@ is any subspace of @X@ (including the empty subspace, and the full subspace). We're going to look at homology "modulo @A@", in the sense that any singular simplex whose image lies completely in @A@ is going to be considered as "completely collapsed", i.e. zero as a chain. Formally, we define the **relative @n@-th singular chain group** to be
@@C_n(X,A;Λ) = C_n(X;Λ)/C_n(A;Λ).@@

Because @∂@ carries chains in @A@ to chains in @A@, we obtain a chain complex "modulo @A@" and we can define relative homology as
@@H_n(X,A;Λ) = Z_n(X,A;Λ)/B_n(X,A;Λ).@@

Any pair @(X,A)@ gives an exact sequence of @Λ@-modules
<div style="display:flex;align-items:center;width:100%;margin-top:12px;margin-bottom:12px;">
<svg style="display:bock;margin:0 auto;" height="30.41321333333333px" style="vertical-align:-0.6691693333333333px;" version="1.1" viewBox="-.500002 -22.309908 389.542968 22.80991" width="519.3906239999999px" xmlns="http://www.w3.org/2000/svg">
<defs>
<path d="M1.594022-1.307098C1.617933-1.42665 1.697634-1.729514 1.721544-1.849066C1.833126-2.279452 1.833126-2.287422 2.016438-2.550436C2.279452-2.940971 2.654047-3.291656 3.188045-3.291656C3.474969-3.291656 3.642341-3.124284 3.642341-2.749689C3.642341-2.311333 3.307597-1.40274 3.156164-1.012204C3.052553-.749191 3.052553-.70137 3.052553-.597758C3.052553-.143462 3.427148 .079701 3.769863 .079701C4.550934 .079701 4.877709-1.036115 4.877709-1.139726C4.877709-1.219427 4.813948-1.243337 4.758157-1.243337C4.662516-1.243337 4.646575-1.187547 4.622665-1.107846C4.431382-.454296 4.096638-.143462 3.793773-.143462C3.666252-.143462 3.602491-.223163 3.602491-.406476S3.666252-.765131 3.745953-.964384C3.865504-1.267248 4.216189-2.183811 4.216189-2.630137C4.216189-3.227895 3.801743-3.514819 3.227895-3.514819C2.582316-3.514819 2.16787-3.124284 1.936737-2.82142C1.880946-3.259776 1.530262-3.514819 1.123786-3.514819C.836862-3.514819 .637609-3.331507 .510087-3.084433C.318804-2.709838 .239103-2.311333 .239103-2.295392C.239103-2.223661 .294894-2.191781 .358655-2.191781C.462267-2.191781 .470237-2.223661 .526027-2.430884C.621669-2.82142 .765131-3.291656 1.099875-3.291656C1.307098-3.291656 1.354919-3.092403 1.354919-2.917061C1.354919-2.773599 1.315068-2.622167 1.251308-2.359153C1.235367-2.295392 1.115816-1.825156 1.083935-1.713574L.789041-.518057C.757161-.398506 .70934-.199253 .70934-.167372C.70934 .01594 .860772 .079701 .964384 .079701C1.107846 .079701 1.227397-.01594 1.283188-.111582C1.307098-.159402 1.370859-.430386 1.41071-.597758L1.594022-1.307098Z" id="g5-110-drasiojs"></path>
<path d="M2.199751-.573848C2.199751-.920548 1.912827-1.159651 1.625903-1.159651C1.279203-1.159651 1.0401-.872727 1.0401-.585803C1.0401-.239103 1.327024 0 1.613948 0C1.960648 0 2.199751-.286924 2.199751-.573848Z" id="g6-58-drasiojs"></path>
<path d="M2.331258 .047821C2.331258-.645579 2.10411-1.159651 1.613948-1.159651C1.231382-1.159651 1.0401-.848817 1.0401-.585803S1.219427 0 1.625903 0C1.78132 0 1.912827-.047821 2.020423-.155417C2.044334-.179328 2.056289-.179328 2.068244-.179328C2.092154-.179328 2.092154-.011955 2.092154 .047821C2.092154 .442341 2.020423 1.219427 1.327024 1.996513C1.195517 2.139975 1.195517 2.163885 1.195517 2.187796C1.195517 2.247572 1.255293 2.307347 1.315068 2.307347C1.41071 2.307347 2.331258 1.422665 2.331258 .047821Z" id="g6-59-drasiojs"></path>
<path d="M2.032379-1.327024C1.613948-.621669 1.207472-.382565 .633624-.3467C.502117-.334745 .406476-.334745 .406476-.119552C.406476-.047821 .466252 0 .549938 0C.765131 0 1.303113-.02391 1.518306-.02391C1.865006-.02391 2.247572 0 2.582316 0C2.654047 0 2.797509 0 2.797509-.227148C2.797509-.334745 2.701868-.3467 2.630137-.3467C2.355168-.37061 2.12802-.466252 2.12802-.753176C2.12802-.920548 2.199751-1.052055 2.355168-1.315068L3.263761-2.82142H6.312329C6.324284-2.713823 6.324284-2.618182 6.336239-2.510585C6.372105-2.199751 6.515567-.956413 6.515567-.729265C6.515567-.37061 5.905853-.3467 5.71457-.3467C5.583064-.3467 5.451557-.3467 5.451557-.131507C5.451557 0 5.559153 0 5.630884 0C5.834122 0 6.073225-.02391 6.276463-.02391H6.957908C7.687173-.02391 8.2132 0 8.225156 0C8.308842 0 8.440349 0 8.440349-.227148C8.440349-.3467 8.332752-.3467 8.153425-.3467C7.49589-.3467 7.483935-.454296 7.44807-.812951L6.718804-8.272976C6.694894-8.51208 6.647073-8.53599 6.515567-8.53599C6.396015-8.53599 6.324284-8.51208 6.216687-8.332752L2.032379-1.327024ZM3.466999-3.16812L5.869988-7.185056L6.276463-3.16812H3.466999Z" id="g6-65-drasiojs"></path>
<path d="M8.930511-8.308842C8.930511-8.416438 8.846824-8.416438 8.822914-8.416438S8.751183-8.416438 8.655542-8.296887L7.830635-7.292653C7.412204-8.009963 6.75467-8.416438 5.858032-8.416438C3.275716-8.416438 .597758-5.798257 .597758-2.988792C.597758-.992279 1.996513 .251059 3.741968 .251059C4.698381 .251059 5.535243-.155417 6.228643-.74122C7.268742-1.613948 7.579577-2.773599 7.579577-2.86924C7.579577-2.976837 7.483935-2.976837 7.44807-2.976837C7.340473-2.976837 7.328518-2.905106 7.304608-2.857285C6.75467-.992279 5.140722-.095641 3.945205-.095641C2.677958-.095641 1.578082-.908593 1.578082-2.606227C1.578082-2.988792 1.697634-5.068991 3.048568-6.635118C3.706102-7.400249 4.829888-8.069738 5.965629-8.069738C7.280697-8.069738 7.866501-6.981818 7.866501-5.762391C7.866501-5.451557 7.830635-5.188543 7.830635-5.140722C7.830635-5.033126 7.950187-5.033126 7.986052-5.033126C8.117559-5.033126 8.129514-5.045081 8.177335-5.260274L8.930511-8.308842Z" id="g6-67-drasiojs"></path>
<path d="M5.678705-4.853798L4.554919-7.47198C4.710336-7.758904 5.068991-7.806725 5.212453-7.81868C5.284184-7.81868 5.415691-7.830635 5.415691-8.033873C5.415691-8.16538 5.308095-8.16538 5.236364-8.16538C5.033126-8.16538 4.794022-8.141469 4.590785-8.141469H3.897385C3.16812-8.141469 2.642092-8.16538 2.630137-8.16538C2.534496-8.16538 2.414944-8.16538 2.414944-7.938232C2.414944-7.81868 2.52254-7.81868 2.677958-7.81868C3.371357-7.81868 3.419178-7.699128 3.53873-7.412204L4.961395-4.088667L2.367123-1.315068C1.936737-.848817 1.422665-.394521 .537983-.3467C.394521-.334745 .298879-.334745 .298879-.119552C.298879-.083686 .310834 0 .442341 0C.609714 0 .789041-.02391 .956413-.02391H1.518306C1.900872-.02391 2.319303 0 2.689913 0C2.773599 0 2.917061 0 2.917061-.215193C2.917061-.334745 2.833375-.3467 2.761644-.3467C2.52254-.37061 2.367123-.502117 2.367123-.6934C2.367123-.896638 2.510585-1.0401 2.857285-1.398755L3.921295-2.558406C4.184309-2.833375 4.817933-3.526775 5.080946-3.789788L6.336239-.848817C6.348194-.824907 6.396015-.705355 6.396015-.6934C6.396015-.585803 6.133001-.37061 5.750436-.3467C5.678705-.3467 5.547198-.334745 5.547198-.119552C5.547198 0 5.66675 0 5.726526 0C5.929763 0 6.168867-.02391 6.372105-.02391H7.687173C7.902366-.02391 8.129514 0 8.332752 0C8.416438 0 8.547945 0 8.547945-.227148C8.547945-.3467 8.428394-.3467 8.320797-.3467C7.603487-.358655 7.579577-.418431 7.376339-.860772L5.798257-4.566874L7.316563-6.192777C7.436115-6.312329 7.711083-6.611208 7.81868-6.73076C8.332752-7.268742 8.810959-7.758904 9.779328-7.81868C9.898879-7.830635 10.018431-7.830635 10.018431-8.033873C10.018431-8.16538 9.910834-8.16538 9.863014-8.16538C9.695641-8.16538 9.516314-8.141469 9.348941-8.141469H8.799004C8.416438-8.141469 7.998007-8.16538 7.627397-8.16538C7.543711-8.16538 7.400249-8.16538 7.400249-7.950187C7.400249-7.830635 7.483935-7.81868 7.555666-7.81868C7.746949-7.79477 7.950187-7.699128 7.950187-7.47198L7.938232-7.44807C7.926276-7.364384 7.902366-7.244832 7.770859-7.10137L5.678705-4.853798Z" id="g6-88-drasiojs"></path>
<path d="M4.315816-8.284932C4.244085-8.524035 4.184309-8.53599 4.052802-8.53599C3.945205-8.53599 3.873474-8.51208 3.813699-8.320797L1.494396-1.147696C1.267248-.454296 .777086-.358655 .37061-.3467V0C.884682-.02391 .908593-.02391 1.422665-.02391C1.745455-.02391 2.331258-.02391 2.630137 0V-.3467C2.020423-.358655 1.793275-.6934 1.793275-.956413C1.793275-1.004234 1.793275-1.0401 1.853051-1.219427L3.718057-6.969863L5.678705-.920548C5.738481-.753176 5.738481-.729265 5.738481-.705355C5.738481-.3467 5.116812-.3467 4.817933-.3467V0C5.092902-.02391 6.01345-.02391 6.348194-.02391C6.694894-.02391 7.436115-.02391 7.746949 0V-.3467C7.10137-.3467 6.874222-.3467 6.73076-.800996L4.315816-8.284932Z" id="g8-3-drasiojs"></path>
<path d="M3.88543 2.905106C3.88543 2.86924 3.88543 2.84533 3.682192 2.642092C2.486675 1.43462 1.817186-.537983 1.817186-2.976837C1.817186-5.296139 2.379078-7.292653 3.765878-8.703362C3.88543-8.810959 3.88543-8.834869 3.88543-8.870735C3.88543-8.942466 3.825654-8.966376 3.777833-8.966376C3.622416-8.966376 2.642092-8.105604 2.056289-6.933998C1.446575-5.726526 1.171606-4.447323 1.171606-2.976837C1.171606-1.912827 1.338979-.490162 1.960648 .789041C2.666002 2.223661 3.646326 3.000747 3.777833 3.000747C3.825654 3.000747 3.88543 2.976837 3.88543 2.905106Z" id="g8-40-drasiojs"></path>
<path d="M3.371357-2.976837C3.371357-3.88543 3.251806-5.36787 2.582316-6.75467C1.876961-8.18929 .896638-8.966376 .765131-8.966376C.71731-8.966376 .657534-8.942466 .657534-8.870735C.657534-8.834869 .657534-8.810959 .860772-8.607721C2.056289-7.400249 2.725778-5.427646 2.725778-2.988792C2.725778-.669489 2.163885 1.327024 .777086 2.737733C.657534 2.84533 .657534 2.86924 .657534 2.905106C.657534 2.976837 .71731 3.000747 .765131 3.000747C.920548 3.000747 1.900872 2.139975 2.486675 .968369C3.096389-.251059 3.371357-1.542217 3.371357-2.976837Z" id="g8-41-drasiojs"></path>
<path d="M5.355915-3.825654C5.355915-4.817933 5.296139-5.786301 4.865753-6.694894C4.375592-7.687173 3.514819-7.950187 2.929016-7.950187C2.235616-7.950187 1.3868-7.603487 .944458-6.611208C.609714-5.858032 .490162-5.116812 .490162-3.825654C.490162-2.666002 .573848-1.793275 1.004234-.944458C1.470486-.035866 2.295392 .251059 2.917061 .251059C3.957161 .251059 4.554919-.37061 4.901619-1.06401C5.332005-1.960648 5.355915-3.132254 5.355915-3.825654ZM2.917061 .011955C2.534496 .011955 1.75741-.203238 1.530262-1.506351C1.398755-2.223661 1.398755-3.132254 1.398755-3.969116C1.398755-4.94944 1.398755-5.834122 1.590037-6.539477C1.793275-7.340473 2.402989-7.711083 2.917061-7.711083C3.371357-7.711083 4.064757-7.436115 4.291905-6.40797C4.447323-5.726526 4.447323-4.782067 4.447323-3.969116C4.447323-3.16812 4.447323-2.259527 4.315816-1.530262C4.088667-.215193 3.335492 .011955 2.917061 .011955Z" id="g8-48-drasiojs"></path>
<path d="M2.199751-4.578829C2.199751-4.901619 1.924782-5.152677 1.625903-5.152677C1.279203-5.152677 1.0401-4.877709 1.0401-4.578829C1.0401-4.220174 1.338979-3.993026 1.613948-3.993026C1.936737-3.993026 2.199751-4.244085 2.199751-4.578829ZM1.996513-.119552C1.996513 .298879 1.996513 1.147696 1.267248 2.044334C1.195517 2.139975 1.195517 2.163885 1.195517 2.187796C1.195517 2.247572 1.255293 2.307347 1.315068 2.307347C1.398755 2.307347 2.235616 1.422665 2.235616 .02391C2.235616-.418431 2.199751-1.159651 1.613948-1.159651C1.267248-1.159651 1.0401-.896638 1.0401-.585803C1.0401-.263014 1.267248 0 1.625903 0C1.853051 0 1.936737-.071731 1.996513-.119552Z" id="g8-59-drasiojs"></path>
</defs>
<g id="page199-drasiojs">
<g fill="currentColor" transform="matrix(1 0 0 1 -168.788 2.98883)">
<use href="#g8-48-drasiojs" x="202.345346" y="-10.35287"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -188.492 2.98883)">
<use href="#g6-67-drasiojs" x="266.291112" y="-10.35287"></use>
<use href="#g5-110-drasiojs" x="274.666157" y="-8.559607"></use>
<use href="#g8-40-drasiojs" x="280.302492" y="-10.35287"></use>
<use href="#g6-65-drasiojs" x="284.854818" y="-10.35287"></use>
<use href="#g8-59-drasiojs" x="293.630164" y="-10.35287"></use>
<use href="#g8-3-drasiojs" x="298.874323" y="-10.35287"></use>
<use href="#g8-41-drasiojs" x="306.999338" y="-10.35287"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -189.432 2.98883)">
<use href="#g6-67-drasiojs" x="350.880518" y="-10.35287"></use>
<use href="#g5-110-drasiojs" x="359.255563" y="-8.559607"></use>
<use href="#g8-40-drasiojs" x="364.891898" y="-10.35287"></use>
<use href="#g6-88-drasiojs" x="369.444224" y="-10.35287"></use>
<use href="#g8-59-drasiojs" x="380.099331" y="-10.35287"></use>
<use href="#g8-3-drasiojs" x="385.34349" y="-10.35287"></use>
<use href="#g8-41-drasiojs" x="393.468505" y="-10.35287"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -196.117 2.98883)">
<use href="#g6-67-drasiojs" x="443.094393" y="-10.35287"></use>
<use href="#g5-110-drasiojs" x="451.469438" y="-8.559607"></use>
<use href="#g8-40-drasiojs" x="457.105773" y="-10.35287"></use>
<use href="#g6-88-drasiojs" x="461.658099" y="-10.35287"></use>
<use href="#g6-59-drasiojs" x="471.662874" y="-10.35287"></use>
<use href="#g6-65-drasiojs" x="476.907033" y="-10.35287"></use>
<use href="#g8-59-drasiojs" x="485.68238" y="-10.35287"></use>
<use href="#g8-3-drasiojs" x="490.926539" y="-10.35287"></use>
<use href="#g8-41-drasiojs" x="499.051553" y="-10.35287"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -170.414 2.98883)">
<use href="#g8-48-drasiojs" x="516.290458" y="-10.35287"></use>
<use href="#g6-58-drasiojs" x="522.143448" y="-10.35287"></use>
</g>
<path d="M44.758-10.351563H71.977" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M69.72661-13.22266C70.17973-11.5 71.19536-10.6875 72.214891-10.351563C71.19536-10.019532 70.17973-9.20703 69.72661-7.48438" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M128.4063-10.351563H155.625" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M153.37854-13.22266C153.83167-11.5 154.84339-10.6875 155.862917-10.351563C154.84339-10.019532 153.83167-9.20703 153.37854-7.48438" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M213.9375-10.351563H241.1563" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M238.90652-13.22266C239.36355-11.5 240.37527-10.6875 241.394802-10.351563C240.37527-10.019532 239.36355-9.20703 238.90652-7.48438" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M312.836-10.351563H340.055" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M337.8081-13.22266C338.26122-11.5 339.27294-10.6875 340.292474-10.351563C339.27294-10.019532 338.26122-9.20703 337.8081-7.48438" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
</g>
</svg>
</div>

From the general theory of abelian categories, we obtain from it a **long exact sequence in homology**:
<div style="display:flex;align-items:center;width:100%;">
<svg style="display:bock;margin:0 auto;" height="141.67343599999998px" style="vertical-align:-0.6691693333333333px;" version="1.1" viewBox="-.500002 -105.755076 389.542968 106.255077" width="519.3906239999999px" xmlns="http://www.w3.org/2000/svg">
<defs>
<path d="M4.315816-8.284932C4.244085-8.524035 4.184309-8.53599 4.052802-8.53599C3.945205-8.53599 3.873474-8.51208 3.813699-8.320797L1.494396-1.147696C1.267248-.454296 .777086-.358655 .37061-.3467V0C.884682-.02391 .908593-.02391 1.422665-.02391C1.745455-.02391 2.331258-.02391 2.630137 0V-.3467C2.020423-.358655 1.793275-.6934 1.793275-.956413C1.793275-1.004234 1.793275-1.0401 1.853051-1.219427L3.718057-6.969863L5.678705-.920548C5.738481-.753176 5.738481-.729265 5.738481-.705355C5.738481-.3467 5.116812-.3467 4.817933-.3467V0C5.092902-.02391 6.01345-.02391 6.348194-.02391C6.694894-.02391 7.436115-.02391 7.746949 0V-.3467C7.10137-.3467 6.874222-.3467 6.73076-.800996L4.315816-8.284932Z" id="g8-3-drasiojs"></path>
<path d="M3.88543 2.905106C3.88543 2.86924 3.88543 2.84533 3.682192 2.642092C2.486675 1.43462 1.817186-.537983 1.817186-2.976837C1.817186-5.296139 2.379078-7.292653 3.765878-8.703362C3.88543-8.810959 3.88543-8.834869 3.88543-8.870735C3.88543-8.942466 3.825654-8.966376 3.777833-8.966376C3.622416-8.966376 2.642092-8.105604 2.056289-6.933998C1.446575-5.726526 1.171606-4.447323 1.171606-2.976837C1.171606-1.912827 1.338979-.490162 1.960648 .789041C2.666002 2.223661 3.646326 3.000747 3.777833 3.000747C3.825654 3.000747 3.88543 2.976837 3.88543 2.905106Z" id="g8-40-drasiojs"></path>
<path d="M3.371357-2.976837C3.371357-3.88543 3.251806-5.36787 2.582316-6.75467C1.876961-8.18929 .896638-8.966376 .765131-8.966376C.71731-8.966376 .657534-8.942466 .657534-8.870735C.657534-8.834869 .657534-8.810959 .860772-8.607721C2.056289-7.400249 2.725778-5.427646 2.725778-2.988792C2.725778-.669489 2.163885 1.327024 .777086 2.737733C.657534 2.84533 .657534 2.86924 .657534 2.905106C.657534 2.976837 .71731 3.000747 .765131 3.000747C.920548 3.000747 1.900872 2.139975 2.486675 .968369C3.096389-.251059 3.371357-1.542217 3.371357-2.976837Z" id="g8-41-drasiojs"></path>
<path d="M2.199751-4.578829C2.199751-4.901619 1.924782-5.152677 1.625903-5.152677C1.279203-5.152677 1.0401-4.877709 1.0401-4.578829C1.0401-4.220174 1.338979-3.993026 1.613948-3.993026C1.936737-3.993026 2.199751-4.244085 2.199751-4.578829ZM1.996513-.119552C1.996513 .298879 1.996513 1.147696 1.267248 2.044334C1.195517 2.139975 1.195517 2.163885 1.195517 2.187796C1.195517 2.247572 1.255293 2.307347 1.315068 2.307347C1.398755 2.307347 2.235616 1.422665 2.235616 .02391C2.235616-.418431 2.199751-1.159651 1.613948-1.159651C1.267248-1.159651 1.0401-.896638 1.0401-.585803C1.0401-.263014 1.267248 0 1.625903 0C1.853051 0 1.936737-.071731 1.996513-.119552Z" id="g8-59-drasiojs"></path>
<path d="M3.474969-1.809215H5.818182C5.929763-1.809215 6.105106-1.809215 6.105106-1.992528S5.929763-2.175841 5.818182-2.175841H3.474969V-4.527024C3.474969-4.638605 3.474969-4.813948 3.291656-4.813948S3.108344-4.638605 3.108344-4.527024V-2.175841H.757161C.645579-2.175841 .470237-2.175841 .470237-1.992528S.645579-1.809215 .757161-1.809215H3.108344V.541968C3.108344 .653549 3.108344 .828892 3.291656 .828892S3.474969 .653549 3.474969 .541968V-1.809215Z" id="g7-43-drasiojs"></path>
<path d="M2.502615-5.076961C2.502615-5.292154 2.486675-5.300125 2.271482-5.300125C1.944707-4.98132 1.522291-4.790037 .765131-4.790037V-4.527024C.980324-4.527024 1.41071-4.527024 1.872976-4.742217V-.653549C1.872976-.358655 1.849066-.263014 1.091905-.263014H.812951V0C1.139726-.02391 1.825156-.02391 2.183811-.02391S3.235866-.02391 3.56264 0V-.263014H3.283686C2.526526-.263014 2.502615-.358655 2.502615-.653549V-5.076961Z" id="g7-49-drasiojs"></path>
<path d="M5.571108-1.809215C5.69863-1.809215 5.873973-1.809215 5.873973-1.992528S5.69863-2.175841 5.571108-2.175841H1.004234C.876712-2.175841 .70137-2.175841 .70137-1.992528S.876712-1.809215 1.004234-1.809215H5.571108Z" id="g2-0-drasiojs"></path>
<path d="M1.594022-1.307098C1.617933-1.42665 1.697634-1.729514 1.721544-1.849066C1.833126-2.279452 1.833126-2.287422 2.016438-2.550436C2.279452-2.940971 2.654047-3.291656 3.188045-3.291656C3.474969-3.291656 3.642341-3.124284 3.642341-2.749689C3.642341-2.311333 3.307597-1.40274 3.156164-1.012204C3.052553-.749191 3.052553-.70137 3.052553-.597758C3.052553-.143462 3.427148 .079701 3.769863 .079701C4.550934 .079701 4.877709-1.036115 4.877709-1.139726C4.877709-1.219427 4.813948-1.243337 4.758157-1.243337C4.662516-1.243337 4.646575-1.187547 4.622665-1.107846C4.431382-.454296 4.096638-.143462 3.793773-.143462C3.666252-.143462 3.602491-.223163 3.602491-.406476S3.666252-.765131 3.745953-.964384C3.865504-1.267248 4.216189-2.183811 4.216189-2.630137C4.216189-3.227895 3.801743-3.514819 3.227895-3.514819C2.582316-3.514819 2.16787-3.124284 1.936737-2.82142C1.880946-3.259776 1.530262-3.514819 1.123786-3.514819C.836862-3.514819 .637609-3.331507 .510087-3.084433C.318804-2.709838 .239103-2.311333 .239103-2.295392C.239103-2.223661 .294894-2.191781 .358655-2.191781C.462267-2.191781 .470237-2.223661 .526027-2.430884C.621669-2.82142 .765131-3.291656 1.099875-3.291656C1.307098-3.291656 1.354919-3.092403 1.354919-2.917061C1.354919-2.773599 1.315068-2.622167 1.251308-2.359153C1.235367-2.295392 1.115816-1.825156 1.083935-1.713574L.789041-.518057C.757161-.398506 .70934-.199253 .70934-.167372C.70934 .01594 .860772 .079701 .964384 .079701C1.107846 .079701 1.227397-.01594 1.283188-.111582C1.307098-.159402 1.370859-.430386 1.41071-.597758L1.594022-1.307098Z" id="g5-110-drasiojs"></path>
<path d="M2.199751-.573848C2.199751-.920548 1.912827-1.159651 1.625903-1.159651C1.279203-1.159651 1.0401-.872727 1.0401-.585803C1.0401-.239103 1.327024 0 1.613948 0C1.960648 0 2.199751-.286924 2.199751-.573848Z" id="g6-58-drasiojs"></path>
<path d="M2.331258 .047821C2.331258-.645579 2.10411-1.159651 1.613948-1.159651C1.231382-1.159651 1.0401-.848817 1.0401-.585803S1.219427 0 1.625903 0C1.78132 0 1.912827-.047821 2.020423-.155417C2.044334-.179328 2.056289-.179328 2.068244-.179328C2.092154-.179328 2.092154-.011955 2.092154 .047821C2.092154 .442341 2.020423 1.219427 1.327024 1.996513C1.195517 2.139975 1.195517 2.163885 1.195517 2.187796C1.195517 2.247572 1.255293 2.307347 1.315068 2.307347C1.41071 2.307347 2.331258 1.422665 2.331258 .047821Z" id="g6-59-drasiojs"></path>
<path d="M2.032379-1.327024C1.613948-.621669 1.207472-.382565 .633624-.3467C.502117-.334745 .406476-.334745 .406476-.119552C.406476-.047821 .466252 0 .549938 0C.765131 0 1.303113-.02391 1.518306-.02391C1.865006-.02391 2.247572 0 2.582316 0C2.654047 0 2.797509 0 2.797509-.227148C2.797509-.334745 2.701868-.3467 2.630137-.3467C2.355168-.37061 2.12802-.466252 2.12802-.753176C2.12802-.920548 2.199751-1.052055 2.355168-1.315068L3.263761-2.82142H6.312329C6.324284-2.713823 6.324284-2.618182 6.336239-2.510585C6.372105-2.199751 6.515567-.956413 6.515567-.729265C6.515567-.37061 5.905853-.3467 5.71457-.3467C5.583064-.3467 5.451557-.3467 5.451557-.131507C5.451557 0 5.559153 0 5.630884 0C5.834122 0 6.073225-.02391 6.276463-.02391H6.957908C7.687173-.02391 8.2132 0 8.225156 0C8.308842 0 8.440349 0 8.440349-.227148C8.440349-.3467 8.332752-.3467 8.153425-.3467C7.49589-.3467 7.483935-.454296 7.44807-.812951L6.718804-8.272976C6.694894-8.51208 6.647073-8.53599 6.515567-8.53599C6.396015-8.53599 6.324284-8.51208 6.216687-8.332752L2.032379-1.327024ZM3.466999-3.16812L5.869988-7.185056L6.276463-3.16812H3.466999Z" id="g6-65-drasiojs"></path>
<path d="M8.942466-7.292653C9.050062-7.699128 9.073973-7.81868 9.92279-7.81868C10.137983-7.81868 10.257534-7.81868 10.257534-8.033873C10.257534-8.16538 10.149938-8.16538 10.078207-8.16538C9.863014-8.16538 9.611955-8.141469 9.384807-8.141469H7.974097C7.746949-8.141469 7.49589-8.16538 7.268742-8.16538C7.185056-8.16538 7.041594-8.16538 7.041594-7.938232C7.041594-7.81868 7.12528-7.81868 7.352428-7.81868C8.069738-7.81868 8.069738-7.723039 8.069738-7.591532C8.069738-7.567621 8.069738-7.49589 8.021918-7.316563L7.292653-4.423412H3.682192L4.399502-7.292653C4.507098-7.699128 4.531009-7.81868 5.379826-7.81868C5.595019-7.81868 5.71457-7.81868 5.71457-8.033873C5.71457-8.16538 5.606974-8.16538 5.535243-8.16538C5.32005-8.16538 5.068991-8.141469 4.841843-8.141469H3.431133C3.203985-8.141469 2.952927-8.16538 2.725778-8.16538C2.642092-8.16538 2.49863-8.16538 2.49863-7.938232C2.49863-7.81868 2.582316-7.81868 2.809465-7.81868C3.526775-7.81868 3.526775-7.723039 3.526775-7.591532C3.526775-7.567621 3.526775-7.49589 3.478954-7.316563L1.865006-.884682C1.75741-.466252 1.733499-.3467 .908593-.3467C.633624-.3467 .549938-.3467 .549938-.119552C.549938 0 .681445 0 .71731 0C.932503 0 1.183562-.02391 1.41071-.02391H2.82142C3.048568-.02391 3.299626 0 3.526775 0C3.622416 0 3.753923 0 3.753923-.227148C3.753923-.3467 3.646326-.3467 3.466999-.3467C2.737733-.3467 2.737733-.442341 2.737733-.561893C2.737733-.573848 2.737733-.657534 2.761644-.753176L3.58655-4.076712H7.208966C7.005729-3.287671 6.396015-.789041 6.372105-.71731C6.240598-.358655 6.049315-.358655 5.34396-.3467C5.200498-.3467 5.092902-.3467 5.092902-.119552C5.092902 0 5.224408 0 5.260274 0C5.475467 0 5.726526-.02391 5.953674-.02391H7.364384C7.591532-.02391 7.84259 0 8.069738 0C8.16538 0 8.296887 0 8.296887-.227148C8.296887-.3467 8.18929-.3467 8.009963-.3467C7.280697-.3467 7.280697-.442341 7.280697-.561893C7.280697-.573848 7.280697-.657534 7.304608-.753176L8.942466-7.292653Z" id="g6-72-drasiojs"></path>
<path d="M5.678705-4.853798L4.554919-7.47198C4.710336-7.758904 5.068991-7.806725 5.212453-7.81868C5.284184-7.81868 5.415691-7.830635 5.415691-8.033873C5.415691-8.16538 5.308095-8.16538 5.236364-8.16538C5.033126-8.16538 4.794022-8.141469 4.590785-8.141469H3.897385C3.16812-8.141469 2.642092-8.16538 2.630137-8.16538C2.534496-8.16538 2.414944-8.16538 2.414944-7.938232C2.414944-7.81868 2.52254-7.81868 2.677958-7.81868C3.371357-7.81868 3.419178-7.699128 3.53873-7.412204L4.961395-4.088667L2.367123-1.315068C1.936737-.848817 1.422665-.394521 .537983-.3467C.394521-.334745 .298879-.334745 .298879-.119552C.298879-.083686 .310834 0 .442341 0C.609714 0 .789041-.02391 .956413-.02391H1.518306C1.900872-.02391 2.319303 0 2.689913 0C2.773599 0 2.917061 0 2.917061-.215193C2.917061-.334745 2.833375-.3467 2.761644-.3467C2.52254-.37061 2.367123-.502117 2.367123-.6934C2.367123-.896638 2.510585-1.0401 2.857285-1.398755L3.921295-2.558406C4.184309-2.833375 4.817933-3.526775 5.080946-3.789788L6.336239-.848817C6.348194-.824907 6.396015-.705355 6.396015-.6934C6.396015-.585803 6.133001-.37061 5.750436-.3467C5.678705-.3467 5.547198-.334745 5.547198-.119552C5.547198 0 5.66675 0 5.726526 0C5.929763 0 6.168867-.02391 6.372105-.02391H7.687173C7.902366-.02391 8.129514 0 8.332752 0C8.416438 0 8.547945 0 8.547945-.227148C8.547945-.3467 8.428394-.3467 8.320797-.3467C7.603487-.358655 7.579577-.418431 7.376339-.860772L5.798257-4.566874L7.316563-6.192777C7.436115-6.312329 7.711083-6.611208 7.81868-6.73076C8.332752-7.268742 8.810959-7.758904 9.779328-7.81868C9.898879-7.830635 10.018431-7.830635 10.018431-8.033873C10.018431-8.16538 9.910834-8.16538 9.863014-8.16538C9.695641-8.16538 9.516314-8.141469 9.348941-8.141469H8.799004C8.416438-8.141469 7.998007-8.16538 7.627397-8.16538C7.543711-8.16538 7.400249-8.16538 7.400249-7.950187C7.400249-7.830635 7.483935-7.81868 7.555666-7.81868C7.746949-7.79477 7.950187-7.699128 7.950187-7.47198L7.938232-7.44807C7.926276-7.364384 7.902366-7.244832 7.770859-7.10137L5.678705-4.853798Z" id="g6-88-drasiojs"></path>
</defs>
<g id="page200-drasiojs">
<g fill="currentColor" transform="matrix(1 0 0 1 -169.1153 44.7659)">
<use href="#g6-58-drasiojs" x="206.288841" y="-135.682475"></use>
<use href="#g6-58-drasiojs" x="211.532999" y="-135.682475"></use>
<use href="#g6-58-drasiojs" x="216.777158" y="-135.682475"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -190.9482 44.7659)">
<use href="#g6-72-drasiojs" x="266.203276" y="-135.682475"></use>
<use href="#g5-110-drasiojs" x="275.902256" y="-133.889212"></use>
<use href="#g2-0-drasiojs" x="281.040459" y="-133.889212"></use>
<use href="#g7-49-drasiojs" x="287.626965" y="-133.889212"></use>
<use href="#g8-40-drasiojs" x="292.35928" y="-135.682475"></use>
<use href="#g6-65-drasiojs" x="296.911606" y="-135.682475"></use>
<use href="#g8-59-drasiojs" x="305.686953" y="-135.682475"></use>
<use href="#g8-3-drasiojs" x="310.931111" y="-135.682475"></use>
<use href="#g8-41-drasiojs" x="319.056126" y="-135.682475"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -191.888 44.7659)">
<use href="#g6-72-drasiojs" x="348.890179" y="-135.682475"></use>
<use href="#g5-110-drasiojs" x="358.589159" y="-133.889212"></use>
<use href="#g2-0-drasiojs" x="363.727362" y="-133.889212"></use>
<use href="#g7-49-drasiojs" x="370.313868" y="-133.889212"></use>
<use href="#g8-40-drasiojs" x="375.046183" y="-135.682475"></use>
<use href="#g6-88-drasiojs" x="379.598509" y="-135.682475"></use>
<use href="#g8-59-drasiojs" x="390.253617" y="-135.682475"></use>
<use href="#g8-3-drasiojs" x="395.497776" y="-135.682475"></use>
<use href="#g8-41-drasiojs" x="403.62279" y="-135.682475"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -198.573 44.7659)">
<use href="#g6-72-drasiojs" x="439.201536" y="-135.682475"></use>
<use href="#g5-110-drasiojs" x="448.900516" y="-133.889212"></use>
<use href="#g2-0-drasiojs" x="454.038718" y="-133.889212"></use>
<use href="#g7-49-drasiojs" x="460.625225" y="-133.889212"></use>
<use href="#g8-40-drasiojs" x="465.35754" y="-135.682475"></use>
<use href="#g6-88-drasiojs" x="469.909866" y="-135.682475"></use>
<use href="#g6-59-drasiojs" x="479.914641" y="-135.682475"></use>
<use href="#g6-65-drasiojs" x="485.1588" y="-135.682475"></use>
<use href="#g8-59-drasiojs" x="493.934147" y="-135.682475"></use>
<use href="#g8-3-drasiojs" x="499.178306" y="-135.682475"></use>
<use href="#g8-41-drasiojs" x="507.30332" y="-135.682475"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -185.5378 44.7659)">
<use href="#g6-72-drasiojs" x="266.203276" y="-93.90594"></use>
<use href="#g5-110-drasiojs" x="275.902256" y="-92.112677"></use>
<use href="#g8-40-drasiojs" x="281.538591" y="-93.90594"></use>
<use href="#g6-65-drasiojs" x="286.090916" y="-93.90594"></use>
<use href="#g8-59-drasiojs" x="294.866263" y="-93.90594"></use>
<use href="#g8-3-drasiojs" x="300.110422" y="-93.90594"></use>
<use href="#g8-41-drasiojs" x="308.235436" y="-93.90594"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -186.478 44.7659)">
<use href="#g6-72-drasiojs" x="348.890179" y="-93.90594"></use>
<use href="#g5-110-drasiojs" x="358.589159" y="-92.112677"></use>
<use href="#g8-40-drasiojs" x="364.225494" y="-93.90594"></use>
<use href="#g6-88-drasiojs" x="368.777819" y="-93.90594"></use>
<use href="#g8-59-drasiojs" x="379.432927" y="-93.90594"></use>
<use href="#g8-3-drasiojs" x="384.677086" y="-93.90594"></use>
<use href="#g8-41-drasiojs" x="392.8021" y="-93.90594"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -193.162 44.7659)">
<use href="#g6-72-drasiojs" x="439.201536" y="-93.90594"></use>
<use href="#g5-110-drasiojs" x="448.900516" y="-92.112677"></use>
<use href="#g8-40-drasiojs" x="454.53685" y="-93.90594"></use>
<use href="#g6-88-drasiojs" x="459.089176" y="-93.90594"></use>
<use href="#g6-59-drasiojs" x="469.093952" y="-93.90594"></use>
<use href="#g6-65-drasiojs" x="474.338111" y="-93.90594"></use>
<use href="#g8-59-drasiojs" x="483.113457" y="-93.90594"></use>
<use href="#g8-3-drasiojs" x="488.357616" y="-93.90594"></use>
<use href="#g8-41-drasiojs" x="496.482631" y="-93.90594"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -190.9482 44.7659)">
<use href="#g6-72-drasiojs" x="266.203276" y="-52.129405"></use>
<use href="#g5-110-drasiojs" x="275.902256" y="-50.336142"></use>
<use href="#g7-43-drasiojs" x="281.040459" y="-50.336142"></use>
<use href="#g7-49-drasiojs" x="287.626965" y="-50.336142"></use>
<use href="#g8-40-drasiojs" x="292.35928" y="-52.129405"></use>
<use href="#g6-65-drasiojs" x="296.911606" y="-52.129405"></use>
<use href="#g8-59-drasiojs" x="305.686953" y="-52.129405"></use>
<use href="#g8-3-drasiojs" x="310.931111" y="-52.129405"></use>
<use href="#g8-41-drasiojs" x="319.056126" y="-52.129405"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -191.888 44.7659)">
<use href="#g6-72-drasiojs" x="348.890179" y="-52.129405"></use>
<use href="#g5-110-drasiojs" x="358.589159" y="-50.336142"></use>
<use href="#g7-43-drasiojs" x="363.727362" y="-50.336142"></use>
<use href="#g7-49-drasiojs" x="370.313868" y="-50.336142"></use>
<use href="#g8-40-drasiojs" x="375.046183" y="-52.129405"></use>
<use href="#g6-88-drasiojs" x="379.598509" y="-52.129405"></use>
<use href="#g8-59-drasiojs" x="390.253617" y="-52.129405"></use>
<use href="#g8-3-drasiojs" x="395.497776" y="-52.129405"></use>
<use href="#g8-41-drasiojs" x="403.62279" y="-52.129405"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -198.573 44.7659)">
<use href="#g6-72-drasiojs" x="439.201536" y="-52.129405"></use>
<use href="#g5-110-drasiojs" x="448.900516" y="-50.336142"></use>
<use href="#g7-43-drasiojs" x="454.038718" y="-50.336142"></use>
<use href="#g7-49-drasiojs" x="460.625225" y="-50.336142"></use>
<use href="#g8-40-drasiojs" x="465.35754" y="-52.129405"></use>
<use href="#g6-88-drasiojs" x="469.909866" y="-52.129405"></use>
<use href="#g6-59-drasiojs" x="479.914641" y="-52.129405"></use>
<use href="#g6-65-drasiojs" x="485.1588" y="-52.129405"></use>
<use href="#g8-59-drasiojs" x="493.934147" y="-52.129405"></use>
<use href="#g8-3-drasiojs" x="499.178306" y="-52.129405"></use>
<use href="#g8-41-drasiojs" x="507.30332" y="-52.129405"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -169.115 44.7659)">
<use href="#g6-58-drasiojs" x="506.740425" y="-52.129405"></use>
<use href="#g6-58-drasiojs" x="511.984584" y="-52.129405"></use>
<use href="#g6-58-drasiojs" x="517.228742" y="-52.129405"></use>
</g>
<path d="M56.262-93.9063H69.43" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M67.18364-96.77738C67.63676-95.05472 68.64848-94.242224 69.668015-93.906286C68.64848-93.570349 67.63676-92.75785 67.18364-91.0391" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M138.0078-93.9063H151.1797" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M148.92986-96.77738C149.38689-95.05472 150.39861-94.242224 151.418137-93.906286C150.39861-93.570349 149.38689-92.75785 148.92986-91.0391" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M221.6367-93.9063H234.8047" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M232.55892-96.77738C233.01205-95.05472 234.02767-94.242224 235.047205-93.906286C234.02767-93.570349 233.01205-92.75785 232.55892-91.0391" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M318.633-93.9063H324.941C327.145-93.9063 328.93-92.1211 328.93-89.9219V-77.0039C328.93-74.8008 327.145-73.0195 324.941-73.0195H190.63282C188.42969-73.0195 184.86329-73.0195 182.6602-73.0195H69.008C66.809-73.0195 65.023-71.2344 65.023-69.0313V-56.11328C65.023-53.91406 66.809-52.128908 69.008-52.128908H74.84" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M72.59378-55C73.04691-53.27735 74.05862-52.464845 75.082062-52.128908C74.05862-51.79297 73.04691-50.98047 72.59378-49.26172" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M132.5977-52.128908H156.5898" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M154.3396-55C154.79663-53.27735 155.80835-52.464845 156.827878-52.128908C155.80835-51.79297 154.79663-50.98047 154.3396-49.26172" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M216.2266-52.128908H240.2188" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M237.96866-55C238.42179-53.27735 239.43741-52.464845 240.456946-52.128908C239.43741-51.79297 238.42179-50.98047 237.96866-49.26172" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M313.223-52.128908H319.531C321.734-52.128908 323.52-50.34375 323.52-48.14453V-35.2266C323.52-33.0234 321.734-31.2422 319.531-31.2422H190.63282C188.42969-31.2422 184.86329-31.2422 182.6602-31.2422H63.598C61.398-31.2422 59.613-29.457 59.613-27.2539V-14.3359C59.613-12.1367 61.398-10.3516 63.598-10.3516H69.43" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M67.18364-13.22263C67.63676-11.49997 68.64848-10.687471 69.668015-10.351533C68.64848-10.019502 67.63676-9.2031 67.18364-7.48435" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M138.0078-10.3516H151.1797" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M148.92986-13.22263C149.38689-11.49997 150.39861-10.687471 151.418137-10.351533C150.39861-10.019502 149.38689-9.2031 148.92986-7.48435" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M221.6367-10.3516H234.8047" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M232.55892-13.22263C233.01205-11.49997 234.02767-10.687471 235.047205-10.351533C234.02767-10.019502 233.01205-9.2031 232.55892-7.48435" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M318.633-10.3516H331.805" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M329.55484-13.22263C330.01187-11.49997 331.02359-10.687471 332.043122-10.351533C331.02359-10.019502 330.01187-9.2031 329.55484-7.48435" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
</g>
</svg>
</div>

This long exact sequence also exists for reduced homology.

An important tool for working with homology is the **excision theorem**: let @A@ and @B@ be two subspaces of @X@ such that their interior cover @X@; then the inclusion @(B,A\cap B) \hookrightarrow (X,A)@ induces isomorphisms
@@H_n(B,A\cap B) \cong H_n(X,A)@@
for all @n \in \mathbb{Z}@. Equivalently, for any subspaces @Z \subseteq A \subseteq X@ such that the closure of @Z@ is contained in the interior of @A@, the obvious inclusion induces isomorphisms
@@H_n(X-Z, A-Z; Λ) \cong H_n(X, A; Λ).@@
This version of the statement is what justifies the name "excision", since it gives us conditions under which we may excise @Z@ from @X@ without changing the homology groups. That is insanely powerful. For instance, here's a proof of the so-called Brouwer's invariance of domain: if @U \subseteq \mathbb{R}^m@ and @V \subseteq \mathbb{R}^n@ are two nonempty homeomorphic open sets, then @m=n@. The idea of the proof is to look at what happens locally around a point, so we define **local homology groups** around some point @p \in X@ by
@@H_{n,p}(X;Λ) = H_n(X,X-\{p\};Λ).@@
Back to the proof. Let @f : U \to V@ be a homeomorphism and pick some point @x \in U@. Then, by excision, we have @H_{n,x}(U) \cong H_{n,x}(\mathbb{R}^m)@. (Hint: in the excision theorem, pick @A@ to be the complement of @\{x\}@ and pick @B@ to be @U@). The long exact sequence for the pair @(\mathbb{R}^m,\mathbb{R}^m-\{x\})@ looks like:
<div style="display:flex;align-items:center;width:100%;">
<svg style="display:bock;margin:0 auto;" height="46.82570533333333px" style="vertical-align:-0.6691693333333333px;" version="1.1" viewBox="-.500002 -34.619277 389.542968 35.119279" width="519.3906239999999px" xmlns="http://www.w3.org/2000/svg">
<defs>
<path d="M7.878456-2.749689C8.081694-2.749689 8.296887-2.749689 8.296887-2.988792S8.081694-3.227895 7.878456-3.227895H1.41071C1.207472-3.227895 .992279-3.227895 .992279-2.988792S1.207472-2.749689 1.41071-2.749689H7.878456Z" id="g3-0-drasiojs"></path>
<path d="M3.383313-7.376339C3.383313-7.854545 3.694147-8.619676 4.99726-8.703362C5.057036-8.715318 5.104857-8.763138 5.104857-8.834869C5.104857-8.966376 5.009215-8.966376 4.877709-8.966376C3.682192-8.966376 2.594271-8.356663 2.582316-7.47198V-4.746202C2.582316-4.27995 2.582316-3.897385 2.10411-3.502864C1.685679-3.156164 1.231382-3.132254 .968369-3.120299C.908593-3.108344 .860772-3.060523 .860772-2.988792C.860772-2.86924 .932503-2.86924 1.052055-2.857285C1.841096-2.809465 2.414944-2.379078 2.546451-1.793275C2.582316-1.661768 2.582316-1.637858 2.582316-1.207472V1.159651C2.582316 1.661768 2.582316 2.044334 3.156164 2.49863C3.622416 2.857285 4.411457 2.988792 4.877709 2.988792C5.009215 2.988792 5.104857 2.988792 5.104857 2.857285C5.104857 2.737733 5.033126 2.737733 4.913574 2.725778C4.160399 2.677958 3.574595 2.295392 3.419178 1.685679C3.383313 1.578082 3.383313 1.554172 3.383313 1.123786V-1.3868C3.383313-1.936737 3.287671-2.139975 2.905106-2.52254C2.654047-2.773599 2.307347-2.893151 1.972603-2.988792C2.952927-3.263761 3.383313-3.813699 3.383313-4.507098V-7.376339Z" id="g3-102-drasiojs"></path>
<path d="M2.582316 1.398755C2.582316 1.876961 2.271482 2.642092 .968369 2.725778C.908593 2.737733 .860772 2.785554 .860772 2.857285C.860772 2.988792 .992279 2.988792 1.099875 2.988792C2.259527 2.988792 3.371357 2.402989 3.383313 1.494396V-1.231382C3.383313-1.697634 3.383313-2.080199 3.861519-2.47472C4.27995-2.82142 4.734247-2.84533 4.99726-2.857285C5.057036-2.86924 5.104857-2.917061 5.104857-2.988792C5.104857-3.108344 5.033126-3.108344 4.913574-3.120299C4.124533-3.16812 3.550685-3.598506 3.419178-4.184309C3.383313-4.315816 3.383313-4.339726 3.383313-4.770112V-7.137235C3.383313-7.639352 3.383313-8.021918 2.809465-8.476214C2.331258-8.846824 1.506351-8.966376 1.099875-8.966376C.992279-8.966376 .860772-8.966376 .860772-8.834869C.860772-8.715318 .932503-8.715318 1.052055-8.703362C1.80523-8.655542 2.391034-8.272976 2.546451-7.663263C2.582316-7.555666 2.582316-7.531756 2.582316-7.10137V-4.590785C2.582316-4.040847 2.677958-3.837609 3.060523-3.455044C3.311582-3.203985 3.658281-3.084433 3.993026-2.988792C3.012702-2.713823 2.582316-2.163885 2.582316-1.470486V1.398755Z" id="g3-103-drasiojs"></path>
<path d="M3.203985-3.753923H3.634371L5.427646-.980324C5.547198-.789041 5.834122-.32279 5.965629-.143462C6.049315 0 6.085181 0 6.360149 0H8.009963C8.225156 0 8.404483 0 8.404483-.215193C8.404483-.310834 8.332752-.394521 8.225156-.418431C7.782814-.514072 7.197011-1.303113 6.910087-1.685679C6.826401-1.80523 6.228643-2.594271 5.427646-3.88543C6.491656-4.076712 7.519801-4.531009 7.519801-5.953674C7.519801-7.615442 5.762391-8.18929 4.351681-8.18929H.597758C.382565-8.18929 .191283-8.18929 .191283-7.974097C.191283-7.770859 .418431-7.770859 .514072-7.770859C1.195517-7.770859 1.255293-7.687173 1.255293-7.089415V-1.099875C1.255293-.502117 1.195517-.418431 .514072-.418431C.418431-.418431 .191283-.418431 .191283-.215193C.191283 0 .382565 0 .597758 0H3.873474C4.088667 0 4.267995 0 4.267995-.215193C4.267995-.418431 4.064757-.418431 3.93325-.418431C3.251806-.418431 3.203985-.514072 3.203985-1.099875V-3.753923ZM5.511333-4.339726C5.846077-4.782067 5.881943-5.415691 5.881943-5.941719C5.881943-6.515567 5.810212-7.149191 5.427646-7.639352C5.917808-7.531756 7.10137-7.161146 7.10137-5.953674C7.10137-5.176588 6.742715-4.566874 5.511333-4.339726ZM3.203985-7.12528C3.203985-7.376339 3.203985-7.770859 3.945205-7.770859C4.961395-7.770859 5.463512-7.352428 5.463512-5.941719C5.463512-4.399502 5.092902-4.172354 3.203985-4.172354V-7.12528ZM1.578082-.418431C1.673724-.633624 1.673724-.968369 1.673724-1.075965V-7.113325C1.673724-7.232877 1.673724-7.555666 1.578082-7.770859H2.940971C2.785554-7.579577 2.785554-7.340473 2.785554-7.161146V-1.075965C2.785554-.956413 2.785554-.633624 2.881196-.418431H1.578082ZM4.124533-3.753923C4.208219-3.765878 4.25604-3.777833 4.351681-3.777833C4.531009-3.777833 4.794022-3.801743 4.97335-3.825654C5.152677-3.53873 6.443836-1.41071 7.436115-.418431H6.276463L4.124533-3.753923Z" id="g0-82-drasiojs"></path>
<path d="M3.88543 2.905106C3.88543 2.86924 3.88543 2.84533 3.682192 2.642092C2.486675 1.43462 1.817186-.537983 1.817186-2.976837C1.817186-5.296139 2.379078-7.292653 3.765878-8.703362C3.88543-8.810959 3.88543-8.834869 3.88543-8.870735C3.88543-8.942466 3.825654-8.966376 3.777833-8.966376C3.622416-8.966376 2.642092-8.105604 2.056289-6.933998C1.446575-5.726526 1.171606-4.447323 1.171606-2.976837C1.171606-1.912827 1.338979-.490162 1.960648 .789041C2.666002 2.223661 3.646326 3.000747 3.777833 3.000747C3.825654 3.000747 3.88543 2.976837 3.88543 2.905106Z" id="g8-40-drasiojs"></path>
<path d="M3.371357-2.976837C3.371357-3.88543 3.251806-5.36787 2.582316-6.75467C1.876961-8.18929 .896638-8.966376 .765131-8.966376C.71731-8.966376 .657534-8.942466 .657534-8.870735C.657534-8.834869 .657534-8.810959 .860772-8.607721C2.056289-7.400249 2.725778-5.427646 2.725778-2.988792C2.725778-.669489 2.163885 1.327024 .777086 2.737733C.657534 2.84533 .657534 2.86924 .657534 2.905106C.657534 2.976837 .71731 3.000747 .765131 3.000747C.920548 3.000747 1.900872 2.139975 2.486675 .968369C3.096389-.251059 3.371357-1.542217 3.371357-2.976837Z" id="g8-41-drasiojs"></path>
<path d="M2.502615-5.076961C2.502615-5.292154 2.486675-5.300125 2.271482-5.300125C1.944707-4.98132 1.522291-4.790037 .765131-4.790037V-4.527024C.980324-4.527024 1.41071-4.527024 1.872976-4.742217V-.653549C1.872976-.358655 1.849066-.263014 1.091905-.263014H.812951V0C1.139726-.02391 1.825156-.02391 2.183811-.02391S3.235866-.02391 3.56264 0V-.263014H3.283686C2.526526-.263014 2.502615-.358655 2.502615-.653549V-5.076961Z" id="g7-49-drasiojs"></path>
<path d="M5.571108-1.809215C5.69863-1.809215 5.873973-1.809215 5.873973-1.992528S5.69863-2.175841 5.571108-2.175841H1.004234C.876712-2.175841 .70137-2.175841 .70137-1.992528S.876712-1.809215 1.004234-1.809215H5.571108Z" id="g2-0-drasiojs"></path>
<path d="M1.490411-.119552C1.490411 .398506 1.378829 .852802 .884682 1.346949C.852802 1.370859 .836862 1.3868 .836862 1.42665C.836862 1.490411 .900623 1.538232 .956413 1.538232C1.052055 1.538232 1.713574 .908593 1.713574-.02391C1.713574-.533998 1.522291-.884682 1.171606-.884682C.892653-.884682 .73325-.661519 .73325-.446326C.73325-.223163 .884682 0 1.179577 0C1.370859 0 1.490411-.111582 1.490411-.119552Z" id="g5-59-drasiojs"></path>
<path d="M2.375093-4.97335C2.375093-5.148692 2.247572-5.276214 2.064259-5.276214C1.857036-5.276214 1.625903-5.084932 1.625903-4.845828C1.625903-4.670486 1.753425-4.542964 1.936737-4.542964C2.14396-4.542964 2.375093-4.734247 2.375093-4.97335ZM1.211457-2.048319L.781071-.948443C.74122-.828892 .70137-.73325 .70137-.597758C.70137-.207223 1.004234 .079701 1.42665 .079701C2.199751 .079701 2.526526-1.036115 2.526526-1.139726C2.526526-1.219427 2.462765-1.243337 2.406974-1.243337C2.311333-1.243337 2.295392-1.187547 2.271482-1.107846C2.088169-.470237 1.761395-.143462 1.44259-.143462C1.346949-.143462 1.251308-.183313 1.251308-.398506C1.251308-.589788 1.307098-.73325 1.41071-.980324C1.490411-1.195517 1.570112-1.41071 1.657783-1.625903L1.904857-2.271482C1.976588-2.454795 2.072229-2.701868 2.072229-2.83736C2.072229-3.235866 1.753425-3.514819 1.346949-3.514819C.573848-3.514819 .239103-2.399004 .239103-2.295392C.239103-2.223661 .294894-2.191781 .358655-2.191781C.462267-2.191781 .470237-2.239601 .494147-2.319303C.71731-3.076463 1.083935-3.291656 1.323039-3.291656C1.43462-3.291656 1.514321-3.251806 1.514321-3.028643C1.514321-2.948941 1.506351-2.83736 1.42665-2.598257L1.211457-2.048319Z" id="g5-105-drasiojs"></path>
<path d="M1.594022-1.307098C1.617933-1.42665 1.697634-1.729514 1.721544-1.849066C1.745455-1.928767 1.793275-2.12005 1.809215-2.199751C1.825156-2.239601 2.088169-2.757659 2.438854-3.020672C2.709838-3.227895 2.972852-3.291656 3.196015-3.291656C3.490909-3.291656 3.650311-3.116314 3.650311-2.749689C3.650311-2.558406 3.602491-2.375093 3.514819-2.016438C3.459029-1.809215 3.323537-1.275218 3.275716-1.060025L3.156164-.581818C3.116314-.446326 3.060523-.207223 3.060523-.167372C3.060523 .01594 3.211955 .079701 3.315567 .079701C3.459029 .079701 3.57858-.01594 3.634371-.111582C3.658281-.159402 3.722042-.430386 3.761893-.597758L3.945205-1.307098C3.969116-1.42665 4.048817-1.729514 4.072727-1.849066C4.184309-2.279452 4.184309-2.287422 4.367621-2.550436C4.630635-2.940971 5.00523-3.291656 5.539228-3.291656C5.826152-3.291656 5.993524-3.124284 5.993524-2.749689C5.993524-2.311333 5.65878-1.39477 5.507347-1.012204C5.427646-.804981 5.403736-.749191 5.403736-.597758C5.403736-.143462 5.778331 .079701 6.121046 .079701C6.902117 .079701 7.228892-1.036115 7.228892-1.139726C7.228892-1.219427 7.165131-1.243337 7.10934-1.243337C7.013699-1.243337 6.997758-1.187547 6.973848-1.107846C6.782565-.446326 6.447821-.143462 6.144956-.143462C6.017435-.143462 5.953674-.223163 5.953674-.406476S6.017435-.765131 6.097136-.964384C6.216687-1.267248 6.567372-2.183811 6.567372-2.630137C6.567372-3.227895 6.152927-3.514819 5.579078-3.514819C5.029141-3.514819 4.574844-3.227895 4.216189-2.733748C4.152428-3.371357 3.642341-3.514819 3.227895-3.514819C2.86127-3.514819 2.375093-3.387298 1.936737-2.81345C1.880946-3.291656 1.498381-3.514819 1.123786-3.514819C.844832-3.514819 .645579-3.347447 .510087-3.076463C.318804-2.701868 .239103-2.311333 .239103-2.295392C.239103-2.223661 .294894-2.191781 .358655-2.191781C.462267-2.191781 .470237-2.223661 .526027-2.430884C.621669-2.82142 .765131-3.291656 1.099875-3.291656C1.307098-3.291656 1.354919-3.092403 1.354919-2.917061C1.354919-2.773599 1.315068-2.622167 1.251308-2.359153C1.235367-2.295392 1.115816-1.825156 1.083935-1.713574L.789041-.518057C.757161-.398506 .70934-.199253 .70934-.167372C.70934 .01594 .860772 .079701 .964384 .079701C1.107846 .079701 1.227397-.01594 1.283188-.111582C1.307098-.159402 1.370859-.430386 1.41071-.597758L1.594022-1.307098Z" id="g5-109-drasiojs"></path>
<path d="M3.993026-3.180075C3.642341-3.092403 3.626401-2.781569 3.626401-2.749689C3.626401-2.574346 3.761893-2.454795 3.937235-2.454795S4.383562-2.590286 4.383562-2.933001C4.383562-3.387298 3.881445-3.514819 3.58655-3.514819C3.211955-3.514819 2.909091-3.251806 2.725778-2.940971C2.550436-3.363387 2.13599-3.514819 1.809215-3.514819C.940473-3.514819 .454296-2.518555 .454296-2.295392C.454296-2.223661 .510087-2.191781 .573848-2.191781C.669489-2.191781 .68543-2.231631 .70934-2.327273C.892653-2.909091 1.370859-3.291656 1.785305-3.291656C2.096139-3.291656 2.247572-3.068493 2.247572-2.781569C2.247572-2.622167 2.15193-2.255542 2.088169-2.000498C2.032379-1.769365 1.857036-1.060025 1.817186-.908593C1.705604-.478207 1.41868-.143462 1.060025-.143462C1.028144-.143462 .820922-.143462 .653549-.255044C1.020174-.342715 1.020174-.67746 1.020174-.68543C1.020174-.868742 .876712-.980324 .70137-.980324C.486177-.980324 .255044-.797011 .255044-.494147C.255044-.127522 .645579 .079701 1.052055 .079701C1.474471 .079701 1.769365-.239103 1.912827-.494147C2.088169-.103611 2.454795 .079701 2.83736 .079701C3.706102 .079701 4.184309-.916563 4.184309-1.139726C4.184309-1.219427 4.120548-1.243337 4.064757-1.243337C3.969116-1.243337 3.953176-1.187547 3.929265-1.107846C3.769863-.573848 3.315567-.143462 2.8533-.143462C2.590286-.143462 2.399004-.318804 2.399004-.653549C2.399004-.812951 2.446824-.996264 2.558406-1.44259C2.614197-1.681694 2.789539-2.383064 2.82939-2.534496C2.940971-2.948941 3.219925-3.291656 3.57858-3.291656C3.618431-3.291656 3.825654-3.291656 3.993026-3.180075Z" id="g5-120-drasiojs"></path>
<path d="M2.199751-.573848C2.199751-.920548 1.912827-1.159651 1.625903-1.159651C1.279203-1.159651 1.0401-.872727 1.0401-.585803C1.0401-.239103 1.327024 0 1.613948 0C1.960648 0 2.199751-.286924 2.199751-.573848Z" id="g6-58-drasiojs"></path>
<path d="M8.942466-7.292653C9.050062-7.699128 9.073973-7.81868 9.92279-7.81868C10.137983-7.81868 10.257534-7.81868 10.257534-8.033873C10.257534-8.16538 10.149938-8.16538 10.078207-8.16538C9.863014-8.16538 9.611955-8.141469 9.384807-8.141469H7.974097C7.746949-8.141469 7.49589-8.16538 7.268742-8.16538C7.185056-8.16538 7.041594-8.16538 7.041594-7.938232C7.041594-7.81868 7.12528-7.81868 7.352428-7.81868C8.069738-7.81868 8.069738-7.723039 8.069738-7.591532C8.069738-7.567621 8.069738-7.49589 8.021918-7.316563L7.292653-4.423412H3.682192L4.399502-7.292653C4.507098-7.699128 4.531009-7.81868 5.379826-7.81868C5.595019-7.81868 5.71457-7.81868 5.71457-8.033873C5.71457-8.16538 5.606974-8.16538 5.535243-8.16538C5.32005-8.16538 5.068991-8.141469 4.841843-8.141469H3.431133C3.203985-8.141469 2.952927-8.16538 2.725778-8.16538C2.642092-8.16538 2.49863-8.16538 2.49863-7.938232C2.49863-7.81868 2.582316-7.81868 2.809465-7.81868C3.526775-7.81868 3.526775-7.723039 3.526775-7.591532C3.526775-7.567621 3.526775-7.49589 3.478954-7.316563L1.865006-.884682C1.75741-.466252 1.733499-.3467 .908593-.3467C.633624-.3467 .549938-.3467 .549938-.119552C.549938 0 .681445 0 .71731 0C.932503 0 1.183562-.02391 1.41071-.02391H2.82142C3.048568-.02391 3.299626 0 3.526775 0C3.622416 0 3.753923 0 3.753923-.227148C3.753923-.3467 3.646326-.3467 3.466999-.3467C2.737733-.3467 2.737733-.442341 2.737733-.561893C2.737733-.573848 2.737733-.657534 2.761644-.753176L3.58655-4.076712H7.208966C7.005729-3.287671 6.396015-.789041 6.372105-.71731C6.240598-.358655 6.049315-.358655 5.34396-.3467C5.200498-.3467 5.092902-.3467 5.092902-.119552C5.092902 0 5.224408 0 5.260274 0C5.475467 0 5.726526-.02391 5.953674-.02391H7.364384C7.591532-.02391 7.84259 0 8.069738 0C8.16538 0 8.296887 0 8.296887-.227148C8.296887-.3467 8.18929-.3467 8.009963-.3467C7.280697-.3467 7.280697-.442341 7.280697-.561893C7.280697-.573848 7.280697-.657534 7.304608-.753176L8.942466-7.292653Z" id="g6-72-drasiojs"></path>
<path d="M5.66675-4.877709C5.284184-4.805978 5.140722-4.519054 5.140722-4.291905C5.140722-4.004981 5.36787-3.90934 5.535243-3.90934C5.893898-3.90934 6.144956-4.220174 6.144956-4.542964C6.144956-5.045081 5.571108-5.272229 5.068991-5.272229C4.339726-5.272229 3.93325-4.554919 3.825654-4.327771C3.550685-5.224408 2.809465-5.272229 2.594271-5.272229C1.374844-5.272229 .729265-3.706102 .729265-3.443088C.729265-3.395268 .777086-3.335492 .860772-3.335492C.956413-3.335492 .980324-3.407223 1.004234-3.455044C1.41071-4.782067 2.211706-5.033126 2.558406-5.033126C3.096389-5.033126 3.203985-4.531009 3.203985-4.244085C3.203985-3.981071 3.132254-3.706102 2.988792-3.132254L2.582316-1.494396C2.402989-.777086 2.056289-.119552 1.422665-.119552C1.362889-.119552 1.06401-.119552 .812951-.274969C1.243337-.358655 1.338979-.71731 1.338979-.860772C1.338979-1.099875 1.159651-1.243337 .932503-1.243337C.645579-1.243337 .334745-.992279 .334745-.609714C.334745-.107597 .896638 .119552 1.41071 .119552C1.984558 .119552 2.391034-.334745 2.642092-.824907C2.833375-.119552 3.431133 .119552 3.873474 .119552C5.092902 .119552 5.738481-1.446575 5.738481-1.709589C5.738481-1.769365 5.69066-1.817186 5.618929-1.817186C5.511333-1.817186 5.499377-1.75741 5.463512-1.661768C5.140722-.609714 4.447323-.119552 3.90934-.119552C3.490909-.119552 3.263761-.430386 3.263761-.920548C3.263761-1.183562 3.311582-1.374844 3.502864-2.163885L3.921295-3.789788C4.100623-4.507098 4.507098-5.033126 5.057036-5.033126C5.080946-5.033126 5.415691-5.033126 5.66675-4.877709Z" id="g6-120-drasiojs"></path>
</defs>
<g id="page227-drasiojs">
<g fill="currentColor" transform="matrix(1 0 0 1 -193.3693 2.81172)">
<use href="#g6-58-drasiojs" x="206.288841" y="-10.529971"></use>
<use href="#g6-58-drasiojs" x="211.532999" y="-10.529971"></use>
<use href="#g6-58-drasiojs" x="216.777158" y="-10.529971"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -214.8735 2.81172)">
<use href="#g6-72-drasiojs" x="265.874583" y="-10.529971"></use>
<use href="#g5-105-drasiojs" x="275.573563" y="-8.736708"></use>
<use href="#g2-0-drasiojs" x="278.456703" y="-8.736708"></use>
<use href="#g7-49-drasiojs" x="285.04321" y="-8.736708"></use>
<use href="#g5-59-drasiojs" x="289.277392" y="-8.736708"></use>
<use href="#g5-120-drasiojs" x="291.629716" y="-8.736708"></use>
<use href="#g8-40-drasiojs" x="296.894747" y="-10.529971"></use>
<use href="#g0-82-drasiojs" x="301.447073" y="-10.529971"></use>
<use href="#g5-109-drasiojs" x="310.081385" y="-14.868407"></use>
<use href="#g8-41-drasiojs" x="318.070043" y="-10.529971"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -222.513 2.81172)">
<use href="#g6-72-drasiojs" x="354.603814" y="-10.529971"></use>
<use href="#g5-105-drasiojs" x="364.302795" y="-8.736708"></use>
<use href="#g8-40-drasiojs" x="367.684066" y="-10.529971"></use>
<use href="#g0-82-drasiojs" x="372.236392" y="-10.529971"></use>
<use href="#g5-109-drasiojs" x="380.870704" y="-14.868407"></use>
<use href="#g3-0-drasiojs" x="391.516026" y="-10.529971"></use>
<use href="#g3-102-drasiojs" x="403.471186" y="-10.529971"></use>
<use href="#g6-120-drasiojs" x="409.448793" y="-10.529971"></use>
<use href="#g3-103-drasiojs" x="416.10088" y="-10.529971"></use>
<use href="#g8-41-drasiojs" x="422.078487" y="-10.529971"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -205.903 2.81172)">
<use href="#g6-72-drasiojs" x="434.363097" y="-10.529971"></use>
<use href="#g5-105-drasiojs" x="444.062077" y="-8.736708"></use>
<use href="#g8-40-drasiojs" x="447.443349" y="-10.529971"></use>
<use href="#g0-82-drasiojs" x="451.995675" y="-10.529971"></use>
<use href="#g5-109-drasiojs" x="460.629987" y="-14.868407"></use>
<use href="#g8-41-drasiojs" x="468.618645" y="-10.529971"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -209.463 2.81172)">
<use href="#g6-72-drasiojs" x="501.07244" y="-10.529971"></use>
<use href="#g5-105-drasiojs" x="510.771421" y="-8.736708"></use>
<use href="#g5-59-drasiojs" x="513.65456" y="-8.736708"></use>
<use href="#g5-120-drasiojs" x="516.006884" y="-8.736708"></use>
<use href="#g8-40-drasiojs" x="521.271915" y="-10.529971"></use>
<use href="#g0-82-drasiojs" x="525.824241" y="-10.529971"></use>
<use href="#g5-109-drasiojs" x="534.458553" y="-14.868407"></use>
<use href="#g8-41-drasiojs" x="542.447211" y="-10.529971"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -193.369 2.81172)">
<use href="#g6-58-drasiojs" x="555.247838" y="-10.529971"></use>
<use href="#g6-58-drasiojs" x="560.491997" y="-10.529971"></use>
<use href="#g6-58-drasiojs" x="565.736155" y="-10.529971"></use>
</g>
<path d="M32.008-10.707032H45.176" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M42.92965-13.57813C43.38277-11.85547 44.39449-11.042969 45.414022-10.707031C44.39449-10.371094 43.38277-9.55859 42.92965-7.83984" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M113.0977-10.707032H126.2656" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M124.01911-13.57813C124.47223-11.85547 125.48786-11.042969 126.507389-10.707031C125.48786-10.371094 124.47223-9.55859 124.01911-7.83984" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M209.4648-10.707032H222.6367" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M220.39014-13.57813C220.84327-11.85547 221.85499-11.042969 222.87452-10.707031C221.85499-10.371094 220.84327-9.55859 220.39014-7.83984" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M272.6172-10.707032H285.7891" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M283.53902-13.57813C283.99606-11.85547 285.00777-11.042969 286.027305-10.707031C285.00777-10.371094 283.99606-9.55859 283.53902-7.83984" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M342.887-10.707032H356.059" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M353.80872-13.57813C354.26575-11.85547 355.27747-11.042969 356.297-10.707031C355.27747-10.371094 354.26575-9.55859 353.80872-7.83984" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
</g>
</svg>
</div>
We saw that @H_i(\mathbb{R}^m)\cong 0@ for every @i \in \mathbb{Z}@. Hence we have a collection of isomorphisms
@@H_{i,x}(\mathbb{R}^m) \cong H_{i+1}(\mathbb{R}^m-\{x\}).@@
Moreover, because @\mathbb{R}^m - \{x\}@ is homotopic to @S^{m-1}@, the homology @H_{i+1}(\mathbb{R}^m-\{x\})@ is @Λ@ for @i+1=m@ and zero otherwise. This gives the following calculation: the homology @H_{i,x}(\mathbb{R}^m)@ is zero if and only if @i=m@. The same reasoning applied to @V@ and @h(x)@ gives the same calculation, and since @h@ induces an isomorphism of homology groups, we must have @m=n@.

## Singular cohomology

Since all elements in a @Λ@-module @M@ may be identified with the @Λ@-linear maps @@Λ \to M,@@ we may dualize and consider linear maps of the same kind but having opposite polarity: this we do. The **@n@-th cochain group** is the dual module
@@C^n(X;Λ) = \operatorname{Hom}_Λ(C_n(X;Λ), Λ),@@
consisting of all @Λ@-linear maps going from the singular chain group into its ring of scalars. A cochain is just a way to (linearly) compute a scalar quantity from a singular chain. There's an analogy to be made with geometry: you have points in some affine space (singular chains), and you have coordinates (cochains), which in a way compute a number from each point. In geometry, there's a strong link between points and coordinates: studying algebraic varieties is essentially the same as studying rings of coordinates, which are basically rings of polynomial functions from the space to the underlying field. However, it is easier to work with coordinates than sets of points, because there's a natural ring structure. Hence, if this analogy is to hold, one would expect a link between homology and cohomology; moreover, it should be easier to work with cohomology than homology. And so it is.

The **value** of a cochain @c@ on a chain @\gamma@ will be denoted @\langle c, \gamma \rangle@ and is defined as
@@\langle c, \gamma \rangle = c(\gamma) \in Λ.@@
Obviously @\langle {-},{-}\rangle : C^n(X;Λ) \times C_n(X;Λ) \to Λ@ is @Λ@-bilinear.

The **coboundary** of a cochain @c \in C^n(X;Λ)@ is defined to be the cochain @\delta c \in C^{n+1}(X;Λ)@ whose value on each @(n+1)@-chain @\alpha@ is determined by the identity
@@\langle \delta c, \alpha\rangle + (-1)^n\langle c, ∂\alpha \rangle = 0.@@
Hence @\delta@ is, up to sign, the dual of @∂@, in the sense that for any cochain @c@, the cochain @\delta c@ is, up to sign, the pullback of @c@ along @∂@:
<div style="display:flex;align-items:center;width:100%;margin-top:12px;">
<svg style="display:bock;margin:0 auto;" height="81.68144666666666px" style="vertical-align:-0.6691693333333333px;" version="1.1" viewBox="-.500002 -60.761083 389.542968 61.261085" width="519.3906239999999px" xmlns="http://www.w3.org/2000/svg">
<defs>
<path d="M4.315816-8.284932C4.244085-8.524035 4.184309-8.53599 4.052802-8.53599C3.945205-8.53599 3.873474-8.51208 3.813699-8.320797L1.494396-1.147696C1.267248-.454296 .777086-.358655 .37061-.3467V0C.884682-.02391 .908593-.02391 1.422665-.02391C1.745455-.02391 2.331258-.02391 2.630137 0V-.3467C2.020423-.358655 1.793275-.6934 1.793275-.956413C1.793275-1.004234 1.793275-1.0401 1.853051-1.219427L3.718057-6.969863L5.678705-.920548C5.738481-.753176 5.738481-.729265 5.738481-.705355C5.738481-.3467 5.116812-.3467 4.817933-.3467V0C5.092902-.02391 6.01345-.02391 6.348194-.02391C6.694894-.02391 7.436115-.02391 7.746949 0V-.3467C7.10137-.3467 6.874222-.3467 6.73076-.800996L4.315816-8.284932Z" id="g8-3-drasiojs"></path>
<path d="M3.88543 2.905106C3.88543 2.86924 3.88543 2.84533 3.682192 2.642092C2.486675 1.43462 1.817186-.537983 1.817186-2.976837C1.817186-5.296139 2.379078-7.292653 3.765878-8.703362C3.88543-8.810959 3.88543-8.834869 3.88543-8.870735C3.88543-8.942466 3.825654-8.966376 3.777833-8.966376C3.622416-8.966376 2.642092-8.105604 2.056289-6.933998C1.446575-5.726526 1.171606-4.447323 1.171606-2.976837C1.171606-1.912827 1.338979-.490162 1.960648 .789041C2.666002 2.223661 3.646326 3.000747 3.777833 3.000747C3.825654 3.000747 3.88543 2.976837 3.88543 2.905106Z" id="g8-40-drasiojs"></path>
<path d="M3.371357-2.976837C3.371357-3.88543 3.251806-5.36787 2.582316-6.75467C1.876961-8.18929 .896638-8.966376 .765131-8.966376C.71731-8.966376 .657534-8.942466 .657534-8.870735C.657534-8.834869 .657534-8.810959 .860772-8.607721C2.056289-7.400249 2.725778-5.427646 2.725778-2.988792C2.725778-.669489 2.163885 1.327024 .777086 2.737733C.657534 2.84533 .657534 2.86924 .657534 2.905106C.657534 2.976837 .71731 3.000747 .765131 3.000747C.920548 3.000747 1.900872 2.139975 2.486675 .968369C3.096389-.251059 3.371357-1.542217 3.371357-2.976837Z" id="g8-41-drasiojs"></path>
<path d="M3.474969-1.809215H5.818182C5.929763-1.809215 6.105106-1.809215 6.105106-1.992528S5.929763-2.175841 5.818182-2.175841H3.474969V-4.527024C3.474969-4.638605 3.474969-4.813948 3.291656-4.813948S3.108344-4.638605 3.108344-4.527024V-2.175841H.757161C.645579-2.175841 .470237-2.175841 .470237-1.992528S.645579-1.809215 .757161-1.809215H3.108344V.541968C3.108344 .653549 3.108344 .828892 3.291656 .828892S3.474969 .653549 3.474969 .541968V-1.809215Z" id="g7-43-drasiojs"></path>
<path d="M2.502615-5.076961C2.502615-5.292154 2.486675-5.300125 2.271482-5.300125C1.944707-4.98132 1.522291-4.790037 .765131-4.790037V-4.527024C.980324-4.527024 1.41071-4.527024 1.872976-4.742217V-.653549C1.872976-.358655 1.849066-.263014 1.091905-.263014H.812951V0C1.139726-.02391 1.825156-.02391 2.183811-.02391S3.235866-.02391 3.56264 0V-.263014H3.283686C2.526526-.263014 2.502615-.358655 2.502615-.653549V-5.076961Z" id="g7-49-drasiojs"></path>
<path d="M2.16787-3.466999C.964384-3.148194 .350685-2.096139 .350685-1.283188C.350685-.390535 1.020174 .095641 1.713574 .095641C2.654047 .095641 3.371357-1.052055 3.371357-2.215691C3.371357-2.980822 3.012702-3.403238 2.741719-3.714072C2.478705-4.024907 1.920797-4.678456 1.920797-5.037111C1.920797-5.212453 2.088169-5.387796 2.351183-5.387796S2.789539-5.276214 3.004732-5.148692C3.196015-5.029141 3.339477-4.96538 3.435118-4.96538C3.634371-4.96538 3.761893-5.156663 3.761893-5.292154C3.761893-5.483437 3.666252-5.507347 3.259776-5.595019C2.805479-5.69066 2.574346-5.69066 2.566376-5.69066C2.223661-5.69066 1.657783-5.523288 1.657783-4.845828C1.657783-4.431382 1.880946-3.977086 2.16787-3.466999ZM2.295392-3.251806C2.574346-2.781569 2.757659-2.383064 2.757659-1.888917C2.757659-1.267248 2.399004-.127522 1.721544-.127522C1.40274-.127522 .908593-.334745 .908593-1.067995C.908593-1.482441 1.147696-2.948941 2.295392-3.251806Z" id="g5-14-drasiojs"></path>
<path d="M3.897385-2.741719C3.785803-3.172105 3.482939-3.642341 2.757659-3.642341C2.000498-3.642341 1.522291-3.291656 1.139726-2.964882C.334745-2.271482 .334745-1.346949 .334745-1.275218C.334745-.781071 .71731 .167372 1.928767 .167372C2.590286 .167372 3.299626-.159402 3.841594-.892653C4.367621-1.609963 4.758157-2.789539 4.758157-3.58655C4.758157-4.877709 3.953176-5.69863 2.893151-5.69863C1.665753-5.69863 1.299128-4.678456 1.299128-4.431382C1.299128-4.2401 1.44259-4.136488 1.609963-4.136488C1.865006-4.136488 2.056289-4.367621 2.056289-4.574844C2.056289-4.678456 2.032379-4.861768 1.713574-4.869738C2.032379-5.387796 2.558406-5.491407 2.885181-5.491407C3.602491-5.491407 4.112578-4.933499 4.112578-4.008966C4.112578-3.57061 4.016936-3.148194 3.905355-2.741719H3.897385ZM1.944707-.071731C1.052055-.071731 1.004234-.828892 1.004234-.988294C1.004234-1.299128 1.235367-2.14396 1.315068-2.343213C1.522291-2.81345 2.016438-3.419178 2.781569-3.419178C3.451059-3.419178 3.737983-2.909091 3.737983-2.351183C3.737983-1.737484 3.180075-.071731 1.944707-.071731Z" id="g5-64-drasiojs"></path>
<path d="M3.259776-3.052553C2.933001-3.012702 2.82939-2.765629 2.82939-2.606227C2.82939-2.375093 3.036613-2.311333 3.140224-2.311333C3.180075-2.311333 3.58655-2.343213 3.58655-2.82939S3.060523-3.514819 2.582316-3.514819C1.45056-3.514819 .350685-2.414944 .350685-1.299128C.350685-.541968 .868742 .079701 1.753425 .079701C3.012702 .079701 3.674222-.72528 3.674222-.828892C3.674222-.900623 3.594521-.956413 3.5467-.956413S3.474969-.932503 3.435118-.884682C2.805479-.143462 1.912827-.143462 1.769365-.143462C1.338979-.143462 .996264-.406476 .996264-1.012204C.996264-1.362889 1.155666-2.207721 1.530262-2.701868C1.880946-3.148194 2.279452-3.291656 2.590286-3.291656C2.685928-3.291656 3.052553-3.283686 3.259776-3.052553Z" id="g5-99-drasiojs"></path>
<path d="M1.594022-1.307098C1.617933-1.42665 1.697634-1.729514 1.721544-1.849066C1.833126-2.279452 1.833126-2.287422 2.016438-2.550436C2.279452-2.940971 2.654047-3.291656 3.188045-3.291656C3.474969-3.291656 3.642341-3.124284 3.642341-2.749689C3.642341-2.311333 3.307597-1.40274 3.156164-1.012204C3.052553-.749191 3.052553-.70137 3.052553-.597758C3.052553-.143462 3.427148 .079701 3.769863 .079701C4.550934 .079701 4.877709-1.036115 4.877709-1.139726C4.877709-1.219427 4.813948-1.243337 4.758157-1.243337C4.662516-1.243337 4.646575-1.187547 4.622665-1.107846C4.431382-.454296 4.096638-.143462 3.793773-.143462C3.666252-.143462 3.602491-.223163 3.602491-.406476S3.666252-.765131 3.745953-.964384C3.865504-1.267248 4.216189-2.183811 4.216189-2.630137C4.216189-3.227895 3.801743-3.514819 3.227895-3.514819C2.582316-3.514819 2.16787-3.124284 1.936737-2.82142C1.880946-3.259776 1.530262-3.514819 1.123786-3.514819C.836862-3.514819 .637609-3.331507 .510087-3.084433C.318804-2.709838 .239103-2.311333 .239103-2.295392C.239103-2.223661 .294894-2.191781 .358655-2.191781C.462267-2.191781 .470237-2.223661 .526027-2.430884C.621669-2.82142 .765131-3.291656 1.099875-3.291656C1.307098-3.291656 1.354919-3.092403 1.354919-2.917061C1.354919-2.773599 1.315068-2.622167 1.251308-2.359153C1.235367-2.295392 1.115816-1.825156 1.083935-1.713574L.789041-.518057C.757161-.398506 .70934-.199253 .70934-.167372C.70934 .01594 .860772 .079701 .964384 .079701C1.107846 .079701 1.227397-.01594 1.283188-.111582C1.307098-.159402 1.370859-.430386 1.41071-.597758L1.594022-1.307098Z" id="g5-110-drasiojs"></path>
<path d="M8.930511-8.308842C8.930511-8.416438 8.846824-8.416438 8.822914-8.416438S8.751183-8.416438 8.655542-8.296887L7.830635-7.292653C7.412204-8.009963 6.75467-8.416438 5.858032-8.416438C3.275716-8.416438 .597758-5.798257 .597758-2.988792C.597758-.992279 1.996513 .251059 3.741968 .251059C4.698381 .251059 5.535243-.155417 6.228643-.74122C7.268742-1.613948 7.579577-2.773599 7.579577-2.86924C7.579577-2.976837 7.483935-2.976837 7.44807-2.976837C7.340473-2.976837 7.328518-2.905106 7.304608-2.857285C6.75467-.992279 5.140722-.095641 3.945205-.095641C2.677958-.095641 1.578082-.908593 1.578082-2.606227C1.578082-2.988792 1.697634-5.068991 3.048568-6.635118C3.706102-7.400249 4.829888-8.069738 5.965629-8.069738C7.280697-8.069738 7.866501-6.981818 7.866501-5.762391C7.866501-5.451557 7.830635-5.188543 7.830635-5.140722C7.830635-5.033126 7.950187-5.033126 7.986052-5.033126C8.117559-5.033126 8.129514-5.045081 8.177335-5.260274L8.930511-8.308842Z" id="g6-67-drasiojs"></path>
<path d="M5.678705-4.853798L4.554919-7.47198C4.710336-7.758904 5.068991-7.806725 5.212453-7.81868C5.284184-7.81868 5.415691-7.830635 5.415691-8.033873C5.415691-8.16538 5.308095-8.16538 5.236364-8.16538C5.033126-8.16538 4.794022-8.141469 4.590785-8.141469H3.897385C3.16812-8.141469 2.642092-8.16538 2.630137-8.16538C2.534496-8.16538 2.414944-8.16538 2.414944-7.938232C2.414944-7.81868 2.52254-7.81868 2.677958-7.81868C3.371357-7.81868 3.419178-7.699128 3.53873-7.412204L4.961395-4.088667L2.367123-1.315068C1.936737-.848817 1.422665-.394521 .537983-.3467C.394521-.334745 .298879-.334745 .298879-.119552C.298879-.083686 .310834 0 .442341 0C.609714 0 .789041-.02391 .956413-.02391H1.518306C1.900872-.02391 2.319303 0 2.689913 0C2.773599 0 2.917061 0 2.917061-.215193C2.917061-.334745 2.833375-.3467 2.761644-.3467C2.52254-.37061 2.367123-.502117 2.367123-.6934C2.367123-.896638 2.510585-1.0401 2.857285-1.398755L3.921295-2.558406C4.184309-2.833375 4.817933-3.526775 5.080946-3.789788L6.336239-.848817C6.348194-.824907 6.396015-.705355 6.396015-.6934C6.396015-.585803 6.133001-.37061 5.750436-.3467C5.678705-.3467 5.547198-.334745 5.547198-.119552C5.547198 0 5.66675 0 5.726526 0C5.929763 0 6.168867-.02391 6.372105-.02391H7.687173C7.902366-.02391 8.129514 0 8.332752 0C8.416438 0 8.547945 0 8.547945-.227148C8.547945-.3467 8.428394-.3467 8.320797-.3467C7.603487-.358655 7.579577-.418431 7.376339-.860772L5.798257-4.566874L7.316563-6.192777C7.436115-6.312329 7.711083-6.611208 7.81868-6.73076C8.332752-7.268742 8.810959-7.758904 9.779328-7.81868C9.898879-7.830635 10.018431-7.830635 10.018431-8.033873C10.018431-8.16538 9.910834-8.16538 9.863014-8.16538C9.695641-8.16538 9.516314-8.141469 9.348941-8.141469H8.799004C8.416438-8.141469 7.998007-8.16538 7.627397-8.16538C7.543711-8.16538 7.400249-8.16538 7.400249-7.950187C7.400249-7.830635 7.483935-7.81868 7.555666-7.81868C7.746949-7.79477 7.950187-7.699128 7.950187-7.47198L7.938232-7.44807C7.926276-7.364384 7.902366-7.244832 7.770859-7.10137L5.678705-4.853798Z" id="g6-88-drasiojs"></path>
</defs>
<g id="page266-drasiojs">
<g fill="currentColor" transform="matrix(1 0 0 1 -109.078 24.9733)">
<use href="#g6-67-drasiojs" x="221.714758" y="-70.327732"></use>
<use href="#g5-110-drasiojs" x="230.089804" y="-68.534469"></use>
<use href="#g7-43-drasiojs" x="235.228006" y="-68.534469"></use>
<use href="#g7-49-drasiojs" x="241.814513" y="-68.534469"></use>
<use href="#g8-40-drasiojs" x="246.546828" y="-70.327732"></use>
<use href="#g6-88-drasiojs" x="251.099153" y="-70.327732"></use>
<use href="#g8-41-drasiojs" x="261.754261" y="-70.327732"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -103.667 24.9733)">
<use href="#g6-67-drasiojs" x="345.799246" y="-70.327732"></use>
<use href="#g5-110-drasiojs" x="354.174292" y="-68.534469"></use>
<use href="#g8-40-drasiojs" x="359.810626" y="-70.327732"></use>
<use href="#g6-88-drasiojs" x="364.362952" y="-70.327732"></use>
<use href="#g8-41-drasiojs" x="375.01806" y="-70.327732"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -90.844 24.97325)">
<use href="#g8-3-drasiojs" x="286.462174" y="-29.348227"></use>
</g>
<path d="M151.6055-37.79297L189.86719-13.5742" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M189.503753-17.199232C188.964686-15.500026 189.386564-14.273459 190.070162-13.445327C189.031096-13.707047 187.738127-13.562509 186.433438-12.351571" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<g fill="currentColor" transform="matrix(1 0 0 1 -33.86 12.1418)">
<use href="#g5-14-drasiojs" x="194.271482" y="-29.348227"></use>
<use href="#g5-99-drasiojs" x="198.317467" y="-29.348227"></use>
</g>
<path d="M162.5742-48.3438H236.3086" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M234.06283-51.21486C234.51596-49.4922 235.52768-48.679699 236.547207-48.343762C235.52768-48.007824 234.51596-47.19532 234.06283-45.47657" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<g fill="currentColor" transform="matrix(1 0 0 1 2.945 -21.8084)">
<use href="#g5-64-drasiojs" x="194.271482" y="-29.348227"></use>
</g>
<path d="M243.7422-37.79297L209.4844-14.1328" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M212.964462-13.046833C211.612905-14.20699 210.316024-14.300735 209.288686-13.996048C209.93712-14.851518 210.308217-16.093706 209.702742-17.769485" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<g fill="currentColor" transform="matrix(1 0 0 1 34.959 9.7669)">
<use href="#g5-99-drasiojs" x="194.271482" y="-29.348227"></use>
</g>
</g>
</svg>
</div>
This sign convention is used in Milnor and Stasheff's book, but not in Hatcher for instance, where he defines @\delta@ as precisely the dual of @∂@. Since my goal is to understand characteristic classes, I'm going to keep the sign convention used in the M&S book.

Again, this definition has intuitive content: since @c@ is able to "measure", or "give coordinates", any @n@-chain, then it should be possible to obtain a way to measure @(n+1)@-chains @\alpha@ by combining measures for the boundaries of @\alpha@.

The coboundary homomorphism, just like its dual friend, verifies @\delta^2 = 0@. Therefore, if we define **@n@-cocycles** to be
@@Z^n(X;Λ) = \ker(\delta : C^n(X; Λ) \to C^{n+1}(X; Λ))@@
and **@n@-coboundaries** to be
@@B^n(X;Λ) = \operatorname{im}(\delta : C^{n-1}(X;Λ) \to C^n(X;Λ),@@
then we may also define the **@n@-th singular cohomology group** by
@@H^n(X;Λ) = Z^n(X;Λ)/B^n(X;Λ).@@

### Universal coefficient theorem for cohomology

Instead of using the ring @Λ@ as coefficients, we may also use any @Λ@-module @M@. If @Λ@ is a principal ideal domain, then there is a natural split exact sequence
<div style="display:flex;align-items:center;width:100%;">
<svg style="display:bock;margin:0 auto;" height="47.78880933333333px" style="vertical-align:-0.6691693333333333px;" version="1.1" viewBox="-.500002 -35.341605 389.542968 35.841607" width="519.3906239999999px" xmlns="http://www.w3.org/2000/svg">
<defs>
<path d="M5.571108-1.809215C5.69863-1.809215 5.873973-1.809215 5.873973-1.992528S5.69863-2.175841 5.571108-2.175841H1.004234C.876712-2.175841 .70137-2.175841 .70137-1.992528S.876712-1.809215 1.004234-1.809215H5.571108Z" id="g2-0-drasiojs"></path>
<path d="M2.327273-5.292154C2.335243-5.308095 2.359153-5.411706 2.359153-5.419676C2.359153-5.459527 2.327273-5.531258 2.231631-5.531258C2.199751-5.531258 1.952677-5.507347 1.769365-5.491407L1.323039-5.459527C1.147696-5.443587 1.067995-5.435616 1.067995-5.292154C1.067995-5.180573 1.179577-5.180573 1.275218-5.180573C1.657783-5.180573 1.657783-5.132752 1.657783-5.061021C1.657783-5.037111 1.657783-5.021171 1.617933-4.877709L.486177-.342715C.454296-.223163 .454296-.175342 .454296-.167372C.454296-.03188 .565878 .079701 .71731 .079701C.844832 .079701 .956413 0 1.020174-.103611C1.044085-.151432 1.107846-.406476 1.147696-.565878L1.331009-1.275218C1.354919-1.39477 1.43462-1.697634 1.458531-1.817186C1.578082-2.279452 1.578082-2.295392 1.753425-2.550436C2.024408-2.940971 2.399004-3.291656 2.933001-3.291656C3.219925-3.291656 3.387298-3.124284 3.387298-2.749689C3.387298-2.311333 3.052553-1.40274 2.901121-1.012204C2.797509-.749191 2.797509-.70137 2.797509-.597758C2.797509-.143462 3.172105 .079701 3.514819 .079701C4.29589 .079701 4.622665-1.036115 4.622665-1.139726C4.622665-1.219427 4.558904-1.243337 4.503113-1.243337C4.407472-1.243337 4.391532-1.187547 4.367621-1.107846C4.176339-.454296 3.841594-.143462 3.53873-.143462C3.411208-.143462 3.347447-.223163 3.347447-.406476S3.411208-.765131 3.490909-.964384C3.610461-1.267248 3.961146-2.183811 3.961146-2.630137C3.961146-3.227895 3.5467-3.514819 2.972852-3.514819C2.526526-3.514819 2.10411-3.323537 1.737484-2.901121L2.327273-5.292154Z" id="g5-104-drasiojs"></path>
<path d="M2.375093-4.97335C2.375093-5.148692 2.247572-5.276214 2.064259-5.276214C1.857036-5.276214 1.625903-5.084932 1.625903-4.845828C1.625903-4.670486 1.753425-4.542964 1.936737-4.542964C2.14396-4.542964 2.375093-4.734247 2.375093-4.97335ZM1.211457-2.048319L.781071-.948443C.74122-.828892 .70137-.73325 .70137-.597758C.70137-.207223 1.004234 .079701 1.42665 .079701C2.199751 .079701 2.526526-1.036115 2.526526-1.139726C2.526526-1.219427 2.462765-1.243337 2.406974-1.243337C2.311333-1.243337 2.295392-1.187547 2.271482-1.107846C2.088169-.470237 1.761395-.143462 1.44259-.143462C1.346949-.143462 1.251308-.183313 1.251308-.398506C1.251308-.589788 1.307098-.73325 1.41071-.980324C1.490411-1.195517 1.570112-1.41071 1.657783-1.625903L1.904857-2.271482C1.976588-2.454795 2.072229-2.701868 2.072229-2.83736C2.072229-3.235866 1.753425-3.514819 1.346949-3.514819C.573848-3.514819 .239103-2.399004 .239103-2.295392C.239103-2.223661 .294894-2.191781 .358655-2.191781C.462267-2.191781 .470237-2.239601 .494147-2.319303C.71731-3.076463 1.083935-3.291656 1.323039-3.291656C1.43462-3.291656 1.514321-3.251806 1.514321-3.028643C1.514321-2.948941 1.506351-2.83736 1.42665-2.598257L1.211457-2.048319Z" id="g5-105-drasiojs"></path>
<path d="M1.594022-1.307098C1.617933-1.42665 1.697634-1.729514 1.721544-1.849066C1.833126-2.279452 1.833126-2.287422 2.016438-2.550436C2.279452-2.940971 2.654047-3.291656 3.188045-3.291656C3.474969-3.291656 3.642341-3.124284 3.642341-2.749689C3.642341-2.311333 3.307597-1.40274 3.156164-1.012204C3.052553-.749191 3.052553-.70137 3.052553-.597758C3.052553-.143462 3.427148 .079701 3.769863 .079701C4.550934 .079701 4.877709-1.036115 4.877709-1.139726C4.877709-1.219427 4.813948-1.243337 4.758157-1.243337C4.662516-1.243337 4.646575-1.187547 4.622665-1.107846C4.431382-.454296 4.096638-.143462 3.793773-.143462C3.666252-.143462 3.602491-.223163 3.602491-.406476S3.666252-.765131 3.745953-.964384C3.865504-1.267248 4.216189-2.183811 4.216189-2.630137C4.216189-3.227895 3.801743-3.514819 3.227895-3.514819C2.582316-3.514819 2.16787-3.124284 1.936737-2.82142C1.880946-3.259776 1.530262-3.514819 1.123786-3.514819C.836862-3.514819 .637609-3.331507 .510087-3.084433C.318804-2.709838 .239103-2.311333 .239103-2.295392C.239103-2.223661 .294894-2.191781 .358655-2.191781C.462267-2.191781 .470237-2.223661 .526027-2.430884C.621669-2.82142 .765131-3.291656 1.099875-3.291656C1.307098-3.291656 1.354919-3.092403 1.354919-2.917061C1.354919-2.773599 1.315068-2.622167 1.251308-2.359153C1.235367-2.295392 1.115816-1.825156 1.083935-1.713574L.789041-.518057C.757161-.398506 .70934-.199253 .70934-.167372C.70934 .01594 .860772 .079701 .964384 .079701C1.107846 .079701 1.227397-.01594 1.283188-.111582C1.307098-.159402 1.370859-.430386 1.41071-.597758L1.594022-1.307098Z" id="g5-110-drasiojs"></path>
<path d="M2.199751-.573848C2.199751-.920548 1.912827-1.159651 1.625903-1.159651C1.279203-1.159651 1.0401-.872727 1.0401-.585803C1.0401-.239103 1.327024 0 1.613948 0C1.960648 0 2.199751-.286924 2.199751-.573848Z" id="g6-58-drasiojs"></path>
<path d="M2.331258 .047821C2.331258-.645579 2.10411-1.159651 1.613948-1.159651C1.231382-1.159651 1.0401-.848817 1.0401-.585803S1.219427 0 1.625903 0C1.78132 0 1.912827-.047821 2.020423-.155417C2.044334-.179328 2.056289-.179328 2.068244-.179328C2.092154-.179328 2.092154-.011955 2.092154 .047821C2.092154 .442341 2.020423 1.219427 1.327024 1.996513C1.195517 2.139975 1.195517 2.163885 1.195517 2.187796C1.195517 2.247572 1.255293 2.307347 1.315068 2.307347C1.41071 2.307347 2.331258 1.422665 2.331258 .047821Z" id="g6-59-drasiojs"></path>
<path d="M8.942466-7.292653C9.050062-7.699128 9.073973-7.81868 9.92279-7.81868C10.137983-7.81868 10.257534-7.81868 10.257534-8.033873C10.257534-8.16538 10.149938-8.16538 10.078207-8.16538C9.863014-8.16538 9.611955-8.141469 9.384807-8.141469H7.974097C7.746949-8.141469 7.49589-8.16538 7.268742-8.16538C7.185056-8.16538 7.041594-8.16538 7.041594-7.938232C7.041594-7.81868 7.12528-7.81868 7.352428-7.81868C8.069738-7.81868 8.069738-7.723039 8.069738-7.591532C8.069738-7.567621 8.069738-7.49589 8.021918-7.316563L7.292653-4.423412H3.682192L4.399502-7.292653C4.507098-7.699128 4.531009-7.81868 5.379826-7.81868C5.595019-7.81868 5.71457-7.81868 5.71457-8.033873C5.71457-8.16538 5.606974-8.16538 5.535243-8.16538C5.32005-8.16538 5.068991-8.141469 4.841843-8.141469H3.431133C3.203985-8.141469 2.952927-8.16538 2.725778-8.16538C2.642092-8.16538 2.49863-8.16538 2.49863-7.938232C2.49863-7.81868 2.582316-7.81868 2.809465-7.81868C3.526775-7.81868 3.526775-7.723039 3.526775-7.591532C3.526775-7.567621 3.526775-7.49589 3.478954-7.316563L1.865006-.884682C1.75741-.466252 1.733499-.3467 .908593-.3467C.633624-.3467 .549938-.3467 .549938-.119552C.549938 0 .681445 0 .71731 0C.932503 0 1.183562-.02391 1.41071-.02391H2.82142C3.048568-.02391 3.299626 0 3.526775 0C3.622416 0 3.753923 0 3.753923-.227148C3.753923-.3467 3.646326-.3467 3.466999-.3467C2.737733-.3467 2.737733-.442341 2.737733-.561893C2.737733-.573848 2.737733-.657534 2.761644-.753176L3.58655-4.076712H7.208966C7.005729-3.287671 6.396015-.789041 6.372105-.71731C6.240598-.358655 6.049315-.358655 5.34396-.3467C5.200498-.3467 5.092902-.3467 5.092902-.119552C5.092902 0 5.224408 0 5.260274 0C5.475467 0 5.726526-.02391 5.953674-.02391H7.364384C7.591532-.02391 7.84259 0 8.069738 0C8.16538 0 8.296887 0 8.296887-.227148C8.296887-.3467 8.18929-.3467 8.009963-.3467C7.280697-.3467 7.280697-.442341 7.280697-.561893C7.280697-.573848 7.280697-.657534 7.304608-.753176L8.942466-7.292653Z" id="g6-72-drasiojs"></path>
<path d="M10.855293-7.292653C10.962889-7.699128 10.9868-7.81868 11.835616-7.81868C12.062765-7.81868 12.170361-7.81868 12.170361-8.045828C12.170361-8.16538 12.086675-8.16538 11.859527-8.16538H10.424907C10.126027-8.16538 10.114072-8.153425 9.982565-7.962142L5.618929-1.06401L4.722291-7.902366C4.686426-8.16538 4.674471-8.16538 4.363636-8.16538H2.881196C2.654047-8.16538 2.546451-8.16538 2.546451-7.938232C2.546451-7.81868 2.654047-7.81868 2.833375-7.81868C3.56264-7.81868 3.56264-7.723039 3.56264-7.591532C3.56264-7.567621 3.56264-7.49589 3.514819-7.316563L1.984558-1.219427C1.841096-.645579 1.566127-.382565 .765131-.3467C.729265-.3467 .585803-.334745 .585803-.131507C.585803 0 .6934 0 .74122 0C.980324 0 1.590037-.02391 1.829141-.02391H2.402989C2.570361-.02391 2.773599 0 2.940971 0C3.024658 0 3.156164 0 3.156164-.227148C3.156164-.334745 3.036613-.3467 2.988792-.3467C2.594271-.358655 2.211706-.430386 2.211706-.860772C2.211706-.980324 2.211706-.992279 2.259527-1.159651L3.90934-7.746949H3.921295L4.913574-.32279C4.94944-.035866 4.961395 0 5.068991 0C5.200498 0 5.260274-.095641 5.32005-.203238L10.126027-7.806725H10.137983L8.404483-.884682C8.296887-.466252 8.272976-.3467 7.436115-.3467C7.208966-.3467 7.089415-.3467 7.089415-.131507C7.089415 0 7.197011 0 7.268742 0C7.47198 0 7.711083-.02391 7.914321-.02391H9.325031C9.528269-.02391 9.779328 0 9.982565 0C10.078207 0 10.209714 0 10.209714-.227148C10.209714-.3467 10.102117-.3467 9.92279-.3467C9.193524-.3467 9.193524-.442341 9.193524-.561893C9.193524-.573848 9.193524-.657534 9.217435-.753176L10.855293-7.292653Z" id="g6-77-drasiojs"></path>
<path d="M5.678705-4.853798L4.554919-7.47198C4.710336-7.758904 5.068991-7.806725 5.212453-7.81868C5.284184-7.81868 5.415691-7.830635 5.415691-8.033873C5.415691-8.16538 5.308095-8.16538 5.236364-8.16538C5.033126-8.16538 4.794022-8.141469 4.590785-8.141469H3.897385C3.16812-8.141469 2.642092-8.16538 2.630137-8.16538C2.534496-8.16538 2.414944-8.16538 2.414944-7.938232C2.414944-7.81868 2.52254-7.81868 2.677958-7.81868C3.371357-7.81868 3.419178-7.699128 3.53873-7.412204L4.961395-4.088667L2.367123-1.315068C1.936737-.848817 1.422665-.394521 .537983-.3467C.394521-.334745 .298879-.334745 .298879-.119552C.298879-.083686 .310834 0 .442341 0C.609714 0 .789041-.02391 .956413-.02391H1.518306C1.900872-.02391 2.319303 0 2.689913 0C2.773599 0 2.917061 0 2.917061-.215193C2.917061-.334745 2.833375-.3467 2.761644-.3467C2.52254-.37061 2.367123-.502117 2.367123-.6934C2.367123-.896638 2.510585-1.0401 2.857285-1.398755L3.921295-2.558406C4.184309-2.833375 4.817933-3.526775 5.080946-3.789788L6.336239-.848817C6.348194-.824907 6.396015-.705355 6.396015-.6934C6.396015-.585803 6.133001-.37061 5.750436-.3467C5.678705-.3467 5.547198-.334745 5.547198-.119552C5.547198 0 5.66675 0 5.726526 0C5.929763 0 6.168867-.02391 6.372105-.02391H7.687173C7.902366-.02391 8.129514 0 8.332752 0C8.416438 0 8.547945 0 8.547945-.227148C8.547945-.3467 8.428394-.3467 8.320797-.3467C7.603487-.358655 7.579577-.418431 7.376339-.860772L5.798257-4.566874L7.316563-6.192777C7.436115-6.312329 7.711083-6.611208 7.81868-6.73076C8.332752-7.268742 8.810959-7.758904 9.779328-7.81868C9.898879-7.830635 10.018431-7.830635 10.018431-8.033873C10.018431-8.16538 9.910834-8.16538 9.863014-8.16538C9.695641-8.16538 9.516314-8.141469 9.348941-8.141469H8.799004C8.416438-8.141469 7.998007-8.16538 7.627397-8.16538C7.543711-8.16538 7.400249-8.16538 7.400249-7.950187C7.400249-7.830635 7.483935-7.81868 7.555666-7.81868C7.746949-7.79477 7.950187-7.699128 7.950187-7.47198L7.938232-7.44807C7.926276-7.364384 7.902366-7.244832 7.770859-7.10137L5.678705-4.853798Z" id="g6-88-drasiojs"></path>
<path d="M3.140224-5.507347C3.092403-5.634869 3.052553-5.69066 2.933001-5.69066S2.773599-5.634869 2.725778-5.507347L1.075965-.797011C.948443-.438356 .70934-.270984 .278954-.263014V0C.533998-.02391 .812951-.02391 1.036115-.02391C1.171606-.02391 1.554172-.02391 1.912827 0V-.263014C1.522291-.270984 1.331009-.462267 1.331009-.669489C1.331009-.70934 1.331009-.72528 1.370859-.828892L2.685928-4.582814L4.064757-.645579C4.104608-.541968 4.104608-.526027 4.104608-.502117C4.104608-.263014 3.666252-.263014 3.459029-.263014V0C4.136488-.02391 4.152428-.02391 4.574844-.02391C4.885679-.02391 5.228394-.02391 5.587049 0V-.263014C5.116812-.263014 4.97335-.263014 4.861768-.581818L3.140224-5.507347Z" id="g7-3-drasiojs"></path>
<path d="M2.502615-5.076961C2.502615-5.292154 2.486675-5.300125 2.271482-5.300125C1.944707-4.98132 1.522291-4.790037 .765131-4.790037V-4.527024C.980324-4.527024 1.41071-4.527024 1.872976-4.742217V-.653549C1.872976-.358655 1.849066-.263014 1.091905-.263014H.812951V0C1.139726-.02391 1.825156-.02391 2.183811-.02391S3.235866-.02391 3.56264 0V-.263014H3.283686C2.526526-.263014 2.502615-.358655 2.502615-.653549V-5.076961Z" id="g7-49-drasiojs"></path>
<path d="M4.315816-8.284932C4.244085-8.524035 4.184309-8.53599 4.052802-8.53599C3.945205-8.53599 3.873474-8.51208 3.813699-8.320797L1.494396-1.147696C1.267248-.454296 .777086-.358655 .37061-.3467V0C.884682-.02391 .908593-.02391 1.422665-.02391C1.745455-.02391 2.331258-.02391 2.630137 0V-.3467C2.020423-.358655 1.793275-.6934 1.793275-.956413C1.793275-1.004234 1.793275-1.0401 1.853051-1.219427L3.718057-6.969863L5.678705-.920548C5.738481-.753176 5.738481-.729265 5.738481-.705355C5.738481-.3467 5.116812-.3467 4.817933-.3467V0C5.092902-.02391 6.01345-.02391 6.348194-.02391C6.694894-.02391 7.436115-.02391 7.746949 0V-.3467C7.10137-.3467 6.874222-.3467 6.73076-.800996L4.315816-8.284932Z" id="g8-3-drasiojs"></path>
<path d="M3.88543 2.905106C3.88543 2.86924 3.88543 2.84533 3.682192 2.642092C2.486675 1.43462 1.817186-.537983 1.817186-2.976837C1.817186-5.296139 2.379078-7.292653 3.765878-8.703362C3.88543-8.810959 3.88543-8.834869 3.88543-8.870735C3.88543-8.942466 3.825654-8.966376 3.777833-8.966376C3.622416-8.966376 2.642092-8.105604 2.056289-6.933998C1.446575-5.726526 1.171606-4.447323 1.171606-2.976837C1.171606-1.912827 1.338979-.490162 1.960648 .789041C2.666002 2.223661 3.646326 3.000747 3.777833 3.000747C3.825654 3.000747 3.88543 2.976837 3.88543 2.905106Z" id="g8-40-drasiojs"></path>
<path d="M3.371357-2.976837C3.371357-3.88543 3.251806-5.36787 2.582316-6.75467C1.876961-8.18929 .896638-8.966376 .765131-8.966376C.71731-8.966376 .657534-8.942466 .657534-8.870735C.657534-8.834869 .657534-8.810959 .860772-8.607721C2.056289-7.400249 2.725778-5.427646 2.725778-2.988792C2.725778-.669489 2.163885 1.327024 .777086 2.737733C.657534 2.84533 .657534 2.86924 .657534 2.905106C.657534 2.976837 .71731 3.000747 .765131 3.000747C.920548 3.000747 1.900872 2.139975 2.486675 .968369C3.096389-.251059 3.371357-1.542217 3.371357-2.976837Z" id="g8-41-drasiojs"></path>
<path d="M5.355915-3.825654C5.355915-4.817933 5.296139-5.786301 4.865753-6.694894C4.375592-7.687173 3.514819-7.950187 2.929016-7.950187C2.235616-7.950187 1.3868-7.603487 .944458-6.611208C.609714-5.858032 .490162-5.116812 .490162-3.825654C.490162-2.666002 .573848-1.793275 1.004234-.944458C1.470486-.035866 2.295392 .251059 2.917061 .251059C3.957161 .251059 4.554919-.37061 4.901619-1.06401C5.332005-1.960648 5.355915-3.132254 5.355915-3.825654ZM2.917061 .011955C2.534496 .011955 1.75741-.203238 1.530262-1.506351C1.398755-2.223661 1.398755-3.132254 1.398755-3.969116C1.398755-4.94944 1.398755-5.834122 1.590037-6.539477C1.793275-7.340473 2.402989-7.711083 2.917061-7.711083C3.371357-7.711083 4.064757-7.436115 4.291905-6.40797C4.447323-5.726526 4.447323-4.782067 4.447323-3.969116C4.447323-3.16812 4.447323-2.259527 4.315816-1.530262C4.088667-.215193 3.335492 .011955 2.917061 .011955Z" id="g8-48-drasiojs"></path>
<path d="M2.199751-4.578829C2.199751-4.901619 1.924782-5.152677 1.625903-5.152677C1.279203-5.152677 1.0401-4.877709 1.0401-4.578829C1.0401-4.220174 1.338979-3.993026 1.613948-3.993026C1.936737-3.993026 2.199751-4.244085 2.199751-4.578829ZM1.996513-.119552C1.996513 .298879 1.996513 1.147696 1.267248 2.044334C1.195517 2.139975 1.195517 2.163885 1.195517 2.187796C1.195517 2.247572 1.255293 2.307347 1.315068 2.307347C1.398755 2.307347 2.235616 1.422665 2.235616 .02391C2.235616-.418431 2.199751-1.159651 1.613948-1.159651C1.267248-1.159651 1.0401-.896638 1.0401-.585803C1.0401-.263014 1.267248 0 1.625903 0C1.853051 0 1.936737-.071731 1.996513-.119552Z" id="g8-59-drasiojs"></path>
<path d="M7.627397-3.060523H7.364384C7.07746-1.195517 6.790535-.3467 4.770112-.3467H3.144209C2.618182-.3467 2.594271-.430386 2.594271-.824907V-4.052802H3.682192C4.829888-4.052802 4.961395-3.682192 4.961395-2.654047H5.224408V-5.798257H4.961395C4.961395-4.770112 4.829888-4.399502 3.682192-4.399502H2.594271V-7.316563C2.594271-7.711083 2.618182-7.79477 3.144209-7.79477H4.734247C6.491656-7.79477 6.862267-7.197011 7.041594-5.475467H7.304608L6.993773-8.141469H.490162V-7.79477H.729265C1.590037-7.79477 1.625903-7.675218 1.625903-7.232877V-.908593C1.625903-.466252 1.590037-.3467 .729265-.3467H.490162V0H7.149191L7.627397-3.060523Z" id="g8-69-drasiojs"></path>
<path d="M7.137235-7.256787C7.137235-7.699128 7.173101-7.81868 8.033873-7.81868H8.272976V-8.16538C7.986052-8.141469 7.005729-8.141469 6.659029-8.141469C6.300374-8.141469 5.32005-8.141469 5.033126-8.16538V-7.81868H5.272229C6.133001-7.81868 6.168867-7.699128 6.168867-7.256787V-4.423412H2.594271V-7.256787C2.594271-7.699128 2.630137-7.81868 3.490909-7.81868H3.730012V-8.16538C3.443088-8.141469 2.462765-8.141469 2.116065-8.141469C1.75741-8.141469 .777086-8.141469 .490162-8.16538V-7.81868H.729265C1.590037-7.81868 1.625903-7.699128 1.625903-7.256787V-.908593C1.625903-.466252 1.590037-.3467 .729265-.3467H.490162V0C.777086-.02391 1.75741-.02391 2.10411-.02391C2.462765-.02391 3.443088-.02391 3.730012 0V-.3467H3.490909C2.630137-.3467 2.594271-.466252 2.594271-.908593V-4.076712H6.168867V-.908593C6.168867-.466252 6.133001-.3467 5.272229-.3467H5.033126V0C5.32005-.02391 6.300374-.02391 6.647073-.02391C7.005729-.02391 7.986052-.02391 8.272976 0V-.3467H8.033873C7.173101-.3467 7.137235-.466252 7.137235-.908593V-7.256787Z" id="g8-72-drasiojs"></path>
<path d="M8.571856-2.905106C8.571856-4.016936 8.571856-4.351681 8.296887-4.734247C7.950187-5.200498 7.388294-5.272229 6.981818-5.272229C5.989539-5.272229 5.487422-4.554919 5.296139-4.088667C5.128767-5.009215 4.483188-5.272229 3.730012-5.272229C2.570361-5.272229 2.116065-4.27995 2.020423-4.040847H2.008468V-5.272229L.382565-5.140722V-4.794022C1.195517-4.794022 1.291158-4.710336 1.291158-4.124533V-.884682C1.291158-.3467 1.159651-.3467 .382565-.3467V0C.6934-.02391 1.338979-.02391 1.673724-.02391C2.020423-.02391 2.666002-.02391 2.976837 0V-.3467C2.211706-.3467 2.068244-.3467 2.068244-.884682V-3.108344C2.068244-4.363636 2.893151-5.033126 3.634371-5.033126S4.542964-4.423412 4.542964-3.694147V-.884682C4.542964-.3467 4.411457-.3467 3.634371-.3467V0C3.945205-.02391 4.590785-.02391 4.925529-.02391C5.272229-.02391 5.917808-.02391 6.228643 0V-.3467C5.463512-.3467 5.32005-.3467 5.32005-.884682V-3.108344C5.32005-4.363636 6.144956-5.033126 6.886177-5.033126S7.79477-4.423412 7.79477-3.694147V-.884682C7.79477-.3467 7.663263-.3467 6.886177-.3467V0C7.197011-.02391 7.84259-.02391 8.177335-.02391C8.524035-.02391 9.169614-.02391 9.480448 0V-.3467C8.88269-.3467 8.583811-.3467 8.571856-.705355V-2.905106Z" id="g8-109-drasiojs"></path>
<path d="M5.487422-2.558406C5.487422-4.100623 4.315816-5.332005 2.929016-5.332005C1.494396-5.332005 .358655-4.064757 .358655-2.558406C.358655-1.028144 1.554172 .119552 2.917061 .119552C4.327771 .119552 5.487422-1.052055 5.487422-2.558406ZM2.929016-.143462C2.486675-.143462 1.948692-.334745 1.601993-.920548C1.279203-1.458531 1.267248-2.163885 1.267248-2.666002C1.267248-3.120299 1.267248-3.849564 1.637858-4.387547C1.972603-4.901619 2.49863-5.092902 2.917061-5.092902C3.383313-5.092902 3.88543-4.877709 4.208219-4.411457C4.578829-3.861519 4.578829-3.108344 4.578829-2.666002C4.578829-2.247572 4.578829-1.506351 4.267995-.944458C3.93325-.37061 3.383313-.143462 2.929016-.143462Z" id="g8-111-drasiojs"></path>
<path d="M2.008468-4.805978H3.694147V-5.152677H2.008468V-7.352428H1.745455C1.733499-6.228643 1.303113-5.080946 .215193-5.045081V-4.805978H1.231382V-1.482441C1.231382-.155417 2.116065 .119552 2.749689 .119552C3.502864 .119552 3.897385-.621669 3.897385-1.482441V-2.163885H3.634371V-1.506351C3.634371-.645579 3.287671-.143462 2.82142-.143462C2.008468-.143462 2.008468-1.255293 2.008468-1.458531V-4.805978Z" id="g8-116-drasiojs"></path>
<path d="M3.347447-2.82142C3.694147-3.275716 4.196264-3.921295 4.423412-4.172354C4.913574-4.722291 5.475467-4.805978 5.858032-4.805978V-5.152677C5.34396-5.128767 5.32005-5.128767 4.853798-5.128767C4.399502-5.128767 4.375592-5.128767 3.777833-5.152677V-4.805978C3.93325-4.782067 4.124533-4.710336 4.124533-4.435367C4.124533-4.23213 4.016936-4.100623 3.945205-4.004981L3.180075-3.036613L2.247572-4.267995C2.211706-4.315816 2.139975-4.423412 2.139975-4.507098C2.139975-4.578829 2.199751-4.794022 2.558406-4.805978V-5.152677C2.259527-5.128767 1.649813-5.128767 1.327024-5.128767C.932503-5.128767 .908593-5.128767 .179328-5.152677V-4.805978C.789041-4.805978 1.016189-4.782067 1.267248-4.459278L2.666002-2.630137C2.689913-2.606227 2.737733-2.534496 2.737733-2.49863S1.80523-1.291158 1.685679-1.135741C1.159651-.490162 .633624-.358655 .119552-.3467V0C.573848-.02391 .597758-.02391 1.111831-.02391C1.566127-.02391 1.590037-.02391 2.187796 0V-.3467C1.900872-.382565 1.853051-.561893 1.853051-.729265C1.853051-.920548 1.936737-1.016189 2.056289-1.171606C2.235616-1.422665 2.630137-1.912827 2.917061-2.283437L3.897385-1.004234C4.100623-.74122 4.100623-.71731 4.100623-.645579C4.100623-.549938 4.004981-.358655 3.682192-.3467V0C3.993026-.02391 4.578829-.02391 4.913574-.02391C5.308095-.02391 5.332005-.02391 6.049315 0V-.3467C5.415691-.3467 5.200498-.37061 4.913574-.753176L3.347447-2.82142Z" id="g8-120-drasiojs"></path>
</defs>
<g id="page285-drasiojs">
<g fill="currentColor" transform="matrix(1 0 0 1 -196.5121 3.58104)">
<use href="#g8-48-drasiojs" x="202.345346" y="-10.945086"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -249.2228 3.58104)">
<use href="#g8-69-drasiojs" x="285.250182" y="-10.945086"></use>
<use href="#g8-120-drasiojs" x="293.214688" y="-10.945086"></use>
<use href="#g8-116-drasiojs" x="299.392845" y="-10.945086"></use>
<use href="#g7-49-drasiojs" x="303.945167" y="-15.959606"></use>
<use href="#g7-3-drasiojs" x="303.945167" y="-7.98957"></use>
<use href="#g8-40-drasiojs" x="310.315808" y="-10.945086"></use>
<use href="#g6-72-drasiojs" x="314.868134" y="-10.945086"></use>
<use href="#g5-110-drasiojs" x="324.567114" y="-9.151823"></use>
<use href="#g2-0-drasiojs" x="329.705316" y="-9.151823"></use>
<use href="#g7-49-drasiojs" x="336.291823" y="-9.151823"></use>
<use href="#g8-40-drasiojs" x="341.024138" y="-10.945086"></use>
<use href="#g6-88-drasiojs" x="345.576464" y="-10.945086"></use>
<use href="#g8-59-drasiojs" x="356.231572" y="-10.945086"></use>
<use href="#g8-3-drasiojs" x="361.475731" y="-10.945086"></use>
<use href="#g8-41-drasiojs" x="369.600745" y="-10.945086"></use>
<use href="#g6-59-drasiojs" x="374.153071" y="-10.945086"></use>
<use href="#g6-77-drasiojs" x="379.39723" y="-10.945086"></use>
<use href="#g8-41-drasiojs" x="391.970837" y="-10.945086"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -218.28 3.58104)">
<use href="#g6-72-drasiojs" x="389.92245" y="-10.945086"></use>
<use href="#g5-110-drasiojs" x="400.54506" y="-15.283522"></use>
<use href="#g8-40-drasiojs" x="406.181394" y="-10.945086"></use>
<use href="#g6-88-drasiojs" x="410.73372" y="-10.945086"></use>
<use href="#g8-59-drasiojs" x="421.388828" y="-10.945086"></use>
<use href="#g8-3-drasiojs" x="426.632987" y="-10.945086"></use>
<use href="#g8-41-drasiojs" x="434.758001" y="-10.945086"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -245.529 3.58104)">
<use href="#g8-72-drasiojs" x="490.901004" y="-10.945086"></use>
<use href="#g8-111-drasiojs" x="499.67635" y="-10.945086"></use>
<use href="#g8-109-drasiojs" x="505.529341" y="-10.945086"></use>
<use href="#g7-3-drasiojs" x="515.284313" y="-9.151823"></use>
<use href="#g8-40-drasiojs" x="521.654954" y="-10.945086"></use>
<use href="#g6-72-drasiojs" x="526.20728" y="-10.945086"></use>
<use href="#g5-105-drasiojs" x="535.90626" y="-9.151823"></use>
<use href="#g8-40-drasiojs" x="539.287532" y="-10.945086"></use>
<use href="#g6-88-drasiojs" x="543.839858" y="-10.945086"></use>
<use href="#g8-59-drasiojs" x="554.494966" y="-10.945086"></use>
<use href="#g8-3-drasiojs" x="559.739124" y="-10.945086"></use>
<use href="#g8-41-drasiojs" x="567.864139" y="-10.945086"></use>
<use href="#g6-59-drasiojs" x="572.416465" y="-10.945086"></use>
<use href="#g6-77-drasiojs" x="577.660624" y="-10.945086"></use>
<use href="#g8-41-drasiojs" x="590.234231" y="-10.945086"></use>
</g>
<g fill="currentColor" transform="matrix(1 0 0 1 -198.138 3.58104)">
<use href="#g8-48-drasiojs" x="571.737956" y="-10.945086"></use>
<use href="#g6-58-drasiojs" x="577.590946" y="-10.945086"></use>
</g>
<path d="M17.031-10.351563H30.203" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M27.95701-13.22267C28.41013-11.50001 29.42185-10.68751 30.441384-10.351572C29.42185-10.019541 28.41013-9.20704 27.95701-7.48438" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M152.6484-10.351563H165.8203" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M163.57434-13.22267C164.02746-11.50001 165.03918-10.68751 166.05871-10.351572C165.03918-10.019541 164.02746-9.20704 163.57434-7.48438" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M226.3789-10.351563H239.5508" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M237.30515-13.22267C237.75828-11.50001 238.77-10.68751 239.789527-10.351572C238.77-10.019541 237.75828-9.20704 237.30515-7.48438" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
<g fill="currentColor" transform="matrix(1 0 0 1 36.493 -2.2206)">
<use href="#g5-104-drasiojs" x="194.271482" y="-10.945086"></use>
</g>
<path d="M354.609-10.351563H367.781" fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width=".47818"></path>
<path d="M365.53166-13.22267C365.98479-11.50001 367.00041-10.68751 368.019946-10.351572C367.00041-10.019541 365.98479-9.20704 365.53166-7.48438" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width=".47818"></path>
</g>
</svg>
</div>
The map @h@ is the canonical map sending a cohomology class represented by a cochain @c@, to the map which sends any homology class represented by a chain @\alpha@ to the element @\langle c, \alpha \rangle@ of @Λ@.

This exact sequence measures how close the cohomology group is to be the dual of homology.