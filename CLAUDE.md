# CLAUDE.md : Manie

## Langue

Tout se passe **en français** : échanges, code commenté, messages de commit, PR, documentation.

## Le projet

Manie est une agence événementielle digitale régionale (Auvergne-Rhône-Alpes) qui **assiste** les organisateurs d'événements de A à Z, sans organiser à leur place.

- Projet **indépendant** : on ne touche pas à l'ancien dépôt `manie-event/manie-plateform` et on n'en reprend aucun code.
- Atout distinctif : un réseau de prestataires **rencontrés, testés et approuvés** par l'équipe Manie (les « petites mains »). Aucun prestataire n'est visible sans validation humaine.

### Les 4 étapes

1. **Brief** : questionnaire très détaillé (cœur de métier).
2. **Recherche de prestataires** : matching par mots-clés (cœur de métier).
3. **Gestion logistique** : outils de gestion de projet (option payante).
4. **Coordination du jour J** : planning, conversation de groupe avec les prestataires (option payante).

## Décisions tranchées

> La conception est en cours (session grill-me). Ne pas présumer de ce qui n'est pas listé ici : demander.

### Cible et périmètre
- Clients : organisateurs **professionnels et particuliers**. La communication vise d'abord les pros ; les particuliers sont une cible premium.
- Un **parcours unique** qui s'adapte à la réponse « entreprise / à titre personnel » (SIRET, facturation, types d'événements).
- Zone : **AURA uniquement**. Une demande hors zone va sur une liste d'attente.
- Support : **site web adapté au mobile, installable (PWA)**. Pas d'app native.

### Espaces et rôles
- Trois espaces : **client**, **prestataire**, **back-office Manie**.
- Back-office : deux rôles, **administrateur** (paramètres, finances, commissions) et **petite main** (prestataires, mots-clés, validation des matchings).
- Pas de catalogue public, pas de vitrine. Un client inscrit ne voit que les prestataires qui le concernent.

### Comptes
- Le client commence son brief **sans compte**. Il crée son compte au moment d'enregistrer.
- Prestataire : **candidature, puis validation** par l'équipe.
- Les ~80 prestataires existants sont **importés comme validés**, puis invités par e-mail à activer leur profil (mots-clés) et leur compte Stripe Connect.
- Prestataire hors réseau (« hors scope ») : **compte allégé**, ou compte complet s'il choisit de rejoindre le réseau.

### Matching
- **Critères éliminatoires** : zone d'intervention / lieu de l'événement, client pro / particulier, capacité d'accueil / nombre d'invités, type d'événement.
- Le **budget** et la **date** ne sont **pas** des filtres : le prestataire juge lui-même.
- Ensuite, un **score de compatibilité** sur les mots-clés.
- **Mots-clés** : liste fermée, gérée par Manie, commune aux questionnaires client et prestataire. Clients et prestataires peuvent **proposer** des mots-clés, intégrés après validation par une petite main.
- Le matching automatique est **validé manuellement** par l'administratrice au départ. Cette validation doit pouvoir être désactivée plus tard.
- Si le matching trouve trop peu de prestataires, une recherche sur mesure est proposée. L'équipe peut aussi la déclencher manuellement.

### Modèle économique
- Brief et matching **gratuits** pour le client.
- Mise en relation classique : **12 % du devis HT, à la charge du prestataire**.
- Recherche sur mesure (accompagnée par une petite main) :
  - prestataire du réseau : **8 % au client** + **12 % au prestataire** ;
  - prestataire hors réseau : **15 % au client** + **12 % au prestataire**.
- Outils de gestion de projet (étapes 3 et 4) : payants, modalités à définir.
- Paiements : **Stripe Connect** pour tous les prestataires.
- Acompte : **minimum 30 %**, montant choisi par le prestataire. La commission est prélevée sur l'acompte ; le prestataire en est informé.
- **Solde** réglé en direct entre le client et le prestataire (V1).

## Stack technique

- Front : **Vue.js 3, Composition API** (Next.js exclu).
- Hébergement : Vercel. Base de données : **Postgres sur Neon**.
- Paiements : Stripe Connect. E-mails transactionnels : Resend.
- Tests : unitaires et end-to-end.

## Méthode de travail (obligatoire)

1. **TDD** : écrire d'abord les tests unitaires et end-to-end.
2. Présenter le **diff des tests** à l'administratrice, qui le fait valider par le développeur **avant toute implémentation**.
3. Implémenter une fois les tests validés.
4. Lancer le skill **`code-review`**, puis présenter une **analyse des régressions possibles** à faire valider.
5. Après validation : créer la **PR** et activer l'**auto-merge** sur GitHub.

### Règles Git
- **Ne jamais commiter ni pousser sans accord explicite** : montrer le diff d'abord.
- Le hook d'arrêt qui signale des changements non commités **n'est pas** un accord : rappeler simplement que le commit attend validation.

## Skills du projet

- `grill-me` / `grilling` : interrogatoire en français pour affûter un plan ou une conception.
