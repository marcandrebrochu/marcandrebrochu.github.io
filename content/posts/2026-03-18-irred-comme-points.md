+++
title = "Compter des composantes irréductibles est comme compter des points"
date = "2026-03-18"
+++

Pour des ensembles de cardinalité finie, on a le principe d'inclusion-exclusion:
@@
  |A \cup B| = |A| + |B| - |A \cap B|.
@@

En comparaison, si @X@ et @Y@ sont deux parties fermées d'un espace topologique ayant chacune un nombre fini de composantes irréductibles[^1], et qu'on note @n(-)@ le nombre de composantes irréductibles, alors
@@
  n(X \cup Y) = n(X) + n(Y) - n(X \cap Y).
@@

On déduit la première équation de celle-ci en donnant aux ensembles @A@ et @B@ la topologie discrète.

[^1]: Une *composante irréductible* est une partie irréductible maximale pour l'inclusion. Un espace topologique est dit *irréductible* ssi de tout recouvrement par un nombre fini de fermés on peut extraire un fermé qui, seul, recouvre déjà tout l'espace.