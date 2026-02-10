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
- [ ] Combats et gestion des combats
- [ ] Upgrade des unités
- [ ] Gestion des unités comme élément de la population d'une ville, possibilité de rattacher une unité à une autre ville
- [ ] Possibilité de dissoudre une unité dans la ville
- [ ] échange de stuff entre unités et villes d'un autre joueur OU système de marché/vente - commerce : échange de stuff verrouillable pour sceller l'accord
- [ ] Protection débutant de 2 semaine par défaut 
- [ ] chat global, chat privé de clan, chat de groupe (canal personnalisé), système de log pour le chat, et traçabilité en cas de plainte IRL
- [ ] Marchand PNJ qui pratique des prix de voleurs, mais permettant d'introduire une monnaie et une valeur de régulation. Personne achètera moins cher que le PNJ et personne vendra plus cher que le PNJ… Donc le PNJ fixe les bornes des prix. Pour éviter l'inflation, mettre au PNJ de l'argent "cloud", afin qu'il ne créé aucune richesse intrinsèque (à étudier en détail) (ou qu'il dispose d'une somme égale à l'or existant divisé par le nombre de joueur ? il faut vraiment creuser le sujet)
- [ ] Commerce entre joueurs
- [ ] modération, système permettant à un Modo ou un Dev de se connecter sans jouer, et accès au chat et au logs du jeu
- [ ] terrain qui changent avec le temps (Cf Le Monde/Vie du territoire)
- [ ] Missions divine et tableau d'honneur, leaderboard par joueur, par ville, par clan
- [ ] trêve de la nuit
- [ ] Saisons !
- [ ] révision du GUI pour un truc beau et surtout unifié / cohérent (mais là faudra du budget)

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