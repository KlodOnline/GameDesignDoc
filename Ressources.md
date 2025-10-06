____
# Ressources
KlodOnline est un jeu de craft et de ressources comme pas mal de MMO. La plupart des RTS proposent des ressources "magiques" qui se stockent dans le cloud et sont utilisées par les unités pour construire des batiments etc. **mais pas Klod**.

todo:
- **Types de Ressources** - Liste des ressources du jeu
- **Production** - Comment obtenir les ressources
- **Commerce** - Système d'échange


## Inventaires
### Description
La plupart des entités du jeu dispose d'un **inventaire**: Unités, Villes, Loot, etc. Cet inventaire est fait de cellules qui sont remplissable par un type d'item sur un certain volume, dépendant de l'item. Par exemple, la nourriture se stocke sur une cellule par paquet de 3000, la pierre par paquet de 1500 etc. Les inventaires sont de tailles différentes en fonction des entités, ou d'option spécifiques. (Villes: 16 à 64, Unités: 1 à 8, Loot: 256 ...).
### Echange
Une unité peut échanger librement du stuff avec une autre unité ou une ville, située sur la même case qu'elle.
### Loot
Une unité ou une ville qui est détruite, ou une unité qui se transforme en une autre qui n'aurait pas autant de slots d'inventaire que la précédente, abandonne sur le terrain du _Loot_.
### Commerce
Plus tard il est à imaginer un système permettant le commerce ou l'échange de stuff avec les autres joueurs.
## Ressources Primaires
Les ressources primaires sont celles extraites de l’environnement, ou obtenues à la destructions d'une ressource secondaire en ville.
### Source
Le jeu implémente des gisements de ressources fixes sur la carte sous forme d'entités _Source_.
Le système fonctionne ainsi :
1. **À chaque tour de jeu** : Le serveur vérifie s'il faut faire apparaître de nouvelles sources de ressources sur la carte
2. **Apparition aléatoire** : De nouvelles mines, forêts, gisements peuvent apparaître dans des zones appropriées selon des règles de probabilité (peu commune, rare, épique, légendaire)
3. **Usure progressive** : Quand un joueur exploite une source (via une ville ou un camp), celle-ci diminue petit à petit jusqu'à disparaître (pour éviter la rétention de ressources et forcer les joueur à être attentif à l'exploitation des ressources)
4. **Cycle continu** : Ce processus se répète à chaque tour, maintenant un équilibre entre consommation et régénération des ressources

Ce système assure que la carte ne se vide jamais complètement de ressources tout en créant une dynamique économique où les joueurs doivent constamment explorer et sécuriser de nouvelles zones d'exploitation.
### Production
Une ville ou un camp d'ouvrier peu produire des ressources à partir de son environnement immédiat. Une ville a plus de zone de production qu'un camp d'ouvrier, mais le camp d'ouvrier est mobile. Toutes les ressources à portée peuvent être exploitée, le joueur choisis lesquelles dans les interface de récolte. Un camp d'ouvrier ne peut choisir qu'une case de récolte.
Une ressource produite arrive dans l'inventaire du récolteur, ville ou unité.
Enfin, certains bâtiments de craft des villes avancées en craft doivent pouvoir permettre de détruire une ressource secondaire pour la ramener à son état primaire, moyennant une perte de 20% des matériaux d'origine.
### Types
Les ressources sont de différents type : 
 - Nourriture (pour les villageois, l'entretien des unités)
 - Bois pierre, matériaux de base (nécessaire à toute constructions)
 - Matériaux peu courant "vert", pour les construction un peu avancées (typiquement, bois exotiques, verroterie, ivoire, marbre etc.)
 - Matériaux rare "bleu" pour les construction importante (pierre précieuse, encens etc.)
 - matériaux épique "violet" pour les constructions incroyables (obsidienne, malachite, arbre-pierre, et autre ressource quasi mystiques)
 - matériaux légendaire "orange" pour une construction quasi unique dans l'empire (larme de déesse, etc.)

Quand je dis "construction", je parle de bâtiment ou d'unités.
Le niveau de rareté doit être surveillé simplement, par un système de nodes. 100% des cases doivent pouvoir générer les matériaux banals, 30% les matériaux "peu courants", 10% les rares, 0.5% les épiques, et 0.1% les légendaires. Ces valeurs pourraient être ajustées en fonctions des retours des joueurs.
## Ressources Secondaires
Les ressources secondaires sont celles produites à l'aides des primaires, pour ensuite être utilisées. Je n'ai pas encore le détail de ce qui sera fait, mais il me semble que les unités middle/high tiers devraient toutes nécessiter des ressources secondaires.
### Production
Les ressources primaires sont amenées en ville, qui, si elle dispose des bon bâtiments, pourra cafter les ressources secondaires comme un ordre de jeu classique.
Exemple : 
 - Pierre de taille
 - ameublement
 - armement
 - engins de siège
 - ...