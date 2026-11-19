

#### Deepseek
activité(j)  = min( métrique_jour(j) / médiane_jour(divinité) , 2.0 )
difficulté(j) = min( métrique_jour(j) / médiane_jour(divinité) , 2.0 )   // ou médiane du décile en V1
points(j)    = Base × (1 + activité(j)) × (1 + difficulté(j))

#### Gemini
$$\text{Points du jour} = \text{Base de Rang} \times \text{Multiplicateur d'Activité}$$


********

### 1. Remplace les maths par une **Jauge de Ferveur** à 3 états

Au lieu d'un multiplicateur de 0.0 à 2.0, le joueur voit simplement son **Gain du jour** (ex. `50 pts` parce qu'il est 1er) et un statut visuel sur sa jauge quotidienne :

- **Dieu indifférent (0 % — Gris) :** Tu n'as pas progressé aujourd'hui. Récompense du jour : **0 pt**. _(Tooltip : « Kael attend une conquête ou un recrutement aujourd'hui pour bénir votre rang. »)_
    
- **Dieu satisfait (100 % — Doré) :** Tu as atteint ton objectif d'activité du jour. Récompense du jour : **100 % de ta prime de rang (50 pts)**.
    
- **Dieu exalté (150 % — Enflammé) :** Tu as explosé ton quota aujourd'hui. Récompense du jour : **150 % de ta prime (75 pts)**.