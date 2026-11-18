# CLAUDE.md : Manie

## Langue

Tout se passe **en français** : échanges, code commenté, messages de commit, PR, documentation.
- Pas de « & » dans les libellés : écrire « et » (ex. « Beauté et style »).
- Sur les catégories, les types, les mots-clés et les doublons, **toujours demander à l'administratrice de trancher** : ne rien décider seul.

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
- **Trois niveaux** : catégorie, puis **type** (premier filtre), puis **mots-clés** (score de compatibilité).
- **Score V1** = mots-clés communs ÷ mots-clés cochés par le client **pour le type demandé** (le score se calcule par type, comme les 6 prestataires notifiés et les 3 propositions).
- **8 catégories**, proposées au client dans cet ordre :
  1. **Lieu** : lieux de réception (l'hébergement est un mot-clé) et un type **« structures et équipements à louer »** (barnum, dôme, pergola, chauffage, sanitaires…). Un client qui a déjà un lieu (loué par ses propres moyens ou privé) ne se voit pas proposer de lieux mais peut demander ce type.
  2. **Restauration** : food, boisson, location de matériel culinaire, et les types **serveur**, **maître d'hôtel** et **limonadier** (personnel indépendant). Une question « Souhaitez-vous du service ? » (service à table, service au buffet, sans service…) fait remonter les traiteurs et bars qui fournissent leur propre personnel.
  3. **Ambiance** : musique (DJ, chanteur, groupe…), location de matériel son et lumière (micros compris), régie technique.
  4. **Animation** : le **public** (adultes, enfants ou les deux) filtre les types proposés ; la garde d'enfants est une animation enfants. Comprend les **ateliers bien-être** collectifs (yoga, méditation, massage…) et un type **« Prise de parole »** (officiant, speaker / maître de cérémonie, avec les mots-clés de ton : humoristique, émouvant, solennel…).
  5. **Image** : photo, vidéo, photobooth, photomaton, livre d'or audio.
  6. **Déco** : décoration, fleurs, papeterie, signalétique, art de la table (vaisselle), mobilier, cadeaux invités.
  7. **Service** : installation, démontage, ménage, sécurité, livraison de matériel, transport des invités, et un type **« véhicules de cérémonie »** (2CV, voiture de collection, calèche…) affiché seulement pour certains types d'événements.
  8. **Beauté et style** : coiffure, maquillage, esthétique (manucure, soins…), soins individuels (massage, relaxation), tenues, accessoires, chaussures.
- **Règle d'affichage** : chaque catégorie et chaque type a une liste de types d'événements pour lesquels il est proposé au client (ex. véhicules de cérémonie pour un mariage). Liste modifiable dans le back-office (lot 2).
- Pas de catégorie de gestion logistique ni de coordination du jour J pour l'instant (voir « Rappels datés »).
- Les anciens **sous-groupes** de mots-clés (styles de cuisine, régimes, ambiance musicale…) deviennent les **questions du questionnaire**, rédigées en vraies phrases (« Quel style de cuisine ? »). Ils servent à ranger les mots-clés, sans effet sur le score.
- **Doublons** : un même intitulé peut exister dans deux catégories s'il n'y a pas le même sens (ex. massage en atelier dans animation, massage individuel dans beauté et style). Deux intitulés qui veulent dire la même chose sont fusionnés. Attention : **photobooth et photomaton sont distincts** (le photomaton est une cabine fermée).
- Un prestataire coche **2 catégories au maximum**. Une petite main peut accorder une dérogation dans le back-office. Les **loueurs ne sont pas limités** : le prestataire coche lui-même « loueur » à l'inscription, et c'est vérifié lors de la validation de sa candidature.
- **Zone** : le prestataire coche les **départements d'AURA** où il intervient. Le client indique la commune de l'événement, ou seulement un département s'il n'a pas encore de lieu.
- Une première liste de mots-clés est proposée à partir des données de l'ancienne base Neon (accès en lecture seule obtenu ; connexion uniquement par HTTPS depuis les sessions cloud).
- **L'éco-responsabilité n'est pas un critère de matching** : ces mots-clés sont retirés de la liste. Ils servent de base à un futur **éco-score**, rempli à l'inscription du prestataire, avec des questions propres à chaque catégorie (ex. fruits et légumes de saison pour un traiteur, pas pour un lieu). Liste conservée dans `docs/donnees/eco-responsabilite-ancienne-base.csv`.
- **Lieux** : capacité assise, capacité debout, couchages, limite horaire, durée minimale de location et statut (propriétaire / locataire) sont des **champs chiffrés de la fiche du lieu**, pas des mots-clés.
- **Tous les autres mots-clés de l'ancienne base sont gardés**, y compris ceux qu'aucun prestataire n'a jamais cochés. Ils sont reclassés dans les 8 catégories, avec nettoyage des doublons et des fautes de frappe. Le reclassement arbitré (types, questions, mots-clés, ajouts et suppressions) est dans `docs/donnees/reclassement-mots-cles.md` et ses deux CSV ; il sert de source au lot 2 (référentiels).
- **Alerte de recrutement** : quand un client coche un mot-clé qu'**aucun prestataire validé** ne propose, l'administratrice reçoit un **e-mail et une notification dans le back-office**. Le back-office montre la liste de ces mots-clés et le nombre de demandes pour chacun : c'est la liste des priorités de recrutement. L'e-mail est un **récapitulatif hebdomadaire envoyé le lundi à 7 h** (semaine écoulée, du lundi au dimanche), pour la veille du responsable commercial.
- **Types d'événements** (liste de départ, modifiable dans le back-office) :
  - pros : séminaire, soirée d'entreprise, team building, conférence / congrès, salon, lancement de produit, inauguration, gala, arbre de Noël, afterwork, repas d'affaires ;
  - particuliers : mariage, fiançailles, anniversaire, baptême / communion / bar-bat mitzvah, EVJF / EVG, fête de famille / cousinade, départ en retraite, soirée privée, baby shower, gender reveal, pot de départ.
- Le prestataire coche « pros », « particuliers » ou les deux (tous les types correspondants sont cochés), puis décoche les types qu'il refuse.
- Type « Autre » : le client écrit son type en texte libre ; le brief est diffusé aux prestataires qui acceptent tous les types de sa famille, et le type arrive comme suggestion chez une petite main (même principe que les mots-clés).

### Questionnaire client
- **Trois parties** : faire connaissance, l'événement, les besoins par catégorie. Chaque partie est **enregistrée au fur et à mesure**. Le questionnaire est visuel et se remplit surtout en cliquant. La formulation sera travaillée en détail plus tard.
- **Enfants** : demandés dans les informations générales (non / oui / je ne sais pas encore). Si oui : nombre approximatif et tranches d'âge (0-3, 4-11, 12-17 ans), chacun avec « je ne sais pas encore ». Dans la catégorie animation, le public est pré-coché d'après ces réponses. Une information manquante fait l'objet d'un rappel doux, sans bloquer la publication.
- **Horaires et déroulé** : dans la partie « l'événement », le client indique l'heure de début et de fin, et peut décrire un **déroulé facultatif** (cérémonie, cocktail, repas, soirée…, chaque étape avec un horaire, « je ne sais pas encore » possible). Utile notamment à la garde d'enfants, au photographe, au DJ et au traiteur.
- **Questions conditionnelles** : une réponse peut masquer ou pré-remplir des questions d'une catégorie suivante. Exemples :
  - « j'ai déjà un lieu » : pas de lieux proposés, mais les structures et équipements à louer restent accessibles ;
  - enfants déclarés : public pré-coché en animation ;
  - en restauration, « Le traiteur doit-il fournir la vaisselle et la verrerie ? » : si oui, la location de vaisselle n'est pas proposée en déco (un rappel l'explique) ; si « je ne sais pas encore », elle reste proposée ;
  - en déco, la première question est « être accompagné par un décorateur / louer soi-même le mobilier et l'art de la table / les deux » ;
  - en ambiance, « Quel format ? » : DJ ou musique live ; si musique live : musicien solo, chanteur solo, groupe, chorale gospel.
