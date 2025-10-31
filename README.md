# Système de Gestion de Bibliothèque Universitaire

## Description

Système complet de gestion pour une bibliothèque universitaire permettant la gestion des livres, des utilisateurs, des emprunts, des réservations et des amendes.

## Fonctionnalités Principales

### Pour les Utilisateurs
- 📚 Recherche et consultation du catalogue
- 📖 Emprunt et renouvellement de livres
- 🔖 Réservation de livres non disponibles
- 👤 Gestion du profil personnel
- 📊 Historique des emprunts
- 💰 Consultation des amendes

### Pour les Administrateurs
- 📋 Gestion complète du catalogue
- 👥 Gestion des utilisateurs et départements
- 📈 Rapports et statistiques
- ⚙️ Configuration du système
- 💸 Gestion des amendes et paiements

## Architecture du Système

### Technologies
- **Backend :** Node.js + Express.js
- **Frontend :** React.js
- **Base de données :** MySQL/PostgreSQL
- **Authentification :** JWT

### Structure
```
├── docs/           # Documentation complète
├── backend/        # API et logique serveur
├── frontend/       # Interface utilisateur
├── database/       # Scripts et migrations
└── scripts/        # Utilitaires
```

## Documentation

- [📋 Schéma de Base de Données](docs/database-schema.md)
- [🎯 Modèle Conceptuel](docs/conceptual-model.md)
- [🔄 Flux de Travail](docs/workflow-diagram.md)
- [🏗️ Structure du Projet](docs/project-structure.md)

## Installation et Configuration

### Prérequis
- Node.js (v16+)
- MySQL/PostgreSQL
- Git

### Installation
```bash
# Cloner le repository
git clone https://github.com/Amine-Charrou/library-management-system.git
cd library-management-system

# Installer les dépendances
npm install

# Configuration de la base de données
# (Voir docs/database-schema.md)

# Lancer l'application
npm run dev
```

## Équipe de Développement

### Rôles Suggérés
- **Chef de Projet :** Coordination et planification
- **Développeur Backend :** API et base de données
- **Développeur Frontend :** Interface utilisateur
- **Testeur/QA :** Tests et qualité
- **Designer :** UI/UX et maquettes

### Workflow de Développement
1. **Créer une branche** pour chaque fonctionnalité
2. **Développer** et tester localement
3. **Pull Request** avec description détaillée
4. **Review** par un autre membre de l'équipe
5. **Merge** après validation

## Phases de Développement

- [ ] **Phase 1 :** Configuration et authentification
- [ ] **Phase 2 :** Gestion des livres et catalogue
- [ ] **Phase 3 :** Système d'emprunt et retour
- [ ] **Phase 4 :** Réservations et amendes
- [ ] **Phase 5 :** Rapports et administration
- [ ] **Phase 6 :** Tests et déploiement

## Contribution

1. Forker le projet
2. Créer une branche feature (`git checkout -b feature/nouvelle-fonctionnalite`)
3. Commiter les changements (`git commit -m 'Ajout nouvelle fonctionnalité'`)
4. Pousser vers la branche (`git push origin feature/nouvelle-fonctionnalite`)
5. Ouvrir une Pull Request

## Conventions

- **Commits :** Messages en français, clairs et descriptifs
- **Branches :** `feature/nom-fonctionnalite`, `bugfix/nom-bug`
- **Code :** Commentaires en français, noms de variables explicites
- **Documentation :** Maintenir à jour avec les changements

## Licence

Projet académique - Université

---

**Note :** Ce projet est développé dans le cadre d'un travail universitaire collaboratif. Tous les membres de l'équipe sont encouragés à contribuer et à apprendre ensemble.

## Contact

Pour toute question ou suggestion, n'hésitez pas à créer une issue ou contacter l'équipe de développement.

---

*Dernière mise à jour : Octobre 2025*