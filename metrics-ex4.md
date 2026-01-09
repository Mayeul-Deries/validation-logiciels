# Exercice 4

## 3 Issues Importantes Identifiées

### 1. Brain Method - Complexité Cognitive Élevée

**Règle :** Refactor to reduce Cognitive Complexity  
**Fichier :** BankAccountApp.java:20 (méthode `main`)  
**Explication :** La méthode `main` a une complexité cognitive de 125 (la limite est à 15) avec 180 lignes de code, 38 variables et 7 niveaux d'imbrication. C'est une "Brain Method" qui gère tout : gestion du menu, opérations bancaires, saisie utilisateur, etc. Elle devrait être décomposée en plusieurs méthodes plus petites pour améliorer la lisibilité et la maintenabilité.

### 2. Paramètre Inutilisé - Code Smell

**Règle :** Remove this unused method parameter "accManager"  
**Fichier :** Bank.java:141 (méthode `saveAccounts`)  
**Explication :** La méthode `saveAccounts(Bank accManager)` possède un paramètre `accManager` qui n'est jamais utilisé dans le corps de la méthode. Au lieu d'utiliser ce paramètre, la méthode accède directement à la variable statique `Accounts`.

### 3. Ressources Non Fermées - Fuite de Mémoire Potentielle

**Règle :** Use try-with-resources or close this "FileOutputStream" in a "finally" clause  
**Fichier :** Bank.java:143-144 (méthode `saveAccounts`)  
**Explication :** La méthode `saveAccounts` utilise `FileOutputStream` et `OutputStreamWriter` avec un try-catch-finally manuel pour fermer les ressources. Cette approche est sujette aux erreurs car si une exception survient avant la fermeture, les ressources peuvent rester ouvertes, causant une fuite de mémoire.

## Corrections Appliquées

### Correction 1 : Suppression du Paramètre Inutilisé

**Issue :** Remove this unused method parameter "accManager"  
**Fichier :** Bank.java:141

**Avant :**

```java
public void saveAccounts(Bank accManager) {
    // Le paramètre accManager n'était jamais utilisé
    FileOutputStream fos = null;
    // ...
}
```

**Après :**

```java
public void saveAccounts() {
    FileOutputStream fos = null;
    // ...
}
```

**Appel mis à jour dans BankAccountApp.java:211 :**

```java
// Avant: accManager.saveAccounts(accManager);
// Après:
accManager.saveAccounts();
```

Cette correction élimine le paramètre inutile et clarifie que la méthode sauvegarde les comptes de l'instance courante.

### Correction 2 : Utilisation du Try-With-Resources

**Issue :** Use try-with-resources to ensure resources are closed properly  
**Fichier :** Bank.java:141-170

**Avant :**

```java
public void saveAccounts() {
    FileOutputStream fos = null;
    OutputStreamWriter osw = null;
    try {
        fos = new FileOutputStream("C:\\Users\\jay4k\\Desktop\\...");
        osw = new OutputStreamWriter(fos);
        for (int i = 0; i < Accounts.size(); i++) {
            BankAccount tmp = Accounts.get(i);
            osw.write(tmp.convertToText(tmp));
        }
    } catch (IOException e) {
        System.out.println("Error writing to file");
    } finally {
        if (osw != null) {
            try { osw.close(); } catch (IOException e) { }
        }
        if (fos != null) {
            try { fos.close(); } catch (IOException e) { }
        }
    }
}
```

**Après :**

```java
public void saveAccounts() {
    try (FileOutputStream fos = new FileOutputStream("C:\\Users\\jay4k\\Desktop\\...");
         OutputStreamWriter osw = new OutputStreamWriter(fos)) {

        for (int i = 0; i < Accounts.size(); i++) {
            BankAccount tmp = Accounts.get(i);
            osw.write(tmp.convertToText(tmp));
        }
    } catch (IOException e) {
        System.out.println("Error writing to file");
    }
}
```

**Avantages :**

- Les ressources sont automatiquement fermées à la fin du bloc try, même si une exception survient
- Code plus court et plus lisible (suppression du bloc finally complexe)
- Aucun risque de fuite de mémoire
- Les ressources sont fermées dans l'ordre inverse de leur création

## Corrélation entre Issues SonarLint et Métriques WMC/CBO

Les issues SonarQube apparaissent plus souvent dans les classes avec des métriques élevées. **BankAccountApp** concentre le plus d'issues critiques avec sa complexité cognitive de 125, tandis que **Person** (WMC=23, LCOM=79) présente plusieurs problèmes liés à son manque de cohésion. En revanche, **Bank** (WMC=14, LCOM=0) n'a que des issues mineures malgré son CBO élevé, démontrant qu'une bonne cohésion compense un couplage modéré.
