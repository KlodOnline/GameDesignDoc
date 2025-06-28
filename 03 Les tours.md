____
# Tour de jeu
## Principe (WIP)
Le principe des tours de jeu est un classique des anciens MMORTS web, le **_TIC_**. Tout les joueurs jouent en même temps, donnent des ordres à leur unités ou leurs villes, et à chaque **_TIC_** le serveur calcule tout ou partie de ces ordres et modifie le monde de jeu. Pendant la durée de cette **_résolution_** le monde est verrouillé et aucun ordre nouveau n'est pris en compte (même si l’interface permet d'en ajouter de nouveau pour la suite).
**Pour faciliter tout le système de jeu, il faut trouver moyen de rendre toute action dans l'interface comme un "ordre" soumis au TIC.**. Même les actions "évidentes" comme renommer une ville ou décharger quelque chose de l'inventaire.
## Ordre d'action
 - Les joueurs paient l'entretien
 - Les villes jouent
	 - des joueurs
	 - de l'IA
 - Les unités jouent
	 - des joueurs
	 - de l'IA
 