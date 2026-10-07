# Roadmap v2 — KlodOnline

**Versionning A.B.C :**
- **A (MAJOR)** : Grand domaine de gameplay livré
- **B (MINOR)** : Fonctionnalité du domaine
- **C (PATCH)** : Correctif

**Départ :** `v0.1.0` → **`v1.0.0`** = fin de BETA, jeu payant

---

## v0.1 — CHAT & COMMUNICATION

- [x] Refactor complet du chat (3 étapes)
- [x] JWT authentication pour le chat
- [x] Message de bienvenue dans le chat
- [x] Notifications Discord
- [x] Commande `/clear`
- [x] Rate-limiter de reconnexion
- [x] Notifications joueur (logs)
- [ ] Canaux de clan
- [ ] Logs et traçabilité du chat
- [ ] Chat de groupe (canal personnalisé)

## v0.2 — MONDE & TERRAIN

- [x] Génération aléatoire du monde
- [x] Fog of war (brouillard de guerre)
- [x] Algorithme anti-morosité (`noisy_spiral`, `LessBoring`)
- [x] Système de reshape du terrain
- [x] Système de perte de territoire
- [x] Irrigation interdite sur cases de ville
- [ ] Terrain qui évolue avec le temps
- [ ] Saisons (climat)
- [ ] Génération spontanée de pistes
- [ ] Monde échelle 1:1 (v2.0)

## v0.3 — VILLES

- [x] Création de villes
- [x] Croissance des villes, territoire (frontières)
- [x] Panel ville complet (rewrite)
- [x] Système de construction de bâtiments
- [x] City level up
- [x] Production / file de production
- [x] Ressources spéciales en ville
- [x] Bâtiments de marché (config XML)
- [ ] Dissoudre une unité dans la ville (DISBAND transfère ressources)
- [ ] Règle de spawn des colons (ville morte → colon seulement si 0 ville ET 0 colon)

## v0.4 — INVENTAIRE & ÉCHANGE

