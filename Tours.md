____
# Tour de jeu
## Principe
Le principe des tours de jeu est un classique des anciens MMORTS web, le **_TIC_**. Tout les joueurs jouent en même temps, donnent des ordres à leur unités ou leurs villes, et à chaque **_TIC_** le serveur calcule tout ou partie de ces ordres et modifie le monde de jeu. Pendant la durée de cette **_résolution_** le monde est verrouillé et aucun ordre nouveau n'est pris en compte (même si l’interface permet d'en ajouter de nouveau pour la suite).
**Pour faciliter tout le système de jeu, il faut trouver moyen de rendre toute action dans l'interface comme un "ordre" soumis au TIC.**. Même les actions "évidentes" comme renommer une ville ou décharger quelque chose de l'inventaire.
## Ordre d'action
### Tour des villes

Les villes des joueurs jouent avant les villes des IA si il y en a. Les villes jouent dans cet ordre :
 - Elle produisent des ressources
 - Elle mangent des ressources (nourriture)
 - Les unités et/ou les bâtiments et/ou les aménagement du territoire etc. peuvent avoir un entretien à payer, en nourriture ou autre. Ne pas payer l'entretien dégrade ou détruit l'item concernée (à définir dans les règles) - l'entretien se fait avant la création de choses.
 - Elle avancent leur constructions (conso d'autre ressources)
 - elle croissent si il y a des ressources & nourriture dispo (pour les maisons etc) (à voir, peut être passer ce truc tout les 12 tours )

### Tour des unités 
Les unités qui ont survécus au coût d'entretien sont ensuite traitées
 - Les unités dans des zones difficile (désert, banquise) perdent 1 point de moral (/100)
 - les unités très loin de leur ville d'attache perdent 1 point de moral
 - 0 point de moral = destruction
 - Les unités qui doivent échanger des stock le font
 - les unités qui doivent ramasser des trucs ou en construire le font (production des camps d'ouvrier)
 - les unités qui doivent se déplacer le font. En cas de case occupée, l'ordre et repoussé en fin de pile de résolution
 - les unités qui doivent se déplacer et ont été bloquées le font de nouveau et si elle sont en présence d'un ennemi, attaquent. Si elles sont de nouveau bloquées mais n'ont pas de guerre déclarée avec l'autre unité, elle passent leur tour sans annuler leur ordre, qu'elle retenteront au prochain TIC (attention à ne pas décrémenter l'ordre
 - Les unités qui doivent attaquer attaquent, mais attention aux cas ou deux unités s'attaquent mutuellement. Dans ce cas particulier, 1 seul combat aura lieu, et l'unité ayant le score de "Moral(1à100) + 1D50" a l'initiative : cela veux dire qu'elle attaque si son score d'attaque est plus élevée que son score de défense - ou autrement dit, qu'elle choisi ce qui lui est avantageux.
 - Une unité qui disparaît laisse choir son loot

### Tour de l'environnement
 - Une zone humide ou "irriguée mais sans propriétaire" peut se transformer en marais ou en forêt
 - Une route "sans propriétaire" se dégrade, un canal sans propriétaire également
 - Nuance pour les canaux : un canal "isolé" (sans voisin océan, rivière, canal) disparaît instantanément
 - Les loots qui traînent se dégradent (-1% du stack max) (par exemple si le bois se stack par 100, il perd 1 bois par tour (toutes les 5 minutes)
 - Les ressources qui n'ont pas de node de production sont générées aléatoirement sur la map

## Echelle de temps/distance
Après plusieurs calculs et recherches voici la base de l'échelle :
 - Avec **1 TIC / 5 min**, il y a **192** TICs par jours de jeu (16h, avec la trêve nocturne).
 - Bien noter que les joueurs on un empant de gameplay de plutôt **8h** = **96 TICs**
 - **1 TIC vaut 1 heure** pour le jeu
 - Donc, une journée IRL vaut **8 jours** dans le jeu (192 TICs/24)
 - **3 mois IRL** font **17.280** TICS, soit **2 ans de vie** dans le jeu.

Les autres bases potentielles :

| TIC sec | TIC/Jour | 16h Jeu | Jours IG pour 1 jour IRL | TIC sur 3 mois IRL | Années IG en 3 mois | Durée IRL d'une saison IG (jours) |
| ------- | -------- | ------- | ------------------------ | ------------------ | ------------------- | --------------------------------- |
| 60      | 960      | 640     | 40                       | 86400              | 9,86                | 2,25                              |
| 120     | 480      | 320     | 20                       | 43200              | 4,93                | 4,5                               |
| 180     | 320      | 213     | 13,33                    | 28800              | 3,29                | 6,75                              |
| 240     | 240      | 160     | 10                       | 21600              | 2,47                | 9                                 |
| 300     | 192      | 128     | 8                        | 17280              | 1,97                | 11,25                             |

| Durée d’un TIC  | 5 tours | 10 tours | 20 tours | 50 tours | 100 tours |
| --------------- | ------- | -------- | -------- | -------- | --------- |
| 60 sec (1 min)  | 5 min   | 10 min   | 20 min   | 50 min   | 1h40      |
| 120 sec (2 min) | 10 min  | 20 min   | 40 min   | 1h40     | 3h20      |
| 240 sec (4 min) | 20 min  | 40 min   | 1h20     | 3h20     | 6h40      |
| 300 sec (5 min) | 25 min  | 50 min   | 1h40     | 4h10     | 8h20      |

