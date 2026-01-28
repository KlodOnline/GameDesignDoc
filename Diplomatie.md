# Game Design Document — Système de Diplomatie
_________
## 1. Vue d’ensemble
Le système de diplomatie régit les interactions politiques entre joueurs : déplacements des unités, contrôle territorial, accès aux ressources et coopération militaire ou économique.

Le monde est **non arbitré** :
- aucune protection automatique,
- aucune correction d’abus,
- la régulation est exclusivement sociale et stratégique.
- La **seule** protection est celle des débutant, de 15 jours à 1 mois (en définition)

La diplomatie repose sur **cinq états relationnels**, progressifs, allant de la destruction totale à la coopération maximale.
## 2. États Diplomatiques

### A. GUERRE (War)

Conflit ouvert visant la destruction ou l’annexion de l’adversaire.

- **Combat** : attaques automatiques à vue.
- **Conquête** : capture active des territoires.  
  Si un joueur n’a plus d’unités ni de ville sur un territoire adjacent à l’agresseur, l’intégralité de la zone peut être conquise. (_à définir : problème des villes des forts, etc._)
- **Siège & Blocage** :
  - zone de contrôle générée par chaque unité,
  - blocage de l’exploitation des ressources ennemies,
  - zone physique empêchant le contournement.

### B. HOSTILE (Hostile)

État de tension extrême et de guerre froide active.  Etat autorisant l’incursion sans combat ouvert, ainsi que le pillage de ressources. HOSTILE est un état de prédation assumée sans engagement total.

- **Stand-off (face-à-face)** :  
  pas de combat automatique.  
  En cas de rencontre, le moteur stoppe les unités et notifie que la guerre est requise pour attaquer.
- **Incursion** :
  - franchissement des frontières autorisé,
  - exploitation des ressources ennemies possible sans contrôle territorial.
- **Siège** :
  Pas de siège, une unité n'empêche pas l'exploitation des ressources par l'autre sauf en cas de fort.
- **Limitation** :
  aucune capture de territoire possible.

### C. NEUTRE (Neutral) — État par défaut

- **Frontières verrouillées** : mur invisible, arrêt automatique des unités.
- **Interactivité moteur** :
  tentative de franchissement → invitation à :
  - demander un droit (PAISIBLE),
  - ou devenir HOSTILE.
- **Transition** :
  nécessite une action diplomatique explicite.

### D. PAISIBLE (Peaceful)

État de coopération négociée, basé sur des droits atomiques.

- **Droit de passage** : traversée libre.
- **Droit d’exploitation** : accès partagé à certaines ressources.
- **Droit commercial** : utilisation des marchés et hôtels des ventes.

Aucune protection militaire implicite.
### E. ALLIÉ (Ally)

Niveau maximal de coopération et seule protection structurelle.

- **Guerre simultanée** :
  Lorsque votre allié passe hostile, ou en guerre, vous êtes notifiés et pouvez alors suivre ou rompre l'Alliance ! En fait tout les changement de statut d'un des Alliés notifie tout les alliés.
- **Conflits d’alliances** :
  obligation de choisir un camp.
- **Communication** :
  canal de chat privé commun.
- **Soutien logistique** :
  transferts de ressources et dons d’unités.

## 3. Actions et Commandes Diplomatiques

### Actions Unilatérales

- Devenir HOSTILE.
- Déclarer la GUERRE.
- Offrir/Révoquer des droits :
  - libre passage,
  - construction (camp, fort, tour),
  - accès aux marchés urbains.

### Accords Mutuels (Validation requise)

- **Déclaration de Bonne Intention** :
  passage de HOSTILE à NEUTRE.
- **Règle de retrait** :
  les unités en incursion peuvent sortir,
  toute nouvelle entrée est interdite.
- **Armistice** :
  passage de GUERRE à HOSTILE.
- **Pacte de Paix** :
  passage direct de GUERRE à NEUTRE.

## 4. Sortie de Guerre — Le Traité de Paix

La guerre ne se termine jamais unilatéralement  
(sauf destruction totale).
### 4.1. Demande d’Armistice
Accord mutuel.
- **Transition immédiate** : GUERRE → HOSTILE.
- **Conséquence** :
  arrêt instantané des combats,
  passage en mode stand-off.
- **Évacuation** :
  les troupes peuvent se retirer sans combat,
  ou rester en incursion pour maintenir la pression.

### 4.2. Traité de Paix Définitif

Accord mutuel.

- **Transition** : GUERRE → NEUTRE.
- **Nettoyage territorial** :
  - toutes les unités présentes en territoire adverse sont poussées vers la frontière la plus proche,
  - ou doivent avoir été évacuées préalablement via HOSTILE + Déclaration de Bonne Intention.

Les frontières redeviennent strictement verrouillées.
### 4.3. Reddition (Capitulation)

Action unilatérale.

- Le joueur cède tous ses territoires contestés
  (ceux sans troupes ni villes).
- **Transition immédiate** : GUERRE → HOSTILE.
- Permet la réorganisation des frontières et des forces.

## 5. Scénarios de Référence

### Scénario : Désescalade

- **Guerre** :
  le joueur A envahit le joueur B, les villes tombent.
- **Armistice** :
  B demande un cessez-le-feu, A accepte.
- **Hostile** :
  les combats cessent,
  les unités de A restent en incursion,
  plus aucune conquête possible.
- **Paix** :
  B offre une ressource rare contre une Déclaration de Bonne Intention.
- **Neutre** :
  A accepte,
  ses unités sont reconduites à la frontière,
  les frontières se verrouillent.

## 6. Intention de Design

Ce système privilégie la **cohérence politique** à l’équité.
- La violence non déclarée est permise.
- L’abus n’est jamais corrigé par le moteur.
- La désescalade est toujours négociée, jamais gratuite.

Les joueurs assument.