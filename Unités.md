# Unités
----
![Unit.png](media/Unit.png)

Les unités sont, avec les villes, le cœur du gameplay, puisqu'elles permettent au joueur d'explorer, de construire, de récolter, de faire la guerre.

## Informations
Pour accéder aux informations d'une unité, _sélectionnez-la_ puis cliquez sur l'icône ![infoicone.png](media/infoicone.png) ou bien utilisez l'un des raccourcis claviers pour accéder directement aux onglets suivants (**si** votre unité dispose d'un tel onglet !) :
 - "**G**" (pour informations **G**énérales)
 - "**I**" (pour **I**nventaire)
 - "**P**" (pour **P**roduction)

![unittab.png](media/unittab.png)

## Donner des ordres
Pour donner des ordres à une unité, _sélectionnez-la_ puis cliquez sur l'ordre de votre choix. 

![unitorder.png](media/unitorder.png)

Un panneau de confirmation s'affichera. Pour tous les ordres permettant le mouvement, cliquez sur la map directement avec votre _clic gauche_ pour ajouter une étape. Vous pouvez déplacer la map avec le _clic centre_ ou les flèches de votre clavier. Vous validez la dernière étape comme une destination en cliquant sur _OK_.

![move.png](media/move.png)

Certains ordres permettent d'**aménager le terrain** (Cf. [Monde](Monde.md))

**Important** : Les ordres de **déplacement** et d'**attaque** sont distincts. Un ordre de mouvement amène l'unité vers sa destination sans intention d'attaquer. Un ordre d'attaque cible explicitement une unité ou ville ennemie.

## Types d'unités
Il existe 4 catégories fonctionnelles d'unités, chacune avec sa propre logique de progression :

### Guerrières (militaire)
Unités de combat, défense et siège. Elles progressent via l'ordre **UPGRADE** en ville, qui les fait monter en tier d'équipement.

 Chaîne principale (Infanterie) :
```
milice ──▶ brfighter ──▶ irfighter ──▶ legion
```

Branches latérales (progression via UPGRADE) :
- **Archers** : archer ──▶ crossbowman
- **Cavalerie** : brfightercavalry ──▶ irfightercavalry ──▶ heavycavalry
- **Navale** : coastguard ──▶ mediumgalley ──▶ quadrireme

Unités sans progression (recrutement direct) : phalanx, warelephant, engins de siège (balista, catapult), espions, généraux, missidominici. Les forts sont uniquement des cibles de MORPH.

### Récolteuses (économie)
Les unités **reaper** récoltent **toutes** les ressources disponibles sur le terrain (nourriture, bois, minerais…). Il n'y a pas de spécialisation par type de ressource.

Le reaper progresse via **UPGRADE** en 4 paliers, chaque palier ajoutant des travailleurs au camp.

```
reaper1 (1 worker) ──▶ reaper2 (2 workers) ──▶ reaper3 (2 workers) ──▶ reaper4 (3 workers)
```

Le reaper peut se transformer en **camp** fixe via l'ordre **MORPH** (ex: `camp_reaper1`), ce qui conquiert le territoire adjacent.

### Transporteuses (économie)
Unités dédiées au transport de ressources. Progressent via **UPGRADE** : plus grosse capacité d'inventaire et meilleure vitesse.

- **Terrestre** : cariole (inv:4, vit:4) ──▶ horsedrawncariole (inv:6, vit:3) ──▶ horsedrawnwagon (inv:8, vit:3)
- **Maritime** : chaland (inv:4, vit:2) ──▶ barge (inv:8, vit:3) ──▶ cabotin (inv:12, vit:4)

### Modificatrices de terrain (craft)
Unités qui aménagent le territoire. Progressent via **UPGRADE** : chaque tier débloque de nouveaux ordres terrain.

```
laborer ──▶ drainer ──▶ masons ──▶ engineers
(pistes)   (+irriguer,   (+routes)  (+ponts)
            +assécher)
```

## Caractéristiques
Les unités ont des caractéristiques :
### Mouvement
#### Actuellement
Les unités ont un score de _déplacement_ de **2 à 4** (Fast=2 / Medium=3 / Slow=4).
Les terrains ont un score de **1 à 5** (Easy=1 / Medium=2 / Medium-Hard=3 / Hard=4 / Very Hard=5).
L'addition du score de l'unité et du score de terrain donne le **nombre de tours** nécessaire au passage à la case suivante. Les **routes** réduisent ce coût de 1. Le score final est compris entre **1 et 12** tours (soit entre 5 minutes et 1 heure avec le TIC de 5 minutes).

#### Ordre "greffe" (à implémenter)
Permet de grouper plusieurs unités pour un déplacement simultané. Le groupe se déplace à la vitesse de l'unité la plus lente. Utile pour escorter des unités civiles avec des militaires.
#### À faire
 - Les unités navales ne peuvent aller sur la terre, sauf les villes qui sont considérées comme des ports dès qu'elles sont en bord d'océan ou de rivière.

