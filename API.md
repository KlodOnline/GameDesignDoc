# Appels API
## Principes
### Cas d'une requête simple pour obtenir une donnée
Il n'existe pas vraiment de "requête simple" et libre permettant au joueur de demander quelque chose d'inattendu côté serveur (c'est peut être une erreur d'ailleurs...).
Au contraire, chaque information du jeu doit être demandé à travers une requête précise qui devrait être optimisée au maximum.
#### 1. Un module du GUI a besoin d'une info
L'objectif est qu'il existe dans le javascript différentes script `EXAMPLE-api.js` qui permettent de récupérer des choses précises. (ordres, info sur une unité, une ville, etc.). Parfois il n'y en a pas, mais cela signifie qu'il faut le créer ou l'extraire du code existant. Ce script génère la requêtes proprement et fourni la réponse à qui le lui demande, en passant par `client-io.js`.
#### 2. AJAX
Ensuite, `client-io.js` formate la requête avec les paramètres `T` (type, soit _CITY_INFO_, _GET_ORDER_, etc.) et `M` (message, soit quelque chose comme _BUILD_UNIT-32,21_). La requête est envoyée en **POST** à `game_api.php` en **AJAX**. En cas de timeout, il redemande une fois après 300ms d'attente, et renvoie la réponse à qui le lui a demandé.
#### 3. API php
Le point d'entrée `game_api.php` va permettre de vérifier l'authentification, filtrer le POST et la gestion de la compression, etc. Il _devrait_ aussi être l'antispam, pour le moment cela est dans le script suivant `request_manager.php`, à qui il passe les requêtes pour ensuite en renvoyer la réponse à l'écran.
#### 4. Backend
Enfin, `request_manager.php` cuisine la réponse. Il utilise pour ça tout ce que l'on trouve dans `common/` et en particulier `board.php` qui est le super objet permettant d'aller chercher ou mettre à jour les infos en BDD, et qui dispose de son propre système de cache. `request_manager.php`  a donc le droit de lire et d'écrire et doit faire attention aux accès concomitants. Il dispose de différents _handlers_, comme (16/07/2025) :
```php
        $handlers = [
            'UORDERS'      => 'handleGetOrder',
            'CSELECT'      => 'handleCitySelection',
            'GET_ORDER'    => 'handleGetOrder',
            'SET_ORDER'    => 'handleSetOrder',
            'CANCEL_ORDER' => 'handleCancelOrder',
            'NEWBIE'       => 'handleNewbie',
            'SCOPEG'       => 'handleScopeGroundRequest',
            'SCOPEA'       => 'handleScopeAllRequest',
            'INIT'         => 'handleInit',
            'CITY_INFO'    => 'handleDetails',
            'UNIT_INFO'    => 'handleDetails',
        ];
```
Certains de ces _handlers_ sont sans doute rationnalisable ou obsolète. La réponse cuisinée retourne ensuite dans l'autre sens au GUI. Lors de la cuisine, on utilise `Board` pour manipuler les objets du jeu, mettre à jour des collection etc. De plus `Board` gère de façon assez proche la BDD via `BDDObjectManager` qui doit à terme permettre des requêtes très précise pour économiser du temps d'accès BDD.
### Cas d'un ordre envoyé du joueur au jeu (écriture)
#### Côté GUI
Bien sûr, un ordre utilise la même route qu'une requête "simple", sauf qu'il y a un peu plus de formatage en amont et de contrôle intermédiaire. Le handler utilisé par `request_manager.php`est `handleSetOrder`. Lorsque le joueur clique sur un élément de l'interface (par exemple pour recruter une unité `city-panel.js:93-111` ou pour valider un déplacement `selection.js:427-433`), l'ordre est  :
 - formaté et modélisé via `OrderFactory.createFromGUI([IDs], 'NOM', jsonData)`. On doit donc connaitre l'ID des objets concernés, l'ordre qu'on veut donner, et les data qui permettent de le réaliser.
 - envoyé au backend PHP via `OrderAPI.sendOrder(order)
#### Côté backend
Il suite ensuite le chemin normal, jusqu'à la `request_manager.php` qui fait sa factory, mais en PHP  `OrderFactory::createOrder` (il faut donc définir l'ordre aussi dans la factory en PHP, qui elle en plus contient les résolutions par le moteur de jeu), et qui si l'ordre à un défaut quelconque ne créé rien. Puis si tout s'est bien passé, sauvegarde.
### Cas de requête d'un ordre par le joueur  (lecture)
C'est beaucoup plus simple. Après `handleGetOrder` qui ne dit finalement que l'id de la chose dont on veut avoir les ordres (_ville_, _unité_...) et l'ordre est ainsi retrouvé par son acteur. Un acteur n'ayant qu'un ordre possible en BDD (pour les chainage d'ordre il y aura des astuces)


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
