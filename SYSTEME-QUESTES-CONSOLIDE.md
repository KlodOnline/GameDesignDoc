# Système de Quêtes Divines — Document Consolidé

> Fusion du GDD (`Les Quetes.md`) et du Plan Technique (`PLAN-DIVINITES-ET-QUETES.md`)
> Dernière mise à jour: 2026-04-29

---

## 1. Vision — Le "Pourquoi"

Le système de quêtes de Klod transforme un simple joueur en légende vivante. L'idée centrale est **l'entonnoir** : on part d'un tutoriel classique pour finir dans une guerre de divinités où chaque joueur ne joue pas forcément au même jeu.

### Ce qui rend ce système unique

1. **Adaptabilité** — Tu joues à Civilization (Artisanat), ton voisin à Total War (Guerre), et vous interagissez via le même moteur.
2. **Secret** — Le moteur génère de l'intrigue politique grâce aux missions cachées (autres joueurs ignorent tes vraie objectifs).
3. **Dynamisme** — Le monde n'est pas figé ; les Fléaux obligent les empires à sortir de leur routine.
4. **Équilibre** — Pas de bonus permanents abusifs. Les Dieux donnent des "coups de pouce" éphémères (Unités/Buffs) qui demandent un effort constant (Faveur).

---

## 2. Le Pantheon — Les Trois Dieux

Le panthéon de Klod est composé de **trois divinités** qui rivalisent pour gagner la faveur du **Dieu des Dieux**.

| Dieu | Domaine | Couleur | Arbre de bâtiments | Style de jeu |
|------|---------|---------|-------------------|---------------|
| **Kael** | Guerre | Rouge | `military` | Conquérir, combattre, dominer, espionner |
| **Erya** | Artisanat | Bleu | `craft` | Construire, produire, crafter, améliorer |
| **Toran** | Économie | Or | `trade` | Échanger, explorer, accumuler, commercer |

### Répartition des arbres de bâtiments

Ces trois dieux correspondent directement aux **trois arbres de bâtiments** existants dans `buildings.xml` :

- Kael → `military`
- Erya → `craft`
- Toran → `trade`

### Choix de la divinité de tutelle

- Le joueur choisit sa divinité **après la chaîne d'initiation** (quand il a goûté aux 3 styles)
- Le choix est **définitif** (ou modifiable avec un gros malus de réputation, à définir)
- La divinité de tutelle donne accès aux **quêtes colorées** de ce dieu + les quêtes hybrides impliquant ce dieu
- Les quêtes **neutres** et les quêtes **d'initiation** sont accessibles à tous

---

## 3. Système de Réputation

### Principe: le réservoir

La réputation est un **score numérique** qui monte et descend, comme un réservoir qui fuit :

```
Réputation = somme(gains_quêtes) - somme(dégradation_temps)
```

### Scores de réputation

Chaque joueur a **4 scores de réputation** :

| Score | Description | Calcul |
|-------|-------------|--------|
| `rep_kael` | Réputation auprès de Kael (Guerre) | Quêtes Kael + hybrides Kael + neutres/3 |
| `rep_erya` | Réputation auprès d'Erya (Artisanat) | Quêtes Erya + hybrides Erya + neutres/3 |
| `rep_toran` | Réputation auprès de Toran (Économie) | Quêtes Toran + hybrides Toran + neutres/3 |
| `rep_total` | Réputation globale (faveur divine) | `rep_kael + rep_erya + rep_toran` |

### Gain de réputation

| Type de quête | Gain rep dieu principal | Gain rep dieu secondaire | Gain rep autres |
|---------------|------------------------|--------------------------|-----------------|
| Colorée (1 dieu) | +100% du reward | — | — |
| Hybride (2 dieux) | +60% du reward | +60% du reward | — |
| Neutre | +33% du reward | +33% du reward | +33% du reward |
| Initiation | Variable (voir section 5) | | |

### Dégradation dans le temps

