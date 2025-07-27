___
# Villes (WIP)
![Ville.png](media/Ville.png)
## Zone d'influence et de production
Les villes définissent l'influence et le territoire des joueurs. Une ville commence avec un territoire d'un rayon de 1 case et peuvent croître jusqu'à un rayon de 3 (pour le moment, cette valeur pourrait évoluer en fonction des retours utilisateurs)
Le joueur "voit" tout ce qui est dans son territoire +1 case (zone claire sur l'image)
Lorsqu'une ville dépasse 6.000 habitant, le rayon de cette zone augmente d'une case (=2).
Lorsqu'une ville dépasse 18.000 habitant, le rayon de cette zone augmente d'une case supplémentaire (=3).
## Population
### Croissance
A la façon de Civilization 1er du nom, la ville commence avec 100 habitants. A chaque tour, elle produira des ressources, de la nourriture...
A chaque tour, en fonction de l'*Espoir* la ville prend entre -2 et +2 habitants. 



Après que la ville apparaît, au bout de 12 tours :
 - Si il y a des stock de nourriture ( de quoi tenir 24h, donc pop/1000x288 ) suffisant, les gens de la ville voient l'avenir radieux, et pensent à avoir des gosses
 - Sil il y a des stock de bois **ou** de pierre suffisant (100), des logements sont naturellement construits (en consommant ces ressources)
Si ces deux conditions sont remplies, la ville prend 1.000 habitants. Sinon, elle retentera au tour prochain directement. Dès qu'elle croît, elle décale sont prochain test de 12 tours.
On ne contrôle pas la population elle se reproduit d'elle même.
A voir pour permettre une croissance infinie. Techniquement, ça me fait envie, mais il faut voir ce que ça donne en jeu.
### Décroissance
Si la ville n'a pas les stock suffisant pour nourrir tout le monde au tour courant, elle perd 100 habitants. Cela peut être déséquilibré, peut être que cela ne se testera que toutes les heures en fonction des retour joueurs.
## Production de ressources
En général un terrain produit entre 1 et 3 unités de ressources. 
1 unité de nourriture nourri 1000 hab. sur 1 TIC. Un stack de nourriture c'est 100 unités.
Si le terrain a un "node" spécial, il produit **en plus** de sa production normale, la production spéciale. Ces nodes ont un stock (en général un stack, à étudier) de ressource qui s'épuise à la production. Les villes spécialisé (ou les ouvriers spécialisés) peuvent vider le stock plus vite que 1/tour.
## Bâtiments
Un bâtiment est créé dans une ville, à l'aide de ressources de base plus ou moins importante et pendant plus ou moins longtemps en fonction de ces ressources. 
Le calcul de base sera "total des ressources additionnée = NB de TIC", dans un premier temps.
Chaque bâtiment construit apportera des points de "culture" (militaire, industrie, commerce), et certain auront des pré-requis de points de culture.
La ville a un nombre de "slots" de bâtiments maximum, en fonction de ces habitants (1 slot/1000 hab.).
Donc une ville peut à la fois tout faire, et en même temps, non, car elle ne peux pas faire n'importe quel bâtiment, cela dépend de ce qui a été fait par le passé.
Les bâtiments interdit à la construction devraient ne pas apparaître du tout. Les "autorisés" mais quand on a pas les ressources, devraient être grisés.
Les arbres de bâtiments sont définissable dans les règles du jeu et pourrait donc être différent d'un serveur à l'autre. 
## Production d'unités
a ecrire
## Garnison
a ecrire


