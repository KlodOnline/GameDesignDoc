# Appels API
## Principes
### Cas d'une requête simple pour obtenir une donnée
Il n'existe pas vraiment de "requête simple" et libre permettant au joueur de demander quelque chose d'inattendu côté serveur.
Au contraire, chaque information du jeu doit être demandée à travers une requête précise qui devrait être optimisée au maximum.
#### 1. Un module du GUI a besoin d'une info
Il existe dans le javascript différents scripts `*-api.js` qui permettent de récupérer des choses précises (ordres, info sur une unité, une ville, etc.). Ce script génère la requête proprement et fournit la réponse à qui le lui demande, en passant par `client-io.js`.
#### 2. AJAX
Ensuite, `client-io.js` formate la requête avec les paramètres `T` (type, soit _CITY_INFO_, _GET_ORDER_, etc.) et `M` (message, soit quelque chose comme _RECRUIT-32_). La requête est envoyée en **POST** à `game_api.php` en **AJAX**. En cas de timeout, il redemande une fois après 300ms d'attente, et renvoie la réponse à qui le lui a demandé.
#### 3. API php
Le point d'entrée `game_api.php` vérifie l'authentification, filtre le POST et gère la compression. Il passe les requêtes au `request_manager.php` qui gère aussi l'anti-spam (rejette les requêtes trop rapides, < 50ms, avec une réponse `nope: true`).
#### 4. Backend
Le `request_manager.php` construit la réponse. Il utilise tout ce qui se trouve dans `common/` et en particulier `board.php` qui est le super objet permettant d'aller chercher ou mettre à jour les infos en BDD, et qui dispose de son propre système de cache. Il dispose de différents _handlers_ :

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

### Cas d'un ordre envoyé du joueur au jeu (écriture)
#### Côté GUI
Un ordre utilise la même route qu'une requête "simple", avec un peu plus de formatage en amont et de contrôle intermédiaire. Le handler utilisé par `request_manager.php` est `handleSetOrder`. Lorsque le joueur clique sur un élément de l'interface, l'ordre est :
 - formaté et modélisé via `OrderFactory.createFromGUI([IDs], 'NOM', jsonData)`
 - envoyé au backend PHP via `OrderAPI.sendOrder(order)`

#### Côté backend
Il suit ensuite le chemin normal, jusqu'au `request_manager.php` qui fait sa factory en PHP `OrderFactory::createOrder`. Si l'ordre a un défaut quelconque, rien n'est créé. Puis si tout s'est bien passé, sauvegarde.
### Cas de requête d'un ordre par le joueur (lecture)
C'est beaucoup plus simple. Après `handleGetOrder` qui ne dit finalement que l'id de la chose dont on veut avoir les ordres (_ville_, _unité_...), l'ordre est retrouvé par son acteur. Un acteur n'ayant qu'un ordre possible en BDD. `handleGetOrder` renvoie ensuite un tableau `tokens` des infos de l'acteur et de son ordre, pour que le _GUI_ sache "ranger tout ça".

Chaque élément du gui dispose de sa façon de présenter l'ordre, mais tous passent par la factory `order-factory.js` qui créé l'objet via `OrderFactory.createFromServer([IDs], orderToken)`.

Il est prévu un concept d'ordres "groupés" pour plusieurs unités, mais ce n'est pas encore clairement modélisé.
