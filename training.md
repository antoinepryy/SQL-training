# 12 Nouveaux Exercices SQL et Corrigés

## Exercice 1

Lister les manifestations visibles sur le site.

```sql
SELECT numero, libelle FROM manifestation WHERE visible_site = 1;
```

## Exercice 2

Afficher les membres qui ont un index inférieur à 10.

```sql
SELECT numero, nom, prenom, FFGindex FROM membre WHERE FFGindex < 10;
```

## Exercice 3

Trouver les événements organisés dans un lieu spécifique (par exemple "Paris").

```sql
SELECT numero, formule FROM evenement WHERE lieu = 'Paris';
```

## Exercice 4

Lister les dotations supérieures à 500€.

```sql
SELECT numero, titre, montant FROM dotation WHERE montant > 500;
```

## Exercice 5

Compter le nombre total de membres par club.

```sql
SELECT club_lic, COUNT(*) AS nb_membres FROM membre GROUP BY club_lic;
```

## Exercice 6

Afficher les événements qui ont atteint leur nombre maximum de joueurs inscrits.

```sql
SELECT e.numero, e.formule
FROM evenement e
JOIN (SELECT evenement, COUNT(DISTINCT numero_membre) AS nb_inscrits FROM inscription GROUP BY evenement) AS insc
ON e.numero = insc.evenement
WHERE insc.nb_inscrits >= e.nbr_joueur_max;
```

## Exercice 7

Lister les membres qui n'ont jamais payé (aucune ligne dans compteA).

```sql
SELECT m.numero, m.nom, m.prenom
FROM membre m
LEFT JOIN compteA c ON m.numero = c.numero_membre
WHERE c.numero_membre IS NULL;
```

## Exercice 8

Afficher les événements avec un coût sur place supérieur au coût anticipé (`cout_surplace > couta`).

```sql
SELECT numero, formule, couta, cout_surplace
FROM evenement
WHERE cout_surplace > couta;
```

## Exercice 9

Trouver les membres qui ont payé avec plusieurs types de règlements différents.

```sql
SELECT numero_membre, COUNT(DISTINCT type_reglement) AS nb_types
FROM compteA
GROUP BY numero_membre
HAVING nb_types > 1;
```

## Exercice 10

Afficher les capitaines et le nombre d'équipes qu'ils dirigent.

```sql
SELECT capitaine, COUNT(*) AS nb_equipes
FROM equipe
GROUP BY capitaine;
```

## Exercice 11

Lister les événements ouverts aux remplaçants.

```sql
SELECT numero, formule FROM evenement WHERE remplacant = 1;
```

## Exercice 12

Afficher les membres avec leur dernier accès (date de connexion).

```sql
SELECT numero, nom, prenom, date_cnx FROM membre ORDER BY date_cnx DESC;
```

Si tu veux, je peux générer un pack complet d’exercices avancés avec CTE, fenêtres (`window functions`), vues, ou même déclencheurs pour aller encore plus loin ! Dis-moi.
