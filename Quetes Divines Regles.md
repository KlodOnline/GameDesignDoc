# Quêtes Divines — Règles

> Détail des mécaniques et règles de jeu
> Dernière mise à jour: 2026-04-29

---

## 1. Le Système de Réputation

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

### Dégradation dans le temps

La réputation se dégrade **à chaque tour d'environnement** (1 fois par jour IRL, soit tous les 288 TICs) :

```
dégradation_quotidienne = réputation_actuelle * TAUX_DEGRADATION
```

| Paramètre | Valeur |
|-----------|--------|
| `TAUX_DEGRADATION` | 0.5% par jour IRL (~15% par mois) |
| `REP_PLANCHER` | 0 (minimum) |
| `REP_PLAFOND` | 100 000 (softcap ; au-delà, dégradation accélérée) |

> **Tour d'environnement:** 288 TICs = 1 jour IRL. Ce tour doit être implémenté dans `turn_manager.php`.

---

## 2. Le Sanctuaire Divin

### Définition

Le **Sanctuaire** est une ville du joueur désignée comme sa Capitale Divine. C'est le lieu sacré où le joueur ancre sa connexion avec les dieux.

### Condition pour être un Sanctuaire

Une ville devient un Sanctuaire si elle contient **au moins 1 bâtiment T2**. Tout bâtiment T2 peut être construit — seul le premier détermine le Sanctuaire.

### Bâtiments T2 et Dieux

| Bâtiment T2 | Dieu associé |
|-------------|--------------|
| Caserne T2 | **Kael** (Guerre) |
| Atelier T2 | **Erya** (Artisanat) |
| Marché T2 | **Toran** (Économie) |

### Déclaration de foi

Le joueur peut déclarer son allégeance aux dieux en fonction des bâtiments T2 présents dans son Sanctuaire :

| Bâtiments T2 présents | Dieux disponibles | Ratio de réputation |
|-----------------------|-------------------|---------------------|
| Caserne seulement | Kael uniquement | 100% pour Kael |
| Atelier seulement | Erya uniquement | 100% pour Erya |
| Marché seulement | Toran uniquement | 100% pour Toran |
| Caserne + Atelier | Kael + Erya | 60% chacun |
| Caserne + Marché | Kael + Toran | 60% chacun |
| Atelier + Marché | Erya + Toran | 60% chacun |
| Caserne + Atelier + Marché | Kael + Erya + Toran | 33% chacun |

### Changer de dieux

Le joueur peut modifier sa déclaration de dieux :
- **Ajouter un dieu:** Construire le bâtiment T2 correspondant dans le Sanctuaire
- **Retirer un dieu:** Détruire le bâtiment T2 correspondant (la réputation pour ce dieu se fige)

### Perte du Sanctuaire

Si la ville Sanctuaire est **capturée** ou **rasée** :
- Le lien avec les dieux est rompu
- Malus de moral important
- Le joueur doit reconstruire un nouveau Sanctuaire dans une autre ville (avec bâtiment T2) pour renouer avec les dieux

---

## 3. Types de Quêtes

### Catégories

| Catégorie | Type | Description |
|-----------|------|-------------|
| `initiation` | PvE | Tutoriel — 7 étapes universelles |
| `absolute` | PvE | Quêtes de divinité — colorées ou hybrides |
| `relative` | PvP | Compétition — classement entre joueurs |

### Sous-types de quêtes `absolute`

| Sous-type | Tag XML | Dieux impliqués | Gain réputation |
|-----------|---------|-----------------|-----------------|
| Neutre | `<deity>all</deity>` | Tous | 33% chacun |
| Colorée Kael | `<deity>kael</deity>` | Kael seul | 100% pour Kael |
| Colorée Erya | `<deity>erya</deity>` | Erya seul | 100% pour Erya |
| Colorée Toran | `<deity>toran</deity>` | Toran seul | 100% pour Toran |
| Hybride Kael+Erya | `<deity>kael,erya</deity>` | Kael + Erya | 60% chacun |
| Hybride Kael+Toran | `<deity>kael,toran</deity>` | Kael + Toran | 60% chacun |
| Hybride Erya+Toran | `<deity>erya,toran</deity>` | Erya + Toran | 60% chacun |

---

## 4. La Chaîne d'Initiation (Quêtes 1-7)

Ces quêtes apprennent les bases du jeu sans engagement divin. Elles sont identiques pour tous les joueurs.

| # | ID | Objectif | Checker | Dieu | Reward rep |
|---|-----|----------|---------|------|------------|
| 1 | `init_01_settle` | Fondé ta première ville | `has_city(count=1)` | Neutre | 50 |
| 2 | `init_02_workshop` | Construire un Atelier Primitif | `has_building(primitiveworkshop,1)` | Erya | 50 |
| 3 | `init_03_craft_weapons` | Crafter des Armes Primitives (500) | `has_resource(primitive_weapons,500)` | Erya | 50 |
| 4 | `init_04_scout` | Recruter un Éclaireur | `has_unit(scout,1)` | Kael | 50 |
| 5 | `init_05_find_green` | Trouver une ressource verte (rareté ≥1) | `has_explored_source(rarity=1)` | Toran | 50 |
| 6 | `init_06_worker` | Créer un ouvrier | `has_unit(gatherer,1)` | Erya | 50 |
| 7 | `init_07_collect_green` | Avoir une ressource verte en inventaire | `has_resource_rarity(1,1)` | Toran | 100 |

> **Fin de l'initiation:** Après la quête 7, le joueur a découvert les 3 styles. Il est prêt à construire son Sanctuaire et choisir ses dieux.

---

## 5. Nouveaux Checkers

