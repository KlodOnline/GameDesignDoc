# Tour de jeu
____

## Cycles de Jeu
Le jeu fonctionne avec un **TIC** (Tour par Intervalle Constant) de **5 minutes** (300 secondes). Chaque tour, le serveur traite l'ensemble des ordres en attente et met à jour l'état du monde.

## Timing
- **1 TIC = 5 minutes IRL = 1 heure en jeu**
- **192 TICs par jour IRL** (avec trêve nocturne de 8h, 128 TICs de gameplay effectif)
- **1 jour IRL = 8 jours en jeu**
- **3 mois IRL = ~2 ans de vie en jeu**

## Principe
Le principe des tours de jeu est un classique des anciens MMORTS web, le **_TIC_**. Tout les joueurs jouent en même temps, donnent des ordres à leur unités ou leurs villes, et à chaque **_TIC_** le serveur calcule tout ou partie de ces ordres et modifie le monde de jeu. Pendant la durée de cette **_résolution_** le monde est verrouillé et aucun ordre nouveau n'est pris en compte (même si l’interface permet d'en ajouter de nouveau pour la suite).
**Pour faciliter tout le système de jeu, il faut trouver moyen de rendre toute action dans l'interface comme un "ordre" soumis au TIC.**. Même les actions "évidentes" comme renommer une ville ou décharger quelque chose de l'inventaire.
## Ordre d'action
### Tour des villes

Les villes des joueurs jouent avant les villes des IA. Les villes jouent dans cet ordre :
 - Elles produisent des ressources (exploitation du terrain par les travailleurs)
 - Elles fabriquent des objets (artisanat)
 - Elles avancent leurs constructions (bâtiments en cours)
 - Elles recrutent des unités (file de recrutement)
 - Elles consomment de la nourriture (entretien de la population)
 - Elles croissent si ressources et nourriture sont disponibles
 - Elles vérifient leur niveau et étendent leur territoire
 - Contre-espionnage : détection passive des espions infiltrés

### Tour des unités 
Les unités qui ont survécu au coût d'entretien sont ensuite traitées :
 - Les unités dans des zones difficiles (désert, banquise) perdent 1 point de moral (/100)
 - Les unités très loin de leur ville d'attache perdent 1 point de moral
 - 0 point de moral = destruction
 - Les unités qui doivent échanger des stocks le font
 - Les unités qui doivent ramasser des choses ou en construire le font (production des camps d'ouvrier)
 - Les unités qui doivent se déplacer le font. En cas de case occupée, l'ordre est repoussé en fin de pile de résolution
 - Les unités qui doivent se déplacer et ont été bloquées le font de nouveau et si elles sont en présence d'un ennemi, attaquent
 - Les unités qui doivent attaquer attaquent. Si deux unités s'attaquent mutuellement, un seul combat a lieu, et l'unité ayant le score "Moral(1à100) + 1D50" a l'initiative
 - Une unité qui disparaît laisse choir son loot

### Tour de l'environnement
 - Les territoires déconnectés sont abandonnés
 - Les joueurs inactifs sont vérifiés (abandon/défaite)
 - Les barbares jouent leur tour (déplacement, attaque, conversion)
 - Les loots qui traînent se dégradent
 - Les sources de ressources sont générées sur la map
 - L'évolution du monde est calculée (terrain qui change)

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

