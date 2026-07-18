# Système de Quêtes
______
## État actuel
Le Système est implémenté, avec panneau de suivi, popup de narration, et éditeur GM.
Quelques quêtes sont en place (17).

## Architecture

### Chaînes disponibles
- **welcome** (tutoriel) : 11 quêtes qui guident le nouveau joueur
- **fallen_angel** (JcE) : 5 quêtes narrative

### Cycle de vie
Chaque quête traverse les états automatiquement :
- **locked** → **available** : conditions de déverrouillage remplies
- **available** → **active** : acceptation automatique (pas d'action joueur)
- **active** → **completed** : objectifs remplis (vérifié chaque TIC)
- **completed** → **claimed** : joueur clique sur le bouton Réclamer

### Vérifications (17 checkers)
Chaque quête peut utiliser un vérificateur existant ou sinon on peut en coder un nouveau

### Récompenses
- Ressources (bois, pierre, etc.)
- Unités spéciales
- Déverrouillage de quêtes suivantes

## À faire (évolutions futures)
- Système de divinités au choix du joueur
- Points d'honneur et scoreboard
- Dégradation de l'honneur avec le temps 