____
# Unités (WIP)
Les unités sont le coeur du gameplay, puis qu'elle permettent au joueur d'explorer, de construire, de récolter, de faire la guerre.
## Type
Il existe différent type d'unités. Elle sont de différentes catégories :
 - Combat
 - Transport
 - Ouvrière
 - Navale
## Mouvement
Les unités peuvent être groupées en stack, pour ensuite réaliser un déplacement simultané. Sur le jeu, on autorise une stack de 3 unités maximum.

Les unités ont un score de déplacement de **1 à 4** (Fast/Medium/Slow/VerySlow).
Les terrains ont un score également, de **2 à 5** (Roaded/Easy/Medium/Hard/VeryHard)

L'addition du score de l'unité et du score de terrain donne le nombre de tour nécessaire au passage à la case suivante. 
Le score final doit donc toujours être compris entre 3 et 9. (15min à 45min pour une case).

Cela devra éventuellement être révisé en fonction du retour des joueurs, en conservant la durée actuellement des TIC mais avec des scores comme 
 - Unité (0.5, 1.5, 2.5, 3.5) / Sols (0.5, 1.5, 2.5, 3.5, 4.5) => échelle de 1 à 8 (5min à 40min)
 - Unité (0.5, 1, 1.5, 2) / Sols (0.5, 1, 1.5, 2, 2.5) => échelle de 1 à 5 (5min à 25min) (arrondi sup.)

## Inventaire
Les unités disposent d'un inventaire avec une place exprimée en slots, et va de 0 à 6 slots.
Lorsqu'elle meurent, elles laissent sur place un loot, qui se degrade avec le temps.
## Combat


## FOV
Le **_FOV_** c'est le "field of view". C'est le nombre de cases (rayon) que voit une unité. Il y a un score en fonction de l'unité, puis un bonus en fonction du terrain. Valeurs classiques :
 - Unités de base : 1
 - Unités de reconnaissances ou d'observation: 2
 - Terrain de base : +0
 - Foret, Jungle : -1
 - Collines : +1
 - Villes : 1 / niveau de ville (Cf. villes), max 4 ou 5

## Campement
La plupart des unités auront un ordre "camper"/"fortifier" etc. en fonction de l'unité, permettant de la "figer" sur place et d'activer quelque chose de spécial comme:
 - camp de mineur
 - tour d'observation
 - camp fortifié
 - ...


