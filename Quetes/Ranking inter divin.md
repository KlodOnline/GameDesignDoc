

#### Deepseek
activité(j)  = min( métrique_jour(j) / médiane_jour(divinité) , 2.0 )
difficulté(j) = min( métrique_jour(j) / médiane_jour(divinité) , 2.0 )   // ou médiane du décile en V1
points(j)    = Base × (1 + activité(j)) × (1 + difficulté(j))

#### Gemini
$$\text{Points du jour} = \text{Base de Rang} \times \text{Multiplicateur d'Activité}$$


********


activité(j) = métrique_jour(j) / médiane_métrique_jour(divinité)

## 2. Le calcul des points de dévotion, adapté à tes quêtes faciles

Pour chaque divinité, tu définis :

text

Points_dévotion_jour(D) = Base × (1 + bonus_activité_D) × (1 + bonus_difficulté_D)

### bonus_activité_D — "as-tu fait progresser la métrique de D aujourd'hui ?"

- **Kael** : nombre d'unités entraînées + cases de territoire gagnées ce jour (normalisé par ta taille).
    
- **Erya** : prestige gagné + mètres de route pavée posés ce jour.
    
- **Toran** : or produit/gagné + cases révélées ce jour.
    

→ Le top passif qui ne fait rien touche la base. Le joueur actif touche le bonus. **Pas de parking.**

### bonus_difficulté_D — "à quel point ta progression était-elle difficile ?"

C'est là que ça devient fin. Pour chaque métrique, tu compares ta progression à **la médiane de progression des joueurs de ta divinité** :

text

bonus_difficulté_D = progression_jour / médiane_progression_divinité_D

- Si tu progresses 2× plus vite que la médiane → bonus élevé.
    
- Si tu progresses moins vite → bonus faible (mais tu touches quand même la base).
    

**Pourquoi c'est anti-gaming** : un joueur qui reste volontairement bas pour "avoir de la marge" ne profite pas, parce que le bonus se calcule sur la **progression du jour**, pas sur l'écart à ta position initiale. Et un top qui stagne touche un bonus faible — ce qui est **normal et sain** : il n'a pas fait d'effort ce jour-là.


### Le rang de divinité = prestige, pas revenu

Le rang 1 de Kael gagne le titre "Champion de Kael" + cosmétique + bonus one-shot en fin de quinzaine. Son revenu quotidien reste soumis au calcul ci-dessus. **Il doit jouer pour toucher.**
