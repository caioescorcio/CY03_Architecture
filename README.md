# Modèle de Dossier d'Architecture (DA)

> Ce fichier rappelle les consignes du projet, les principes du modèle, la terminologie employée et des conseils de rédaction. **Lisez-le avant de commencer.** En cas de doute, le document de sujet distribué par l'enseignant fait foi (calendrier, barème, scénarios).

## Rappel des consignes du projet

### Ce que contient le modèle
Le modèle est distribué sous forme d'archive ZIP de fichiers Markdown, à compléter directement :

- six fichiers de chapitres : [contexte](01_contexte.md), [vue métier](02_vue_metier.md), [vue applicative](03_vue_applicative.md), [vue infrastructure](04_vue_infrastructure.md), [vue cybersécurité](05_vue_cybersecurite.md) et [annexes](06_annexes.md) ;
- un répertoire `decisions/` destiné aux ADR, avec un modèle commenté ([sample-adr.md](decisions/sample-adr.md)) et trois sous-répertoires : `metier/`, `solution/`, `infrastructure/` ;
- un répertoire `diagrammes/` contenant, dans `diagrammes/exemples/`, des exemples de diagrammes C4 au format PlantUML. **Ce sont des exemples destinés à illustrer le formalisme : ils doivent être retirés du dossier final** (les laisser est décompté de la note) ;
- ce fichier `README.md`.

### Ce qu'il faut rendre
Une **archive ZIP reprenant l'arborescence du modèle**, comprenant :

- les fichiers Markdown complétés ;
- les ADR dans `decisions/` ;
- les **sources** des diagrammes (`.puml` ou `.drawio`) **et** leur rendu (`.svg` ou `.png`), dans `diagrammes/` ;
- le support de présentation de l'ARB.

Vous pouvez utiliser un dépôt Git pour travailler à plusieurs ; ce n'est ni imposé ni évalué.

### Travaux à réaliser
Le dossier décrit une **solution cible** répondant au scénario attribué. Toutes les informations ne sont pas fournies : faites des recherches, envisagez plusieurs options et tranchez, toujours avec une justification. Vous pouvez ajouter des exigences au scénario pour définir une architecture plus satisfaisante, à condition de l'expliquer dans un ADR. Le modèle peut être complété si c'est pertinent, en ajoutant la mention `NEW` devant le titre du chapitre ou du fichier ajouté.

