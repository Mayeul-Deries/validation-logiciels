# Exercice 3

## Tableau des Métriques

| Classe      | LOC | WMC | CBO | LCOM | Notes                                                                                             |
| ----------- | --- | --- | --- | ---- | ------------------------------------------------------------------------------------------------- |
| Bank        | 393 | 14  | 4   | 0    | CBO le plus élevé (4), mais excellente cohésion (LCOM=0). Classe centrale                         |
| BankAccount | 412 | 21  | 3   | 46   | WMC élevé (21), LCOM moyen (46), mélange logique métier et persistence                            |
| Person      | 294 | 23  | 1   | 79   | MC le plus élevé (23), LCOM le plus élevé (79) - manque de cohésion critique, faible couplage (1) |

## Analyse

### Classe avec le WMC le plus élevé

**Person** est la classe avec le WMC le plus élevé avec 23 méthodes.

### Classe avec le CBO le plus élevé

**Bank** est la classe avec le plus élevé CBO (4). Couplage le plus élevé car elle interagit avec BankAccount, Person, et des services externes. C'est normal car c'st la classe centrale.

### Classe à laquelle il faut faire attention pour la maintenance future

**Person** est la classe la plus préoccupante pour la maintenance future :

1. LCOM très élevé (79) : Indique un manque de cohésion critique - les méthodes travaillent sur des groupes d'attributs différents sans relation forte entre elles
2. WMC très élevé (23) : Trop de responsabilités concentrées dans une seule classe
3. Ratio méthodes/LOC faible : 23 méthodes pour seulement 294 lignes suggère beaucoup de getters/setters simples, mais pas de logique métier cohérente
4. Faible couplage (CBO=1) : Bien que le faible couplage soit généralement positif, si le LCOM est élevé, cela confirme que Person est une classe isolée qui essaie de tout gérer seule
