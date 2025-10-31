# Modèle Conceptuel - Système de Gestion de Bibliothèque Universitaire

## Entités Principales

### 1. **UTILISATEUR** (User)
- **Attributs :**
  - ID utilisateur (clé primaire)
  - Numéro étudiant/personnel
  - Nom, Prénom
  - Email, Téléphone
  - Type d'utilisateur (étudiant, professeur, personnel, admin)
  - Département
  - Statut (actif, suspendu, diplômé)
  - Nombre maximum de livres autorisés

### 2. **LIVRE** (Book)
- **Attributs :**
  - ID livre (clé primaire)
  - ISBN
  - Titre, Sous-titre
  - Auteur, Éditeur
  - Année de publication, Édition
  - Catégorie, Localisation
  - Nombre total d'exemplaires
  - Nombre d'exemplaires disponibles

### 3. **CATÉGORIE** (Category)
- **Attributs :**
  - ID catégorie (clé primaire)
  - Nom de la catégorie
  - Code catégorie
  - Description
  - Catégorie parent (hiérarchie)

### 4. **DÉPARTEMENT** (Department)
- **Attributs :**
  - ID département (clé primaire)
  - Nom du département
  - Code département
  - Faculté
  - Responsable du département

## Relations Principales

### 1. **EMPRUNTER** (Borrowing)
- **Relation :** Utilisateur ↔ Livre (N:M)
- **Attributs :**
  - Date d'emprunt
  - Date d'échéance
  - Date de retour
  - Statut (actif, rendu, en retard, perdu)
  - Nombre de renouvellements
  - Montant de l'amende

### 2. **RÉSERVER** (Reservation)
- **Relation :** Utilisateur ↔ Livre (N:M)
- **Attributs :**
  - Date de réservation
  - Date d'expiration
  - Statut (active, satisfaite, annulée, expirée)
  - Niveau de priorité

### 3. **APPARTIENT À** (Belongs to)
- **Relation :** Livre → Catégorie (N:1)

### 4. **MEMBRE DE** (Member of)
- **Relation :** Utilisateur → Département (N:1)

### 5. **AMENDE** (Fine)
- **Relation :** Utilisateur ↔ Emprunt (1:N)
- **Attributs :**
  - Type d'amende (retard, dégât, perte)
  - Montant
  - Date d'émission
  - Date de paiement
  - Statut (en attente, payée, annulée)

## Règles de Gestion

### Contraintes d'Intégrité
1. Un utilisateur ne peut pas emprunter plus que son quota autorisé
2. Un livre ne peut être emprunté que s'il y a des exemplaires disponibles
3. Une réservation expire automatiquement après 7 jours
4. Un utilisateur avec des amendes impayées ne peut pas emprunter
5. La durée d'emprunt varie selon le type d'utilisateur :
   - Étudiants : 14 jours
   - Professeurs/Personnel : 30 jours
   - Administrateurs : 60 jours

### Règles Métier
1. **Emprunt :** Un utilisateur peut renouveler un livre 2 fois maximum
2. **Réservation :** Seuls les livres non disponibles peuvent être réservés
3. **Amendes :** 1€/jour de retard, 50€ pour un livre perdu
4. **Priorité :** Les professeurs ont la priorité sur les réservations
5. **Suspension :** Un utilisateur avec plus de 30€ d'amendes est suspendu

## Diagramme Entité-Association (Textuel)

```
UTILISATEUR (1,N) ----EMPRUNTER---- (0,N) LIVRE
    |                                    |
    |                                    |
(N,1)|                                (N,1)|
DÉPARTEMENT                         CATÉGORIE
    |                                    |
    |                                    |
UTILISATEUR (1,N) ----RÉSERVER----- (0,N) LIVRE
    |                                    
    |                                    
(1,N)|                                
AMENDE                               
```

## Types d'Utilisateurs et Privilèges

### Étudiant
- Emprunter jusqu'à 5 livres
- Durée : 14 jours
- Renouvellement : 2 fois
- Réserver des livres

### Professeur/Personnel
- Emprunter jusqu'à 10 livres
- Durée : 30 jours
- Renouvellement : 3 fois
- Priorité sur les réservations

### Administrateur
- Accès complet au système
- Gestion des utilisateurs et des livres
- Génération de rapports
- Gestion des amendes