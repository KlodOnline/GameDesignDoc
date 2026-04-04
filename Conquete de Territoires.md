_____
# Conquête de Territoires
## Principe
Les territoires sont les terrains revendiqués par un joueur. Ils apparaissent sur la carte avec une frontière colorée, de la couleur du joueur.

## Règles de territoires
 - On revendique du territoire avec n'importe quelle **unité statique** ou une **ville**.
 - On conquiert du territoire (prise à un autre joueur) avec une **ville** ou un **fort** (unité statique militaire)
 - Le rayon d'influence d'une ville dépend de sa population : commence à 1 case, peut atteindre 3 cases maximum
 - Les unités statiques (forts, camps) conquièrent les cases adjacentes lors de leur transformation
 - Un territoire est perdu s'il n'y a aucune occupation du joueur dessus (détection automatique des îlots déconnectés)

## Conséquences des territoires
Certains événements sont notifié, même si l'on ne peut pas "voir" sur la map les unités concernées :
 - Circulation d'unité étrangère
 - Récupération d'un loot
 - Exploitation d'une ressource
De plus le territoire donne certains avantages :
 - Contrairement aux pistes, les routes ne se détruisent pas tant qu'elles sont sur le territoire d'un joueur (et PAS d'un NPC !)
 - Les autres joueurs ne peuvent circuler dessus que si il y a soit **libre passage** ou mieux, soit **hostilité** ou pire

## Capture de ville
 - Une ville non défendue par des unités militaires peut être capturée directement par une unité militaire ennemie
 - La capture transfère la propriété de la ville **et** de tous les territoires dans sa zone d'influence
 - Le renommage de la ville est réinitialisé après une conquête
 - Si un joueur perd toutes ses villes et unités, il est considéré comme vaincu