| Key | Vérifie |
|-----|---------|
| `has_deity` | Le joueur a choisi sa(ses) divinité(s) via son Sanctuaire |
| `has_sanctuary` | Le joueur a une ville Sanctuaire (avec ≥1 bâtiment T2) |
| `has_sanctuary_building` | Le Sanctuaire contient un type de bâtiment T2 précis |
| `has_explored_source` | Le joueur a découvert une source de rareté donnée |
| `has_resource_rarity` | Le joueur a ≥N items de rareté donnée en inventaire |
| `has_killed` | Le joueur a détruit ≥N unités (cumulatif) |
| `has_crafted` | Le joueur a crafté ≥N d'une ressource (cumulatif) |
| `has_explored` | Le joueur a exploré ≥N cases (cumulatif) |
| `reputation_gte` | La réputation du joueur pour un dieu ≥ valeur |

---

## 6. Compteurs Cumulatifs (player_stats)

Ces compteurs trackent les actions du joueur dans le temps pour les quêtes.

| Colonne | Description |
|---------|-------------|
| `kills_total` | Unités détruites (cumulatif) |
| `kills_military` | Unités militaires détruites |
| `crafted_total` | Items craftés (cumulatif) |
| `explored_total` | Cases explorées (cumulatif) |
| `buildings_built` | Bâtiments construits |
| `cities_founded` | Villes fondées |
| `cities_captured` | Villes capturées |
| `resources_traded` | Ressources échangées (quantité) |
| `territory_max` | Record de cases contrôlées |

### Points d'injection dans le code existant

| Compteur | Emplacement | Méthode |
|----------|-------------|---------|
| `kills_total` | `board_combat.php` → `deleteUnit()` | Après destruction |
| `crafted_total` | Production de la ville | Après craft |
| `explored_total` | `board_fov.php` | Nouvelle case dans FOV |

---

## 7. Tables SQL

### player_reputation

```sql
CREATE TABLE player_reputation (
    player_id VARCHAR(36) PRIMARY KEY,
    deity_count INT NOT NULL DEFAULT 0,  -- 1, 2 ou 3 dieux vénérés
    rep_kael INT NOT NULL DEFAULT 0,
    rep_erya INT NOT NULL DEFAULT 0,
    rep_toran INT NOT NULL DEFAULT 0,
    sanctuary_city_id VARCHAR(36) NULL,  -- FK vers la ville Sanctuaire
    deity_kael BOOLEAN DEFAULT FALSE,
    deity_erya BOOLEAN DEFAULT FALSE,
    deity_toran BOOLEAN DEFAULT FALSE,
    FOREIGN KEY (player_id) REFERENCES players(id) ON DELETE CASCADE,
    FOREIGN KEY (sanctuary_city_id) REFERENCES cities(id) ON DELETE SET NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

### player_stats

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

## 8. Scoreboard / Leaderboard

### Classements

| Classement | Score | Description |
|------------|-------|-------------|
| **Faveur Divine** (global) | `rep_total` | Somme des 3 réputation |
| **Champion de Kael** | `rep_kael` | Meilleur guerrier |
| **Champion d'Erya** | `rep_erya` | Meilleur artisan |
| **Champion de Toran** | `rep_toran` | Meilleur commerçant |
| **Dieu Dominant** | Somme `rep_X` des fidèles | Quel dieu mène |

### Requêtes SQL

```sql
-- Top 50 global
SELECT p.name, pr.rep_kael + pr.rep_erya + pr.rep_toran AS rep_total
FROM player_reputation pr
JOIN players p ON p.id = pr.player_id
ORDER BY rep_total DESC LIMIT 50;

-- Top par dieu
SELECT p.name, pr.rep_kael FROM player_reputation pr
JOIN players p ON p.id = pr.player_id
WHERE pr.deity_kael = TRUE
ORDER BY pr.rep_kael DESC LIMIT 50;

-- Dieu dominant
SELECT
    (SELECT SUM(rep_kael) FROM player_reputation WHERE deity_kael=TRUE) +
    (SELECT SUM(rep_erya) FROM player_reputation WHERE deity_erya=TRUE) +
    (SELECT SUM(rep_toran) FROM player_reputation WHERE deity_toran=TRUE) AS total
GROUP BY deity;
```

---

## 9. Distribution de Réputation au Claim

```php
// QuestManager::distributeReputation()
$rep = (int) $quest->reputation;
$deities = explode(',', $quest->deity);

if ($deities === ['all']) {
    // Neutre: 33% chacun
    $share = round($rep / 3);
    addRep($pid, 'kael', $share);
    addRep($pid, 'erya', $share);
    addRep($pid, 'toran', $share);
} elseif (count($deities) === 1) {
    // Colorée: 100%
    addRep($pid, $deities[0], $rep);
} else {
    // Hybride: 60% chacun
    $share = round($rep * 0.6);
    foreach ($deities as $d) {
        addRep($pid, $d, $share);
    }
}
```

---

## 10. Questions Ouvertes

1. **Nom du Dieu des Dieux** — Le Chroniqueur ? L'Ancien ? Klod ?
2. **Changement de divinité** — Cooldown ? Perte de réputation ?
3. **Nombre de quêtes actives simultanées** — 1 seule ? 3 ? Illimité ?
4. **Quêtes "relative" (PvP)** — Ranking temps réel ou par tour ?
5. **Récompenses uniques** — Items spéciaux par dieu ? Titres ? Cosmetics ?
6. **Quêtes cycliques** — daily/weekly ?
7. **Difficulté progressive** — Scaling des récompenses ?
8. **Impact "Dieu dominant"** — Buff global pour les fidèles du dieu en tête ?
9. **Sanctuaire unique ou multiple** — Une seule ville peut-elle être Sanctuaire ?