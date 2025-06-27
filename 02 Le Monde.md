____
# Le Monde
## Grille de référence
Le monde se joue sur une carte **cylindrique** composée de cases **hexagonale**. Autrement dit, tout ce qui sort à gauche revient par la droite, et vice versa. Les hexagones présentent l'avantage d'équilibrer les vitesses et distances de déplacement dans toutes les directions (contrairement aux cases carrées ou les diagonales sont plus rapides que les autres déplacements).
## Dimensions
Techniquement, une ville devrait pouvoir avoir une zone d'influence de *3* ou *4* cases de rayons, et chaque joueur devrait piloter *1* à *5* villes.
Donc on peut compter 61 cases d'aire pour une ville, *305* pour un joueur. On voudrait au moins 200 *joueurs* par monde, donc un *minimum* de *61.000* cases. Il faudrait compter également les zones inexploitables, etc. 
C'est pourquoi j'ai choisi comme valeur par défaut un monde de *320x200*. Je pense qu'il pourrait passer à 450x300 si les joueurs sont trop à l'étroit, et en fonction des retour, si 200 joueurs est suffisant ou non, si 5 villes à jouer c'est trop peu ou non ...
## Génération procédurale
Je n'y peux rien, j'aime ça. De plus l'exploration me fait toujours plaisir. Donc la carte doit être générée de façon procédurale avec une cohérence réaliste. Donc :
 - On veut un équateur 
 - On veux des tropiques à X% de l'équateur, au nord et au sud
 - On veut des cercles polaires à X% des poles
 - On veux des chaines de montagnes et des océans cohérent sur les continents
 - On veut des zones plus ou moins humide qui créeront des désert, non pas au hasard, mais en fonction de l'humidité logique obtenue par les précipitations
