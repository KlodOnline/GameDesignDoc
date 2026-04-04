# Gameplay Général
______
## Pitch
Klod Online est un **jeu de stratégie massivement multijoueur** basé sur des **tours synchronisés toutes les 5 minutes** (300 secondes). Chaque joueur incarne un empire indépendant, qui évolue dans un monde commun persistant, généré de façon procédurale, et composé d'hexagones (grille 320x250 avec wrapping cylindrique). Ils peuvent choisir de se faire la guerre, de coopérer, ou d'extraire des ressources plus ou moins rares.

## Gameplay classique ...
Comme dans beaucoup de 4X, le jeu propose :
 - **Exploration de la map** par joueur avec brouillard de guerre optimisé par bitmask
 - **Brouillard de guerre** fonction du champ de vue des unités et des villes, et du terrain
 - **Création d'unités** (45 types) et **création de villes** via les colons
 - **Combats** (attaque/défense, unités de siège, retraite), **alliances** (5 statuts diplomatiques), **commerce** (système de troc et pièces)
 - **IA PNJ** ("Barbarians") avec unités qui zonent sur le monde
 - **Gestion des villes fine** : population (croissance sigmoïde), nourriture, famine, bâtiments (55 types), file de recrutement, artisans, technologie

## ...et innovations !
Au-delà du gameplay classique des 4X on trouve comme innovations principales :
 - Un **_MMO_** avec support de 200+ joueurs par monde (31 joueurs actifs actuellement)
 - Une gestion des ressources via des **_inventaires_** (façon WoW) avec un mécanisme de rareté : commun (blanc), peu commun (vert), rare (bleu), épique (violet), légendaire (orange) — 37 types de ressources
 - Une **_logistique_** détaillée : aucun système magique d'envoi de ressources entre joueurs, tout passe par les unités de jeu (inventaires, butin au sol, échange direct)
 - Une gestion des villes où chaque ville se **_spécialise_** avec un arbre de progrès/talents propre
 - Un terrain **_modifié_** par les joueurs : routes (pistes, routes pavées, ponts), irrigation, drainage de marais, déforestation
 - ~~Un système de _**missions individualisées**_~~ — **NON IMPLÉMENTÉ** (prévu pour la diplomatie fine)

### Inspirations
World of Warcraft, Risk, Mortal Online
Civilisation, Travian, Heroes of Might and Magic Kingdom etc.
 - [Cry Havoc](http://www.cryhavocfan.org/fr/suite/cryhavoc/chlejeu.htm)
 - [Jeux et Strat](https://laurent36.typepad.com/blog/2007/12/les-encarts-de-jeux-et-strat%C3%A9gie-n-51-%C3%A0-60.html)
