# YO Digital Space - Plateforme Immersive et Agent Vocal Intelligent en Temps Reel

Projet de Fin d'Annee (PFA) - Ingenierie Logicielle, Intelligence Artificielle 
Auteur : Ilyass EL-OGRI  
Annee Academique : 2026 - 2027  

---

## Illustrations Principales du Projet

<table>
  <tr>
    <td align="center">
      <img src="img/1.jpeg" alt="Aperçu Général 1" width="250">
    </td>
    <td align="center">
      <img src="img/2.jpeg" alt="Aperçu Général 2" width="250">
    </td>
    <td align="center">
      <img src="img/3.jpeg" alt="Aperçu Général 3" width="250">
    </td>
  </tr>
</table>

<p align="center">
  <img src="img/4.webp" alt="Aperçu Général 4" width="400">
</p>

---

## Sommaire

1. [Presentation Generale et Cadre du Projet](#1-presentation-generale-et-cadre-du-projet)
   - [Contexte et Problematique](#contexte-et-problematique)
   - [Objectifs du Projet](#objectifs-du-projet)
   - [Perimetre Fonctionnel](#perimetre-fonctionnel)
   - [Decoupage Methodologique](#decoupage-methodologique)
2. [Conception et Modelisation UML](#2-conception-et-modelisation-uml)
   - [Architecture Globale du Systeme](#architecture-globale-du-systeme)
   - [Diagrammes des Cas d'Utilisation](#diagrammes-des-cas-dutilisation)
   - [Modelisation Conceptuelle et Relationnelle](#modelisation-conceptuelle-et-relationnelle)
3. [Architecture Back-end et Persistance](#3-architecture-back-end-et-persistance)
   - [Organisation Modulaire NestJS](#organisation-modulaire-nestjs)
   - [Couche de Donnees et Schema Prisma](#couche-de-donnees-et-schema-prisma)
   - [Familles d'Endpoints REST](#familles-dendpoints-rest)
   - [Mecanisme de Cache Memoire](#mecanisme-de-cache-memoire)
   - [Securite et Authentification Administrative OTP](#securite-et-authentification-administrative-otp)
4. [Intelligence Artificielle Vocale et Traitement Temps Reel](#4-intelligence-artificielle-vocale-et-traitement-temps-reel)
   - [Pipeline Audio Bidirectionnel](#pipeline-audio-bidirectionnel)
   - [Passerelle WebSocket et Orchestration](#passerelle-websocket-et-orchestration)
   - [Protocole de Tool Calling](#protocole-de-tool-calling)
   - [Machine a Etats Emotionnels](#machine-a-etats-emotionnels)
   - [Gestion des Interruptions et Protection Acoustique](#gestion-des-interruptions-et-protection-acoustique)
5. [Architecture Front-end et Rendu Graphique Immersif](#5-architecture-front-end-et-rendu-graphique-immersif)
   - [Technologies Client et Structure Applicative](#technologies-client-et-structure-applicative)
   - [Rendu 3D WebGL, Three.js, OGL et Shaders GLSL](#rendu-3d-webgl-threejs-ogl-et-shaders-glsl)
   - [Moteur d'Animation GSAP et Defilement Fluide](#moteur-danimation-gsap-et-defilement-fluide)
6. [Administration, Validation et Resultats](#6-administration-validation-et-resultats)
   - [Tableau de Bord Administratif](#tableau-de-bord-administratif)
   - [Synthese des Resultats et Performances](#synthese-des-resultats-et-performances)
   - [Limites Identifiees et Perspectives](#limites-identifiees-et-perspectives)
7. [Deploiement Conteneurise et Reverse Proxy Nginx](#7-deploiement-conteneurise-et-reverse-proxy-nginx)
   - [Architecture All-in-One du Conteneur Unique](#architecture-all-in-one-du-conteneur-unique)
   - [Routage et Configuration Nginx](#routage-et-configuration-nginx)
   - [Supervision des Processus avec Supervisor](#supervision-des-processus-avec-supervisor)
   - [Guide de Demarrage et Commandes d'Execution](#guide-de-demarrage-et-commandes-dexecution)
   - [Variables d'Environnement Requises](#variables-denvironnement-requises)

---

## 1. Presentation Generale et Cadre du Projet

### Contexte et Problematique

Dans l'ecosysteme actuel du web, les plateformes corporatives se limitent generalement a des sites vitrines statiques ou a des interfaces transactionnelles traditionnelles. Les interfaces conversationnelles integrees restent frequemment cantonnees a des widgets de messagerie textuelle a base de regles deterministes ou a des modeles asynchrones souffrant d'une forte latence.

Le projet **YO Digital Space** repond a une double exigence :
1. Construire une vitrine technologique hautement immersive dediee a un studio d'ingenierie logicielle, combinant graphisme 3D avance, animations complexes et design interactif.
2. Integrer un agent conversationnel vocal temps reel (le CEO IA) capable d'echanger naturellement par la voix avec les visiteurs, d'ajuster son expression emotionnelle en direct et d'acceder aux donnees metier de l'entreprise via un protocole d'appels d'outils (Tool Calling).

La problematique centrale du projet s'enonce ainsi :  
*Comment concevoir et deployer une plateforme web unifiee, combinant rendu 3D temps reel, gestion dynamique de contenus et interaction vocale bidirectionnelle a ultra-faible latence, tout en garantissant la coherence des connaissances et la haute disponibilite de l'infrastructure ?*

### Objectifs du Projet

- **Objectif general** : Developper et conteneuriser une solution logicielle complete unifiant front-end immersif, back-end robuste et intelligence artificielle multimodale native audio.
- **Objectifs fonctionnels** :
  - Exposition detaillee du portfolio de realisations, des services d'ingenierie et des articles techniques.
  - Collecte structuree des demandes de contact et qualification de leads.
  - Espace d'administration securise pour le pilotage integral de la base de connaissances et des contenus.
  - Agent vocal conversationnel avec flux audio direct (Full-Duplex), gestion de l'interruption (barge-in) et expressions faciales synchronisees.
- **Objectifs techniques** :
  - Architecture decoupee en couches avec typage statique de bout en bout (TypeScript).
  - Traitement audio PCM lineaire a faible latence via WebSocket.
  - Cache memoire avec temps de reponse inferieur a 1 milliseconde pour les donnees consultees par l'IA.
  - Deploiement sous forme d'image Docker unique autonome distribuee via Nginx et orchestree par Supervisor.

### Perimetre Fonctionnel

| Domaine | Fonctionnalites Principales | Finalite Technique et Metier |
|---|---|---|
| Vitrine Immersive | Scene 3D temps reel, carrousel cylindrique, shaders GLSL, scroll inertiel | Engagement utilisateur et demonstration de savoir-faire |
| Portfolio et Blog | Projets bilingues (FR/EN), etudes de cas, articles techniques, systeme de filtres | Presentation de l'expertise technique et referencement |
| Relation Client | Formulaire de contact intelligent, qualification des besoins (ERP, CRM, IA, Web) | Capture structuree et transmission par notification e-mail |
| Agent Vocal CEO Live | Dialogue audio bidirectionnel, TTS/STT unifie, mecanisme anti-echo | Assistance interactive et conversion des visiteurs |
| Administration | Gestion CRUD des projets, services, forfaits, FAQ et profils d'entreprise | Mise a jour sans recompilation ni redepoiement |
| Base de Connaissances | Indexation memoire et fourniture d'outils fonctionnels au modele IA | Reponses verifiees sans hallucination sur les donnees du studio |

### Decoupage Methodologique

Le projet a ete structure selon un calendrier rigoureux de huit semaines, articule autour des phases suivantes :

| Phase | Description des Travaux | Livrables Cles |
|---|---|---|
| S1 - S2 | Analyse des besoins, formalisation du cahier des charges et modelisation UML | Diagrammes de cas d'utilisation, modele de domaine |
| S3 - S4 | Conception de la base de donnees, developpement du back-end NestJS et de l'API REST | Schemas Prisma, controleurs, services, securite OTP |
| S4 - S6 | Developpement de l'interface React 19, integration 3D (Three.js/OGL) et animations | Composants, stores Zustand, shaders, layout immersif |
| S5 - S7 | Implementation de la passerelle WebSocket, protocole audio et session multimodale | Gateway temps reel, gestion des outils, pipeline audio |
| S7 - S8 | Tests d'integration, conteneurisation Docker/Nginx, audit de performance | Image Docker finale, documentation d'architecture |

---

## 2. Conception et Modelisation UML

### Architecture Globale du Systeme

Le systeme repose sur une separation stricte entre la couche de presentation, la couche d'orchestration applicative, la couche de persistance et les services tiers d'intelligence artificielle et de diffusion multimedia.

![Architecture globale du systeme](img/arch.png)

*Figure 2.1 : Architecture globale du systeme montrant l'interaction entre le navigateur client, le proxy inverse Nginx, le serveur NestJS, PostgreSQL et l'API multimodale.*

Le flux architectural s'organise selon trois axes majeurs :
1. **Canal Statique et REST** : Le navigateur charge les artefacts compilés du front-end via Nginx. Les requetes d'administration et de consultation standard transitent en HTTP/JSON vers les controleurs NestJS.
2. **Canal Temps Reel Full-Duplex** : L'interaction avec le CEO IA s'effectue au travers d'un tunnel WebSocket persistant. La passerelle NestJS relaie le flux audio vers le moteur d'intelligence artificielle et execute les fonctions metier requises.
3. **Canal de Persistance** : NestJS interagit avec PostgreSQL via Prisma ORM en appliquant une barriere d'isolation memoire pour les lectures recurrentes.

### Diagrammes des Cas d'Utilisation

La modelisation fonctionnelle explicite les interactions des trois acteurs identifies : le Visiteur, l'Administrateur et l'Agent IA Vocal.

![Diagramme UML des cas d'utilisation](img/usecas.png)

*Figure 2.2 : Diagramme UML global des cas d'utilisation de la plateforme.*

#### Cas d'Utilisation du Visiteur

Le visiteur accede aux ressources publiques sans obligation d'authentification. Il peut explorer les projets, filtrer les services, soumettre une demande commerciale ou initialiser une session audio immersive.

![Diagramme UML des cas d'utilisation du visiteur](img/user.png)

*Figure 2.3 : Diagramme des cas d'utilisation dedie au Visiteur.*

#### Cas d'Utilisation de l'Administrateur

L'administrateur dispose de privileges etendus lui permettant de modifier le referentiel documentaire de l'entreprise, d'administrer les etudes de cas du portfolio et de gerer les sollicitations entrantes.

![Diagramme UML des cas d'utilisation de l'administrateur](img/adm.png)

*Figure 2.4 : Diagramme des cas d'utilisation dedie a l'Administrateur.*

#### Cas d'Utilisation de l'Agent IA Vocal

L'agent conversationnel intervient en tant qu'acteur autonome au sein de la session de communication : il ecoute l'utilisateur, sollicite les fonctions du serveur pour acquerir les faits et emet simultanement sa synthese vocale et son etat emotionnel.

![Diagramme UML des cas d'utilisation de l'agent IA vocal](img/ai.png)

*Figure 2.5 : Diagramme des cas d'utilisation dedie a l'Agent IA Vocal.*

### Modelisation Conceptuelle et Relationnelle

Le modele conceptuel de donnees a ete structure pour concilier rigueur relationnelle et flexibilite editoriale grace a des attributs JSON reserves aux contenus bilingues.

![Diagramme UML des entites et de la structure de la base de donnees](img/dia_class.png)

*Figure 2.6 : Diagramme de classes UML representant la structure entites-relations du systeme.*

#### Dictionnaire des Tables Principales

| Entite | Type Prisma | Description Fonctionnelle | Attributs Cles |
|---|---|---|---|
| `Project` | Table | Realisations et etudes de cas presentees dans le portfolio | `id`, `slug`, `images` (JSON), `fr` (JSON), `en` (JSON), `createdAt` |
| `Blog` | Table | Publications techniques et actualites du studio | `id`, `slug`, `date`, `readTime`, `category`, `image`, `fr`, `en` |
| `Contact` | Table | Demandes de contact et sollicitations de devis | `id`, `fullName`, `company`, `email`, `phone`, `need`, `message`, `status` |
| `AdminOtp` | Table | Codes a usage unique pour l'authentification administrative | `id`, `code`, `email`, `expiresAt`, `createdAt` |
| `CompanyProfile` | Table | Identite, mission, vision et coordonnees du studio | `id`, `name`, `tagline`, `email`, `phone`, `address`, `fr`, `en` |
| `Service` | Table | Catalogue d'offres logicielles et prestations | `id`, `slug`, `category`, `fr`, `en`, `order` |
| `PricingPlan` | Table | Grille tarifaire indicative et forfaits d'intervention | `id`, `slug`, `category`, `startingAt`, `timeline`, `fr`, `en`, `order` |
| `Faq` | Table | Base de questions frequentes et reponses certifiees | `id`, `category`, `fr`, `en`, `order` |
| `CeoConversation` | Table | Historique et transcriptions des echanges avec le CEO IA | `id`, `fullName`, `email`, `phone`, `messages` (JSON), `transcript` |

---

## 3. Architecture Back-end et Persistance

### Organisation Modulaire NestJS

Le back-end s'appuie sur le framework NestJS, exploitant le patron d'injection de dependances et une decoupe par modules metier hautement cohesifs.

![Organisation fonctionnelle du back-end](img/backend.png)

*Figure 3.1 : Organisation modulaire et separation des couches au sein du serveur NestJS.*

Chaque module regroupe son controleur (exposition des routes), son service (regles metier et validation) et ses fournisseurs d'acces aux donnees.

![Structure des modules et services back-end](img/srcbk.png)

*Figure 3.2 : Arborescence des sources du back-end montrant l'isolation par domaine fonctionnel.*

### Couche de Donnees et Schema Prisma

L'acces a la base de donnees PostgreSQL hebergee sur Supabase est gere par Prisma ORM. Cette couche apporte un typage statique strict et elimine les risques d'injections SQL.

![Resultat de la base de donnees](img/dbs.png)

*Figure 3.3 : Interface de gestion relationnelle et validation du schema de persistance.*

Le schema relationnel s'articule autour de definitions Declaratives (`schema.prisma`) :

```prisma
datasource db {
  provider  = "postgresql"
  url       = env("DATABASE_URL")
  directUrl = env("DIRECT_URL")
}

model Project {
  id        String   @id @default(uuid())
  slug      String   @unique
  images    Json     // Format : { mainImage, image2, image3 }
  fr        Json     // Structure bilingue Francais
  en        Json     // Structure bilingue Anglais
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}

model CeoConversation {
  id         String   @id @default(uuid())
  fullName   String
  email      String
  phone      String?  @default("")
  messages   Json     @default("[]")
  transcript String?  @default("") @db.Text
  createdAt  DateTime @default(now())
  updatedAt  DateTime @updatedAt

  @@map("ceo_conversations")
}
```

### Familles d'Endpoints REST

L'API REST suit les conventions de conception standard :

| URI de Base | Methode | Role Fonctionnel | Controle d'Acces |
|---|---|---|---|
| `/projects` | `GET` | Recuperation de l'ensemble des etudes de cas | Public |
| `/projects/:slug` | `GET` | Consultation detaillee d'un projet specifique | Public |
| `/projects` | `POST` / `PUT` / `DELETE` | Creation, mise a jour ou suppression d'un projet | Administrateur |
| `/blog` | `GET`, `POST`, `PUT`, `DELETE` | Gestion du flux d'articles editoriaux | Public (GET) / Admin |
| `/knowledge/*` | `GET` | Consultation des services, tarifs, FAQ et profil | Public / Interne |
| `/knowledge/*` | `PUT` / `POST` | Mise a jour du referentiel de connaissances | Administrateur |
| `/contact` | `POST` | Envoi d'une demande de devis ou prise de contact | Public (Rate-limited) |
| `/auth/send-otp` | `POST` | Generation et expedition du code de securite | Public |
| `/auth/verify-otp` | `POST` | Verification du code et delivrance du jeton | Public |

### Mecanisme de Cache Memoire

Pour eviter que chaque question posee a l'agent vocal n'engendre des interrogations directes vers la base de donnees distribuée (entrainant une degradation inacceptable de la latence), un cache memoire a ete integre directement au sein de `CeoGateway`.

- **Temps d'acces** : Moins de 1 ms en lecture locale.
- **Strategie d'invalidation** : Rafraichissement automatique quotidien (TTL de 24 heures) couple a un mecanisme de rechargement reactif declenche lors de chaque modification administrative (`refreshCache()`).
- **Resilience reseau** : Les interrogations de pre-chargement sont ordonnancees de maniere sequentielle afin de prevenir toute saturation du pooler de connexions Supabase.

### Securite et Authentification Administrative OTP

L'acces a la console d'administration est verifie par un systeme OTP (One-Time Password) sans mot de passe persistant :
1. L'administrateur sollicite une connexion en transmettant son adresse e-mail.
2. Un code aleatoire a haute entropie est genere, chiffre et stocke avec une duree de validite limitee (10 minutes).
3. Le code est achemine par courrier electronique securise via Nodemailer.
4. Une fois valide, le code est immediatement revoque en base et un jeton de session est assigne.

---

## 4. Intelligence Artificielle Vocale et Traitement Temps Reel

### Pipeline Audio Bidirectionnel

L'interaction vocale avec le CEO IA fonctionne selon un flux audio continu (Full-Duplex) a faible latence, articulé autour de WebSockets et du format lineaire PCM.

```
Navigateur (Micro) ───[ PCM 16 kHz ]───> Nginx Proxy ───> NestJS CeoGateway
                                                               │
                                                               ▼
Navigateur (Speakers) <───[ PCM 24 kHz ]─── Nginx Proxy <─── API Gemini Live
```

- **Format Audio Entrant** : Echantillonnage a 16 000 Hz, flux PCM lineaire 16-bit mono, transcode en fragments Base64.
- **Format Audio Sortant** : Echantillonnage a 24 000 Hz, flux audio direct reconstitue et planifie sans coupure via la Web Audio API du navigateur.

### Passerelle WebSocket et Orchestration

La passerelle `CeoGateway` (ecoutant sur le chemin `/ceo-live`) maintient une session active par client. A chaque initialisation :
1. Une liaison WebSocket est ouverte avec le serveur de l'API multimodale.
2. Une directive d'instructions systeme (`CEO_SYSTEM_INSTRUCTION`) est transmise, definissant l'attitude, la posture, la concision des reponses et la politique d'usage des langues (Francais, Anglais, Arabe).
3. Les specifications d'outils (`CEO_TOOLS`) sont declarees, permettant au modele d'interroger la memoire de l'entreprise.

### Protocole de Tool Calling

Pour garantir l'exactitude des informations financieres, techniques et contractuelles formulees par l'agent vocal, celui-ci n'a pas les donnees figees dans son invite, mais dispose d'outils d'interrogation :

| Nom de l'Outil | Description Technique | Donnees Retournees |
|---|---|---|
| `getCompanyInfo` | Consultation de la vision, de la mission et des coordonnees | Profil structure de YO Digital Space |
| `getServices` | Restitution des offres logicielles et d'ingenierie | Liste des services (Web, Mobile, IA, ERP) |
| `getPricing` | Recuperation des fourchettes budgetaires et delais moyens | Grille tarifaire et conditions de livraison |
| `getProjects` | Consultation des etudes de cas et projets precedents | Titres, technologies et problematiques resolues |
| `getFaq` | Recherche des reponses aux interrogations habituelles | Propriete intellectuelle, modalites de paiement |
| `setEmotion` | Synchronisation faciale prealable a la reponse orale | Identifiant d'etat emotionnel |

### Machine a Etats Emotionnels

Afin de conférer a l'avatar 3D un comportement anthropomorphique credible, l'agent vocal est tenu d'invoquer la fonction `setEmotion` prealablement a toute prise de parole.

![Etats emotionnels de l'agent conversationnel](img/emotion.png)

*Figure 4.1 : Machine a etats emotionnels et synchronisation visuelle de l'avatar.*

| Etat Emotionnel | Contexte d'Activation | Expression Visuelle |
|---|---|---|
| `neutral` | Etat de repos, attente et ecoute active | Regard attentif, expression calme |
| `friendly` | Accueil, salutations initiales, remerciements polis | Sourire chaleureux, posture bienveillante |
| `happy` | Validation d'un partenariat, eloges, enthousiasme | Sourire marque, dynamisme visuel |
| `thinking` | Resolution d'un probleme complexe, calcul d'estimation | Regard concentre, tete legerement inclinee |
| `confident` | Presentation d'atouts technologiques, engagements de qualite | Regard fixe, port de tete assure |
| `serious` | Sujets de cybersecurite, contraintes contractuelles critiques | Expression sobre, concentration accrue |

### Gestion des Interruptions et Protection Acoustique

Dans un environnement navigateur sans casque audio, le retour acoustique des haut-parleurs vers le microphone presente un risque de rebouclage (larsen ou auto-interruption).

Le systeme combine deux mecanismes de protection :
1. **Verrouillage Acoustique Semi-Duplex Logiciel** : Des l'emission d'un paquet audio sortant, la capture du micro est temporairement inhibee jusqu'a la fin du signal, augmentee d'une marge de garde (echo guard time).
2. **Annulation Instantanee des Buffers (Barge-in)** : Si l'utilisateur exprime une volonte d'interruption alors que le modele parle, le client stoppe immediatement la file d'attente de la Web Audio API et transmet un signal de synchronisation pour interrompre la reponse en cours cote serveur.

---

## 5. Architecture Front-end et Rendu Graphique Immersif

### Technologies Client et Structure Applicative

L'interface web publique est construite a l'aide de **React 19** et pilotee par **Vite 8**. Le routage est assure par React Router, tandis que la gestion de l'etat d'affichage et des informations globales repose sur des stores **Zustand**.

La mise en page emploie **Tailwind CSS v4** associe a des utilitaires de composition modernes permettant un rendu fluide et adaptatif sur l'ensemble des ecrans.

### Rendu 3D WebGL, Three.js, OGL et Shaders GLSL

L'experience visuelle se distingue par l'integration de technologies de rendu graphique avancees :
- **Three.js & React Three Fiber** : Mise en scene de la composition tridimensionnelle du Hero header, integrant lumieres volumetriques, geometries interactives et materiaux personnalises.
- **Shaders GLSL sur-mesure** : Effets de distorsion, ondulations liquides et reflets dynamiques calcules sur GPU.
- **OGL (Minimal WebGL Library)** : Utilise pour le carrousel cylindrique de presentation des projets, garantissant une empreinte memoire reduite et des performances a 60 images par seconde constantes.

![Interfaces et parcours principaux du front-end](img/prthero.png)

*Figure 5.1 : Vue de l'interface d'accueil combinant scene 3D immersive et typographie dynamique.*

### Moteur d'Animation GSAP et Defilement Fluide

- **GSAP & ScrollTrigger** : Orchestration des apparitions sequentielles des elements d'interface et coordination des trajectoires de camera lors du defilement.
- **Lenis Scroll** : Prise en charge d'un lissage d'inertie sur le defilement, assurant une continuite visuelle entre les sections textuelles et les transitions 3D.

---

## 6. Administration, Validation et Resultats

### Tableau de Bord Administratif

L'interface de gestion permet a l'equipe du studio de maintenir son catalogue sans aucune modification du code source ni redepoiement.

![Resultat de l'espace d'administration](img/admdsh.png)

*Figure 6.1 : Tableau de bord d'administration centralisant le suivi des leads et l'edition des contenus.*

Le panneau administratif permet notamment :
- L'ajout et la reorganisation des projets du portfolio avec upload des captures visuelles.
- La publication d'articles techniques bilingues pour le blog.
- La consultation des demandes de contact et le suivi des statuts de prospection (`UNREAD`, `READ`, `REPLIED`).
- La mise a jour directe de la base de connaissances mobilisee par l'agent IA.

### Synthese des Resultats et Performances

Les evaluations experimentales attestent de l'efficience de l'architecture retenue tant sur le plan applicatif que sur le pipeline de traitement de l'agent conversationnel.

![Synthese des resultats](img/res.jpeg)

*Figure 6.2 : Tableau synthetique des resultats, performances et validations techniques.*

| Metrique Evaluee | Valeur Constatee | Objectif Initial | Resultat |
|---|---|---|---|
| Latence de reponse vocale (Premier token audio) | 680 ms - 1100 ms | < 1500 ms | Conforme |
| Temps d'acces aux outils en cache memoire | < 1 ms | < 5 ms | Depasse |
| Taux de fluidite de la scene 3D (Desktop) | 60 FPS constants | >= 50 FPS | Conforme |
| Temps de chargement initial (First Contentful Paint) | 1.1 seconde | < 2.0 secondes | Conforme |
| Empreinte memoire du conteneur unifie au repos | ~180 Mo RAM | < 512 Mo RAM | Conforme |

### Limites Identifiees et Perspectives

1. **Evolutivité du Cache Multi-Noeuds** : Le cache memoire actuel reside dans le processus de l'instance NestJS. Dans le cas d'un deploiement horizontal distribue a grande echelle, l'integration d'un store Redis centralise avec notifications Pub/Sub permettra une synchronisation inter-noeuds instantanee.
2. **Audio Worklet Multi-Thread** : La capture et l'encodage audio s'executent actuellement sur le contexte Web Audio principal. La migration vers des modules `AudioWorklet` dedies garantira une isolation totale vis-a-vis des operations de rendu graphique intensives.
3. **Plafonnement des Sessions Visiteurs** : Afin de prevenir la surconsommation de l'API multimodale, une limitation des sessions vocales a 15 minutes par adresse IP / cookie est mise en place.

---

## 7. Deploiement Conteneurise et Reverse Proxy Nginx

### Architecture All-in-One du Conteneur Unique

L'integralite de la solution logicielle est packagee dans **une image Docker unique et autonome**, garantissant une portabilite absolue et une mise en production en une seule commande.

```
                              Client Web (Navigateur)
                                         │
                                         ▼ Port 80
   ┌────────────────────────────────────────────────────────────────────────┐
   │                  CONTENEUR DOCKER UNIQUE (All-in-One)                  │
   │                                                                        │
   │  ┌──────────────────────────────────────────────────────────────────┐  │
   │  │                      Nginx (Point d'Entree)                      │  │
   │  └───────────────┬──────────────────────────────────┬───────────────┘  │
   │                  │                                  │                  │
   │   / (Fichiers    │                                  │ /api/*, /auth/*, │
   │      Statiques)  │                                  │ /projects/*,     │
   │   /assets/*      │                                  │ /ceo-live (WS)   │
   │                  ▼                                  ▼                  │
   │      ┌──────────────────────┐           ┌──────────────────────────┐   │
   │      │   Frontend Statique  │           │   Serveur NestJS         │   │
   │      │   (/var/www/html)    │           │   (127.0.0.1:3000)       │   │
   │      └──────────────────────┘           └─────────────┬────────────┘   │
   │                                                       │                │
   │  ┌─────────────────────────────────────────────────┐  │                │
   │  │   Supervisor (Gestionnaire de Processus Linux)  │  │                │
   │  └─────────────────────────────────────────────────┘  │                │
   └───────────────────────────────────────────────────────┼────────────────┘
                                                           │
                                                           ▼
                                                [PostgreSQL Distant]
```

### Routage et Configuration Nginx

Nginx assure une triple mission au sein du conteneur :
1. **Distribution Haute Performance du Front-end** : Service direct des fichiers HTML, CSS, JavaScript et assets avec compression Gzip et en-tetes de cache adaptes.
2. **Proxy Inverse pour l'API REST** : Reacheminement transparent des routes `/projects`, `/blog`, `/contact`, `/auth`, `/knowledge` et `/uploads` vers `http://127.0.0.1:3000`.
3. **Passerelle WebSocket Temps Reel** : Prise en charge des en-tetes `Upgrade` et `Connection` sur le chemin `/ceo-live` avec allongement des delais d'inactivite (`proxy_read_timeout 3600s`).

Extrait de la configuration de routage Nginx :

```nginx
# Routage de l'API REST vers NestJS
location ~ ^/(projects|blog|contact|auth|knowledge|uploads|api) {
    proxy_pass http://127.0.0.1:3000;
    proxy_http_version 1.1;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}

# Passerelle WebSocket Full-Duplex pour le CEO IA
location /ceo-live {
    proxy_pass http://127.0.0.1:3000/ceo-live;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_set_header Host $host;
    proxy_read_timeout 3600s;
    proxy_send_timeout 3600s;
}

# Fallback pour le routage SPA React
location / {
    try_files $uri $uri/ /index.html;
}
```

### Supervision des Processus avec Supervisor

Le demarrage et la resilience des deux services fondamentaux (Node.js et Nginx) sont confies a **Supervisor** (`supervisord`), qui garantit un redemarrage automatique en cas de defaillance inattendue.

```ini
[supervisord]
nodaemon=true
user=root
logfile=/var/log/supervisor/supervisord.log
pidfile=/var/run/supervisord.pid

[program:backend]
command=node dist/main.js
directory=/app/backend
autostart=true
autorestart=true
stdout_logfile=/var/log/supervisor/backend.out.log
stderr_logfile=/var/log/supervisor/backend.err.log
environment=NODE_ENV="production"

[program:nginx]
command=/usr/sbin/nginx -g "daemon off;"
autostart=true
autorestart=true
stdout_logfile=/var/log/supervisor/nginx.out.log
stderr_logfile=/var/log/supervisor/nginx.err.log
```

### Guide de Demarrage et Commandes d'Execution

#### Pre-requis
- Docker Engine installe (version 20.10 ou superieure)
- Acces internet pour la resolution des paquets npm et la communication avec les APIs distantes

#### Option A : Execution Standard via Docker CLI

1. **Construction de l'Image Unique** :
```bash
docker build -t yo-digital-space .
```

2. **Lancement du Conteneur** :
```bash
docker run -d \
  --name yo-app \
  -p 80:80 \
  -p 3000:3000 \
  --env-file ./Backend/.env \
  yo-digital-space
```

#### Option B : Execution Simplifiee via Docker Compose

```bash
# Demarrage en arriere-plan avec compilation automatique
docker compose up -d --build

# Surveillance des journaux d'evenements
docker compose logs -f

# Arret complet du conteneur
docker compose down
```

### Variables d'Environnement Requises

Les variables d'environnement suivantes doivent etre definies au niveau du fichier `.env` ou transmises lors du lancement du conteneur :

| Variable | Exemple / Format | Role |
|---|---|---|
| `DATABASE_URL` | `postgresql://user:pwd@host:6543/postgres?pgbouncer=true` | Connexion vers le pooler PostgreSQL Supabase |
| `DIRECT_URL` | `postgresql://user:pwd@host:5432/postgres` | Connexion directe sans pooling pour les migrations Prisma |
| `GEMINI_API_KEY` | `AIzaSy...` | Cle d'acces a l'API multimodale pour le flux audio temps reel |
| `MAIL_HOST` | `smtp.gmail.com` | Hote SMTP pour l'envoi des codes d'acces OTP |
| `MAIL_USER` | `contact@yodigitalspace.com` | Identifiant du service d'expedition e-mail |
| `MAIL_PASS` | `mot_de_passe_application` | Secret d'application SMTP |
| `ADMIN_EMAIL` | `direction@yodigitalspace.com` | Adresse e-mail du compte administrateur autorise |

---

## Annexe : Points d'Acces Reseau du Projet

Apres demarrage de l'image Docker, l'ensemble des services est accessible selon la topologie suivante :

| Point d'Acces | URL Locale | Description |
|---|---|---|
| Application Web (Front-end) | `http://localhost/` | Interface immersive SPA servie par Nginx |
| Espace d'Administration | `http://localhost/admin` | Console de pilotage et d'administration |
| API REST via Nginx | `http://localhost/projects` | Points d'entree d'API proxifies vers NestJS |
| Canal WebSocket CEO IA | `ws://localhost/ceo-live` | Tunnel audio bidirectionnel temps reel |
| Sonde de Sante (Healthcheck) | `http://localhost/healthz` | Verification de la disponibilite du service Nginx |
| API NestJS (Acces Direct) | `http://localhost:3000/` | Port d'ecoute direct du serveur d'application Node.js |
