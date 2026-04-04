# Tour de jeu
____

## Cycles de Jeu
- **TIC (Tour)** : 300 secondes (5 minutes)
- **192 TICs par jour IRL** (sans trêve nocturne — la trêve nocturne n'est pas encore implémentée)
- **1 TIC = 1 heure** en temps de jeu
- **1 jour IRL = 8 jours** dans le jeu
- **3 mois IRL = ~1,97 années** en jeu

## Timing et synchronisation
Le serveur fonctionne en **tours synchronisés**. Tous les joueurs jouent en même temps, donnent des ordres à leurs unités ou villes, et à chaque **TIC** le serveur calcule les ordres et modifie le monde. Pendant la **résolution**, le monde est verrouillé (`lock: true` dans `status.json`) et aucun nouvel ordre n'est exécuté (mais l'interface permet d'en ajouter pour le prochain tour).

Toute action dans l'interface est soumise au système d'ordres, y compris le renommage de ville ou les transferts d'inventaire.

## Ordre d'exécution d'un tour
Implémenté dans `TurnManager::playTurn()` :

### 1. Nettoyage et rechargement
- Nettoyage des collections : Players, Locatables, Orders, InventoryCells, Diplomacy
- Rechargement complet depuis la base de données
- Reset du cache anti-spam de notifications

### 2. Diplomatie
- Création des relations diplomatiques manquantes entre joueurs

### 3. Tour des villes (`cityTurn`)
- Production de ressources (récolte, craft)
- Consommation de nourriture
- Gestion de la population (croissance sigmoïde, famine)
- Avancement des constructions
- Avancement des recrutements
- Gestion de la main d'œuvre

### 4. Tour des unités (`unitTurn`)
- Production des unités (camps de récolte)
- Consommation de nourriture
- Capture de territoire

### 5. Décrémentation des ordres (`turnOrderDecrease`)
- Réduction des compteurs de tours restants pour chaque ordre en attente

### 6. Exécution des ordres (`turnOrderExecute`)
- Exécution des ordres dont le compteur est à 0
- Boucle de retry pour les ordres reportés (case occupée, conflits)
- Fallback : les ordres restants voient leur tour incrémenté

### 7. Vérifications de sécurité (`unitSafetyChecks`)
- Destruction des unités terrestres sur l'eau
- Réversion des espions infiltrés invalides

### 8. Tour des joueurs (`playerTurn`)
- Gestion des joueurs abandonnés/inactifs

### 9. Tour des PNJ (`npcTurn`)
- Comportement des villes barbares (recrutement, nettoyage unités excédentaires)
- ~200/288 de chance par tour de recruter si ≥2 travailleurs inactifs

### 10. Usure du butin (`lootWear`)
- Dégradation progressive des loots au sol

### 11. Génération des sources (`generateSources`)
- Placement aléatoire de nouvelles sources de ressources selon la rareté

### 12. Évolution du monde (`worldEvolution`)
- Dégradation/entretien des routes (+10/tour si entretenues, -1/tour sinon)
- Dégradation/entretien de l'irrigation (+1 si exploitée, -1 sinon)
- Conversion des terrains non entretenus (irrigation → forêt/marais)
- Réassignation des hexagones orphelins aux "Barbarians"

### 13. Sauvegarde et déverrouillage
- Sauvegarde de toutes les collections en base
- Déverrouillage du serveur

## Échelle de temps/distance
Avec **1 TIC / 5 min**, il y a **192** TICs par jour IRL.

| TIC sec | TIC/Jour | 16h Jeu | Jours IG pour 1 jour IRL | TIC sur 3 mois IRL | Années IG en 3 mois |
| ------- | -------- | ------- | ------------------------ | ------------------ | ------------------- |
| 300     | 192      | 128     | 8                        | 17280              | 1,97                |

| Durée d'un TIC  | 5 tours | 10 tours | 20 tours | 50 tours | 100 tours |
| --------------- | ------- | -------- | -------- | -------- | --------- |
| 300 sec (5 min) | 25 min  | 50 min   | 1h40     | 4h10     | 8h20      |

## Non implémenté
- **Trêve nocturne** : Les ordres de mouvement ne sont pas figés la nuit
- **Stacks d'unités** : Le mouvement simultané de groupes n'est pas encore actif (max stack = 4 configuré mais non utilisé pour le déplacement groupé)
- **Unités terrestres sur rivières** : Les unités terrestres ne peuvent pas traverser les rivières (elles sont considérées comme amphibies)

