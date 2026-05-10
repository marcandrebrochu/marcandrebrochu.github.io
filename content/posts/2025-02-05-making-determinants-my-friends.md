+++
title = "The determinant of a matrix is just the product of its columns"
date = "2025-02-05"
+++

A fact I've known for a very long time, but never bothered to prove for myself, is the unicity of the determinant for square matrices. More precisely, let @A@ be any commutative ring with identity; then the determinant is the only @A@-valued function on matrices that: (i) is linear on each column, (ii) is such that switching two columns changes the sign, and (iii) sends the identity matrix to 1.

A nice way to prove this is to find an explicit formula for the determinant of a square matrix using only these three properties. Let's do the 2x2 matrices for a start. The linearity in the columns means we can decompose the problem into smaller ones:

@@
\begin{align*}
\begin{vmatrix}
a & b \\
c & d
\end{vmatrix} =
ad\begin{vmatrix}1 & 0 \\ 0 & 1\end{vmatrix} +
cd\begin{vmatrix}0 & 0 \\ 1 & 1\end{vmatrix} +
ab\begin{vmatrix}1 & 1 \\ 0 & 0\end{vmatrix} +
bc\begin{vmatrix}0 & 1 \\ 1 & 0\end{vmatrix}.
\end{align*}
@@

From the fact switching two columns changes the sign, the determinants in the middle give out zero, and the one on the right evaluates to @-bc@. Hence the determinant comes out to be @ad-bc@, as expected.

The idea of the general proof is contained in the previous 2x2 case. The argument is as follows. From linearity in the columns, we can split the general determinant problem into computing the determinant of all matrices which are made up of standard basis vectors (i.e. in each column there is exactly one 1 and the rest are zeroes). As soon as two columns are identical, the determinant vanishes, hence the only determinants left to calculate are those for matrices made up of standard basis vectors that are all different, that is to say, matrices where there's exactly one 1 in each row and each column, the rest being zeroes. In other words, the only things left are all of the column (or rows) permutations of the identity matrix. From that description we can simply read off the known determinant formula:

@@
\begin{align*}
\begin{vmatrix}
a_{11} & a_{12} & \dots & a_{1n} \\
a_{21} & a_{22} & \dots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{n1} & a_{n2} & \dots & a_{nn}
\end{vmatrix} = \sum_{\sigma \in S_n} \operatorname{sign}(\sigma)\cdot a_{\sigma(1),1}a_{\sigma(2),2}\dots a_{\sigma(n),n}.
\end{align*}
@@

## Computing the determinant is just multiplying the columns

Let's get a little more abstract. Consider @V@ to be a @n@-dimensional vector space over some field @\kappa@. We could use free @A@-modules instead, where @A@ is a commutative ring with unity, but I believe you'll forgive me if we stick with the vector space. The @n@-th exterior power @V^{\wedge n}@ is a one-dimensional vector space over @\kappa@. The proof is left to the reader; it's fun and it uses the same idea as the proof outline above. Anyways, writing @(e_i)_{1\leq i \leq n}@ for a basis for @V@, the @n@-blade @e_1 \wedge e_2 \wedge \dots \wedge e_n@ is a basis for @V^{\wedge n}@.

Multilinear alternating maps @F : V^n \to \kappa@ are in a natural bijective correspondence with linear maps @F' : V^{\wedge n} \to \kappa@ such that @F(v_1,v_2,\dots,v_n) = F'(v_1 \wedge v_2 \wedge \dots \wedge v_n)@. The proof is left to the reader hehe. Hence there is a unique multilinear alternating map @V^n \to \kappa@ that sends the identity matrix to @1 \in \kappa@; we call that map the determinant. What!! Isn't the determinant a number?? Well, yes and no. We often identify complicated objects with their images for simplicity. The determinant-number is the image of the determinant-map. Notice that we have *one* determinant-map, which is able to compute determinants for any correctly-sized matrix you throw at it.

Basically as a consequence of the universal property I mentioned in the previous paragraph, defining the determinant in this way gives us the following equation:
@@v_1 \wedge v_2 \wedge \dots \wedge v_n = \det(v_1,v_2, \dots, v_n)\cdot e_1 \wedge e_2 \wedge \dots \wedge e_n.@@
Hence to compute the determinant you just multiply the columns using the wedge product, and reduce in @V^{\wedge n}@ until you find it.

For instance,
@@
\begin{align*}
\begin{vmatrix}a&b\\c&d\end{vmatrix} &:\text{\ computed by\ } (ae_1+ce_2)\wedge (be_1 + de_2) \\
&= ae_1 \wedge be_1 + ae_1\wedge de_2 + ce_2 \wedge be_1 + ce_2\wedge de_2 \\
&= ab\cdot e_1\wedge e_1 + ad\cdot e_1\wedge e_2 + cb\cdot e_2\wedge e_1 + cd\cdot e_2 \wedge e_2 \\
&= (ad - bc)\cdot e_1 \wedge e_2.
\end{align*}
@@

If you can accept that the @n@-blade @e_1 \wedge e_2 \wedge\dots \wedge e_n@ represents the volume of the @n@-dimensional cube, then this formula says the determinant is the volume of the @n@-parallelotope spanned by the columns of the matrix.