# Corrigés des Exercices SQL

## Exercice 1

Lister tous les membres avec leur nom et club.

```sql
SELECT numero, nom, prenom, club_lic FROM membre;
```

## Exercice 2

Afficher tous les événements après le 1er janvier 2025.

```sql
SELECT * FROM evenement WHERE date_debut > '2025-01-01';
```

## Exercice 3

Trouver tous les paiements supérieurs à 200€ dans `compteA`.

```sql
SELECT * FROM compteA WHERE montant > 200;
```

## Exercice 4

Compter combien d'inscriptions chaque événement a.

```sql
SELECT evenement, COUNT(*) AS nb_inscriptions FROM inscription GROUP BY evenement;
```

## Exercice 5

Afficher le montant total dépensé par membre (`compteB`).

```sql
SELECT numero_membre, SUM(montant) AS total_depense FROM compteB GROUP BY numero_membre;
```

## Exercice 6

Lister les événements avec moins de 10 inscriptions.

```sql
SELECT evenement, COUNT(*) AS nb_inscriptions
FROM inscription
GROUP BY evenement
HAVING nb_inscriptions < 10;
```

## Exercice 7

Obtenir les 5 membres qui ont payé le plus dans `compteA`.

```sql
SELECT numero_membre, SUM(montant) AS total_paye
FROM compteA
GROUP BY numero_membre
ORDER BY total_paye DESC
LIMIT 5;
```

## Exercice 8

Trouver les membres ayant participé à plus de 3 événements.

```sql
SELECT numero_membre, COUNT(DISTINCT evenement) AS nb_evenements
FROM inscription
GROUP BY numero_membre
HAVING nb_evenements > 3;
```

## Exercice 9

Calculer le délai moyen de paiement dans `compteB`.

```sql
SELECT AVG(DATEDIFF(date_reglement, date_achat)) AS delai_moyen
FROM compteB
WHERE date_reglement IS NOT NULL AND date_achat IS NOT NULL;
```

## Exercice 10

Joindre les tables `membre` et `inscription` pour lister les membres avec leurs dates d'inscription.

```sql
SELECT m.numero, m.nom, m.prenom, i.date_inscription
FROM membre m
JOIN inscription i ON m.numero = i.numero_membre;
```

## Exercice 11

Trouver les types de règlements les plus utilisés.

```sql
SELECT type_reglement, COUNT(*) AS nb_utilisation
FROM compteA
GROUP BY type_reglement
ORDER BY nb_utilisation DESC;
```

## Exercice 12

Afficher les événements avec leur lieu et leur nombre maximal de joueurs.

```sql
SELECT e.numero, e.formule, e.lieu, e.nbr_joueur_max
FROM evenement e;
```