La réputation se dégrade **à chaque tour d'environnement** (1 fois par jour IRL, soit tous les 288 TICs) :

```
dégradation_quotidienne = réputation_actuelle * TAUX_DEGRADATION
```

| Paramètres proposés | Valeur |
|---------------------|--------|
| `TAUX_DEGRADATION` | 0.5% par jour IRL (~15% par mois) |
| `REP_PLANCHER` | 0 (la réputation ne peut pas être négative) |
| `REP_PLAFOND` | 100 000 (softcap ; au-delà, la dégradation s'accélère) |

> **Note:** Le "tour d'environnement" (288 TICs = 1 jour) n'existe pas encore dans le code. Il faut l'implémenter dans `turn_manager.php`.

---

## 4. Phases de Jeu

### Phase 1: L'Éveil (Tutoriel)

- **Interlocuteur:** La Mascotte (un petit esprit, un vieux scribe)
- **But:** Apprendre les bases (fonder, construire, explorer)
- **Mécanique:** Ligne droite — tout le monde fait la même chose
- **Fin de phase:** Le joueur peut produire ses premières ressources de palier 2 ("Bleu")

### Phase 2: La Quête du Sanctuaire (Le Grand Choix)

C'est le pivot du jeu. Le joueur n'est plus un débutant, il attire l'attention des Dieux.

- **Le défi:** Ériger un bâtiment spécifique (Forge 2, Marché 2, etc.) dans la ville de son choix
- **Le Serment:** En terminant ce bâtiment, la ville devient son **Sanctuaire**
- **Choix:** Le joueur choisit sa divinité (Simple ou Hybride)
- **Impact:** Ce choix débloque son "style de jeu"

### Phase 3: Le Régime des Quêtes Divines (Coeur du jeu)

Trois types d'objectifs une fois le Sanctuaire établi:

#### A. Les Missions Sacrées (Objectifs Secrets)

Comme au Risk ou aux Aventuriers du Rail, le Dieu donne une mission que les autres ne voient pas.

- _Exemple:_ "Contrôle toutes les sources de Fer dans un rayon de 20 cases"
- _Le sel:_ Tes voisins voient que tu t'étends, mais ils ignorent que c'est pour satisfaire ton Dieu

#### B. Les Épreuves de Faveur (Quêtes Cycliques)

Des quêtes régulières pour gagner de la **Faveur**. La Faveur est une monnaie divine qui "fuit".

- _Récompense:_ Tu dépenses ta Faveur pour acheter des **Miracles** (Buffs de 72h) ou invoquer des **Unités Légendaires** (Pégase, Géant)

#### C. Les Fléaux (World Events)

Les Dieux s'adressent à tout le monde. Moment "Britannia" ou "L'Iliade".

- _L'événement:_ La Peste ou les Sauterelles s'abattent sur le monde
- _La résolution:_ Les joueurs doivent collaborer ou s'affronter

### Phase 4: La Phase de Légende (Haut Niveau)

- **Le Classement d'Honneur:** Accomplir des quêtes divines est le seul moyen de monter dans le Panthéon
- **La Chute:** Si ton Sanctuaire est capturé ou rasé, tu perds le lien avec ton Dieu (malus de moral + chance de changer de divinité)

---

## 5. Types de Quêtes et Catégories

### Récapitulatif des catégories

| Catégorie | Type | Description |
|-----------|------|-------------|
| `initiation` | PvE | Tutoriel — 7 étapes universelles |
| `absolute` | PvE | Quêtes de divinité — colorées (1 dieu) ou hybrides (2 dieux) |
| `relative` | PvP | Compétition — classement, comparaison entre joueurs |

### Sous-classification des quêtes `absolute`

| Sous-type | Tag XML | Dieux impliqués | Exemple |
|-----------|---------|-----------------|---------|
| Neutre | `<deity>all</deity>` | Tous (gain /3 chacun) | "Atteindre 2000 habitants" |
| Colorée Kael | `<deity>kael</deity>` | Kael seul | "Détruire 3 unités ennemies" |
| Colorée Erya | `<deity>erya</deity>` | Erya seul | "Crafter 50 outils" |
| Colorée Toran | `<deity>toran</toran>` | Toran seul | "Posséder 5000 de bois" |
| Hybride Kael+Erya | `<deity>kael,erya</deity>` | Kael et Erya | "Construire un barracks et crafter des armes" |
| Hybride Kael+Toran | `<deity>kael,toran</deity>` | Kael et Toran | "Explorer 50 cases et détruire un barbare" |
| Hybride Erya+Toran | `<deity>erya,toran</deity>` | Erya et Toran | "Crafter des outils et les stocker dans un entrepôt" |

---

## 6. Chaîne d'Initiation — Les 7+1 Quêtes

| # | ID | Objectif | Checker | Dieu | Reward rep | Objectif pédagogique |
|---|-----|----------|---------|------|------------|---------------------|
| 1 | `init_01_settle` | Fondé ta première ville | `has_city(count=1)` | Neutre (all) | 50 | Apprendre à fonder une ville |
| 2 | `init_02_workshop` | Construire un Atelier Primitif | `has_building(primitiveworkshop,1)` | **Erya** | 50 | Découvrir les bâtiments & l'arbre de tech |
| 3 | `init_03_craft_weapons` | Crafter des Armes Primitives | `has_resource(primitive_weapons,500)` | **Erya** | 50 | Découvrir le craft |
| 4 | `init_04_scout` | Recruter un Éclaireur (nécessite `rangershall`) | `has_unit(scout,1)` | **Kael** | 50 | Découvrir le recrutement militaire |
| 5 | `init_05_find_green` | Trouver une ressource verte (rareté >=1) sur la carte | `has_explored_source(rarity=1)` | **Toran** | 50 | Découvrir l'exploration et les sources |
| 6 | `init_06_worker` | Créer un ouvrier (gatherer/woodcutter/miner) | `has_unit(gatherer,1)` | **Erya** | 50 | Découvrir les unités civiles |
| 7 | `init_07_collect_green` | Avoir une ressource verte dans un inventaire | `has_resource_rarity(1,1)` | **Toran** | 100 | Comprendre la chaîne logistique |
| 8 | `init_08_choose_deity` | Choisir sa divinité de tutelle | `has_deity` | — | 0 | Le pivot du jeu |

### Comment les rewards s'enchaînent

1. Quête 1 (fonder ville): le joueur a déjà les ressources de départ
2. Quête 2 (atelier): la reward donne les ressources pour construire le `rangershall` (quête 4)
3. Quête 3 (armes): les armes sont nécessaires pour recruter le scout (quête 4)
4. Quête 4 (scout): le scout permet d'explorer et de trouver des ressources vertes (quête 5)
5. Quête 5 (trouver vert): maintenant il faut aller le chercher
6. Quête 6 (ouvrier): pour pouvoir exploiter et ramener la ressource
7. Quête 7 (collecter vert): validation du cycle complet exploration -> exploitation -> logistique
8. Quête 8 (choix): le joueur a goûté aux 3 domaines et choisit sa voie

---

## 7. Exemples de Quêtes Post-Initiation

### Quêtes colorées Kael (Guerre)

```xml
<quest>
  <id>abs_kael_01</id>
  <category>absolute</category>
  <deity>kael</deity>
  <reputation>100</reputation>
  <conditions>
    <condition class="has_building"><building>guardhouse</building><count>1</count></condition>
    <condition class="has_unit"><unit_type>militia</unit_type><count>2</count></condition>
  </conditions>
  <rewards><primitive_weapons>1000</primitive_weapons></rewards>
</quest>
<!-- "Levée en masse": Construis un corps de garde et recrute 2 miliciens -->

<quest>
  <id>abs_kael_02</id>
  <category>absolute</category>
  <deity>kael</deity>
  <reputation>200</reputation>
  <unlock><condition class="quest_done"><quest>abs_kael_01</quest></condition></unlock>
  <conditions><condition class="has_killed"><count>1</count></condition></conditions>
  <rewards><food>3000</food></rewards>
</quest>
<!-- "Premier Sang": Détruis une unité ennemie ou barbare -->
```

### Quêtes colorées Erya (Artisanat)

```xml
<quest>
  <id>abs_erya_01</id>
  <category>absolute</category>
  <deity>erya</deity>
  <reputation>100</reputation>
  <conditions>
    <condition class="has_building"><building>primitiveworkshop</building><count>1</count></condition>
    <condition class="has_crafted"><resource>primitive_tools</resource><count>500</count></condition>
  </conditions>
  <rewards><wood>500</wood><stone>500</stone></rewards>
</quest>
<!-- "Les Premiers Outils": Construis un atelier et fabriques 500 outils primitifs -->
```

### Quêtes colorées Toran (Économie)

```xml
<quest>
  <id>abs_toran_01</id>
  <category>absolute</category>
  <deity>toran</deity>
  <reputation>100</reputation>
  <conditions>
    <condition class="has_building"><building>warehouse1</building><count>1</count></condition>
    <condition class="has_resource"><resource>food</resource><count>5000</count></condition>
  </conditions>
  <rewards><wood>1000</wood></rewards>
</quest>
<!-- "Le Grenier du Sage": Construis un entrepôt et accumule 5000 de nourriture -->
```

### Quête neutre

```xml
<quest>
  <id>abs_neutral_01</id>
  <category>absolute</category>
  <deity>all</deity>
  <reputation>75</reputation>
  <conditions>
    <condition class="has_population"><count>2000</count></condition>
  </conditions>
  <rewards><food>2000</food></rewards>
</quest>
<!-- "Le Village Grandissant": Atteins 2000 habitants dans ton empire -->
```

---

## 8. Nouveaux Checkers Necessaires

| Key | Classe | Paramètres | Vérifie |
|-----|--------|------------|---------|
| `has_deity` | `HasDeityChecker` | (aucun) | Le joueur a choisi sa divinité de tutelle |
| `has_explored_source` | `HasExploredSourceChecker` | `rarity` | Le joueur a découvert au moins 1 source de rareté >= rarity |
| `has_resource_rarity` | `HasResourceRarityChecker` | `rarity`, `count` | Le joueur a >= count items de rareté >= rarity dans un inventaire |
| `has_killed` | `HasKilledChecker` | `count`, `target`(opt) | Le joueur a détruit >= count unités |
| `has_crafted` | `HasCraftedChecker` | `resource`, `count` | Le joueur a craft >= count de cette ressource (cumulatif) |
| `has_explored` | `HasExploredChecker` | `count` | Le joueur a exploré >= count cases (FOV cumulé) |
| `reputation_gte` | `ReputationChecker` | `deity`, `value` | La rep du joueur auprès de deity >= value |

> **Note:** `has_killed`, `has_crafted`, `has_explored` nécessitent des **compteurs cumulatifs**.

---

## 9. Compteurs Cumulatifs — Table `player_stats`

### Table `player_stats`

| Colonne | Type | Description |
|---------|------|-------------|
| `player_id` | `VARCHAR(36) PK` | Joueur |
| `kills_total` | `INT DEFAULT 0` | Nombre d'unités détruites (cumulatif) |
| `kills_military` | `INT DEFAULT 0` | Nombre d'unités militaires détruites |
| `crafted_total` | `INT DEFAULT 0` | Nombre d'items craftés (cumulatif) |
| `explored_total` | `INT DEFAULT 0` | Nombre de cases explorées (cumulatif) |
| `buildings_built` | `INT DEFAULT 0` | Nombre de bâtiments construits |
| `cities_founded` | `INT DEFAULT 0` | Nombre de villes fondées |
| `cities_captured` | `INT DEFAULT 0` | Nombre de villes capturées |
| `resources_traded` | `INT DEFAULT 0` | Quantité totale de ressources échangées |
| `territory_max` | `INT DEFAULT 0` | Record de cases contrôlées |

### Points d'injection dans le code existant

- `kills_total`: dans `board_combat.php` → `deleteUnit()` (ligne 633)
- `crafted_total`: dans `board_craft.php` ou production de la ville
- `explored_total`: dans `board_fov.php` quand une nouvelle case entre dans le FOV

---

## 10. Base de Données

### Table `player_reputation`

```sql
CREATE TABLE player_reputation (
    player_id VARCHAR(36) PRIMARY KEY,
    deity ENUM('kael','erya','toran') NULL DEFAULT NULL,
    rep_kael INT NOT NULL DEFAULT 0,
    rep_erya INT NOT NULL DEFAULT 0,
    rep_toran INT NOT NULL DEFAULT 0,
    deity_chosen_at BIGINT NULL DEFAULT NULL,
    FOREIGN KEY (player_id) REFERENCES players(id) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

### Table `player_stats`

```sql
CREATE TABLE player_stats (
    player_id VARCHAR(36) PRIMARY KEY,
    kills_total INT NOT NULL DEFAULT 0,
    kills_military INT NOT NULL DEFAULT 0,
    crafted_total INT NOT NULL DEFAULT 0,
    explored_total INT NOT NULL DEFAULT 0,
    buildings_built INT NOT NULL DEFAULT 0,
    cities_founded INT NOT NULL DEFAULT 0,
    cities_captured INT NOT NULL DEFAULT 0,
    resources_traded INT NOT NULL DEFAULT 0,
    territory_max INT NOT NULL DEFAULT 0,
    FOREIGN KEY (player_id) REFERENCES players(id) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

---

## 11. Fichiers à Créer / Modifier

### Nouveaux fichiers

| Fichier | Rôle |
|---------|------|
| `common/param/rules/quests.xml` | Définitions des quêtes |
| `common/quests/checkers/*.php` | 7 nouveaux checkers |
| `www/includes/requests/choose_deity.php` | Handler: choix de divinité |
| `www/js/panels/types/quest-panel.js` | Panel: liste des quêtes |
| `www/js/panels/types/scoreboard-panel.js` | Panel: leaderboard |
| `www/js/lang/panels/dict-quest.js` | i18n des quêtes |

### Modifications de fichiers existants

| Fichier | Modification |
|---------|-------------|
| `game/turn_manager.php` | Ajouter dégradation reputation + tour d'environnement (288 TICs) |
| `common/includes/board/board_combat.php` | Incrémenter `player_stats.kills_total` dans `deleteUnit()` |
| `common/includes/board/board_fov.php` | Incrémenter `player_stats.explored_total` |
| `www/js/panels/panel.js` | Ajouter `quest: QuestPanel` dans panelMap |
| `www/js/menubar.js` | Ajouter raccourcis pour les quêtes |

---

## 12. Scoreboard / Leaderboard

### Catégories de classement

| Classement | Score | Description |
|------------|-------|-------------|
| **Faveur Divine** (global) | `rep_total` | Classement principal — somme des 3 réputations |
| **Champion de Kael** | `rep_kael` | Meilleur guerrier |
| **Champion d'Erya** | `rep_erya` | Meilleur artisan |
| **Champion de Toran** | `rep_toran` | Meilleur commerçant |
| **Dieu dominant** | somme `rep_X` de tous les fidèles du dieu X | Quel dieu "gagne" la faveur du Dieu des Dieux |

### Requêtes SQL

```sql
-- Top 50 global
SELECT p.name, pr.rep_kael + pr.rep_erya + pr.rep_toran AS rep_total,
       pr.deity
FROM player_reputation pr
JOIN players p ON p.id = pr.player_id
ORDER BY rep_total DESC
LIMIT 50;

-- Dieu dominant
SELECT pr.deity, SUM(pr.rep_kael + pr.rep_erya + pr.rep_toran) AS total
FROM player_reputation pr
WHERE pr.deity IS NOT NULL
GROUP BY pr.deity
ORDER BY total DESC;
```

---

## 13. Intégration avec l'Existant

### Système de Tutorial existant

Le système actuel de `tutorial.js` guide les nouveaux joueurs via des scénarios.

**Question ouverte:** Comment les quêtes d'initiation interagissent-elles avec le Tutorial existant ?
- Option A: Les quêtes 1-7 remplacent le Tutorial actuel
- Option B: Le Tutorial Guide les quêtes 1-7 (le système de quêtes derrière le rideau)
- Option C: Les deux fonctionnent en parallèle

### Tour d'environnement

Le "tour d'environnement" (1 jour IRL = 288 TICs) n'existe pas. Il faut:
1. Ajouter un compteur dans `turn_manager.php`
2. Déclencher la dégradation de réputation à ce moment

---

## 14. Questions Ouvertes (à trancher avant implémentation)

1. **Nom du Dieu des Dieux** — Le Chroniqueur ? L'Ancien ? Klod ?
2. **Changement de divinité** — Interdit ? Possible avec perte de 50% de rep ? Cooldown ?
3. **Nombre de quêtes actives simultanées** — 1 seule ? 3 (une par dieu) ? Illimité ?
4. **Quêtes "relative" (PvP)** — Comment gérer le ranking en temps réel ? Vérification toutes les X tours ?
5. **Récompenses uniques** — Des items spéciaux par dieu ? Des titres ? Des cosmetics ?
6. **Quêtes cycliques** — Certaines quêtes se re-proposent périodiquement (daily/weekly) ?
7. **Difficulté progressive** — Les quêtes d'un même chain deviennent-elles plus dures ? Quel scaling ?
8. **Impact du "Dieu dominant"** — Buff global pour tous les fidèles du dieu en tête ? Événement spécial ?
9. **Interaction Tutorial** — Les quêtes d'initiation remplacent ou complètent le système de Tutorial existant ?

---

## 15. Ordre d'Implémentation Suggéré

| Phase | Quoi | Prérequis |
|-------|------|-----------|
| **Phase 1** | Tables SQL (`player_reputation`, `player_stats`) + BDDObject + bases QuestManager | Nothing |
| **Phase 2** | `quests.xml` avec la chaîne d'initiation (7+1 quêtes) + intégration `turn_manager` | Phase 1 |
| **Phase 3** | Frontend: Quest Panel + Quest Tracker + i18n | Phase 2 |
| **Phase 4** | Handler `CHOOSE_DEITY` + Quête 8 (choix divinité) + update `player_reputation` | Phase 3 |
| **Phase 5** | Quêtes post-initiation (colorées + hybrides + neutres) + nouveaux checkers | Phase 4 |
| **Phase 6** | Scoreboard Panel + dégradation réputation + compteurs `player_stats` | Phase 5 |
| **Phase 7** | GM GUI Quest Editor | Quand nécessaire |

---

## Annexe: Distribution de la réputation au claim

```php
// Dans QuestManager::claimReward()
$rep = (int) $questXml->reputation;
$deities = explode(',', (string) $questXml->deity);

if ($deities === ['all']) {
    // Neutre: répartition égale
    $share = (int) round($rep / 3);
    addRep($pid, 'kael', $share);
    addRep($pid, 'erya', $share);
    addRep($pid, 'toran', $share);
} elseif (count($deities) === 1) {
    // Colorée: 100% au dieu
    addRep($pid, $deities[0], $rep);
} else {
    // Hybride: 60% chacun
    $share = (int) round($rep * 0.6);
    foreach ($deities as $d) {
        addRep($pid, $d, $share);
    }
}
```