# Roadmap de développement
**ALPHA** → **BETA** → **1.0**
## Stade ALPHA
### Objectif
Implémenter toutes les fonctionnalités du **Gameplay de base** de Klod Online, même si il y a des bugs ou des problèmes de performances.
### Déploiement
Un serveur **KlodWorld** nomme *DEV-Alpha* qui utilise la branche **develop** et se met à jour toutes les **5 minutes**, et redémarre le monde si nécessaire.
### Diffusion
Toutes personnes souhaitant regarder le stade de développement ou souhaitant participer au debug sont libre de s'inscrire, mais doivent être clairement averti que le jeu n'est pas jouable. On ne fait pas vraiment de pub en ligne pour le moment - ou très peu.
### Fonctionnalités à implémenter durant cette phase
- [x] Déplacement des unités 
- [x] Ville qui permettent de créer des unités
- [x] chat permettant de communiquer, et de linker des coordonnées
- [x] Exploration et brouillard de guerre fonctionnel
- [x] Croissance des villes, territoire (frontières) des villes 
- [ ] inventaire des unités et des villes
- [ ] ressources qui popent sur la carte et qui sont exploitable
- [ ] exploitation des ressources par des unités spécifiques dédiées ou les villes
- [ ] Coût en ressource pour les bâtiments, les unités, les villes
- [ ] Création de bâtiments dans les villes, avec les limitations en fonction des bâtiments précédents
- [ ] Ordre d'unités de "transformation" de l'unité, comme "fortification", "tour d'observation", etc. 
- [ ] Unité qui aménage le territoire (route, irrigation, canaux, raser une forêt....)
- [ ] échange de stuff entre unités et villes, amies ou non
- [ ] système de loot en cas de mort d'une unité ou d'une ville
- [ ] disparition du loot dans le temps
- [ ] Moral des unités et consommation de ressources

## Stade BETA
### Objectif
Implémenter et optimiser toutes les fonctionnalités du **Gameplay étendu**. Debugger pour une version **1.0** soignée. Faire également des équilibrages de règles de jeu.
### Déploiement
 - Un serveur **KlodWorld** nomme *DEV-Alpha* qui utilise la branche *develop* et se met à jour toutes les **5 minutes**, et redémarre le monde si nécessaire.
 - Un serveur **KlodWorld** nomme *DEV-Beta* qui utilise la branche *main* et se met à jour tout les **jours à minuit**, et redémarre le monde si nécessaire.
 - On pousse de *develop* vers *main* quand une fonctionnalité est considérée *debuggée*.

### Diffusion
Large. Il faut faire connaitre le jeu un maximum, pour permettre des tests de  charge. Récompenser les 50 premiers joueurs d'un abonnement à vie ?
### Fonctionnalités à implémenter durant cette phase
- [ ] diplomatie : pacte de paix, libre circulation, échange de carte, création de "clans" (alliances large à plusieurs joueurs), messagerie
- [ ] Combats et gestion des combats
- [ ] Protection débutant de une semaine ou deux
- [ ] commerce : échange de stuff verrouillable pour sceller l'accord
- [ ] chat global, chat privé de clan, chat de groupe (canal personnalisé), système de log pour le chat, et traçabilité en cas de plainte IRL
- [ ] modération, système permettant à un Modo ou un Dev de se connecter sans jouer, et accès au chat et au logs du jeu
- [ ] vie et mort des Empire; ajouter le système permettant à l'empire de vieillir et devenir barbare en cas d'abandon de jeu du joueur
- [ ] terrain qui changent avec le temps (Cf Le Monde/Vie du territoire)
- [ ] Missions divine et tableau d'honneur, leaderboard par joueur, par ville, par clan
- [ ] trêve de la nuit

## Version 1.0
### Objectif
Code debuggé, minifié, sécurisé, légalisé, fonctionnel.
### Déploiement
Un serveur **KlodWorld** de démo nommé *Lucius* qui utilise la branche **main** et se met à jour tout les **dimanches à minuit**, et redémarre le monde si nécessaire. Il reset sa BDD tout les mois.
Un serveur **KlodWorld** payant nommé *Maximus* qui utilise la branche **main** et se met à jour tout les **dimanches à minuit**, et redémarre le monde si nécessaire.
### Diffusion
Grand public. Tenter d'atteindre JDG le meilleur ambassadeur de la stratégie et des MMO ;-)
### Fonctionnalités à implémenter durant cette phase
 - Monde de Demo qui reset tout les 1er de chaque mois : automatisation du process.
 - Monde permanent 1 "Maximus"

## Version 1.0++
### Objectif
Ajouter des nouvelles fonctionnalités utiles ou agréables. Lorsqu'une fonctionnalité est testée validée etc. elle peux passer sur la branche **main**, ce qui met à jour les serveurs de jeu.
### Déploiement
Un serveur **KlodWorld** nomme *DEV-Beta* qui utilise la branche **develop** et se met à jour tout les **jours à minuit**, et redémarre le monde si nécessaire. Il ne reset pas mais n'est accessible qu'au abonnés.
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
 - Un monde qui se voit zoom/dezoome comme Google Earth
 - échelle 1:1 pour le monde; (~ 8000 heures pour faire le tour de l'équateur à pied.)
 - ?