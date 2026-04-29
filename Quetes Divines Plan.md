# Quêtes Divines — Plan d'Implémentation

> Guide technique et organisation du code
> Dernière mise à jour: 2026-04-29

---

## 1. Fichiers à Créer

### 1.1 Base de données

| Fichier | Description |
|---------|-------------|
| `setup/migrations/YYYY-MM-DD_add_quest_tables.sql` | Tables `player_reputation`, `player_stats` |

### 1.2 Règles XML

| Fichier | Description |
|---------|-------------|
| `common/param/rules/quests.xml` | Définitions de toutes les quêtes |

### 1.3 PHP — Quest System

| Fichier | Description |
|---------|-------------|
| `common/quests/quest_manager.php` | Gestionnaire central des quêtes |
| `common/quests/checkers/has_deity_checker.php` | Vérifie allégeance divine |
| `common/quests/checkers/has_sanctuary_checker.php` | Vérifie existence Sanctuaire |
| `common/quests/checkers/has_sanctuary_building_checker.php` | Vérifie bâtiment T2 dans Sanctuaire |
| `common/quests/checkers/has_explored_source_checker.php` | Source découverte par rareté |
| `common/quests/checkers/has_resource_rarity_checker.php` | Item par rareté en inventaire |
| `common/quests/checkers/has_killed_checker.php` | Compteur de kills |
| `common/quests/checkers/has_crafted_checker.php` | Compteur de crafts |
| `common/quests/checkers/has_explored_checker.php` | Compteur d'exploration |
| `common/quests/checkers/reputation_checker.php` | Seuil de réputation |

### 1.4 PHP — SQL Objects

| Fichier | Description |
|---------|-------------|
| `common/includes/sql_objects/player_reputation.php` | BDDObject pour reputation |
| `common/includes/sql_objects/player_stats.php` | BDDObject pour stats |

### 1.5 PHP — Handlers

| Fichier | Description |
|---------|-------------|
| `www/includes/requests/get_quests.php` | Récupère les quêtes disponibles |
| `www/includes/requests/claim_quest.php` | Claim la récompense d'une quête |
| `www/includes/requests/designate_sanctuary.php` | Désigne une ville comme Sanctuaire + choisit les dieux |
| `www/includes/requests/modify_sanctuary_deities.php` | Ajoute/retire un dieu de la protection (-50% rep si retrait) |

### 1.6 JavaScript — Panels

| Fichier | Description |
|---------|-------------|
| `www/js/panels/types/quest-panel.js` | Panel principal des quêtes |
| `www/js/panels/types/scoreboard-panel.js` | Panel du leaderboard |

### 1.7 JavaScript — Langue

| Fichier | Description |
|---------|-------------|
| `www/js/lang/panels/dict-quest.js` | Traductions du panel de quêtes |

### 1.8 CSS

| Fichier | Description |
|---------|-------------|
| `www/css/2-components/quest-panel.css` | Styles du panel de quêtes |
| `www/css/2-components/scoreboard-panel.css` | Styles du leaderboard |

---

## 2. Fichiers à Modifier

### 2.1 PHP — Core

| Fichier | Modification |
|---------|--------------|
| `game/turn_manager.php` | Ajouter: - Tour d'environnement (288 TICs) - Dégradation réputation quotidienne |
| `common/includes/board/board_combat.php` | Incrémenter `player_stats.kills_total` dans `deleteUnit()` |
| `common/includes/board/board_fov.php` | Incrémenter `player_stats.explored_total` pour chaque nouvelle case explorée |
| `common/includes/board/board_city.php` | Ajouter `designateSanctuary()`, `modifyDeityProtection()`, `removeDeityProtection()` (avec -50% rep) |

### 2.2 PHP — Request Manager

| Fichier | Modification |
|---------|--------------|
| `www/includes/request_manager.php` | Ajouter handlers `GET_QUESTS`, `CLAIM_QUEST`, `DESIGNATE_SANCTUARY`, `MODIFY_SANCTUARY_DEITIES` |

### 2.3 JavaScript — Panels

