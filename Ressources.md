# Ressources
____
KlodOnline est un jeu de craft et de ressources comme pas mal de MMO. La plupart des RTS proposent des ressources "magiques" qui se stockent dans le cloud et sont utilisées par les unités pour construire des batiments etc. **mais pas Klod**.

## Inventaires
La plupart des entités du jeu possèdent un inventaire (unités, villes, loot…).  
Un inventaire est constitué de slots dans lesquels peuvent être rangés des items selon leur type et leur volume.

### Capacités :
- **Villes** : 16 slots de base, extensible à 32 / 48 / 64 via des bâtiments d’entreposage.
- **Unités** : 1 à 8+ slots selon le type d’unité.
- **Loot** : 255.

### Échange d’objets
Une unité peut transférer des objets avec une autre unité, une ville ou un loot présent sur la même case.  
L'échange vérifie uniquement :
- que la cible a de la place
- qu’elle appartient au même joueur ou est neutre.

### Loot
Lorsqu’une unité ou ville est détruite, ou lorsqu’une unité est transformée en une autre disposant d’un inventaire plus petit, le surplus devient du loot au sol.  
Ce loot se dégrade progressivement avec le temps.

---

## Ressources Primaires
Ce sont les ressources extraites directement du terrain.

### Sources naturelles
Des gisements fixes existent sur la carte pour chaque ressource.

À chaque tour :
- le jeu vérifie si de nouvelles sources doivent apparaître.
- le nombre de sources dépend de la rareté :  
  - Rareté 1 : ~180  
  - Rareté 2 : ~60  
  - Rareté 3 : ~20  
  - Rareté 4 : ~7  
  - Rareté 5 : ~2  

Placement :
- une ressource n’apparaît que sur les types de terrain compatibles.
- plus la ressource est rare, plus l’exclusion autour d’elle est large pour éviter les clusters.

Exploitation :
- une source exploitée perd 1 point de volume par tour.
- elle disparaît une fois arrivée à 0.

> Ce système repose sur un nombre cible absolu de sources.  
> La logique de génération devra évoluer pour un pourcentage du nombre de cases.

---

### Production par les villes
Les villes peuvent récolter autour d’elles selon un rayon dépendant de leur population.  
Les travailleurs sont assignés à des cases de ressource.

### Camps de récolteurs
Certaines unités peuvent se transformer en camp fixe pour extraire :
- nourriture (gcamp)
- bois (wcamp)
- minéraux (mcamp)

Ces camps ont un seul travailleur et exploitent une seule case.

Filtrage :
- chaque ressource possède un type de travailleur associé (farmer / woodcutter / miner).
- l’exploitation n’est possible que si le type correspond.

Priorité :
1. Les sources naturelles sont exploitées en premier.
2. Ensuite vient la production de terrain standard.

La ressource produite va dans l’inventaire du récolteur (unité ou ville).

### Déconstruction de ressources secondaires (prévu)
Certains bâtiments avancés permettront de convertir une ressource secondaire en ses composants primaires, avec une perte de ~20%.

---

## Classification des ressources

### Rareté
- **1 – Communes** : nourriture, bois, pierre. Nécessaires à toutes les constructions.
- **2 – Peu communes (vert)** : matériaux pour constructions avancées.
- **3 – Rares (bleu)** : matériaux pour bâtiments d’importance.
- **4 – Épiques (violet)** : matériaux pour constructions majeures uniques.
- **5 – Légendaires (orange)** : ressources mythiques extrêmement rares.

---

## Ressources Secondaires
Ce sont les ressources fabriquées en ville à partir des ressources primaires.

### Système de craft
- La ville possède une file d’objets à fabriquer.
- Chaque recette définit :
  - le coût en ressources primaires
  - le bâtiment requis pour le craft
- Le système vérifie la présence du bâtiment.
- Les ressources sont consommées.
- Le produit est ajouté à l’inventaire de la ville.
- Plus il y a d'artisans et plus ça produit

### Exemples de ressources secondaires
- armes primitives  
- outils primitifs  
- engins de siège  
- ...

---

## Commerce (prévu)
Un système futur permettra l’échange de ressources entre joueurs.

---

## Conclusion
KlodOnline repose sur une logique matérielle stricte :  
pas de stockage magique, pas de ressources « virtuelles », tout prend de la place, tout s’échange physiquement, tout peut être perdu, looté ou capturé.
