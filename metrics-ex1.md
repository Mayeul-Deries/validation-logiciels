## Exercice 1

| Classe         | LOC | NOM | Short Description of responsibility                                                                                             |
| -------------- | --- | --- | ------------------------------------------------------------------------------------------------------------------------------- |
| Bank           | 393 | 14  | Manages a collection of bank accounts with operations like add, delete, find, transfer, and statistical calculations            |
| BankAccount    | 405 | 20  | Represents an individual bank account with deposit/withdraw operations, balance management, and persistence capabilities        |
| Person         | 294 | 23  | Represents account holder information including personal attributes (name, age, gender, physical characteristics, contact info) |
| BankAccountApp | 447 | 2   | Main application entry point providing user interface for bank account management operations                                    |

### Do you feel its size roughly matches its responsibility?

Dans l'ensemble la taille des classes ne corresnd pas bien à leurs responsabilités. Les métriques LOC et NOM indiquent des classes surchargées ou mal découpées, notamment BankAccountApp qui a 447 lignes pour seulement 2 méthodes, ce qui indique que toute la logique de l'interface utililsateur est concentrée dans une seule méthode trop complexe.