**Chapitres** — les **quatre vues sont obligatoires** : métier, applicative, infrastructure, cybersécurité. Le chapitre de contexte (l'entreprise et ses produits) et les annexes les complètent. Chaque vue **part d'un schéma** que les rubriques viennent expliquer, et **se termine par l'impact de l'évolution** souhaitée par l'entreprise.

**ADR** — au moins **cinq**, couvrant obligatoirement :
1. le **modèle de déploiement** retenu (§4.1) ;
2. le recours à un **produit du marché ou à un développement spécifique** pour au moins un composant important (§3.2) ;
3. le **mode d'intégration** entre applications (§3.5) ;
4. le mécanisme d'**authentification et d'autorisation**, des utilisateurs **et** des appels inter-applicatifs (§5.2) ;
5. le choix de **persistance des données** pour au moins un jeu de données important (§4.4).

> ⚠️ Un ADR qui ne contient pas **au moins deux options écartées et le critère qui a fait pencher la balance** ne rapporte pas de points. Le critère doit être **rattaché au scénario** : une exigence, une contrainte réglementaire, un ordre de grandeur de volumétrie, une taille d'équipe. « PostgreSQL est plus répandu » n'est pas un critère ; « la volumétrie annoncée est de 60 To en trois ans et l'équipe compte deux administrateurs » en est un. Voir [sample-adr.md](decisions/sample-adr.md).

**Schémas attendus, et niveau C4 correspondant**

| Schéma | Emplacement | Formalisme |
|:-------- |:-------- |:-------- |
| Positionnement de l'entreprise dans son écosystème (facultatif, sans aucun composant technique) | §1.5 | libre |
| Cartographie des fonctions métier principales | §2.1 | libre (blocs fonctionnels, BPMN pour un processus) — pas de C4 |
| Contexte système : le SI vu comme un tout, ses acteurs et les systèmes externes — c'est le schéma d'ensemble lisible en une page | §3.1 | **C4 niveau 1** |
| Cartographie applicative : les applications et leurs flux | §3.1 | **C4 niveau 2 (conteneurs)** |
| Flux détaillé d'un scénario intéressant, avec un cas d'erreur | §3.3 | UML séquence ou **C4 dynamique** |
| Hébergement et répartition du SI | §4.1 | **C4 déploiement** ou schéma d'infrastructure classique |
| Sécurité | §5.3 | pas de schéma dédié ; annoter au besoin celui du §3.1 ou du §4.1 |

Le **niveau 3 de C4 (composants, l'intérieur d'une application) n'est pas attendu**, sauf si une application le mérite dans votre scénario. Au moins une vue du dossier doit être formalisée en C4 : elle est attendue au §3.1.

Les schémas doivent figurer **dans le dossier lui-même**, pas seulement dans le support de présentation.

**Présentation à l'ARB (Architecture Review Board)**
- **30 minutes de présentation suivies de 10 minutes de questions** ; tous les membres du groupe présentent, et **chaque étudiant présente au moins une partie qu'il n'a pas rédigée lui-même**.
- Posez le contexte en deux minutes, puis déroulez les **schémas d'architecture aux différents niveaux** (fonctions métier → contexte système → applications → infrastructure) en expliquant à chaque niveau **les décisions prises et ce qui les justifie**. Ne déroulez pas le dossier chapitre par chapitre.

**Calendrier** (détail dans le sujet)
- Point d'étape en séance 4 : présentation de la **vue métier** en 10 minutes (+ 5 minutes facultatives pour un schéma d'ensemble à l'état d'ébauche).
- Remise de l'archive ZIP **une semaine avant l'ARB** ; aucune modification n'est prise en compte après cette date.
- ARB en séance 7.

## Principes du modèle
Le dossier se lit comme une **descente progressive** :

1. le [contexte](01_contexte.md) : l'entreprise, son métier, ses produits et services, l'évolution qu'elle souhaite et ses contraintes — sans architecture ;
2. la [vue métier](02_vue_metier.md) : ce que le SI doit permettre de faire (fonctions métier principales) et qui l'utilise (acteurs) ;
3. la [vue applicative](03_vue_applicative.md) : quelles applications supportent ces fonctions, avec quelles technologies, comment elles échangent (nature, protocole, volume des flux) et quelle application fait référence pour chaque donnée ;
4. la [vue infrastructure](04_vue_infrastructure.md) : où et comment s'exécute le SI (hébergement, réseaux, modèle de service et mode d'exécution, stockage, sauvegarde, continuité, exploitation) ;
5. la [vue cybersécurité](05_vue_cybersecurite.md) : quelles données sont sensibles, comment le SI est protégé au bon niveau, et qui en assure le maintien en condition de sécurité ;
6. les [annexes](06_annexes.md) : glossaire, sources et liste des ADR.

Chaque vue découle de la précédente : une application doit pouvoir être rattachée à une fonction métier, une donnée à l'application qui en est la référence, un composant d'infrastructure à une application, une mesure de sécurité à une donnée ou un flux.

Chaque fois qu'un chapitre repose sur une décision structurante, **faites le lien vers l'ADR correspondant** (par exemple : « voir [ADR-SOLUTION-02](decisions/solution/adr-solution-02.md) »).

### Organisation des ADR
- Un fichier par décision, rangé selon son domaine : `decisions/metier/`, `decisions/solution/` ou `decisions/infrastructure/`.
- Nommage : `adr-<domaine>-<NN>.md` (ex. `decisions/infrastructure/adr-infrastructure-01.md`), avec l'identifiant `ADR-<DOMAINE>-<NN>` repris dans le titre.
- Chaque ADR est listé dans le tableau du [§6.3 des annexes](06_annexes.md).

