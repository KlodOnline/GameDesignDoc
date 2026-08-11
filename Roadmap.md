# Roadmap de développement
____
**ALPHA** → **BETA** → **1.0**

Ne sont indiqués ici que ce qu'il reste à faire, les objectifs accomplis pouvant être trouvé dans [Roadmap_Archives](Roadmap_Archives.md).

______
## Stade BETA
**_(depuis Janvier 2026)_**
### Objectif
Implémenter et optimiser toutes les fonctionnalités du **Gameplay étendu**. Debugger pour une version **1.0** soignée. Faire également des équilibrages de règles de jeu.
#### Objectif secondaire
Avoir des abonnés. L'argent permettrait : 
 - de faire de ce loisir un travail à **temps plein**
 - d'embaucher une équipe technique et **artistique** et de **se débarrasser de l'IA** (pour la musique, les graphismes, peut être les traductions, etc.)
 - d'avoir une entreprise et de lancer d'**autres projets** (DragonsRun, Ultimate Buhurt Championship, MaenaSola, BlackSails, DesertCars, ArticRailroads, etc.)

### Déploiement
 - Un serveur **KlodWorld** nomme *DEV-Alpha* qui utilise la branche *develop* et se met à jour toutes les **5 minutes**, et redémarre le monde si nécessaire.
 - Un serveur **KlodWorld** nomme *DEV-Beta* qui utilise la branche *main* et se met à jour tout les **jours à minuit**, et redémarre le monde si nécessaire.
 - On pousse de *develop* vers *main* quand une fonctionnalité est considérée *debuggée*.

### Diffusion
Large. Il faut faire connaitre le jeu un maximum, pour permettre des tests de  charge. Récompenser les 50 premiers joueurs d'un abonnement à vie ? Autoriser les abonnements de soutiens.
### Fonctionnalités à implémenter durant cette phase
- [x] Augmentation de la durée de création des colons en fonction de la population des empires
- [x] Possibilité d'affecter les habitants des villes aux tâches : Production, Crafting, Bâtiments
- [x] vie et mort des empires, abandon des joueurs
- [x] "barbares" (IA mobs)
- [x] Protection débutant de 2 semaine par défaut

#### Affinages et compléments de gameplay
- [x] **Unités civiles à 0 en attaque** : les civils ne peuvent pas attaquer
- [x] **Multi-bateau au choix** : faciliter l'embarquement quand plusieurs navires sont sur la même case (icône inventaire plein)
- [x] **Suppression multiple de mails**
- [x] **Option "cabotage"** : permettre aux bateaux de longer les côtes pour éviter la haute mer

### Prioritaire

#### Missions
- [ ] Ajouter le choix de la divinité
- [ ] Générer des missions divines aléatoires par type de gameplay
- [ ] Suivre la progression des missions divines
- [ ] Ajouter les récompenses uniques des missions divines

### A Faire

#### Diplomatie
- [ ] Implémenter les alliances multi-joueurs (clans)
- [ ] Implémenter l'échange de carte entre joueurs

#### Progression et gestion des unités
- [ ] Ajouter les unités à la population d'une ville
- [ ] Rattacher une unité à une autre ville
- [ ] Dissoudre une unité dans sa ville
- [ ] Transférer les ressources d'une unité dissoute vers sa ville

#### Commerce
- [ ] Autoriser les échanges d'objets avec les unités d'un autre joueur selon les relations diplomatiques
- [ ] Autoriser les échanges d'objets avec les villes d'un autre joueur selon les relations diplomatiques
- [ ] Permettre de verrouiller un échange pour sceller l'accord

#### Communication
- [ ] Ajouter le chat privé de clan
- [ ] Ajouter le chat de groupe avec canal personnalisé
- [ ] Enregistrer les logs du chat
- [ ] Assurer la traçabilité des messages en cas de plainte

#### Modération
- [ ] Permettre à un modérateur de se connecter sans jouer
- [ ] Permettre à un développeur de se connecter sans jouer
- [ ] Donner accès au chat depuis l'interface de modération
- [ ] Donner accès aux logs du jeu depuis l'interface de modération

