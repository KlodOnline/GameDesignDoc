

#### Deepseek
activité(j)  = min( métrique_jour(j) / médiane_jour(divinité) , 2.0 )
difficulté(j) = min( métrique_jour(j) / médiane_jour(divinité) , 2.0 )   // ou médiane du décile en V1
points(j)    = Base × (1 + activité(j)) × (1 + difficulté(j))

#### Gemini
$$\text{Points du jour} = \text{Base de Rang} \times \text{Multiplicateur d'Activité}$$

**Comment gagner des points de dévotion ?**
- **+10 automatiques** si tu as joué aujourd'hui (participation).  
- **+0 à +45** selon ton effort par rapport aux autres joueurs de ta divinité (tu es récompensé si tu fais plus qu'eux).
- **+0 à +45** selon ta progression par rapport à ton niveau (tu es récompensé si tu progresses plus vite que les joueurs de ton niveau).
- **Ton rang ne te donne aucun point passif.** Être 1er ne te rapporte rien si tu ne joues pas.

**Ton score de dévotion : 73** (▲ +5 par rapport à hier)
- Tu as fait **plus d'efforts** que hier → +3
- Ton **niveau a augmenté**, donc l'effort relatif compte plus → +2

- Clic 1 : je vois ma note sur 100 + mon delta.
- Clic 2 : je vois la décomposition en 3 lignes (participation / effort vs autres / effort vs niveau).
- Clic 3 : je vois la carte de référence ("comment gagner des points").

**Concrètement, pour Kael (unités de combat) :**
- Tu as entraîné 600 unités aujourd'hui.
- La **médiane** des disciples de Kael a entraîné 300 unités aujourd'hui.
- Ton ratio = 600 / 300 = **2.0** → plafonné à 2.0.
- Tu es **au-dessus de la médiane** → tu touches le maximum de la brique : **+45**.

Si tu avais entraîné 150 unités (ratio 0.5) → tu touches **+22** (la moitié).  
Si tu n'as rien entraîné (ratio 0) → **+0**.

→ **La brique Effort mesure "as-tu fait plus que les autres disciples de ton dieu aujourd'hui ?"** C'est ça, le "+0 à +45".

 - Brique 1 — Participation : +10 automatique
 - Brique 2 — Effort : +0 à +45 selon ton activité vs les autres disciples du dieu
 - Brique 3 — Progression : +0 à +45 selon ta progression vs ton propre niveau











********

### 1. Remplace les maths par une **Jauge de Ferveur** à 3 états

Au lieu d'un multiplicateur de 0.0 à 2.0, le joueur voit simplement son **Gain du jour** (ex. `50 pts` parce qu'il est 1er) et un statut visuel sur sa jauge quotidienne :

- **Dieu indifférent (0 % — Gris) :** Tu n'as pas progressé aujourd'hui. Récompense du jour : **0 pt**. _(Tooltip : « Kael attend une conquête ou un recrutement aujourd'hui pour bénir votre rang. »)_
    
- **Dieu satisfait (100 % — Doré) :** Tu as atteint ton objectif d'activité du jour. Récompense du jour : **100 % de ta prime de rang (50 pts)**.
    
- **Dieu exalté (150 % — Enflammé) :** Tu as explosé ton quota aujourd'hui. Récompense du jour : **150 % de ta prime (75 pts)**.