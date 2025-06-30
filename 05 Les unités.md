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
Le mouvement des unités est calculé :
 - en fonction de la vitesse de l'unité
 - en fonction de la difficulté du terrain
Cela donne un résultat en nombre de tour qu'il faut passer avant de déplacer effectivement l'unité sur une autre case.
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


