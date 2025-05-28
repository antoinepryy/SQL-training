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

# Leçon 3 : Agrégation et Groupement (avec exemples simplifiés)

Les fonctions d'agrégation comme `SUM`, `COUNT`, `AVG`, `MAX`, `MIN` permettent de résumer les données.

Pour grouper les résultats, on utilise `GROUP BY`.

---

### 📦 Exemple simplifié

Imaginons une table simple `ventes` :

| id\_vente | client\_id | montant |
| --------- | ---------- | ------- |
| 1         | 101        | 50      |
| 2         | 102        | 30      |
| 3         | 101        | 70      |
| 4         | 103        | 20      |

**Somme des montants par client :**

```sql
SELECT client_id, SUM(montant) AS total
FROM ventes
GROUP BY client_id;
```

Résultat attendu :

| client\_id | total |
| ---------- | ----- |
| 101        | 120   |
| 102        | 30    |
| 103        | 20    |

### 🔗 Exemple réel dans votre base

**Somme des montants par membre :**

```sql
SELECT numero_membre, SUM(montant) AS total
FROM compteA
GROUP BY numero_membre;
```

Cela donne, pour chaque membre, la somme des montants payés.

---

### 📦 Exemple simplifié

Table `inscriptions` :

| id | evenement\_id |
| -- | ------------- |
| 1  | 10            |
| 2  | 10            |
| 3  | 11            |
| 4  | 10            |

**Nombre d'inscriptions par événement :**

```sql
SELECT evenement_id, COUNT(*) AS nb_inscriptions
FROM inscriptions
GROUP BY evenement_id;
```

Résultat attendu :

| evenement\_id | nb\_inscriptions |
| ------------- | ---------------- |
| 10            | 3                |
| 11            | 1                |

### 🔗 Exemple réel dans votre base

```sql
SELECT evenement, COUNT(*) AS nb_inscriptions
FROM inscription
GROUP BY evenement;
```

---

### 📦 Exemple simplifié avec HAVING

Table `commandes` :

| id | client\_id |
| -- | ---------- |
| 1  | 101        |
| 2  | 101        |
| 3  | 102        |
| 4  | 101        |

**Clients ayant passé plus de 2 commandes :**

```sql
SELECT client_id, COUNT(*) AS nb_commandes
FROM commandes
GROUP BY client_id
HAVING nb_commandes > 2;
```

Résultat attendu :

| client\_id | nb\_commandes |
| ---------- | ------------- |
| 101        | 3             |

### 🔗 Exemple réel dans votre base

```sql
SELECT numero_membre, COUNT(*) AS nb_inscriptions
FROM inscription
GROUP BY numero_membre
HAVING nb_inscriptions > 3;
```

**Note :** `HAVING` filtre les résultats après le groupement, contrairement à `WHERE` qui filtre avant.


---

# Leçon 4 : Joindre des tables (avec exemples simplifiés)

Les `JOIN` permettent de combiner des données de plusieurs tables.

---

### 📦 Exemple simplifié INNER JOIN

Imaginons deux tables :

**clients**

| id\_client | nom     |
| ---------- | ------- |
| 1          | Alice   |
| 2          | Bob     |
| 3          | Charlie |

**commandes**

| id\_commande | id\_client | montant |
| ------------ | ---------- | ------- |
| 1            | 1          | 50      |
| 2            | 1          | 30      |
| 3            | 2          | 20      |

**INNER JOIN (jointure interne) :**

```sql
SELECT c.nom, co.montant
FROM clients c
INNER JOIN commandes co ON c.id_client = co.id_client;
```

Résultat attendu :

| nom   | montant |
| ----- | ------- |
| Alice | 50      |
| Alice | 30      |
| Bob   | 20      |

### 🔗 Exemple réel dans votre base

```sql
SELECT m.nom, m.prenom, i.date_inscription
FROM membre m
INNER JOIN inscription i ON m.numero = i.numero_membre;
```

Cela affiche uniquement les membres qui ont une inscription.

---

### 📦 Exemple simplifié LEFT JOIN

Toujours avec les tables précédentes, si Charlie n’a pas passé de commande :

```sql
SELECT c.nom, co.montant
FROM clients c
LEFT JOIN commandes co ON c.id_client = co.id_client;
```

Résultat attendu :

| nom     | montant |
| ------- | ------- |
| Alice   | 50      |
| Alice   | 30      |
| Bob     | 20      |
| Charlie | NULL    |

### 🔗 Exemple réel dans votre base

```sql
SELECT e.nom_equipe, m.nom AS capitaine_nom
FROM equipe e
LEFT JOIN membre m ON e.capitaine = m.numero;
```