| Fichier | Modification |
|---------|--------------|
| `www/js/panels/panel.js` | Ajouter `quest: QuestPanel` et `scoreboard: ScoreboardPanel` dans `panelMap` |
| `www/js/menubar.js` | Ajouter raccourcis clavier (ex: `Q` pour quêtes, `L` pour leaderboard) |

---

## 3. Structure du quests.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<quests>
    <!-- ==================== INITIATION ==================== -->
    <quest>
        <id>init_01_settle</id>
        <chain>initiation</chain>
        <order>1</order>
        <category>initiation</category>
        <deity>all</deity>
        <reputation>50</reputation>
        <conditions>
            <condition class="has_city"><count>1</count></condition>
        </conditions>
        <rewards/>
    </quest>

    <quest>
        <id>init_02_workshop</id>
        <chain>initiation</chain>
        <order>2</order>
        <category>initiation</category>
        <deity>erya</deity>
        <reputation>50</reputation>
        <unlock>
            <condition class="quest_done"><quest>init_01_settle</quest></condition>
        </unlock>
        <conditions>
            <condition class="has_building"><building>primitiveworkshop</building><count>1</count></condition>
        </conditions>
        <rewards>
            <resource id="wood">100</resource>
            <resource id="stone">200</resource>
        </rewards>
    </quest>

    <!-- ... quêtes 3-7 ... -->

    <!-- ==================== KAEL (GUERRE) ==================== -->
    <quest>
        <id>abs_kael_01</id>
        <chain>kael</chain>
        <order>1</order>
        <category>absolute</category>
        <deity>kael</deity>
        <reputation>100</reputation>
        <unlock>
            <condition class="has_sanctuary_building"><building>guardhouse</building></condition>
            <condition class="has_deity"><deity>kael</deity></condition>
        </unlock>
        <conditions>
            <condition class="has_building"><building>guardhouse</building><count>1</count></condition>
            <condition class="has_unit"><unit_type>militia</unit_type><count>2</count></condition>
        </conditions>
        <rewards>
            <resource id="primitive_weapons">1000</resource>
        </rewards>
    </quest>

    <!-- ==================== ERYA (ARTISANAT) ==================== -->

    <!-- ==================== TORAN (ÉCONOMIE) ==================== -->

    <!-- ==================== HYBRIDES ==================== -->

    <!-- ==================== NEUTRES ==================== -->

</quests>
```

---

## 4. Désignation du Sanctuaire

### Interaction via UI

1. Quand un joueur construit un **bâtiment T2** dans une ville, une **icône divine** apparaît à côté du nom de la ville
2. Le joueur peut cliquer sur cette icône pour **désigner** cette ville comme son Sanctuaire
3. Après désignation, une interface permet de choisir **1, 2 ou 3 dieux** à protéger (selon les bâtiments T2 présents)

### Logique dans `board_city.php` et nouveau handler

```php
// Quand un joueur clique sur l'icône divine pour désigner son Sanctuaire
public function designateSanctuary(City $city, array $chosenDeities): void {
    $player = $city->getOwner();
    $reputation = $player->getReputation();

    // Vérifier que la ville a au moins 1 T2
    $t2Buildings = $city->getBuildings()->filter(fn($b) => $b->tier === 2);
    if ($t2Buildings->isEmpty()) {
        throw new Exception('__ERROR_NO_T2_BUILDING__');
    }

    // Vérifier que les dieux choisis sont valides (bâtiments correspondants existent)
    $availableDeities = $this->getAvailableDeities($city);
    foreach ($chosenDeities as $deity) {
        if (!in_array($deity, $availableDeities)) {
            throw new Exception('__ERROR_INVALID_DEITY__');
        }
    }

    // Sauvegarder
    $reputation->sanctuary_city_id = $city->id;
    $reputation->deity_kael = in_array('kael', $chosenDeities);
    $reputation->deity_erya = in_array('erya', $chosenDeities);
    $reputation->deity_toran = in_array('toran', $chosenDeities);
    $reputation->deity_count = count($chosenDeities);
    $reputation->save();

    notifyPlayer('__SANCTUARY_DESIGNATED__', $player->id);
}

