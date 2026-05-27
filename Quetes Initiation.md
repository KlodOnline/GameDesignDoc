# Quêtes pour Débutants (Onboarding)

## État actuel
Ce système de quêtes d'introduction **n'est pas encore implémenté**. Il est conçu pour être disponible dès le début du jeu, avant même le choix de la divinité.

## Concept
Les quêtes pour débutants servent à familiariser les nouveaux joueurs avec les mécaniques de base de Klod Online :
- Déplacement et utilisation des unités de départ (settler + scout)
- Fondation de la première ville via FOUND_CITY
- Gestion de la ville (population, workers, production de ressources)
- Construction de bâtiments et arbre de points (requisitePoints)
- Craft dans les ateliers (primitiveworkshop)
- Recrutement et déploiement d'unités (reaper, militia)
- Collecte de ressources automatisée via les camps de récolteurs
- Exploration de la carte avec l'éclaireur (scout)
- Premiers combats contre les barbares
- Choix de la divinité tutélaire

Ces quêtes sont obligatoires et guident le joueur à travers les premières étapes essentielles du jeu. Chaque quête réussie récompense le joueur avec des ressources de base et prépare le terrain pour le choix de la divinité.

## Structure
Les quêtes pour débutants suivent une chaîne linéaire appelée "initiation" (init). Chaque quête débloque la suivante, formant un parcours pédagogique complet basé sur les mécaniques réelles du jeu accessibles dès le début.

### Mécaniques de départ (vérifiées via le code)
- Le joueur commence avec **1 settler (id=0, 3000 food en inventaire)** + **1 scout (id=3)**
- Ordres settler : MOVE, EXCHANGE, FOUND_CITY, EMBARK, DISBAND — **ne peut PAS collecter de ressources**
- Ordres scout : MOVE, EXCHANGE, MOVE_MORPH, EMBARK, DISBAND — **ne peut PAS collecter de ressources**
- Le scout a fov=2 et peut MOVE_MORPH en tower (fov=3, def=1, statique)
- Aucune ville au démarrage — le settler doit utiliser FOUND_CITY
- FOUND_CITY instantané pour la première ville : consomme le settler, transfère son inventaire (3000 food) à la ville
- Après FOUND_CITY : ville pop=1000, 2 workers auto-affectés à la nourriture via `cityGetJoblessToWork($city, 2)`
- Garantie terrain : ≥3 cases food≥2, ≥1 case bois>0, ≥1 case pierre>0
- Pour obtenir bois/pierre : réaffecter manuellement les workers de la ville (food → wood → stone via `assignWorkerToGround`)
- La ville n'a aucune ressource en inventaire au démarrage (hormis food transférée du settler)

### Liste des quêtes d'initiation (WIP)

#### Chaîne d'initiation générale

- **init_01_starting_units** : Vos unités de départ
  - Vous commencez avec 1 settler (3000 food en inventaire) et 1 scout
  - Objectif : Sélectionner votre settler et observer ses ordres disponibles
  - Récompense : Aucun (état initial du jeu)

- **init_02_scout_surroundings** : Première exploration (! long !)
  - Utiliser votre scout pour révéler quelques cases inconnues autour de votre position de départ
  - Le scout a fov=2, permettant de voir 2 cases de distance
  - Récompense : 

##### CHAIN QUESTS : CITY BASICS

- **init_03_found_city** : Fondation de la première ville
  - Déplacer votre settler vers une case appropriée et utiliser l'ordre FOUND_CITY
  - La première ville est instantanée ; le settler est consommé et ses 3000 food passent à la ville
  - Récompense : 

