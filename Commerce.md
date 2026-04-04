# Commerce
_______
## État actuel
L'échange de ressources entre entités sur la **même case** est implémenté (unités ↔ unités, unités ↔ villes, unités ↔ loot). Le commerce entre joueurs et le système de marché avec PNJ marchand **ne sont pas encore implémentés**.

## Échange local
Une unité peut transférer des objets avec une autre unité, une ville ou un loot présent sur la même case.  
L'échange vérifie uniquement :
- que la cible a de la place
- qu'elle appartient au même joueur ou à aucun

## Principe (à implémenter)
 - Le commerce ne doit pas casser le côté **logistique** de Klod Online. Il faut transporter des ressources !
 - La monnaie doit être très utile au commerce et devenir un outil de référence sans être excessivement rigide.
 - Les joueurs doivent être plus que **neutres** pour cela, un **accord commercial** doit être signé.

## Bâtiments (prévu)
 - Marché (Marketplace) :
	 - 1 slot PNJ Magique
	 - 2 slots PJ d'achat ou de vente
 - Marché Moyen (Medium Market)
	 - 2 slots PNJ Magique
	 - 4 slots PJ d'achat ou de vente
 - Grand Marché (Big Market)
	 - 3 slots PNJ Magique
	 - 8 slots PJ d'achat ou de vente

Chaque slot est paramétrable en achat ou en vente, PNJ comme PJ.
Chaque slot PJ permet de programmer des échanges contre 1 ressource en troc ou un prix en argent, paramétrable pour ce slot.

Les slots "PNJ magique" (Marchand de la ville) ne sont connus que du joueur (et des espions). Il peut acheter ou vendre n'importe quelle ressource. Il convertit automatiquement une ressource en argent. 
Le PNJ "magique" propose des prix voleurs : il achète pour `/10` de la valeur de base et vend pour `x10` la valeur de base.

## Monnaie (configuré mais non implémenté)
 - Les joueurs pourront créer des pièces de cuivre (CC), d'argent (SC), ou d'or (GC) via le bâtiment Hôtel de la Monnaie (Mint).
 - Le ratio prévu est :
	 - 1 Pièce d'Or (PO/GC) = 10 Pièces d'Argent (PA/SC) = 2500 Pièces de Cuivre (PC/CC).
	 - 1 Pièce d'Argent (PA/SC) = 250 Pièces de Cuivre (PC/CC).