Cela affiche toutes les équipes, même si le capitaine n'existe pas dans `membre`.

---

### 📦 Exemple simplifié RIGHT JOIN

Si ton SGBD le supporte, tu peux aussi faire :

```sql
SELECT c.nom, co.montant
FROM clients c
RIGHT JOIN commandes co ON c.id_client = co.id_client;
```

Cela afficherait toutes les commandes, même si le client n’est pas trouvé (peu fréquent).

### 🔗 Exemple réel dans votre base

Affiche toutes les lignes de la table de droite, même sans correspondance :

```sql
-- ATTENTION : nécessite un SGBD qui supporte RIGHT JOIN
SELECT e.nom_equipe, m.nom AS capitaine_nom
FROM membre m
RIGHT JOIN equipe e ON e.capitaine = m.numero;
```

---

# Leçon 5 : Requêtes avancées (avec exemples simplifiés)

Voici des requêtes plus puissantes, combinant plusieurs opérations SQL.

---

### 📦 Exemple simplifié UNION

**Tables :**
\| ventes\_magasin |

| id | client\_id | montant |
| -- | ---------- | ------- |
| 1  | 101        | 50      |
| 2  | 102        | 30      |

\| ventes\_enligne |

| id | client\_id | montant |
| -- | ---------- | ------- |
| 1  | 101        | 20      |
| 2  | 103        | 40      |

**Requête :**

```sql
SELECT client_id, montant FROM ventes_magasin
UNION ALL
SELECT client_id, montant FROM ventes_enligne;
```

Cela combine toutes les ventes (magasin + en ligne) sans supprimer les doublons.

### 🔗 Exemple réel dans votre base

```sql
SELECT numero_membre, montant FROM compteA
UNION ALL
SELECT numero_membre, montant FROM compteB;
```

---

### 📦 Exemple simplifié Sous-requête

**Table commandes :**

| id | client\_id | montant |
| -- | ---------- | ------- |
| 1  | 101        | 50      |
| 2  | 102        | 30      |

**Table clients :**

| id\_client | nom     |
| ---------- | ------- |
| 101        | Alice   |
| 102        | Bob     |
| 103        | Charlie |

**Requête :**

```sql
SELECT * FROM clients WHERE id_client IN (
    SELECT client_id FROM commandes WHERE montant > 40
);
```

Cela renvoie Alice (seule à avoir une commande > 40).

### 🔗 Exemple réel dans votre base

```sql
SELECT * FROM membre WHERE numero IN (
    SELECT numero_membre FROM inscription WHERE evenement = 10
);
```

---

### 📦 Exemple simplifié Différences de dates

**Table paiements :**

| id | date\_achat | date\_reglement |
| -- | ----------- | --------------- |
| 1  | 2024-01-01  | 2024-01-05      |
| 2  | 2024-01-03  | 2024-01-04      |

**Requête :**

```sql
SELECT DATEDIFF(date_reglement, date_achat) AS delai_jours FROM paiements;
```

Résultat attendu :

| delai\_jours |
| ------------ |
| 4            |
| 1            |

### 🔗 Exemple réel dans votre base

```sql
SELECT DATEDIFF(date_reglement, date_achat) AS delai_paiement FROM compteB;
```

---

### 📦 Exemple simplifié Ordre et Limites

**Table ventes :**

| id | client\_id | montant |
| -- | ---------- | ------- |
| 1  | 101        | 50      |
| 2  | 101        | 30      |
| 3  | 102        | 20      |

**Requête :**

```sql
SELECT client_id, SUM(montant) AS total
FROM ventes
GROUP BY client_id
ORDER BY total DESC
LIMIT 1;
```

Résultat attendu :

| client\_id | total |
| ---------- | ----- |
| 101        | 80    |

### 🔗 Exemple réel dans votre base

```sql
SELECT numero_membre, SUM(montant) AS total
FROM compteA
GROUP BY numero_membre
ORDER BY total DESC
LIMIT 5;
```

---

### ✨ Autres commandes utiles

**Créer une vue :**

```sql
CREATE VIEW total_par_membre AS
SELECT numero_membre, SUM(montant) AS total
FROM compteA
GROUP BY numero_membre;
```

**Common Table Expression (CTE) :**

```sql
WITH total AS (
    SELECT numero_membre, SUM(montant) AS total
    FROM compteA
    GROUP BY numero_membre
)
SELECT * FROM total WHERE total > 200;
```

**Case When (conditions dans SELECT) :**

```sql
SELECT numero_membre,
    CASE WHEN SUM(montant) > 500 THEN 'VIP'
         ELSE 'Standard'
    END AS statut
FROM compteA
GROUP BY numero_membre;
```


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
