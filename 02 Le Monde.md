____
# Le Monde
## Grille de référence
Le monde se joue sur une carte **cylindrique** composée de cases **hexagonale**. Autrement dit, tout ce qui sort à gauche revient par la droite, et vice versa. Les hexagones présentent l'avantage d'équilibrer les vitesses et distances de déplacement dans toutes les directions (contrairement aux cases carrées ou les diagonales sont plus rapides que les autres déplacements).
## Dimensions
Techniquement, une ville devrait pouvoir avoir une zone d'influence de **_3_** ou **_4_** cases de rayons, et chaque joueur devrait piloter **_1_** à **_5_** villes.
Donc on peut compter 61 cases d'aire pour une ville, **_305_** pour un joueur. On voudrait au moins 200 **_joueurs_** par monde, donc un **_minimum_** de **_61.000_** cases. Il faudrait compter également les zones inexploitables, etc. 
C'est pourquoi j'ai choisi comme valeur par défaut un monde de **_320x200_**. Je pense qu'il pourrait passer à 450x300 si les joueurs sont trop à l'étroit, et en fonction des retour, si 200 joueurs est suffisant ou non, si 5 villes à jouer c'est trop peu ou non ...
## Génération procédurale (WIP)
<<<<<<< HEAD
Je n'y peux rien, j'aime ça. De plus l'exploration me fait toujours plaisir. Donc la carte doit être générée de façon procédurale avec une cohérence réaliste. Donc :
=======
Je n'y peux rien, j'aime ça. De plus l'exploration me fait toujours plaisir. Donc la carte doit être générée de façon procédurale avec une cohérence réaliste. Voici comment cela devrait être fait :
 - Soit H la distance pole nord/pole sud du monde (le nombre de rangées)
 - Le cercle polaire, c'est 1/14 de H
 - Les tropiques, sont à 1/8 de H de l'équateur
 - Les zones chaudes sont entre les deux tropiques
 - Les zones froides au delà des cercles polaire
 - Les zones gelées, pour éviter d'en prendre trop sur la carte, sont limitées à 4 cases des bords nord/sud
 - L'équateur, à la moitié du monde, permet de calculer les tropiques,  
 - 
>>>>>>> 573deb4 (reset du depot local)
 - On veut un équateur 
 - On veux des tropiques à X% de l'équateur, au nord et au sud
 - On veut des cercles polaires à X% des poles
 - On veux des chaines de montagnes et des océans cohérent sur les continents
 - On veut des zones plus ou moins humide qui créeront des désert, non pas au hasard, mais en fonction de l'humidité logique obtenue par les précipitations
 - 
