## Exercice 2

**Méthode choisie :** `withdrawMoney(double withdrawAmount)`

**Complexité Cyclomatique:** 5

### Points de Décision Identifiés

La méthode contient 4 conditions dans une seule instruction `if` :

1. `withdrawAmount >= 0` - Vérifie si le montant du retrait est positif
2. `balance >= withdrawAmount` - Vérifie si le solde est suffisant
3. `withdrawAmount < withdrawLimit` - Vérifie si le retrait est sous la limite
4. `withdrawAmount + amountWithdrawn <= withdrawLimit` - Vérifie si les retraits cumulés ne dépassent pas la limite

Ainsi qu'un `else`, donnant une complexité cyclomatique totale de 5.

### Refactoring Proposé

Pour réduire la complexité, on peut extraire toute la validation du retrait dans une seule méthode `canWithdraw(double withdrawAmount)` qui encapsule les conditions `if`. Cette refactorisation rendrait le code plus lisible, testable et réduirait la complexité cyclomatique de la méthode principale à 2 au lieu de 5.

### Bonus - Implémentation du Refactoring

**Méthode créée :** `canWithdraw(double withdrawAmount)`

- Encapsule les validations dans une seule méthode privée
- Complexité cyclomatique de `canWithdraw` : 5 (4 conditions + 1)

**Méthode simplifiée :** `withdrawMoney(double withdrawAmount)`

- Complexité cyclomatique réduite à **2**. On a réduis de 3 points de compléxité (5 à 2).

Le refactoring permet de déplacer la complexité dans une méthode dédiée à la validation, rendant `withdrawMoney` plus simple et plus facile à comprendre.
