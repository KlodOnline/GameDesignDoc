# Appels API
## Principes
### Cas d'une requête simple pour obtenir une donnée
Il n'existe pas vraiment de "requête simple" et libre permettant au joueur de demander quelque chose d'inattendu côté serveur (c'est peut être une erreur d'ailleurs...).
Au contraire, chaque information du jeu doit être demandé à travers une requête précise qui est débord répondue avec une logique générique qui sera ensuite optimisée au maximum.
#### 1. Un module du GUI a besoin d'une info
L'objectif est qu'il existe dans le javascript différentes script `EXAMPLE-api.js` qui permettent de récupérer des choses précises. (ordres, info sur une unité, une ville, etc.). Parfois il n'y en a pas, mais cela signifie qu'il faut le créer ou l'extraire du code existant. Ce script génère la requêtes proprement et fourni la réponse à qui le lui demande, en passant par `client-io.js`.
#### 2. AJAX
Ensuite, `client-io.js` demande à `game_api.php` en AJAX ce qu'il faut, après avoir formaté sa requête (_CITY_INFO_, _GET_ORDER_, etc.). En cas de timeout, il redemande une fois après 300ms d'attente, et renvoie la réponse à qui le lui a demandé.
#### 3. API php
Le point d'entrée `game_api.php` va permettre de vérifier l'authentification, filtrer le POST et la gestion de la compression, etc. Il _devrait_ aussi être l'antispam, pour le moment cela est dans le script suivant `request_manager.php`, à qui il passe les requêtes pour ensuite en renvoyer la réponse à l'écran.
#### 4. Backend
Enfin, `request_manager.php` cuisine la réponse. Il utilise pour ça tout ce que l'on trouve dans `common/` et en particulier `board.php` qui est le super objet permettant d'aller chercher ou mettre à jour les infos en BDD, et qui dispose de son propre système de cache. `request_manager.php`  a donc le droit de lire et d'écrire et doit faire attention aux accès concomitants.

### Cas d'un ordre envoyé du joueur au jeu
**1. Clic du joueur (Frontend)**  
Le joueur clique sur un élément de l'interface, par exemple pour recruter une unité dans une ville `city-panel.js:93-111` ou pour valider un ordre d'objet sélectionné `selection.js:427-433`.

L'ordre est alors 
 - formaté et modélisé via `OrderFactory.createFromGUI([IDs], 'NOM', jsonData)`. On doit donc connaitre l'ID des objets concernés, l'ordre qu'on veut donner, et les data qui permettent de le réaliser.
 - envoyé au frontend PHP via `OrderAPI.sendOrder(order)



______________
# génération deepwiki à relire :

**2. Création de la requête (ClientIO)**  
L'action déclenche un appel via `ClientIO.ask_data()` qui formate la requête avec les paramètres `T` (type) et `M` (message) client-io.js:32-35 . La requête est envoyée en POST vers `game_api.php` client-io.js:59-63 .

**3. Traitement serveur (RequestManager)**  
Le `RequestManager` reçoit la requête et la route vers le bon handler selon le type request_manager.php:70-82 . Il charge les données du joueur si nécessaire request_manager.php:145-157 .

**4. Manipulation des données (Board)**  
Le handler utilise l'objet `Board` pour manipuler les données de jeu. Par exemple, pour un ordre, il crée l'objet via `OrderFactory` puis l'ajoute aux collections via `updateCollection()` request_manager.php:427-445 .

**5. Sauvegarde en base (BDDObjectManager)**  
La méthode `saveBoardCollection()` du `RequestManager` déclenche la sauvegarde request_manager.php:167-175 . Le `Board` utilise `saveCollection()` pour persister les changements board.php:420-430 .

**6. Exécution SQL**  
Le `BDDObjectManager` génère et exécute les requêtes SQL d'insertion/mise à jour bdd_object_manager.php:254-264 via la couche `bdd_io` qui gère la connexion MySQL bdd_io.php:45-49 .


### Protection anti-spam

Le système inclut une protection qui rejette les requêtes trop rapides (< 50ms) avec une réponse `nope: true` request_manager.php:52-58 , déclenchant un retry automatique côté client client-io.js:72-84 .

## Notes

Le système utilise un pattern de collections avec cache pour optimiser les performances. Les données passent par plusieurs couches d'abstraction (Board → BDDObjectManager → bdd_io) avant d'atteindre MySQL. Le `RequestManager` agit comme contrôleur principal orchestrant ce flux.
