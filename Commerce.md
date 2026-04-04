# Commerces
_______
## Principe
 - Le commerce ne doit pas casser le côté **logistique** de Klod Online. Il faut transporter des ressources !
 - La monnaie doit être très utile au commerce et devenir un outil de référence sans être excessivement rigide.
 - Les joueurs doivent être plus que **neutre** pour cela, un **accord commercial** doit être signé.

## Bâtiments
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
Chaque slot PJ permet de programmer des échanges contre 1 ressource en troc ou un prix en argent, paramétrable pour ce slot. On peut interdire un des deux usages cependant.

Les slots "PNJ magique" (Marchand de la ville) ne sont connus que du joueur (et des espions). Il peut acheter ou vendre n'importe quelle ressource. Il convertit automatiquement une ressource en argent. 
Le PNJ "magique" propose des prix voleurs : il achète pour `/10` de la valeur de base et vend pour `x10` la valeur de base. Ses échanges sont calculés automatiquement pour atteindre au moins 1 Pièce de Cuivre.

## Monnaie
 - Les joueurs peuvent créer des pièces de cuivre (CC), d'argent (SC), ou d'or (GC) via le bâtiment Hôtel de la Monnaie (Mint).
 - La valeur des monnaies est définie dans les règles du jeu.
 - On peut fondre des pièces pour en refaire des lingots (via la fonderie adaptée).
 - Le ratio implémenté est :
	 - 1 Pièce d'Or (PO/GC) = 10 Pièces d'Argent (PA/SC) = 2500 Pièces de Cuivre (PC/CC).
	 - 1 Pièce d'Argent (PA/SC) = 250 Pièces de Cuivre (PC/CC).
 - *Note: Le concept de Pièce de Pierre (PP) n'est pas implémenté.*

## Plus tard ...
Permettre de "battre monnaie" manuellement ? Est-ce utile ou intelligent d'un point de vue du gameplay ? Pour le moment c'est inutile, à voir plus tard.