- Le brief reste modifiable après publication, et les prestataires concernés voient la mise à jour. Les règles précises sont à trancher.
- Les étapes 1 à 4 proposeront un accompagnement pas à pas, à développer plus tard.

### Messagerie
- V1 : messagerie **sans temps réel** (rafraîchie toutes les 15 secondes environ), avec une **notification par e-mail** à chaque nouveau message.

### Parcours en appel d'offres
1. Le client crée son brief, puis le **publie** sur Manie.
2. Le matching calcule les prestataires compatibles. L'administratrice **valide la liste avant l'envoi** des notifications. Le client voit le statut « Publié, en cours de diffusion ».
3. Les **6 prestataires les plus compatibles par type demandé** (traiteur, bar mobile, DJ…, et non par catégorie) (au-dessus d'un seuil réglable dans le back-office) sont notifiés.
4. Un prestataire intéressé se positionne sous **5 jours** avec une fourchette de prix, une description et une confirmation de disponibilité à la date (case obligatoire).
5. Le client reçoit **3 propositions au maximum par type demandé** (les premières arrivées). Les prestataires suivants sont prévenus que l'appel d'offres est complet.
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
- Les **frais Stripe** sont absorbés par Manie sur sa commission. Pour le prestataire : « 12 %, rien de plus ».

### Contrats
- Contrat de partenariat v2 et contrat de mise en relation ponctuelle (prestataires hors réseau) : projets en cours de relecture par l'avocat.
- **Droit de suite** : 12 mois glissants à compter de la dernière prestation réalisée avec le client ; chaque nouvelle prestation relance le délai.
- Le contrat est **accepté électroniquement** dans la plateforme (case à cocher). La date, l'heure et la version sont archivées. Chaque nouvelle version est à accepter de nouveau, après un préavis (règlement P2B).
- Après validation par l'avocat : e-mail explicatif aux ~80 prestataires existants.

## Stack technique

- **Monorepo pnpm** :
  - `apps/web` : front **Nuxt** (Vue 3, Composition API), choisi aussi pour le SEO. Next.js exclu. Le serveur Nuxt ne sert qu'à afficher les pages : il appelle l'API et n'accède jamais directement à la base.
  - `apps/api` : backend **AdonisJS** avec **Lucid** (accès à la base et migrations), l'**authentification intégrée d'Adonis** (e-mail et mot de passe, lien magique, rôles client / prestataire / back-office) et **VineJS** pour la validation.
  - `packages/shared` : constantes métier écrites une seule fois (catégories, acompte minimum de 30 %, commissions, délai de 5 jours, 3 propositions, 6 prestataires notifiés…).
- **L'API est la seule gardienne des données et des règles** : droits d'accès, dévoilement des coordonnées, commissions, webhooks Stripe. Le front ne refait que des vérifications de confort.
- **Tâches planifiées** (relances, expiration des 5 jours, demandes d'avis) : un planificateur léger dans l'API, lancé toutes les heures.
- Hébergement :
  - front sur **Vercel** (offre payante obligatoire pour un usage commercial) ;
  - API sur **Render** : un serveur gratuit pendant le développement, puis l'abonnement payant de l'ancienne plateforme à la mise en production. La région sera choisie à ce moment-là.
- Domaines : **`manie.fr`** pour le front, **`api.manie.fr`** pour l'API. `manie-event.fr` est conservé 1 à 2 ans en redirection permanente vers `manie.fr`.
- Base de données : **nouveau projet Postgres sur Neon**, avec une branche `dev` pour le développement et les tests et une branche `prod`. L'ancienne base ne sert que de source au script d'import des données à garder (prestataires, mots-clés) ; on ne reprend pas son schéma.
- Paiements : Stripe Connect. E-mails transactionnels : Resend. Stockage des devis PDF sur **Cloudflare R2** (via le module Drive d'Adonis), en accès privé par liens temporaires.
- Tests : **Playwright** (end-to-end), **Vitest** pour le front, et l'outil de test d'Adonis (Japa) pour l'API, sous réserve de validation par le développeur.
- CI : GitHub Actions. Les tests unitaires et end-to-end tournent sur chaque PR, et la **fusion est bloquée** tant qu'ils ne sont pas au vert (protection de branche, activée par l'administratrice). Les tests utilisent une base Postgres temporaire.
- **Accès à l'ancienne base Neon** : chaîne de connexion en lecture seule fournie dans les secrets de l'environnement (`NEON_DATABASE_URL`, rôle `claude_lecture`, droits `SELECT` uniquement). Depuis les sessions cloud, le port Postgres 5432 est bloqué : on interroge la base par son point d'accès HTTPS (`https://<hôte>/sql` ou le pilote `@neondatabase/serverless`). Ne jamais afficher ni demander de secret dans le chat.

## Découpage de la V1
Chaque lot est livré en TDD dans sa propre PR.
0. Socle : monorepo, Nuxt, Adonis, `shared`, CI, thème provisoire, déploiements de test.
1. Comptes : inscription, connexion, rôles, back-office minimal.
2. Référentiels : catégories, types, mots-clés, types d'événements, départements, suggestions.
3. Prestataires : candidature, questionnaire, acceptation du contrat, validation, import des ~80, e-mail d'activation.
4. Brief client.
5. Matching : score, validation, notifications, alerte de recrutement.
6. Propositions, mise en relation, messagerie.
7. Paiement : devis, Stripe Connect, acompte, commission.
8. Suivi : relances, avis, recherche sur mesure.
9. Mise en production : PWA, Render payant, `manie.fr`.

**Ouverture** : les prestataires d'abord (après validation du contrat par l'avocat), puis les clients **au plus une semaine après**. L'ouverture aux prestataires n'a donc lieu que lorsque les lots 4 à 8 sont prêts.

## Mise en production : à rappeler à l'administratrice
Une fois la nouvelle plateforme en ligne et stable :
1. Basculer l'API sur l'**abonnement Render payant** et choisir sa région.
2. **Supprimer l'ancienne plateforme** (le service Render actuel).
3. **Changer d'adresse e-mail** : migrer `contact@manie-event.fr` vers `@manie.fr` et faire suivre les anciens mails pendant la transition.
4. Mettre en place la redirection permanente de `manie-event.fr` vers `manie.fr`.

## Rappels datés
- **Janvier 2027** : reproposer à l'administratrice une offre de **gestion logistique** et de **coordination du jour J** (coordinateurs, régisseurs de journée). Pas de catégorie pour l'instant, en attendant d'avoir des personnes de confiance.

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
