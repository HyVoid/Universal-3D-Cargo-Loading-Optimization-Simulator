[ 🌐 عربي ](README.ar.md) | [ 🇩🇪 Deutsch ](README.de.md) | [ 🇫🇷 Français ](README.fr.md) | [ 🇳🇱 Nederlands ](README.nl.md) | [ 🇪🇸 Español ](README.sp.md) | [ 🇨🇳 中文 ](README.zh.md) | [ 🇬🇧 English ](README.md)
# 🚛 Simulateur universel d'optimisation du chargement de conteneurs 3D

## ❓ Problème

À l'expédition, estimer « combien de cartons tiennent dans un conteneur » par l'expérience mène généralement à l'un de deux résultats : sous-remplissage et gaspillage du coût de fret, ou dépassement de capacité à la dernière minute et changement de conteneur dans la précipitation. Même avec un chiffre, on ne sait toujours pas *comment* charger — quelle orientation plaquer contre la paroi, par où commencer le chargement, ou si la marchandise va se déplacer et se heurter en transit.

---

## 🔍 Pourquoi cela arrive

Le chargement 3D (bin-packing) est fondamentalement un problème NP-difficile. À mesure que la combinaison des dimensions de carton et de conteneur croît, le nombre d'agencements possibles augmente exponentiellement — le calcul manuel exhaustif n'est pas viable. Même avec une seule spécification produit, quelques centimètres de différence dans l'orientation du carton contre la largeur interne du conteneur peuvent s'accumuler en une grande zone morte à l'arrière.

Les logiciels professionnels d'empilement existants ciblent soit les clients logistiques d'entreprise à un coût prohibitif, soit s'accompagnent d'une interface complexe peu pratique pour une estimation rapide avant expédition.

---

## 💰 Conséquence commerciale

- Une baisse de 5 % du taux de chargement se traduit directement par une augmentation de 5 %–8 % du coût de fret effectif pour cette expédition
- Les mouvements latéraux de marchandise et les dommages par collision en transit sont courants dans le transport de marchandises sèches, mais tendent à être classés comme « usure et perte normales » sans suivi quantifié
- Sans chiffre de chargement clair, les expéditeurs commandent par défaut un conteneur supplémentaire « par précaution » — une habitude qui accumule des coûts significatifs à grande échelle

---

## 💡 Logique de la solution

Ce simulateur répond à ces enjeux par quatre mécanismes centraux :

**① Algorithme anti-balancement à jeu nul**

Teste exhaustivement les deux orientations (longueur × largeur) du produit pour trouver l'agencement qui correspond exactement à la largeur interne du conteneur, éliminant le jeu latéral à la source.

**② Logique de chargement en profondeur d'abord**

Charge de l'arrière du conteneur vers l'avant, garde le centre de gravité stable et rend le déchargement côté porte simple — conforme à la pratique terrain standard.

**③ Gestion des tampons sur quatre côtés**

Tout en maximisant l'utilisation de l'espace, contrôle la distribution des écarts entre la marchandise et toutes les parois intérieures, réduisant le risque de choc de la marchandise dû aux vibrations du transport.

**④ Stabilisation du centre de gravité par la physique**

Applique strictement la séquence « bas-d'abord → arrière-d'abord », empêchant la marchandise de flotter librement et gardant le centre de gravité du véhicule vers l'avant, conformément aux normes de sécurité du transport routier.

---

## 📋 Mode d'emploi

**Étape 1 : Ouvrir le simulateur**

[Cliquer ici pour ouvrir le simulateur →](https://hyvoid.github.io/Universal-3D-Cargo-Loading-Optimization-Simulator/)

**Étape 2 : Saisir les paramètres** (unité : **cm**)

| Paramètre | Description |
|-----------|-------------|
| 🚚 Dimensions du conteneur | Longueur, largeur et hauteur internes réellement utilisables de votre camion ou conteneur |
| 📦 Dimensions du produit | Longueur, largeur et hauteur extérieures du carton (la hauteur est fixée à la verticale ; l'algorithme n'intervertit que longueur et largeur) |
| 🎯 Nombre de chargement cible | Saisissez votre quantité de commande ; laissez vide ou mettez `0` pour calculer la capacité maximale du conteneur |

**Étape 3 : Générer le plan**

Cliquez le bouton bleu **« Générer le plan 3D optimal »**. Le système exécute le calcul et produit automatiquement une visualisation 3D.

**Étape 4 : Interagir et examiner**

| Action | Fonction |
|--------|----------|
| 🖱️ Clic gauche & glisser | Rotation panoramique à 360° |
| 🖱️ Clic droit & glisser | Déplacer la vue |
| ⚙️ Molette de souris | Zoomer pour le détail ou dézoomer pour la vue d'ensemble |
| 📊 Tableau de bord statistique | Apparaît automatiquement après la génération, affichant la limite de capacité, les largeurs d'écart et l'espace restant près de la porte |

---

## 📌 Exemple

**Scénario** : Un expéditeur prévoit d'expédier 800 cartons. Chaque carton mesure 60×40×30 cm (dimensions extérieures). Le conteneur prévu a des dimensions internes de 1200×240×260 cm.

**Entrée** : Saisissez les dimensions ci-dessus dans le panneau de commande, réglez le nombre de chargement cible sur `800`, puis cliquez « Générer le plan 3D optimal ».

**Sortie** : Le système sélectionne l'orientation qui correspond le mieux à la largeur du conteneur, rend l'agencement complet couche par couche en 3D, et produit : la quantité réellement chargeable, l'écart latéral par rangée et l'espace mort longitudinal à l'arrière.

**Référence de décision** : Si le plan optimal donne 780 cartons contre un objectif de 800, l'expéditeur peut évaluer s'il doit scinder l'expédition, ajuster les dimensions du carton, ou confirmer une tolérance acceptable avec l'acheteur.

---

## ⚠️ Limites

- Prend en charge **une seule spécification produit** — le chargement mixte multi-SKU n'est pas encore disponible
- L'algorithme opère sur des frontières physiques absolues. Pour les opérations réelles, il est recommandé de **soustraire une marge de tolérance de 25 cm** aux dimensions du conteneur pour tenir compte de la déformation des cartons, des écarts d'empilement et de l'espace de travail
- Ne convient pas aux denrées périssables sous chaîne du froid, aux marchandises fragiles ou à la cargaison nécessitant un arrimage spécialisé
- Le rendu 3D est une illustration de planification, pas un document d'instruction de chargement formel

---

## 🔬 À propos de la méthode

Ce simulateur utilise un **algorithme exhaustif déterministe** — pas de recherche heuristique ni de génération par IA. Des entrées identiques produisent toujours des sorties identiques ; le processus est entièrement reproductible.

Pile technologique : HTML5 / CSS3 / JavaScript (ES6), [Three.js](https://threejs.org/) (moteur de rendu 3D WebGL), [Tailwind CSS](https://tailwindcss.com/) (chargé via CDN). L'ensemble de l'outil est empaqueté en un **fichier `.html` unique** — aucun Node.js, Python ou base de données requis. Double-cliquez et exécutez dans tout navigateur moderne.

**Cet outil est entièrement gratuit pour la planification de fret sec standard. Ne convient pas aux denrées périssables sous chaîne du froid ni aux articles fragiles.**

---

## 📄 Licence

Ce projet est sous licence **MIT License** — libre d'utilisation, de modification et de distribution avec attribution.
