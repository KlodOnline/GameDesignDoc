# Le Monde


## Types de Terrains
21 types de terrains implémentés : Océan, plaine, forêt, montagnes, désert, toundra, jungle, savane, marais, rivière, banquise, côte, rivage (foreshore), et leurs variantes avec collines. Voir `lands.xml` pour la liste complète.

## Système Climatique
Zones de température (chaude, tempérée, froide, gelée) basées sur la latitude :
- Cercles polaires : 1/14 de la hauteur totale
- Tropiques : à 1/8 de l'équateur
- Zones gelées limitées à 4 cases des bords nord/sud

## Rivières
Générées depuis les montagnes/collines humides, courent jusqu'à l'océan. Minimum 15 hexagones de longueur, espacées de 25 hexagones minimum entre sources.

## Côtes et Îles
Zones littorales avec côtes et rivages (foreshore). Chaque île garantit au moins un accès foreshore.

## Grille de référence
Le monde se joue sur une carte **cylindrique** composée de cases **hexagonales** (320 colonnes × 250 rangées). Autrement dit, tout ce qui sort à gauche revient par la droite, et vice versa. Les hexagones présentent l'avantage d'équilibrer les vitesses et distances de déplacement dans toutes les directions.

## Dimensions
Valeurs actuelles (config.ini) :
- Monde : **320×250** hexagones (80 000 cases)
- Rayon d'influence max d'une ville : **3** cases
- Inventaire de base d'une ville : **16** slots
- Protection nouveau joueur : **2 semaines** (1 209 600 secondes / 4 032 tours)
- Limite d'inactivité : **1 mois** (2 592 000 secondes)
- Stack max d'unités par case : **4**

## Génération procédurale
La carte est générée de façon procédurale via `WorldGenerator` avec un pipeline en plusieurs étapes :

### Pipeline de génération
1. **`clearWorld()`** — Reset complet en plaines
2. **`createTectonicPlates()`** — Simulation de plaques tectoniques pour continents, montagnes et océans
3. **`lessBoring()`** — Ajout de variété (montagnes, marais, forêts) dans les zones uniformes
4. **`humidity()`** — Simulation des vents dominants et humidité pour placer les forêts
5. **`latitudeClimate()`** — Application des zones climatiques (savane, toundra, banquise)
6. **`rivers()`** — Génération des rivières depuis les montagnes
7. **`desertsCoasts()`** — Finalisation des déserts et lignes de côte
8. **`foreshores()`** — Ajout des rivages avec garantie d'accès par île

## Aménagement du territoire
Les unités ouvrières peuvent modifier le territoire :
- **Déforestation** (`CHOP_WOOD`) : Forêt/Jungle → Plaine (durée variable selon le terrain)
- **Drainage** (`DRAIN_SWAMP`) : Marais → Plaine (4 tours)
- **Irrigation** (`IRRIGATE`) : Plaine/Savane irriguée (+1 production nourriture), nécessite adjacency à rivière/océan/irrigation existante
- **Piste** (`MOVE_TRACK`) : 2000 points de route en terre, sans coût
- **Route pavée** (`MOVE_ROAD`) : 4000 points, coûte 200 pierres
- **Pont** (`MOVE_BRIDGE`) : Traverse les rivières, coûte 400 pierres

### Usure des infrastructures
- **Routes** : +10/tour si entretenues (ville/unité présente), -1/tour si abandonnées. Se dégradent jusqu'à 0.
- **Irrigation** : +1/tour si exploitée (producteur de nourriture actif), -1/tour sinon. À 0, le terrain peut redevenir forêt/marais (20% de chance).

## Vie du territoire
Implémenté dans `worldEvolution()` (chaque tour) :
- Les routes se dégradent ou sont entretenues selon la présence de villes/unités
- L'irrigation non entretenue se dégrade et peut transformer le terrain
- Les hexagones dont le propriétaire n'existe plus sont réassignés aux "Barbarians"