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

### Parcours en appel d'offres
1. Le client crée son brief, puis le **publie** sur Manie.
2. Le matching calcule les prestataires compatibles. L'administratrice **valide la liste avant l'envoi** des notifications. Le client voit le statut « Publié, en cours de diffusion ».
3. Les **6 prestataires les plus compatibles par catégorie** (au-dessus d'un seuil réglable dans le back-office) sont notifiés.
4. Un prestataire intéressé se positionne sous **5 jours** avec une fourchette de prix, une description et une confirmation de disponibilité à la date (case obligatoire).
5. Le client reçoit **3 propositions au maximum par catégorie** (les premières arrivées). Les prestataires suivants sont prévenus que l'appel d'offres est complet.
6. Le client accepte ou refuse chaque proposition. S'il accepte, la **mise en relation** est créée et **horodatée**, les **coordonnées sont dévoilées** des deux côtés et une **messagerie interne** s'ouvre.
7. Le prestataire **dépose le PDF du devis et saisit le montant HT**. Le client coche une attestation sur l'honneur, valide, puis paie l'acompte sur Stripe.
- Relances automatiques sur l'avancement de la mise en relation (« Avez-vous signé ? »).
- Pas de correspondance : le client remplit un **formulaire de recherche sur mesure**, qui crée un dossier assigné à une petite main dans le back-office.

### Modèle économique
- Brief et matching **gratuits** pour le client.
- Mise en relation classique : **12 % du devis HT, à la charge du prestataire**.
- Recherche sur mesure (accompagnée par une petite main) :
  - prestataire du réseau : **8 % au client** + **12 % au prestataire** ;
  - prestataire hors réseau : **15 % au client** + **12 % au prestataire**.
- Outils de gestion de projet (étapes 3 et 4) : payants, modalités à définir.
- Paiements : **Stripe Connect** pour tous les prestataires.
- Acompte : **minimum 30 %**, montant choisi par le prestataire. La commission est prélevée sur l'acompte ; le prestataire en est informé.
- Le client paie l'acompte (et, pour une recherche sur mesure, les frais client de 8 % ou 15 %) en **un seul paiement Stripe**. La commission est prélevée et le **reste est reversé immédiatement** au prestataire. Aucune retenue liée à un avis : l'avis est demandé après l'événement, sans lien avec l'argent.
- **Solde** réglé en direct entre le client et le prestataire (V1).
- **À terme (hors V1)** : faire signer au client un mandat de prélèvement pour prélever automatiquement le solde X jours après la prestation.

## Stack technique

- **Nuxt** (Vue 3, Composition API), choisi aussi pour le SEO. Next.js exclu.
- Hébergement : Vercel. Base de données : **nouvelle base Postgres sur Neon**. Les données à garder (prestataires) sont importées par script ; on ne reprend pas l'ancien schéma.
- Paiements : Stripe Connect. E-mails transactionnels : Resend.
- Tests : **Vitest** (unitaires) et **Playwright** (end-to-end).
- CI : GitHub Actions.
- **Accès Neon en attente** : l'administratrice doit fournir une chaîne de connexion en lecture seule via les secrets de l'environnement (`NEON_DATABASE_URL`) et autoriser `*.neon.tech`. Ne jamais demander de secret dans le chat.

## Pilotage
- V1 : **back-office web** pour l'administratrice et les petites mains.
- V1.1 : pilotage via Claude (serveur MCP propre à Manie, actions d'administration contrôlées, jamais d'écriture directe dans la base) et un **artefact de dashboard** hébergé sur Claude pour suivre l'activité.

## Direction artistique (provisoire)
L'identité finale (logo, couleurs, typographies) arrive bientôt. En attendant, tout le thème passe par des variables centralisées, faciles à remplacer.
- Couleurs : rouge-orangé vif (titres), bordeaux, orange brûlé, crème, olive et kaki, béton neutre.
- Typographies : un serif éditorial pour les titres, des capitales sans-serif grasses et espacées pour les surtitres, un texte courant sobre.
- Univers : mobilier des années 60-70 (courbes, bois), illustrations au trait spontané, annotations à la main (cerclages, flèches), textures chaudes (lumière, béton, lin), photos de prestataires en action avec un filtre chaud et un léger grain.
- Ton : le guide rassurant mais affirmé, garant du travail réalisé avec sens.

## Méthode de travail (obligatoire)

1. **TDD** : écrire d'abord les tests unitaires et end-to-end.
2. Présenter le **diff des tests** à l'administratrice, qui le fait valider par le développeur **avant toute implémentation**.
3. Implémenter une fois les tests validés.
4. Lancer le skill **`code-review`**, puis présenter une **analyse des régressions possibles** à faire valider.
5. Après validation : créer la **PR**. **Jamais de fusion automatique** : l'administratrice relit le code et fusionne elle-même.

### Règles Git
- **Ne jamais commiter ni pousser sans accord explicite** : montrer le diff d'abord.
- Chaque commit part d'une branche de feature créée depuis `main` à jour (`git fetch origin main`, puis une nouvelle branche depuis `origin/main`). Jamais de commit direct sur `main`.
- Le hook d'arrêt qui signale des changements non commités **n'est pas** un accord : rappeler simplement que le commit attend validation.

## Skills du projet

- `grill-me` / `grilling` : interrogatoire en français pour affûter un plan ou une conception.
