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
- [ ] diplomatie : pacte de paix, libre circulation, échange de carte, création de "clans" (alliances large à plusieurs joueurs), messagerie
  - _Manquent : la messagerie inter-joueurs, les alliances multi-joueurs (clans), et l'échange de carte._
- [ ] Combats et gestion des combats
  - _Note : Le système de combat est implémenté (calcul attaque/défense, retraite, rapports de combat, prise de ville). Des ajustements d'équilibrage sont attendus._
- [ ] Upgrade des unités
- [ ] Gestion des unités comme élément de la population d'une ville, possibilité de rattacher une unité à une autre ville
- [ ] Possibilité de dissoudre une unité dans la ville
  - _Note : L'ordre DISBAND existe mais ne transfère pas les ressources dans la ville._
- [ ] échange de stuff entre unités et villes d'un autre joueur OU système de marché/vente - commerce : échange de stuff verrouillable pour sceller l'accord
- [x] Protection débutant de 2 semaine par défaut
- [ ] chat global, chat privé de clan, chat de groupe (canal personnalisé), système de log pour le chat, et traçabilité en cas de plainte IRL
  - _Note : Le serveur chat Socket.io est en place. Manquent : canaux de clan, logs, traçabilité._
- [ ] Marchand PNJ qui pratique des prix de voleurs, mais permettant d'introduire une monnaie et une valeur de régulation.
  - _Note : Les constantes et bâtiments de marché sont définis dans la config XML. La logique de marchand PNJ n'est pas encore codée._
- [ ] Commerce entre joueurs
- [ ] modération, système permettant à un Modo ou un Dev de se connecter sans jouer, et accès au chat et au logs du jeu
  - _Note : Un GM GUI existe pour l'administration._
- [ ] terrain qui changent avec le temps (Cf Le Monde/Vie du territoire)
- [ ] Missions divine et tableau d'honneur, leaderboard par joueur, par ville, par clan
- [ ] trêve de la nuit
- [ ] Saisons !
- [ ] révision du GUI pour un truc beau et surtout unifié / cohérent (mais là faudra du budget)

#### Affinages et compléments de gameplay
- [ ] **Espionnage avancé** : détection de l'espion en mouvement sur case adverse, limite d'un espion infiltré par ville, les espions invisibles ne comptent pas dans le "crowded", rumeurs d'intrusion améliorées (préciser civil/militaire, pas d'alerte pour alliés, pas pour unités invisibles)
- [ ] **Ordre "greffe"** : grouper des unités qui se déplacent ensemble à la vitesse de la plus lente
- [ ] **Distinguer ordre MOVE et ATTAQUE** : séparer clairement le déplacement de l'attaque dans l'interface
- [ ] **Échange en tant qu'ordre** : transformer l'échange de ressources en ordre soumis au TIC (pas instantané)
- [ ] **File de construction** : permettre de planifier au moins une construction de plus par ville
- [ ] **Points de Culture** : les oisifs génèrent de la culture, seuils de déblocage pour progrès avancés
- [ ] **Moral des unités en ville** : les villes remontent le moral des unités présentes, même sans nourriture, sauf en cas de famine
- [ ] **Règle de spawn des colons** : le jeu ne génère un colon que si le joueur n'a aucune ville ET aucun colon
- [ ] **Irrigation interdite sur les cases de ville**
- [ ] **Unités civiles à 0 en attaque** : les civils ne peuvent pas attaquer
- [ ] **Multi-bateau au choix** : faciliter l'embarquement quand plusieurs navires sont sur la même case (icône inventaire plein)
- [ ] **Traité d'amitié étendu** : permet de voir toutes les relations diplomatiques de son ami
- [ ] **Suppression multiple de mails**
- [ ] **Classement et stats joueurs** : pouvoir cliquer sur un joueur pour voir ses statistiques (utile pour la diplomatie)
- [ ] **Options/Divinités** : nouveau menu de sélection de divinité
- [ ] **Génération spontanée de pistes** sur la carte
- [ ] **Option "cabotage"** : permettre aux bateaux de longer les côtes pour éviter la haute mer
- [ ] **Easter egg** : case spéciale avec référence à Poulpe au milieu de l'océan
- [ ] **Événements : les Harukans** — tempêtes qui diminuent la production des villes, disbloquent les unités civiles, endommagent les bâtiments, et créent des unités militaires sauvages

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