// Retourne les dieux disponibles selon les bâtiments T2 de la ville
private function getAvailableDeities(City $city): array {
    $t2Buildings = $city->getBuildings()->filter(fn($b) => $b->tier === 2);
    $deities = [];
    // NOTE: Les types de bâtiments ci-dessous sont des placeholders.
    // TODO: Remplacer par les IDs réels des bâtiments T2 les plus coûteux/significatifs de chaque arbre.
    if ($t2Buildings->any(fn($b) => $b->type === 'guardhouse')) $deities[] = 'kael';
    if ($t2Buildings->any(fn($b) => $b->type === 'workshop')) $deities[] = 'erya';
    if ($t2Buildings->any(fn($b) => $b->type === 'market')) $deities[] = 'toran';
    return $deities;
}
```

### Nouveau handler `DESIGNATE_SANCTUARY`

```php
// www/includes/requests/designate_sanctuary.php
class DesignateSanctuary extends BaseRequest {
    public function execute(array $post_data): array {
        $city_id = $this->request_manager->itemIdCleaner($post_data['city_id'] ?? '');
        $deities = $post_data['deities'] ?? []; // ex: ['kael', 'erya']

        if (!$city_id || empty($deities)) return [];
        if (count($deities) > 3) return []; // Max 3 dieux

        $this->request_manager->loadCurrentPlayerIfNeeded();
        $this->board->loadCities();

        $city = $this->board->getCityById($city_id);
        if ($city === null || $city->player_id !== META_ID) return [];

        $this->board->designateSanctuary($city, $deities);
        $this->request_manager->saveBoardCollection(['City']);

        return ['success' => true, 'sanctuary_city_id' => $city_id];
    }
}
```

---

## 5. Exemples de Quêtes par Type

### 5.1 Quêtes Colorées Kael (Guerre)

```xml
<quest>
    <id>abs_kael_01</id>
    <chain>kael</chain>
    <category>absolute</category>
    <deity>kael</deity>
    <reputation>100</reputation>
    <conditions>
        <condition class="has_building"><building>guardhouse</building><count>1</count></condition>
        <condition class="has_unit"><unit_type>militia</unit_type><count>2</count></condition>
    </conditions>
    <rewards>
        <resource id="primitive_weapons">1000</resource>
    </rewards>
</quest>

<quest>
    <id>abs_kael_02</id>
    <chain>kael</chain>
    <category>absolute</category>
    <deity>kael</deity>
    <reputation>200</reputation>
    <unlock>
        <condition class="quest_done"><quest>abs_kael_01</quest></condition>
    </unlock>
    <conditions>
        <condition class="has_killed"><count>1</count></condition>
    </conditions>
    <rewards>
        <resource id="food">3000</resource>
    </rewards>
</quest>
```

### 5.2 Quêtes Hybrides Kael+Erya

```xml
<quest>
    <id>abs_hybrid_ke_01</id>
    <chain>kael</chain>
    <category>absolute</category>
    <deity>kael,erya</deity>
    <reputation>250</reputation>
    <unlock>
        <condition class="quest_done"><quest>abs_kael_01</quest></condition>
        <condition class="quest_done"><quest>abs_erya_01</quest></condition>
    </unlock>
    <conditions>
        <condition class="has_crafted"><resource>primitive_weapons</resource><count>2000</count></condition>
        <condition class="has_unit"><unit_type>militia</unit_type><count>4</count></condition>
    </conditions>
    <rewards>
        <resource id="iron_ore">200</resource>
    </rewards>
</quest>
```

### 5.3 Quêtes Neutres

```xml
<quest>
    <id>abs_neutral_01</id>
    <chain>common</chain>
    <category>absolute</category>
    <deity>all</deity>
    <reputation>75</reputation>
    <conditions>
        <condition class="has_population"><count>2000</count></condition>
    </conditions>
    <rewards>
        <resource id="food">2000</resource>
    </rewards>
