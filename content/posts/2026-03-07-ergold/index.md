+++
title = "Passer du clavier CSA à Ergo-L"
date = "2026-03-07"
showFullContent = false
+++

Jusqu'à maintenant, je me suis presque[^1] toujours servi de la [disposition canadienne multilingue standard](https://en.wikipedia.org/wiki/CSA_keyboard).
Elle permet d'écrire en anglais et en français sans trop de mal.
Un objectif principal de cette disposition est de minimiser les touches mortes.
Par exemple, on peut entrer les caractères "à", "ç" et "è" directement, ce qui est assez pratique.
Cependant! Mes doigts partent en incartade quand je leur demande une paire de crochets ou des accolades.
Ma main fait des frasques si j'ai le malheur de lui quémander un diacritique tout nu.
Je fige si je dois fermer une balise HTML ou ouvrir une commande TeX.

Malgré tout ça, je me suis habitué à la disposition canadienne et je vis avec ses défauts lorsque j'écris du code ou que je fais de la mise en page.
Après tout, on s'habitue à tout...
Oui!.. mais!.. si, un samedi matin pluvieux, on tombe par hasard sur la prometteuse [disposition Ergo-L](https://ergol.org/), on serait fou de ne pas au moins tenter de briser l'habitude!

Cette toute nouvelle disposition promet:

- de supporter l'anglais [mieux](https://ergol.org/stats/) que Dvorak;
- de supporter le français [mieux](https://ergol.org/stats/) que Bépo;
- de réduire les extensions de doigt, les déviations ulnaires, l’effort de saisie (bref, de m'éviter le pirouettage quand je programme);
- de préserver les raccourcis clavier et les chiffres en direct.

Pour ce faire, la disposition Ergo-L intègre l'approche 1DFH, "1u distance from home", une contrainte de design qui me mènera supposément à ne jamais devoir déplacer mes doigts de plus d'une touche ("1 unité") par rapport à la position de repos.
Les concepteurs d'Ergo-L ont décidé de n’utiliser essentiellement aucune touche en dehors du pavé de 3×10 touches centrales.
Au lieu de s'étendre sur le clavier, la disposition est organisée en couches, ce qui lui permet de rester compacte.

![](ergol.svg)

On note la touche morte "étoile" en haut à droite.
Elle permet d'accéder aux caractères de couleur verte.
Vu la fréquence des accents en français, devoir taper deux touches pour écrire "é" me semble presque rédhibitoire.
Je ne laisse pas cette critique me décourager: seule l'expérience m'apprendra si c'est vraiment défavorable, et à quel point.

On apprécie aussi que les touches Q-A-S-X-V sont à la même place qu'avec la disposition canadienne, ce qui va me permettre de continuer à profiter des raccourcis claviers standards pour sauvegarder, coller, tout sélectionner, etc., qui sont bien incrustés dans ma mémoire musculaire.

Finalement, on note que les touches de couleur lavande sont accessibles en gardant la touche AltGr appuyée (le Alt du pouce droit).
Disons que je suis sceptique.
Par exemple, la fréquence à laquelle j'utilise le tiret "-" me pousse à croire que devoir appuyer préalablement sur AltGr va être ultra chiant.

(Je ne sais pas pour le moment ce que fait la touche "alpha" en rouge en bas à droite -- keep tuned).

## Plan d'apprentissage

Je vais utiliser la disposition Ergo-L dès que possible, sans nécessairement connaître l'emplacement de toutes les touches.
Ce faisant, je vais prioriser la précision à la vitesse, et je m'engage à mettre fin à une séance d'entraînement dès que je m'emmerde.
Je vais me servir du site web [Monkeytype](https://monkeytype.com/) afin de mesurer mon progrès.
Après un test de 60 secondes sur Monkeytype en utilisant le corpus french 2k, je fais du 71 mots par minute avec une précision de 98%.

Pour s'entraîner, en plus de Monkeytype, le site mère du projet Ergo-L donne accès à une [page pour apprendre](https://ergol.org/dactylo/#ergol).
Sur cette page, on peut s'initier à Ergo-L, que le pilote soit installé sur son ordi ou pas (il est très facile à installer, soit dit en passant).

Mes objectifs sont:

- d'atteindre 35 mots par minute avec une précision d'au moins 95% d'ici le 1er avril;
- de voir si mes jugements au sujet de la touche étoile et AltGr sont légitimes;
- d'évaluer si c'est réellement plus ergonomique lorsque j'écris du code;
- d'estimer si la disposition me permettra d'éventuellement dépasser les 100 wpm.

[^1]: Pendant une courte période, j'ai tenté l'expérience [Optimot](https://bepo.fr/wiki/Optimot). Cependant, il n'y avait pas de pilote natif Windows et il fallait utiliser AutoHotkey. J'espère que ce n'est plus comme ça parce que c'est absolument horrible. En plus, je commençais un nouveau travail en tant que développeur et je ne voulais pas être "that guy". J'ai donc abandonné le projet Optimot; reprendre Qwerty après ça était une expérience psychédélique.