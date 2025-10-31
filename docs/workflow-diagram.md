# Flux de Travail - Système de Gestion de Bibliothèque Universitaire

## 1. Processus d'Emprunt de Livre

```
[DÉBUT] 
    ↓
[Utilisateur recherche un livre]
    ↓
[Livre disponible ?] ----NON---→ [Proposer réservation]
    ↓ OUI                              ↓
[Vérifier profil utilisateur]          [Processus de réservation]
    ↓                                   ↓
[Quota atteint ?] ----OUI---→ [Refuser emprunt] → [FIN]
    ↓ NON
[Amendes impayées ?] ----OUI---→ [Demander paiement] → [FIN]
    ↓ NON
[Enregistrer emprunt]
    ↓
[Calculer date d'échéance]
    ↓
[Mettre à jour stock livre]
    ↓
[Imprimer reçu/notification]
    ↓
[FIN]
```

## 2. Processus de Retour de Livre

```
[DÉBUT]
    ↓
[Scanner/Saisir ID livre]
    ↓
[Identifier l'emprunt]
    ↓
[Emprunt trouvé ?] ----NON---→ [Erreur : Emprunt non trouvé] → [FIN]
    ↓ OUI
[Vérifier état du livre]
    ↓
[Livre endommagé ?] ----OUI---→ [Calculer amende dégât]
    ↓ NON                           ↓
[Retour dans les délais ?] ----NON---→ [Calculer amende retard]
    ↓ OUI                           ↓
[Enregistrer retour]              [Enregistrer amende]
    ↓                               ↓
[Mettre à jour stock] ←-----------←
    ↓
[Vérifier liste d'attente]
    ↓
[Réservation en attente ?] ----OUI---→ [Notifier utilisateur]
    ↓ NON                              ↓
[Livre disponible pour emprunt] ←-----←
    ↓
[FIN]
```

## 3. Processus de Réservation

```
[DÉBUT]
    ↓
[Utilisateur sélectionne livre]
    ↓
[Livre disponible ?] ----OUI---→ [Suggérer emprunt direct] → [FIN]
    ↓ NON
[Vérifier profil utilisateur]
    ↓
[Utilisateur éligible ?] ----NON---→ [Refuser réservation] → [FIN]
    ↓ OUI
[Réservation existante ?] ----OUI---→ [Informer position dans queue] → [FIN]
    ↓ NON
[Enregistrer réservation]
    ↓
[Calculer priorité]
    ↓
[Ajouter à la queue]
    ↓
[Définir date d'expiration]
    ↓
[Confirmer réservation]
    ↓
[FIN]
```

## 4. Processus de Gestion des Amendes

```
[DÉBUT : Vérification quotidienne]
    ↓
[Identifier emprunts en retard]
    ↓
[Pour chaque emprunt en retard]
    ↓
[Calculer jours de retard]
    ↓
[Calculer montant amende]
    ↓
[Créer/Mettre à jour amende]
    ↓
[Envoyer notification utilisateur]
    ↓
[Amende > seuil suspension ?] ----OUI---→ [Suspendre compte]
    ↓ NON                                  ↓
[Emprunt suivant] ←-----------------------←
    ↓
[Tous traités ?] ----NON---→ [Emprunt suivant]
    ↓ OUI
[Générer rapport amendes]
    ↓
[FIN]
```

## 5. Processus d'Inscription Utilisateur

```
[DÉBUT]
    ↓
[Saisir informations personnelles]
    ↓
[Valider format données]
    ↓
[Données valides ?] ----NON---→ [Afficher erreurs] → [Corriger]
    ↓ OUI                                              ↑
[Vérifier email unique] ←---------------------------------
    ↓
[Email existant ?] ----OUI---→ [Erreur : Email déjà utilisé] → [FIN]
    ↓ NON
[Assigner numéro utilisateur]
    ↓
[Définir quotas selon type]
    ↓
[Créer compte utilisateur]
    ↓
[Envoyer email confirmation]
    ↓
[Activer compte]
    ↓
[FIN]
```

## 6. Processus de Recherche de Livre

```
[DÉBUT]
    ↓
[Saisir critères de recherche]
    ↓
[Type de recherche ?]
    ↓
[Titre] → [Rechercher par titre]
    ↓
[Auteur] → [Rechercher par auteur]
    ↓
[ISBN] → [Rechercher par ISBN]
    ↓
[Catégorie] → [Rechercher par catégorie]
    ↓
[Recherche avancée] → [Combiner critères]
    ↓
[Exécuter requête]
    ↓
[Résultats trouvés ?] ----NON---→ [Suggérer recherche alternative]
    ↓ OUI                          ↓
[Trier résultats]                [FIN]
    ↓
[Afficher disponibilité]
    ↓
[Proposer actions : Emprunter/Réserver]
    ↓
[FIN]
```

## États des Entités Principales

### États d'un Livre
- **Disponible** : Peut être emprunté
- **Emprunté** : En cours d'emprunt
- **Réservé** : Livre rendu mais réservé
- **Maintenance** : En réparation/reliure
- **Retiré** : Plus disponible

### États d'un Emprunt
- **Actif** : En cours
- **En retard** : Dépassé la date d'échéance
- **Rendu** : Retourné à temps
- **Rendu en retard** : Retourné après échéance
- **Perdu** : Déclaré perdu

### États d'une Réservation
- **Active** : En attente
- **Notifiée** : Utilisateur prévenu
- **Expirée** : Délai de récupération dépassé
- **Satisfaite** : Livre emprunté
- **Annulée** : Annulée par l'utilisateur

### États d'un Utilisateur
- **Actif** : Peut emprunter
- **Suspendu** : Temporairement bloqué
- **Bloqué** : Définitivement bloqué
- **Diplômé** : Ancien étudiant (accès limité)