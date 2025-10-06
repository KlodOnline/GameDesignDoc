____
# Unités
Les unités sont le cœur du gameplay, puis qu'elle permettent au joueur d'explorer, de construire, de récolter, de faire la guerre.
## Informations
Pour accéder aux informations d'une unité, _sélectionnez là_ puis cliquez sur l'icône ![[Pasted image 20251006114527.png]] ou bien utilisez l'un des raccourcis claviers pour accéder directement aux onglets suivants (**si** votre unité dispose d'un tel onglet !) :
 - "**G**" (pour informations **G**énérales)
 - "**I**" (pour **I**nventaire)
 - "**P**" (pour **P**roduction)

## 

## Types

## Caractéristiques
## Mécaniques de jeu
## Prérequis
## Listing




## Type
Il existe différent type d'unités. Elle sont de différentes catégories :
 - Combat
 - Transport
 - Ouvrière
 - Navale

## Moral des unités
C'est l'équivalent de la vie des unités. échelle de 0 à 100. Lorsque l'unité tombe à 0 elle disparait.
### Conditions
#### Perte
 - Dans le désert ou la banquise : -1pt/tour
 - Au combat, suivant les dommages subits
 - Si pas de nourriture sur soi : -1pt/tour mais max 50/100 (=on doit chasser, on est en disette, mais on ne meure pas)
 - (éventuellement ?) Trêve nocturne en dehors de ses frontières ou des alliées : -25 points (mais max 1/100, on ne meure pas du mal du pays) (à voir peut être mauvaise idée)
#### Gain
 - Moral entre 1 et 50 : 
	 - +1pt/tour partout sauf en banquise ou désert
 - Moral entre 50 et 100 : 
	 - +1pt/tour si nourriture dans l'inventaire, ou dans une ville qui a de la nourriture en stock
		 - entre 1 et 10 unités de nourriture consommée / tour suivant le type d'unité (échelle : 1000hab=100 nourriture)
 - Première victoire du jour = +25 moral (cap 100) (à voir, si c'est facile à mettre en place ou non)

## Combat
Les principes de combat sont assez simples. Les unités ont des scores d'attaque et de défense, les terrains ont un score de combat. Le calcul devient :
	(Score Attaque + Score terrain) - (Score Defense + Score terrain) = Resultat
Les Attaque/Defense vont de 1 à 5, les bonus du terrain, de -1 à 2. Il peut y avoir des bonus de fortification en cas de combat depuis une ville ou un fortin (+1 à +3 max en fonction du niveau)
Donc en théorie un Résultat peut être de -10 à +10.
Un résultat positif signifie une attaque réussie, et le défenseur perd (Résultat)x10 moral.
Un résultat négatif signifie une attaque échouée, et l'attaquant perd (Résultat)x10 moral.
Le moral de base est 100. Une unité peux mourir en un combat dans les cas extrêmes.
## Mouvement
Les unités peuvent être groupées en stack, pour ensuite réaliser un déplacement simultané. Sur le jeu, on autorise une stack de 3 unités maximum.

Les unités ont un score de déplacement de **1 à 4** (Fast/Medium/Slow/VerySlow).
Les terrains ont un score également, de **2 à 5** (Roaded/Easy/Medium/Hard/VeryHard)

L'addition du score de l'unité et du score de terrain donne le nombre de tour nécessaire au passage à la case suivante. 
Le score final doit donc toujours être compris entre 3 et 9. (15min à 45min pour une case).

Cela devra éventuellement être révisé en fonction du retour des joueurs, en conservant la durée actuellement des TIC mais avec des scores comme 
 - Unité (0.5, 1.5, 2.5, 3.5) / Sols (0.5, 1.5, 2.5, 3.5, 4.5) => échelle de 1 à 8 (5min à 40min)
 - Unité (0.5, 1, 1.5, 2) / Sols (0.5, 1, 1.5, 2, 2.5) => échelle de 1 à 5 (5min à 25min) (arrondi sup.)

La nuit, tout les ordres de mouvements sont figés, de 22h00 à 7h00, même si le jeu fonctionne et est accessible. Cela permet d'éviter la victoire automatique des no-life.

Les unités terrestre ne peuvent aller sur l'eau, sauf les rivieres. Si une unité terrestre est sur une rivière elle ne peut que la quitter. Autrement dit elle n'ont que le droit de traverser les rivières. 
Les unités navales ne peuvent aller sur la terre, sauf les villes qui sont considéré comme des ports dès qu'elles sont en bord d’océan ou de rivière. Ce n'est pas très précis, mais cela apportera beaucoup au gameplay.

## Inventaire
Les unités disposent d'un inventaire avec une place exprimée en slots, et va de 0 à 6 slots.
Lorsqu'elle meurent, elles laissent sur place un loot, qui se degrade avec le temps.
## FOV
Le **_FOV_** c'est le "field of view". C'est le nombre de cases (rayon) que voit une unité. Il y a un score en fonction de l'unité, puis un bonus en fonction du terrain. Valeurs classiques :
 - Unités de base : 1
 - Unités de reconnaissances ou d'observation: 2
 - Terrain de base : +0
 - Foret, Jungle : -1
 - Collines : +1
 - Villes : 1 / niveau de ville (Cf. villes), max 4 ou 5

## Campement
La plupart des unités auront un ordre "camper"/"fortifier" etc. en fonction de l'unité, permettant de la "figer" sur place et d'activer quelque chose de spécial comme:
 - camp de mineur
 - tour d'observation
 - camp fortifié
 - ...

## Look
prévoir le tour de l'unité en fonction :
	selectionnée ou non
	rareté
	statut diplomatique
Ou alors :
	tour unité = selection
	Border epaisse interne = statut diplo
	ombre du dessin = rareté


