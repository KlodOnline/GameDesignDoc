# Quêtes Divines - Règles

> Règles communes du système de quêtes divines
> Dernière mise à jour: 2026-05-29

## Portée du document

Ce fichier décrit uniquement les règles transversales du système divin. Il ne détaille pas les chaînes de quêtes elles-mêmes.

- La chaîne débutant est décrite dans [Quêtes Initiation](Quetes%20Initiation.md).
- Les quêtes récurrentes sont décrites dans [Quêtes Cycliques](Quetes%20Cycliques.md).
- La vision globale est décrite dans [Quêtes Divines Pitch](Quetes%20Divines%20Pitch.md).

## Principes

- Les quêtes d'initiation sont la première phase de jeu, pas un tutoriel séparé.
- Le joueur doit apprendre progressivement les délais du jeu: action immédiate, déplacement, construction, craft, recrutement, attente stratégique.
- Les quêtes divines prennent le relais après l'initiation et donnent une direction de long terme.
- Les récompenses doivent lisser la progression sans annuler les contraintes matérielles de Klod Online.
- Les quêtes doivent s'appuyer sur les systèmes existants: villes, unités, inventaires, ressources, bâtiments, territoires, combat, commerce.

## Dieux

| Dieu | Domaine | Objectifs typiques |
|------|---------|--------------------|
| **Kael** | Guerre | Recruter, défendre, attaquer, conquérir |
| **Erya** | Artisanat | Construire, produire, crafter, améliorer |
| **Toran** | Exploration / économie | Explorer, découvrir, exploiter, échanger |

## Types de quêtes

| Catégorie | Rôle | Document source |
|-----------|------|-----------------|
| `initiation` | Début de partie obligatoire et progressif | [Quêtes Initiation](Quetes%20Initiation.md) |
| `divine` | Objectifs liés aux dieux après l'initiation | Ce document, puis fichiers dédiés à créer |
| `cyclic` | Objectifs récurrents mensuels, trimestriels ou mondiaux | [Quêtes Cycliques](Quetes%20Cycliques.md) |

## Réputation

La réputation représente la relation durable du joueur avec les dieux.

- Elle augmente via les quêtes divines.
- Elle peut servir au classement et à l'accès à certaines récompenses.
- Elle peut décroître avec le temps si on veut forcer une activité régulière.
- Elle ne doit pas être dépensée comme une monnaie classique.

Réputation et faveur doivent rester séparées.

## Faveur

La faveur est une ressource temporaire gagnée surtout par les quêtes cycliques ou les épreuves de faveur.

- Elle peut servir à acheter des miracles, bonus temporaires ou unités spéciales.
- Elle peut fuir avec le temps.
- Elle est plus consommable que la réputation.

La réputation débloque. La faveur paie.

## Choix divin

Le choix divin doit arriver après une initiation suffisamment riche pour que le joueur comprenne les grands styles de jeu.

Le système peut commencer simplement avec une divinité tutélaire choisie à la fin de l'initiation. Les mécaniques plus avancées de sanctuaire, multi-dieux, changement de foi ou pénalités peuvent être ajoutées ensuite si elles servent vraiment le gameplay.

Règle de design: ne pas bloquer l'initiation derrière des prérequis trop avancés comme un bâtiment T2 si le but est d'amener le joueur progressivement vers le système divin.

## Récompenses

Les récompenses peuvent prendre plusieurs formes:

- ressources de base pour éviter un blocage;
- accélération ponctuelle d'un ordre ou bâtiment;
- petite quantité de réputation;
- faveur pour les quêtes cycliques;
- révélation ou signalement d'un objectif proche;
- accès à une nouvelle catégorie de quêtes.

Une récompense ne doit pas rendre inutile l'action que la quête vient d'apprendre. Par exemple, une quête de recrutement ne devrait pas donner gratuitement la même unité en double sauf si c'est explicitement voulu.

## Checkers nécessaires

Les checkers exacts dépendront de l'implémentation, mais les familles utiles sont:

| Famille | Exemples |
|---------|----------|
| Ville | ville fondée, bâtiment construit, worker réaffecté |
| Production | ressource possédée, ressource produite, craft terminé |
| Unités | unité recrutée, unité déplacée, unité transformée |
| Exploration | cases révélées, source découverte, territoire atteint |
| Combat | barbare tué, ville défendue, territoire conquis |
| Divin | dieu choisi, réputation atteinte, faveur gagnée |

## Compteurs utiles

Certains objectifs doivent être suivis de manière cumulative.

| Compteur | Usage |
|----------|-------|
| `kills_total` | Quêtes de combat |
| `crafted_total` | Quêtes d'artisanat |
| `explored_total` | Quêtes d'exploration |
| `buildings_built` | Quêtes de développement |
| `cities_founded` | Quêtes d'expansion |
| `cities_captured` | Quêtes de conquête |
| `resources_traded` | Quêtes économiques |
| `territory_max` | Quêtes de domination territoriale |

## Questions ouvertes ou réponses

1. Seule la faveur décroît avec le temps.
2. Le choix de divinité de fin d'initiation est modifiable, mais à grand prix.
3. Les sanctuaires sont le lieu de communication avec les dieux. Quand le joueur a accumulé une certaine réputation, les dieux lui demandent de figurer dans sa ville sanctuaire, ou de faire construire un autel à leur gloire. Cela active ensuite la voix des dieux via les prêtres.
