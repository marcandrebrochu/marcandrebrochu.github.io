---
title: Le radical est l'intersection des idéaux maximaux
tags: géométrie algébrique, notes
---

$\DeclareMathOperator{\ev}{ev}$
L'exercice 1.1 d'Ottem et Ellingsrud demande:

> In any ring the radical of an ideal $\mathfrak{a}$ equals the intersection of the prime ideals containing the ideal. Show, using the Nullstellensatz, that in the polynomial ring $k[x_1,\dots,x_n]$ the radical $\sqrt{\mathfrak{a}}$ equals the intersection of all the *maximal* ideals containing $\mathfrak{a}$.

Tout d'abord, je souhaite me rafraîchir la mémoire et redémontrer la première assertion qu'ils font, c'est-à-dire que le radical d'un idéal est en fait l'intersection de tous les idéaux premiers qui le contiennent. Je trouve que c'est une caractérisation intéressante du radical. Peut-être même que je vais créer un autre article spécifiquement pour ça ! La preuve n'est pas triviale, en tout cas pour l'une des deux inclusions.
La première inclusion est facile à voir: soit $\{\mathfrak{p}_i\}_{i\in I}$ la collection de tous les idéaux premiers qui contiennent $\mathfrak{a}$. Vu que pour tout idéal premier $x^n \in \mathfrak{p_i}$ implique que $x\in\mathfrak{p_i}$ (pour un certain entier $n\geq 1$), il est clair que $\sqrt{\mathfrak{a}}\subseteq \bigcap_{i\in I}\mathfrak{p_i}$.
C'est la seconde inclusion qui pose problème. Je vais la montrer par contrapositive: soit $x\notin \sqrt{\mathfrak{a}}$. Je considère la collection $\mathcal{I}$ des idéaux $\mathfrak{b}\supseteq \mathfrak{a}$ tels que $x^n\notin\mathfrak{b}$ pour tout entier $n\geq 1$.
Si j'ordonne partiellement cette collection par l'inclusion, le lemme de Zorn me donne l'existence d'un élément maximal $\mathfrak{p}\in\mathcal{I}$. Je veux montrer que $\mathfrak{p}$ est premier. Soit $a$ et $b$ deux éléments de l'anneau tels que $a,b\notin \mathfrak{p}$. Par maximalité, ni $\mathfrak{p}+(a)$ ni $\mathfrak{p}+(b)$ ne font partie de la collection $\mathcal{I}$. Par exemple, comme $a\notin \mathfrak{p}$, l'idéal $\mathfrak{p}+(a)$ (i.e. le plus petit idéal qui contient à la fois $\mathfrak{p}$ et $(a)$) contient strictement $\mathfrak{p}$. Donc il existe deux entiers $n$ et $m$ tels que $x^n\in \mathfrak{p}+(a)$ et $x^m\in\mathfrak{p}+(b)$. Puisque l'idéal $\mathfrak{p}+(ab)$ contient $x^{n+m}$, il n'est lui non plus pas contenu dans $\mathcal{I}$. En particulier $ab\notin\mathfrak{p}$ car sinon ajouter $(ab)$ à $\mathfrak{p}$ n'aurait rien changé, ce qui n'est pas le cas. Cela prouve que $\mathfrak{p}$ est premier. Mais alors $\bigcap_{i\in I}\mathfrak{p}_i\subseteq \mathfrak{p}$ et puisque $x\notin \mathfrak{p}$ par construction, je retrouve bien que $x\notin\bigcap_{i\in I}\mathfrak{p_i}$, ce qu'il fallait démontrer.

Tout ce gros paragraphe n'est toutefois pas ce qu'il faut faire dans l'exercice, oops. En fait l'exercice est beaucoup plus facile. Déjà, comme tout idéal maximal est premier, j'obtiens par le même argument que dans le paragraphe précédent l'inclusion $\sqrt{\mathfrak{a}}\subseteq \bigcap_{i\in I}\mathfrak{m_i}$, où $\{\mathfrak{m}_i\}_{i\in I}$ est la collection des idéaux maximaux contenant $\mathfrak{a}$.
Pour l'autre inclusion, la version faible du Nullstellensatz nous donne que tous les idéaux maximaux de $k[x_1,\dots,x_n]$ sont précisément ceux de la forme $(x_1-a_1,\dots,x_n-a_n)$ pour $a\in \mathbb{A}^n(k)$.

Il est utile de noter que $(x_1-a_1,\dots,x_n-a_n)$ est exactement le noyau de l'application d'évaluation, $\ker(\ev_a)$. En effet, il est évident que $(x_1-a_1,\dots,x_n-a_n)\subseteq \ker(\ev_a)$. Soit $f\in \ker(\ev_a)$; l'astuce est de prendre un autre polynôme $g$ tel que $g(x-a)=f(x)$ (ça devrait vous rappeller *fortement* la preuve de l'existence d'une factorisation lorsque le polynôme n'a qu'une seule variable, où le truc consiste à enlever le terme constant du polynôme qu'on cherche à factoriser). Alors par construction $g\in\ker(\ev_0)$ et il est clair que $\ker(\ev_0)=(x_1,\dots,x_n)$. Donc $f(x)=(x_1-a_1)p_1(x)+\dots+(x_n-a_n)p_n(x)$, ce qui démontre que $(x_1-a_1,\dots,x_n-a_n)\supseteq \ker(\ev_a)$. Un corollaire immédiat est que $\ker(\ev_a)$ est un idéal maximal puisque $k$ est un corps (mais nous savions déjà cela).

Soit $x\in Z(\mathfrak{a})$. Clairement $\mathfrak{a}\subseteq \ker(\ev_x)$, d'où nous concluons que $\bigcap_{i\in I}\mathfrak{m}_i \subseteq \ker(\ev_x)$. Comme c'est vrai pour chaque $x$,
$$\bigcap_{i\in I}\mathfrak{m}_i\subseteq \bigcap_{x\in Z(\mathfrak{a})} \ker(\ev_x)$$
et si nous avons un polynôme $f\in \bigcap_{i\in I}\mathfrak{m}_i$, nous pouvons conclure que $f$ s'annule sur tous les éléments de $Z(\mathfrak{a})$, i.e. $f\in I(Z(\mathfrak{a}))=\sqrt{\mathfrak{a}}$.