- [x] Inventaire des unités et villes
- [x] Déplacement et split de stacks
- [x] Échange unité ↔ ville
- [x] Système de loot (mort d'unité/ville)
- [x] Disparition du loot dans le temps
- [x] GameAPI rewrite + board cache

## v0.5 — RESSOURCES & PRODUCTION

- [x] Ressources qui popent sur la carte
- [x] Exploitation des ressources par les villes
- [x] Exploitation par unités dédiées
- [x] Craft dans les villes
- [x] Production, inventaire des traits
- [x] Moral des unités et consommation de ressources
- [ ] Points de Culture (oisifs → culture, déblocages)

## v0.6 — INTERFACE & INTERNATIONALISATION

- [x] Refactor CSS (fichiers séparés)
- [x] Internationalisation (multilingue)
- [x] Sauvegarde du choix de langue
- [x] Système de police unifié
- [x] Encyclopédie
- [x] Tooltip au survol (unité, terrain, propriétaire)
- [x] Panel stat du monde
- [ ] Révision complète du GUI (unifié/cohérent)
- [ ] Barre de progression / frise du temps (1.0++)
- [ ] Chaînage d'ordres (1.0++)
- [ ] Renommer unités/villes (1.0++)

## v0.7 — COMBAT

- [x] Système de combat (attaque/défense, retraite)
- [x] Rapports de combat
- [x] Prise de ville
- [x] PvP
- [x] Ajustements d'équilibrage
- [ ] Distinguer ordre MOVE et ATTAQUE

## v0.8 — UNITÉS

- [x] Création d'unités en ville
- [x] Panel liste d'unités
- [x] Upgrade des unités
- [x] Limite d'unités
- [x] Embarquement dans les bateaux
- [x] Migration d'unité
- [x] Ordre `move morph`
- [x] Filtres par type d'unité/ordre/inventaire
- [x] Barre de moral
- [x] Unités civiles à 0 en attaque
- [x] Multi-bateau au choix
- [x] Option cabotage
- [x] Barbares (IA mobs)
- [ ] Ordre "greffe" (groupement d'unités)
- [ ] Gestion des unités comme élément de population
- [ ] Rattachement d'unité à une autre ville
- [ ] Baby-sitting de compte (1.0++)

## v0.9 — ESPIONNAGE

- [x] Espions
- [x] Contre-espionnage
- [x] Rumeurs d'intrusion
- [ ] Détection de l'espion en mouvement
- [ ] Limite d'un espion infiltré par ville
- [ ] Espions invisibles ne comptent pas dans le "crowded"
- [ ] Rumeurs améliorées (civil/militaire, pas d'alerte alliés)

## v0.10 — ÉCONOMIE & COMMERCE

- [x] Système de commerce (trading)
- [x] Échange de stuff entre unités et villes amies
- [x] Message box (gamemails)
- [x] Filtres de gamemails
- [ ] Marchand PNJ (monnaie de régulation)
- [ ] Commerce entre joueurs
- [ ] Échange verrouillable

## v0.11 — JOUEURS & SOCIÉTÉ

- [x] Vie et mort des empires
- [x] Abandon des joueurs
- [x] NPC (IA)
- [x] Protection débutant (2 semaines)
- [x] Classement / leaderboard
- [x] Panel joueur (stats)
- [x] Logs d'empire
- [x] Meilleur placement des nouveaux venus
- [ ] Traité d'amitié étendu (voir relations alliés)
- [ ] Trêve de la nuit
- [ ] Options/Divinités (menu de sélection)

## v0.12 — ADMIN & MODÉRATION

- [x] Interface GM (administration)
- [x] Fonctionnalités admin
- [x] Analytics (Rybbit / Plausible)
- [x] KlodReviewAI
- [ ] Système de modération (Modo/Dev sans jouer)
- [ ] Accès aux logs du jeu pour modération

## v0.13 — QUÊTES & TUTORIEL

- [x] Tutoriel de bienvenue
- [x] Système de quêtes (quest system)
- [x] Quêtes d'initiation (welcome quest chain)
- [x] Quêtes multi-pages (flavor narrative)
- [x] Objets divins (Time Catalyst)
- [x] Animations (sparkles, snowfall)
- [ ] Tableau d'honneur / leaderboard par quêtes
- [ ] Nouvelles quêtes divines (1.0++)

## v0.14 — INFRASTRUCTURE

- [x] Docker / Docker Compose
- [x] Makefile
- [x] CI (PR lint, Twitter, Discord)
- [x] Vite integration
- [x] Split docker-compose (prod/dev)
- [x] Reverse proxy (FrankenPHP)
- [x] Healthcheck
- [x] Outils de dev (linter, phpcsfixer, etc.)
- [ ] Monde de Demo reset mensuel (1.0)
- [ ] Monde permanent "Maximus" (1.0)

## v0.15 — QUALITÉ DE VIE

- [x] Qualité de vie (#133)
- [x] Qualité de vie (#159)
- [x] Aide en jeu (#169)
- [x] UI & Quality of Life (#156)
- [x] Bug Fixes and UI Improvements (#188)
- [x] Correctifs de sécurité (#189)
- [ ] Easter egg (case Poulpe)

---

## v1.0.0 — BÊTA TERMINÉE / JEU PAYANT

### Objectif
- Code debuggé, minifié, sécurisé, légalisé, fonctionnel
- Tous les domaines v0.1 à v0.15 livrés et stabilisés

### Déploiement
- Serveur **Maximus** (payant, branche `main`)
- 1 mois gratuit (dont 2 semaines protection débutant)
- Serveurs **EU** supplémentaires si saturation

---

## v1.x — AMÉLIORATIONS (ex-1.0++)

- [ ] Barre de progression des ordres en cours
- [ ] Renommer unités et villes (avec contrôle modo)
- [ ] Skins civilisation (look différent)
- [ ] Gestion des saisons (climat hebdomadaire)
- [ ] Chaînage des ordres
- [ ] Baby-sitting de compte
- [ ] Mondes "flash" (TIC à 30s au lieu de 5min)
- [ ] Nouvelles quêtes divines

---

## v2.0 — ÈRE RENAISSANCE

- [ ] Époque Renaissance
- [ ] Monde zoom/dézoom (Google Earth-like)
- [ ] Échelle 1:1 (~8000h pour tour équateur à pied)
- [ ] Vision terrain avancée (montagnes occultent la vue)
