# Roadmap de développement
ALPHA → BETA → 1.0

## Stade ALPHA

Branche Git : develop

Objectif : jeu en ligne avec PULL AUTO à chaque merge

Fréquence : toutes les minutes

Fonctionnalité : il faut un mécanisme pour prévenir via le chat (TCHAT) les joueurs des changements

Marketing :

Le site web doit pouvoir prévenir les joueurs même si les données sont de test (DEV)

Tout le monde peut créer des comptes et jouer

## Stade BETA

Branche Git : develop

Objectif : toutes les fonctionnalités de la version 1.0 sont en place

Notes : version ni optimisée, ni déboguée

PULL AUTO : toutes les mises à jour sont appliquées quotidiennement

Marketing : commencer à large diffusion

Version fixe avec toutes les fonctionnalités OR + Debug

Acceptation de PULL AUTO tous les dimanches à minuit

## Version 1.0

Branche Git : main

Version finale avec toutes les fonctionnalités

Acceptation de debug encore possible

PULL AUTO : mise à jour automatique tous les dimanches

Code minifié et sécurisé

Conforme aux besoins légaux (sécurité, loi)

# Fonctionnalités
Ce document décrit toutes les fonctionnalité souhaitées et attendues pour considérer KlodOnline terminé.

## Version Alpha 

## Fonctionnalités de la v0.1 (début de Beta)
Pour pouvoir commencer à accueillir des joueurs, on voudrait avoir les fonctionnalités de jeu suivantes :
 - Déplacement des unités
 - Ordre d'unités de "transformation" de l'unité, comme "fortification", "tour d'observation", etc.
 - Ville qui permettent de créer des unités
 - chat permettant de communiquer, et de linker des coordonnées
 - Exploration et brouillard de guerre fonctionnel

## Fonctionnalités prioritaire de la Beta
Des que la Beta est lancées il faut au plus vite faire cela
 - ressources qui popent sur la carte et qui sont exploitable
 - inventaire des unités et des villes
 - exploitation des ressources par des unités spécifiques dédiées ou les villes
 - Coût en ressource pour les bâtiments, les unités, les villes
 - échange de stuff entre unités et villes, amies ou non
 - système de loot en cas de mort d'une unité ou d'une ville

## Fonctionnalités de la v1.0 (fin de Beta)
Pour considérer la Beta comme finie, il faut les fonctionnalités suivante, sans bug
 - Croissance des villes, territoire (frontières) des villes 
 - Création de bâtiments dans les villes, avec les limitations en fonction des bâtiments précédents
 - commerce : échange de stuff verrouillable pour sceller l'accord
 - Unité qui aménage le territoire (route, irrigation, canaux, raser une forêt....)
 - terrain qui changent avec le temps (Cf Le Monde/Vie du territoire)
 - disparition du loot dans le temps
 - diplomatie : pacte de paix, libre circulation, échange de carte, création de "clans" (alliances large à plusieurs joueurs)
 - chat global, chat privé de clan, chat de groupe (canal personnalisé), système de log pour le chat, et traçabilité en cas de plainte IRL
 - modération, système permettant à un Modo ou un Dev de se connecter sans jouer, et accès au chat et au logs du jeu
 - vie et mort des Empire; ajouter le système permettant à l'empire de vieillir et devenir barbare en cas d'abandon de jeu du joueur
 - Missions divine et tableau d'honneur, leaderboard par joueur, par ville, par clan
 - trêve de la nuit
 - Monde de Demo qui reset tout les 1er de chaque mois
 - Monde permanent 1 "Maximus"

## Fonctionnalités post-Release
 - Barre de progression des ordre en court "frise du temps"
 - permettre le changement de nom d'unités ou de ville (avec contrôle du modo)
 - permettre un look différent d'unité et de ville dans des style globalement historiques (antiquité européenne, inca, asiatique, orient, etc.)
 - permettre un chaînage des ordres
 - permettre le baby-sitting de compte
 - création de monde "flash" avec un TIC à 30 secondes au lieu de 5 minutes
 - Ajout de nouvelles quêtes divines

## Fonctionnalités v2.0
 - Un monde qui se voit zoom/dezoome comme Google Earth
 - échelle 1:1 pour le monde; (~ 8000 heures pour faire le tour de l'équateur à pied.)
 - 