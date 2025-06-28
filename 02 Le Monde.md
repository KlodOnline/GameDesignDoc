____
# Le Monde
## Grille de référence
Le monde se joue sur une carte **cylindrique** composée de cases **hexagonale**. Autrement dit, tout ce qui sort à gauche revient par la droite, et vice versa. Les hexagones présentent l'avantage d'équilibrer les vitesses et distances de déplacement dans toutes les directions (contrairement aux cases carrées ou les diagonales sont plus rapides que les autres déplacements).
## Dimensions
Techniquement, une ville devrait pouvoir avoir une zone d'influence de **_3_** ou **_4_** cases de rayons, et chaque joueur devrait piloter **_1_** à **_5_** villes.
Donc on peut compter 61 cases d'aire pour une ville, **_305_** pour un joueur. On voudrait au moins 200 **_joueurs_** par monde, donc un **_minimum_** de **_61.000_** cases. Il faudrait compter également les zones inexploitables, etc. 
C'est pourquoi j'ai choisi comme valeur par défaut un monde de **_320x200_**. Je pense qu'il pourrait passer à 450x300 si les joueurs sont trop à l'étroit, et en fonction des retour, si 200 joueurs est suffisant ou non, si 5 villes à jouer c'est trop peu ou non ...
## Génération procédurale
Je n'y peux rien, j'aime ça. De plus l'exploration me fait toujours plaisir. Donc la carte doit être générée de façon procédurale avec une cohérence réaliste. Voici comment cela devrait être fait :
### Températures
 - Soit H la distance pole nord/pole sud du monde (le nombre de rangées)
 - Le cercle polaire, c'est 1/14 de H
 - Les tropiques, sont à 1/8 de H de l'équateur
 - Les zones chaudes sont entre les deux tropiques
 - Les zones froides au delà des cercles polaire
 - Les zones gelées, pour éviter d'en prendre trop sur la carte, sont limitées à 4 cases des bords nord/sud
### Océans et montagnes
 Ensuite, les plaques tectoniques doivent simplement séparer des plaques continentales par des **montagnes** ou des **océans** (que l'on garde volontairement en forme de couloir pour maximiser les lieux de jeux des joueurs).
### Humidité
C'est simple, sur terre il existe un vent dominant Est-Ouest du fait de la rotation de la Terre à hauteur de l'équateur. Pour une raison que j'ignore, ils sont dominant Ouest-est prêt des pôles. et entre les deux ils se repoussent en altitude. Bref, l'humidité permet de calculer la pousse des **forêts**, qui est en fait là ou les nuages arrosent le plus. Les montagnes empêche le passage des nuages créant des zones "sans forêt".
### Rivières
Très simple, tirage aléatoire d'une montagne avec de la plaine adjacente, définie alors comme source, et la rivière courre "aléatoirement" jusqu'à trouver un océan.
### Déserts
 Facile, une plaine en zone chaude devient une savane. Une grande zone de savane créé un désert en son sein.
 
