_____
# Conquête de Territoires
## Principe
Les territoires sont les terrains revendiqués par un joueur. Ils apparaissent sur la carte avec une frontière colorée, de la couleur du joueur.

## Règles de territoires
 - On conquiert des terrains en fondant une **ville** ou un **fort** (unité statique militaire)
 - Un territoire est un ensemble de cases adjacentes possédées par le même joueur
 - Le rayon d'influence d'une ville dépend de sa population : commence à 1 case, peut atteindre 3 cases maximum
 - Les unités statiques (forts, camps) conquièrent les cases adjacentes lors de leur transformation
 - Un territoire est perdu s'il n'y a aucune occupation militaire dessus (détection automatique des îlots déconnectés)

## Conséquences des territoires
 - Toute unité étrangère est signalée lorsqu'elle circule dans le territoire
 - Les ressources du territoire sont exploitées par la ville qui le contrôle
 - Les routes et irrigations sur le territoire appartiennent au propriétaire

## Capture de ville
 - Une ville non défendue par des unités militaires peut être capturée directement par une unité militaire ennemie
 - La capture transfère la propriété de la ville **et** de tous les territoires dans sa zone d'influence
 - Le renommage de la ville est réinitialisé après une conquête
 - Si un joueur perd toutes ses villes et unités, il est considéré comme vaincu