### Conseils sur la rédaction de votre dossier d'architecture
* **Rester bref**, chaque mot doit avoir son utilité. **La concision est un critère d'évaluation, pas un défaut.** Pas d'explication bateau type « ceci est l'introduction », pas de recopie du scénario ni de l'histoire de l'entreprise ;
* **Partir des schémas** : dans chaque vue, le texte explique le schéma, il ne le remplace pas ;
* Se concentrer sur ce qui est **propre au métier de l'entreprise** ; les fonctions et applications support communes à toutes les entreprises ne sont pas à détailler ;
* Si une rubrique n'est pas applicable, ne la laissez pas vide : indiquez `N/A` ;
* `TODO` peut servir pendant la rédaction, mais **aucun `TODO` ne doit subsister dans le dossier remis** ;
* Les textes d'aide sous chaque titre du modèle décrivent ce qui est attendu : **remplacez-les** par votre contenu.

Les [diagrammes C4](https://c4model.com/) utilisent la personnalisation [C4 de PlantUML](https://github.com/plantuml-stdlib/C4-PlantUML). Il est possible d'utiliser l'éditeur en ligne [https://www.planttext.com/](https://www.planttext.com/) pour créer et modifier les diagrammes C4. Draw.io est également accepté (joindre le fichier `.drawio`).

## Terminologie

> 💡 Les documentations d'architecture utilisent souvent plusieurs termes synonymes pour le même concept, de façon interchangeable et possiblement ambiguë. Afin d'éviter toute confusion, nous avons choisi de définir précisément les termes utilisés dans ce modèle.

- **Fonction métier** : Capacité que l'entreprise doit exercer pour réaliser son activité (vendre, planifier, produire, livrer…), indépendamment des applications qui la supportent. C'est le socle de la vue métier de ce modèle.

- **Processus métier** : Enchaînement d'activités, portées par plusieurs fonctions et plusieurs acteurs, qui produit un résultat pour un client ou pour l'entreprise. Un processus traverse les fonctions ; on ne le représente que lorsqu'il est structurant pour le scénario.

- **Système de référence** (d'une donnée) : Application qui crée et met à jour une donnée et qui fait autorité sur elle ; les autres applications en reçoivent une copie. Un référentiel dédié à ce rôle pour plusieurs objets est un MDM.

- **Application** : Ensemble logiciel cohérent qui supporte une ou plusieurs fonctions métier. En architecture monolithique, une application d'un seul tenant ; en architecture microservices, un ensemble logique de modules.

- **Module** : Unité de code qui regroupe des fonctionnalités ou des services liés : API (qui contiennent des **endpoints**), traitements par lots ou **batchs** (qui contiennent des **jobs**), **IHM/GUI** (qui contiennent des pages).

- **Flux** : Échange d'information entre un acteur et une application, ou entre deux applications, caractérisé par sa nature (synchrone, asynchrone, batch), son protocole et son volume.

- **Composant d'infrastructure** : Exécutable tiers ou équipement proposant des services d'infrastructure : persistance pour une base de données, messaging pour les queues, répartition de charge pour un load-balancer, etc.

- **Modèle de déploiement** : Lieu où s'exécute la solution (on-premise, cloud public ou privé, sites locaux, edge, hybride).

- **Modèle de service** : Partage des responsabilités pour un composant — géré en propre, infrastructure louée, plateforme managée, logiciel en service ; dans le cloud, IaaS, PaaS ou SaaS.

- **Mode d'exécution** : Serveur physique, machine virtuelle, conteneur ou exécution sans serveur.

- **MCS (maintien en condition de sécurité)** : Ensemble des activités qui maintiennent le niveau de sécurité du SI dans le temps : mises à jour de sécurité, surveillance, gestion des vulnérabilités, réponse aux incidents.

- **Niveaux C4** : le modèle [C4](https://c4model.com/) décrit un système à quatre niveaux — contexte système (le SI et son environnement), conteneurs (les applications et services déployables), composants (l'intérieur d'une application), code — auxquels s'ajoutent deux diagrammes complémentaires : le diagramme **dynamique** (l'enchaînement des échanges pour un scénario) et le diagramme de **déploiement** (sur quels nœuds s'exécutent les conteneurs).