#### Classement
- [ ] Ajouter les points d'honneur
- [ ] Ajouter la dégradation de l'honneur avec le temps
- [ ] Ajouter le classement des joueurs
- [ ] Ajouter le classement des villes
- [ ] Ajouter le classement des clans
- [ ] Afficher les statistiques d'un joueur depuis son profil

#### Monde vivant
- [ ] Ajuster la repousse naturelle des forêts et jungles
- [ ] Ajuster l'évolution naturelle des plaines vers la savane
- [ ] Ajuster l'évolution naturelle de la savane vers le désert
- [ ] Ajouter les catastrophes naturelles
- [ ] Ajouter la génération spontanée de pistes

#### Règles et interface
- [ ] Implémenter le cycle des saisons
- [ ] Appliquer les effets climatiques des saisons
- [ ] Unifier la cohérence visuelle du GUI
- [ ] Améliorer l'aspect visuel du GUI

#### Affinages et compléments de gameplay
- [ ] Implémenter l'ordre "greffe"
- [ ] Faire générer des points de culture par les oisifs
- [ ] Ajouter les seuils de déblocage liés aux points de culture
- [ ] Générer un colon uniquement si le joueur n'a aucune ville ni colon
- [ ] Ajouter un easter egg au milieu de l'océan

## Version 1.0
### Objectif
Code debuggé, minifié, sécurisé, légalisé, fonctionnel.
#### Objectif secondaire
Réfléchir à un moyen de jouer gratuitement contre la conso de pub pour 3€? Est ce possible? Est ce souhaitable? (pas sûr, est ce que je veux vraiment faire de la pub pour la concurrence ?!)
### Déploiement
Un serveur **KlodWorld** payant nommé *Maximus* qui utilise la branche **main** et se met à jour tout les **dimanches à minuit**, et redémarre le monde si nécessaire. 
Les joueurs disposent d'**un mois gratuit** le temps de découvrir le jeu (dont 2 semaines protection débutants), puis ils doivent s'abonner pour continuer.
Si le serveur est plein, il faudra créer d'autres serveurs **EU**.

### Diffusion
Grand public. Tenter d'atteindre JDG le meilleur ambassadeur de la stratégie et des MMO ;-)
### Fonctionnalités à implémenter durant cette phase
 - Monde de Demo qui reset tout les 1er de chaque mois : automatisation du process.
 - Monde permanent 1 "Maximus"

## Version 1.0++
### Objectif
Ajouter des nouvelles fonctionnalités utiles ou agréables. Lorsqu'une fonctionnalité est testée validée etc. elle peux passer sur la branche **main**, ce qui met à jour les serveurs de jeu.
### Déploiement
Un serveur **KlodWorld** nomme *DEV-Beta* qui utilise la branche **develop** et se met à jour tout les **jours à minuit**, et redémarre le monde si nécessaire. Il ne reset pas sauf cas particulier mais n'est accessible qu'au abonnés.
### Fonctionnalités à implémenter durant cette phase
 - Barre de progression des ordre en court "frise du temps"
 - permettre le changement de nom d'unités ou de ville (avec contrôle du modo)
 - permettre un look différent d'unité et de ville dans des style globalement historiques (antiquité européenne, inca, asiatique, orient, etc.)
 - permettre la gestion des saisons (climat) d'une semaine
 - permettre un chaînage des ordres
 - permettre le baby-sitting de compte
 - création de monde "flash" avec un TIC à 30 secondes au lieu de 5 minutes
 - Ajout de nouvelles quêtes divines

## Version 2.0
### Fonctionnalités à implémenter durant cette phase
 - Situer cette fois le jeu dans la **Renaissance** ?
 - Un monde qui se voit zoom/dezoome comme Google Earth
 - échelle 1:1 pour le monde; (~ 8000 heures pour faire le tour de l'équateur à pied.) (ou peut être 1:2 à réfléchir suivant le gameplay)
 - Vision en fonction du terrain, mais avancée : les montagne occulte le territoire "derrière"
 - ?
