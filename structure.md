# 📊 Aide visuelle : Tables importantes et leur structure

Voici un résumé des tables clés et de leurs colonnes principales pour t'aider à visualiser la base.

---

### 🏦 **Table `2024_compteA`**

| Colonne         | Description             |
| --------------- | ----------------------- |
| numero\_membre  | Identifiant du membre   |
| manifestation   | Manifestation liée      |
| titre           | Titre de l'écriture     |
| date\_ecriture  | Date de l'écriture      |
| type\_reglement | Type de règlement       |
| montant         | Montant payé            |
| ref\_reglement  | Référence du règlement  |
| caddie          | Info caddie             |
| commentaire     | Commentaire             |
| lettrage        | Code lettrage comptable |

---

### 🏦 **Table `2024_compteB`**

| Colonne         | Description             |
| --------------- | ----------------------- |
| numero          | Numéro unique           |
| numero\_membre  | Identifiant du membre   |
| manifestation   | Manifestation liée      |
| evenement       | Événement lié           |
| titre           | Titre de l'achat        |
| taille          | Taille de l'article     |
| quantite        | Quantité achetée        |
| date\_achat     | Date d'achat            |
| date\_reglement | Date de règlement       |
| type\_reglement | Type de paiement        |
| montant         | Montant total           |
| prix\_unitaire  | Prix par unité          |
| ref\_reglement  | Référence du paiement   |
| caddie          | Info caddie             |
| commentaire     | Commentaire             |
| lettrage        | Code lettrage comptable |

---

### 🏆 **Table `2024_equipe`**

| Colonne        | Description          |
| -------------- | -------------------- |
| numero         | Identifiant équipe   |
| manifestation  | Manifestation liée   |
| evenement      | Événement            |
| capitaine      | ID du capitaine      |
| equipier       | ID de l'équipier     |
| type\_joueur   | Type (simple/double) |
| nom\_equipe    | Nom de l'équipe      |
| numero\_equipe | Numéro d'équipe      |
| lettre\_tni    | Lettre TNI           |
| valide         | Validation (oui/non) |

---

### 📅 **Table `2024_evenement`**

| Colonne                      | Description             |
| ---------------------------- | ----------------------- |
| numero                       | Identifiant événement   |
| manifestation                | Manifestation liée      |
| formule                      | Formule de jeu          |
| lieu                         | Lieu                    |
| date\_debut                  | Date de début           |
| heure\_debut                 | Heure de début          |
| ouvert                       | Statut d'ouverture      |
| couta, coutb, cout\_surplace | Coûts                   |
| nbr\_joueur\_max             | Max joueurs             |
| nbr\_joueur\_equipe          | Max joueurs par équipe  |
| remplacant                   | Acceptation remplaçants |

---

### 📝 **Table `2024_inscription`**

| Colonne                  | Description               |
| ------------------------ | ------------------------- |
| numero                   | Identifiant inscription   |
| manifestation            | Manifestation liée        |
| evenement                | Événement                 |
| numero\_membre           | Membre inscrit            |
| type\_equipier           | Type d'équipier           |
| date\_inscription        | Date d'inscription        |
| validation\_membre       | Validation par le membre  |
| date\_validation\_membre | Date de validation membre |
| validation\_assgf        | Validation par l'asso     |
| date\_validation\_assgf  | Date de validation asso   |
| attente                  | En attente ?              |
| inscrit\_par\_un\_autre  | Inscription par tiers ?   |

---

### 📣 **Table `2024_manifestation`**

| Colonne                | Description               |
| ---------------------- | ------------------------- |
| numero                 | Identifiant manifestation |
| date\_debut            | Date de début             |
| date\_fin              | Date de fin               |
| libelle                | Nom/titre                 |
| nature                 | Nature/Type               |
| capitaine, capitaine2  | Responsables              |
| inscription\_ouverte   | Ouverture inscription     |
| visible\_site          | Visible sur site ?        |
| region, club           | Région, Club associés     |
| index\_min, index\_max | Index minimum/maximum     |
| droit\_inscription     | Droit d'inscription       |
| nbr\_equipe            | Nombre d'équipes          |

---

### 👤 **Table `membre`**

| Colonne              | Description         |
| -------------------- | ------------------- |
| numero               | Identifiant membre  |
| nom, prenom          | Nom, Prénom         |
| licence              | Numéro de licence   |
| club\_lic            | Club d'affiliation  |
| FFGindex             | Index officiel      |
| date\_maj            | Date de mise à jour |
| date\_cnx            | Dernière connexion  |
| email\_personnel     | Email personnel     |
| tel\_mobile          | Téléphone mobile    |
| adresse, ville, pays | Adresse complète    |

---