- **init_05_reassign_to_wood** : Réaffecter un worker au bois
  - Placer 1 worker sur une case bois dans le rayon de la ville
  - La production de nourriture baisse, mais vous obtenez du bois
  - Récompense : 100 bois supplémentaires (total: 100 bois pour l'atelier)

- **init_06_reassign_to_stone** : Réaffecter un worker à la pierre
  - Placer 1 worker sur une case pierre dans le rayon de la ville
  - Vous avez maintenant ~1 food, ~1 wood, ~1 stone par tour
  - Récompense : 100 pierre supplémentaires (total: 200 pierre pour l'atelier)

- **init_07_build_workshop** : Lancer la construction du primitiveworkshop
  - Construire un primitiveworkshop (id=42) dans votre ville (coût: 100 bois, 200 pierre, 0 point requis)
  - Récompense : Accélération du temps sur le batiment !

##### CHAIN QUESTS : WARRIOR

- **init_11_build_guardhouse** : Construire un poste de garde
  - Construire un guardhouse (id=5) dans votre ville (coût: 100 bois, 200 pierre, 0 point requis)
  - Récompense : Accès au recrutement d'unités militaires (militia, id=2)

- **init_19_craft_weapons_for_militia** : Forger 500 armes pour la milice
  - Produire 450 primitive_weapons supplémentaires dans votre atelier (vous en avez déjà 50)
  - Coût : 450 bois, 450 pierre
  - Récompense : 100 primitive_weapons (total cumulé : assez pour recruter militia)

- **init_21_recruit_militia** : Recruter votre première milice
  - Créer votre première unité de militia (id=2) dans votre ville
  - Coût : 500 primitive_weapons, 4 tours, guardhouse requis
  - Récompense : 1 unité de militia + 100 nourriture

- **init_18_build_rangershall** : Construire un hall de rangers
  - Construire un rangershall (id=6) dans votre ville (coût: 100 bois, 200 pierre, 0 point requis)
  - Récompense : Accès au recrutement de scouts supplémentaires (scout, id=3)

- **init_22_recruit_scout** : Recruter un deuxième scout
  - Créer un scout supplémentaire (id=3) dans votre ville
  - Coût : 500 primitive_weapons, 4 tours, rangershall requis
  - Récompense : 1 unité de scout

##### CHAIN QUESTS : GATHER 

- **init_13_build_harvesters_hut** : Construire une cabane de récolteurs
  - Construire une cabane_recolte (id=55) dans votre ville (coût: 400 bois, 200 pierre, 1 point requis)
  - Récompense : Accès au recrutement d'unités de récolte (reaper1, id=45)

- **init_14_craft_tools_for_reaper** : Forger 500 outils pour le récolteur
  - Produire 450 primitive_tools supplémentaires dans votre atelier (vous en avez déjà 50)
  - Coût : 450 bois, 450 pierre
  - Récompense : 100 primitive_tools (total cumulé : assez pour recruter reaper1)

- **init_15_recruit_harvester** : Recruter votre premier récolteur
  - Créer votre première unité de reaper1 (id=45) dans votre ville
  - Coût : 500 primitive_tools, 4 tours de recrutement, cabane_recolte requis
  - Récompense : 1 unité de reaper1 + 50 bois (pour ses déplacements)

- **init_16_deploy_camp** : Déployer votre camp de récolte
  - Déplacer votre reaper1 vers une case bois ou pierre et utiliser MOVE_MORPH pour le transformer en camp_reaper1
  - Le camp s'auto-affecte à la meilleure ressource (food → wood → stone) et capture le territoire (conquest=true)
  - Récompense : 1 camp_reaper1 (1 worker, production automatique)

- **init_17_ramp_up_resources** : Développer votre production (moteur triche et met une ressource verte dans les 4 cases autour ?)
  - Laisser votre camp_reaper1 et les workers de la ville produire des ressources rares (vertes)
  - Objectif : 
  - Récompense : 

##### CHAIN QUESTS : EXPAND

- **init_23_scout_surroundings** : Explorer en profondeur
  - Utiliser vos scouts pour explorer 8 cases inconnues autour de votre ville
  - Les scouts ont fov=2 et peuvent utiliser MOVE_MORPH en tower (fov=3) pour une meilleure vision
  - Récompense : Révélation des ressources rares à proximité (minerais, chevaux, etc.)

- **init_24_first_combat** : Premier combat contre les barbares
  - Détruire une petite bande de barbares voisine avec votre militia
  - Récompense : 150 or + 100 nourriture + 100 bois (ressources substantielles pour progresser)

- **init_25_expand_harvesting** : Étendre vos capacités de récolte
  - Recruter un deuxième reaper1 et le déployer en camp
  - Coût : 500 primitive_tools, 4 tours
  - Récompense : 1 unité de reaper1 (deuxième camp de récolte)

- **init_26_choose_deity** : Choix de la divinité tutélaire
  - Sélectionner votre divinité tutélaire (Kael pour la guerre, Erya pour l'artisanat, Toran pour la diplomatie/exploration)
  - Récompense : 100 points de réputation avec la divinité choisie + 100 or
  - Débloque : Accès au système de missions divines

#### Chaîne d'initiation spécifique à chaque divinité (après init_26)
Après avoir choisi une divinité, des quêtes d'initiation spécifiques sont disponibles :
- Pour Kael (guerre) : quêtes orientées vers le renforcement militaire et la conquête territoriale de base
- Pour Erya (artisanat) : quêtes orientées vers l'amélioration du craft et la production de ressources
- Pour Toran (diplomatie) : quêtes orientées vers l'exploration avancée et l'établissement de premiers contacts

## Intégration avec le système de missions divines
Les quêtes d'initiation servent de prérequis au système de missions divines :
- Aucune mission divine ne peut être entreprise avant d'avoir complété init_26_choose_deity
- La réputation initiale avec la divinité choisie est basée sur la réussite de init_26
- Les quêtes d'initiation spécifiques à chaque divinité préparent le joueur aux types de missions qu'il rencontrera ensuite

## Récompenses et progression
- Chaque quête d'initiation fournit des ressources de base essentielles pour bien démarrer
- Aucune perte de réputation ou de ressources en cas d'échec (elles peuvent être répétées)
- Compléter toute la chaîne d'initiation générale donne un bon départ dans toutes les ressources de base
- Les quêtes spécifiques à chaque divinité offrent une première poussée dans le domaine de spécialité choisi

## Notes de conception
- Les quêtes d'initiation doivent être simples mais gratifiantes
- Elles doivent enseigner une mécanique spécifique sans surcharger le joueur
- L'enchaînement doit paraître naturel et fluide (unités de départ → exploration → fondation de ville → workers → atelier → craft → poste de garde → cabane → récolteurs → camps → rangershall → recrutement → exploration → combat → spécialisation)
- Le choix de la divinité doit être présenté comme une étape importante mais pas intimidante
- Les récompenses doivent être suffisamment substantielles pour avoir un impact réel sur le début de partie
- Les quêtes spécifiques à chaque divinité doivent clairement illustrer le style de jeu associé à chacune