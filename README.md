# Leçons SQL & Exercices

## Leçon 1 : Sélectionner des données

En SQL, la commande `SELECT` est utilisée pour récupérer des données d'une table.

**Exemple simple :**

```sql
SELECT * FROM membre;
```

Ceci sélectionne toutes les colonnes de la table `membre`.

**Sélectionner des colonnes spécifiques :**

```sql
SELECT nom, prenom FROM membre;
```

Cela ne renvoie que les colonnes `nom` et `prenom`.

---

## Leçon 2 : Filtrer les données

On utilise `WHERE` pour filtrer les lignes selon des conditions.

**Exemple :**

```sql
SELECT * FROM compteA WHERE montant > 100;
```

Cela renvoie les paiements supérieurs à 100€.

**Exemple avec plusieurs conditions :**

```sql
SELECT * FROM membre WHERE club_lic = 'CLUB001' AND region = 'Nord';
```

Ici, on applique deux conditions combinées avec `AND`.

---

## Leçon 3 : Agrégation et Groupement

Les fonctions d'agrégation comme `SUM`, `COUNT`, `AVG`, `MAX`, `MIN` permettent de résumer les données.

Pour grouper les résultats, on utilise `GROUP BY`.

**Somme des montants par membre :**

```sql
SELECT numero_membre, SUM(montant) AS total
FROM compteA
GROUP BY numero_membre;
```

Cela donne, pour chaque membre, la somme des montants payés.

**Nombre d'inscriptions par événement :**

```sql
SELECT evenement, COUNT(*) AS nb_inscriptions
FROM inscription
GROUP BY evenement;
```

**Attention :** Chaque colonne non agrégée doit apparaître dans le `GROUP BY`.

**Filtrer après agrégation (avec HAVING) :**

```sql
SELECT numero_membre, COUNT(*) AS nb_inscriptions
FROM inscription
GROUP BY numero_membre
HAVING nb_inscriptions > 3;
```

`HAVING` filtre les résultats après le groupement, contrairement à `WHERE` qui filtre avant.

---

## Leçon 4 : Joindre des tables

Les `JOIN` permettent de combiner des données de plusieurs tables.

**INNER JOIN (jointure interne) :**

```sql
SELECT m.nom, m.prenom, i.date_inscription
FROM membre m
INNER JOIN inscription i ON m.numero = i.numero_membre;
```

Cela affiche uniquement les membres qui ont une inscription.

**LEFT JOIN (jointure externe gauche) :**

```sql
SELECT e.nom_equipe, m.nom AS capitaine_nom
FROM equipe e
LEFT JOIN membre m ON e.capitaine = m.numero;
```

Cela affiche toutes les équipes, même si le capitaine n'existe pas dans `membre`.

**RIGHT JOIN (moins fréquent, selon le SGBD) :**
Affiche toutes les lignes de la table de droite, même sans correspondance.

---

## Leçon 5 : Requêtes avancées

**UNION (combiner plusieurs requêtes) :**

```sql
SELECT numero_membre, montant FROM compteA
UNION ALL
SELECT numero_membre, montant FROM compteB;
```

`UNION` enlève les doublons, `UNION ALL` les conserve.

**Sous-requêtes :**

```sql
SELECT * FROM membre WHERE numero IN (
    SELECT numero_membre FROM inscription WHERE evenement = 10
);
```

**Calculer des différences de dates :**

```sql
SELECT DATEDIFF(date_reglement, date_achat) AS delai_paiement
FROM compteB;
```

Cela calcule le nombre de jours entre deux dates.

**Ordre et limites :**

```sql
SELECT numero_membre, SUM(montant) AS total
FROM compteA
GROUP BY numero_membre
ORDER BY total DESC
LIMIT 5;
```

Cela donne les 5 membres qui ont le plus payé.

---

## Exercices (sans réponses)

1. Lister tous les membres avec leur nom et club.
2. Afficher tous les événements après le 1er janvier 2025.
3. Trouver tous les paiements supérieurs à 200€ dans `compteA`.
4. Compter combien d'inscriptions chaque événement a.
5. Afficher le montant total dépensé par membre (`compteB`).
6. Lister les événements avec moins de 10 inscriptions.
7. Obtenir les 5 membres qui ont payé le plus dans `compteA`.
8. Trouver les membres ayant participé à plus de 3 événements.
9. Calculer le délai moyen de paiement dans `compteB`.
10. Joindre les tables `membre` et `inscription` pour lister les membres avec leurs dates d'inscription.
11. Trouver les types de règlements les plus utilisés.
12. Afficher les événements avec leur lieu et leur nombre maximal de joueurs.

---

Si tu veux, je peux aussi préparer un fichier téléchargeable, des corrigés, ou même un jeu de données d'exemple pour t'entraîner ! Dis-moi.