</quest>
```

---

## 6. Ordre d'Implémentation

### Phase 1: Fondations
- [ ] Migration SQL (`player_reputation`, `player_stats`)
- [ ] BDDObject pour `player_reputation` et `player_stats`
- [ ] QuestManager de base avec `quests.xml`

### Phase 2: Initiation
- [ ] Quêtes 1-7 d'initiation dans `quests.xml`
- [ ] Checkers de base (`has_city`, `has_building`, `has_unit`, `has_resource`)
- [ ] Handler `GET_QUESTS`

### Phase 3: Sanctuaire
- [ ] Détection automatique du Sanctuaire dans `board_city.php`
- [ ] Mise à jour de `player_reputation` lors de la détection
- [ ] Propagation de la réputation aux quêtes disponibles

### Phase 4: Post-Initiation
- [ ] Quêtes colorées (1 par dieu)
- [ ] Quêtes hybrides
- [ ] Quêtes neutres
- [ ] Nouveaux checkers (`has_killed`, `has_crafted`, `has_explored`)

### Phase 5: Frontend
- [ ] Quest Panel (`quest-panel.js`)
- [ ] Scoreboard Panel (`scoreboard-panel.js`)
- [ ] i18n pour les 5 langues

### Phase 6: Comptage & Dégradation
- [ ] Instrumentation de `board_combat.php` (kills)
- [ ] Instrumentation de `board_fov.php` (exploration)
- [ ] Tour d'environnement dans `turn_manager.php`
- [ ] Dégradation quotidienne de la réputation

### Phase 7: Polish
- [ ] Handler `CLAIM_QUEST` avec animations
- [ ] GM Quest Editor (quand nécessaire)

---

## 7. Points d'Attention

### 7.1 Instrumentation du code existant

Lors de l'ajout des compteurs (`kills_total`, `explored_total`, etc.), attention à:
- Ne pas créer de effets de bord dans le flux normal du jeu
- Utiliser des transactions pour les mises à jour
- Prévoir le cas où `player_stats` n'existe pas encore (migration)

### 7.2 Tour d'environnement

Le tour d'environnement (288 TICs = 1 jour) n'existe pas encore. Il faut:
1. Ajouter un champ `last_environment_turn` dans `world_info`
2. Dans `turn_manager.php`, vérifier si `current_turn - last_environment_turn >= 288`
3. Si oui, exécuter la dégradation de réputation pour tous les joueurs

### 7.3 Modification des dieux et perte du Sanctuaire

**Modifier les dieux protégés (via UI):**
- Le joueur ouvre l'interface du Sanctuaire et modifie sa sélection de dieux (1 à 3)
- **Retirer un dieu:** Appel à `removeDeityProtection($deity)` → -50% de réputation pour ce dieu
- **Ajouter un dieu:** Vérifier que le bâtiment T2 correspondant existe dans le Sanctuaire
- **Retirer tous les dieux:** Appel à `clearAllDeities()` → la ville perd son statut de Sanctuaire

**Perte du Sanctuaire par capture/rasement:**
- Appel à `onSanctuaryLost()`:
  - `sanctuary_city_id` → NULL
  - `deity_kael/erya/toran` → FALSE
  - `deity_count` → 0
  - **Perte de 75% de réputation** dans chaque dieu précédemment protégé
- Malus de moral appliqué
- La réputation est conservée (attachée au joueur, pas à la ville)

**Récupération:**
- Le joueur peut recapturer la ville et la re-désigner comme Sanctuaire
- Ou désigner une autre ville (avec T2) comme nouveau Sanctuaire

---

## 8. Annexe: Checklist avant merge

- [ ] Migration SQL testée sur base propre
- [ ] Toutes les quêtes XML validées (schema ou parser)
- [ ] Checkers testés individuellement
- [ ] Détection Sanctuaire testée (construire T2 → devient-on Sanctuaire ?)
- [ ] Frontend: panel s'ouvre sans erreur console
- [ ] i18n: toutes les touches traduites en FR, EN, ES, ZH, AR
- [ ] Linting PHP et JS passé
- [ ] Tests unitaires pour les nouveaux checkers