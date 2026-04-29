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
| `game/turn_manager.php` | Ajouter: - Tour d'environnement (288 TICs) - Dégradation réputation quotidienne - Détection automatique du Sanctuaire |
| `common/includes/board/board_combat.php` | Incrémenter `player_stats.kills_total` dans `deleteUnit()` |
| `common/includes/board/board_fov.php` | Incrémenter `player_stats.explored_total` pour chaque nouvelle case explorée |
| `common/includes/board/board_city.php` | Détecter quand une ville devient Sanctuaire (bâtiment T2 construit) |

### 2.2 PHP — Request Manager

| Fichier | Modification |
|---------|--------------|
| `www/includes/request_manager.php` | Ajouter handlers `GET_QUESTS` et `CLAIM_QUEST` |

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

## 4. Détection Automatique du Sanctuaire

### Logique dans `board_city.php`

```php
// Quand un bâtiment T2 est construit
public function onBuildingConstructed(City $city, Building $building): void {
    if ($building->tier !== 2) return;

    $player = $city->getOwner();
    $reputation = $player->getReputation();

    // Si le joueur n'a pas encore de Sanctuaire
    if ($reputation->sanctuary_city_id === null) {
        $reputation->sanctuary_city_id = $city->id;
        $this->setSanctuaryDeities($player, $city);
        $reputation->save();
        notifyPlayer('__SANCTUARY_ESTABLISHED__', $player->id);
    }
}

// Déterminer les dieux disponibles selon les bâtiments T2
private function setSanctuaryDeities(Player $player, City $city): void {
    $t2Buildings = $city->getBuildings()->filter(fn($b) => $b->tier === 2);
    $hasCasern = $t2Buildings->any(fn($b) => $b->type === 'guardhouse');
    $hasWorkshop = $t2Buildings->any(fn($b) => $b->type === 'workshop');
    $hasMarket = $t2Buildings->any(fn($b) => $b->type === 'market');

    $reputation = $player->getReputation();
    $reputation->deity_kael = $hasCasern;
    $reputation->deity_erya = $hasWorkshop;
    $reputation->deity_toran = $hasMarket;
    $reputation->deity_count = (int)$hasCasern + (int)$hasWorkshop + (int)$hasMarket;
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

### 7.3 Sanctuaire et transfert de ville

Quand une ville Sanctuaire est capturée:
- Le nouveau propriétaire peut-il en faire son Sanctuaire ? (Oui)
- L'ancien propriétaire perd-il immédiatement sa connexion divine ? (Oui)
- La réputation est-elle conservée ? (Oui, elle estattachée au joueur, pas à la ville)

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