### Vision
#### Actuellement
Couramment nommé **FOV** ("field of view"), c'est le nombre de cases (rayon) que voit une unité. Il y a un score d'unité, de **1 à 2**, et un bonus de terrain, de **0 à 2**.

### Moral
C'est l'équivalent de la vie des unités, sur une échelle de 0 à 100. Lorsque l'unité tombe à 0, elle disparaît.
#### Actuellement
 - Dans le désert ou la banquise : -1pt par tour
 - 0 moral = destruction de l'unité
 - Les unités dans une ville voient leur moral remonté par la présence de la ville, même sans nourriture en stock (sauf si la ville est en famine)
> **Note** : La trêve nocturne et le bonus de première victoire ont été abandonnés.

## Zone de contrôle (ZoC)
Cf. [Zone de contrôle](Zone%20de%20Controle.md)

## Conquête de territoires
Cf. [Conquête de territoires](Conquete%20de%20Territoires.md)

## Combat
### Actuellement
Le combat utilise les scores d'attaque et de défense des unités, combinés aux bonus du terrain et au moral. Le calcul prend en compte :
 - Bonus de terrain (défensif ou offensif)
 - Score d'attaque ou de défense de l'unité
 - Aléatoire (-50% à +50%)
 - Moral de l'unité (multiplicateur)
 - Bonus de fortification (si combat depuis une ville ou un fort)

Les combats génèrent des rapports détaillés envoyés aux deux joueurs. Les unités perdantes peuvent tenter de battre en retraite. Si une ville n'est pas défendue par d'unités militaires, elle peut être capturée directement.

**Règle importante** : Les unités civiles ont un score d'attaque de **0**. Elles ne peuvent pas attaquer.

## Inventaire
Les unités disposent d'un **inventaire** avec un nombre de slots qui va de **0 à 8+** selon le type. Lorsqu'elles meurent, elles laissent sur place un **loot** qui se dégrade avec le temps **(-1 item/tour)**.

Le loot d'une unité morte contient les ressources qui ont servi à la construire, avec une part d'aléatoire.

## MORPH vs UPGRADE
Deux ordres permettent de transformer une unité — ils sont distincts et ne se substituent pas :

- **MORPH** : transformation *bidirectionnelle* (A ↔ B), gratuite et rapide. Exemple : reaper ↔ camp_reaper, milice ↔ fort en bois. Peut se faire n'importe où sur le terrain. L'ID de l'unité est conservé.
- **UPGRADE** : progression *one-way* (A → B, sans retour) vers une unité plus puissante. Se fait **en ville uniquement**, coûte des ressources et du temps, requiert les bâtiments appropriés (ex: `farmershouse` pour upgrade un gatherer). L'ID de l'unité est conservé.

## Campement
Les unités récolteuses et militaires peuvent se transformer en **structures statiques** via l'ordre **MORPH** : le reaper devient un camp de récolte, la milice devient un fort en bois, etc.

Ce faisant (sauf pour les tours d'observation), l'unité **conquiert le territoire** immédiatement adjacent.

## Espionnage
Le système d'espionnage permet d'infiltrer une ville ennemie pour obtenir des informations secrètes sur celle-ci.

#### Espion
L'unité **espion** est une unité spéciale qui se déplace secrètement sur la carte. Elle est invisible aux autres joueurs et peut se déplacer librement dans les territoires ennemis.

L'infiltration se fait via l'ordre **MORPH** lorsque l'espion est physiquement présent dans une ville ennemie. Il devient alors un **espion infiltré**.

#### Contre-mesures
 - Le propriétaire de la ville ne peut pas voir l'espion infiltré directement
 - Chaque tour, la ville a une chance de détecter l'espion basée sur sa population, la présence militaire et le nombre d'espions infiltrés
 - Si détecté, l'espion infiltré est détruit
 - L'espion peut se dés-infiltrer à tout moment avec l'ordre **MORPH** (retour à l'état espion normal)
 - Si la ville est capturée ou détruite, l'espion infiltré redevient un espion normal
 - **Limite** : un seul espion infiltré par ville
 - Les espions invisibles ne comptent pas dans le calcul de "case occupée" (crowded) pour les joueurs qui ne les possèdent pas
 - **Détection en mouvement** : un espion qui se déplace sur une case contenant des unités adverses risque d'être détecté
 - **Rumeurs d'intrusion** : la ville notifie son propriétaire d'une suspicion d'intrusion
   - Les alliés ne déclenchent pas de rumeurs
   - La rumeur précise si l'intrus est militaire ou civil
   - Les unités invisibles (espions non infiltrés) ne génèrent aucune rumeur

### À faire
 - **Missions d'espionnage** (sabotage, assassinat, vol de ressources)
 - **Réseaux d'espions** (un espion peut gérer plusieurs villes)
 - **Espionnage économique** (voir les ressources, les échanges commerciaux)
