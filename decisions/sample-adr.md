# ADR-<DOMAINE>-<NN> — Titre simple de la décision

> Modèle commenté. Copiez ce fichier dans `decisions/metier/`, `decisions/solution/` ou `decisions/infrastructure/` sous le nom `adr-<domaine>-<NN>.md`, remplacez les rubriques « Ce que doit contenir » et « Exemple » par votre contenu, puis référencez l'ADR dans le tableau du §6.3 des annexes.
>
> ⚠️ Un ADR qui ne contient pas **au moins deux options écartées** et **le critère, issu du scénario, qui a fait pencher la balance** ne rapporte pas de points.

## Statut
**Ce que doit contenir :**  
Le statut actuel de la décision (par exemple : Proposée, Acceptée, Rejetée, Supplantée par ADR-xxx).

**Exemple :**  
Acceptée

## Contexte
**Ce que doit contenir :**  
Le problème ou le besoin ayant mené à la décision, **exprimé avec les éléments du scénario** : exigences (EF/ENF) concernées, contraintes réglementaires, volumétries, taille et compétences des équipes, existant.

**Exemple :**  
Le SI doit faire communiquer douze applications hétérogènes (ERP, CRM, portail client, facturation…). Trois progiciels de l'existant ne savent échanger que par fichiers. Le portail client doit afficher le statut d'une commande moins de 5 secondes après sa mise à jour dans l'ERP (ENF-2). L'équipe d'intégration compte deux personnes.

## Options envisagées
**Ce que doit contenir :**  
Au moins **trois options** (la retenue et au moins deux écartées), chacune avec ses avantages et inconvénients **dans ce contexte précis**. Des alternatives citées pour la forme, sans analyse, ne comptent pas.

**Exemple :**
- **Intégration point à point** entre chaque application — simple au départ ; mais jusqu'à 66 interfaces à maintenir pour douze applications, ingérable par deux personnes.
- **ESB centralisant tous les échanges** — sait gérer les échanges de fichiers des trois progiciels ; mais produit lourd, compétence rare, et la latence d'une orchestration centrale ne garantit pas les 5 secondes de l'ENF-2.
- **Messagerie d'événements (broker) + API Gateway**, avec des connecteurs fichier pour les trois progiciels — découplage et temps réel ; mais cohérence à terme (*eventual consistency*) à gérer côté portail.

## Critère décisif
**Ce que doit contenir :**  
Le ou les critères **rattachés au scénario** qui ont fait pencher la balance. Un critère générique (« X est plus répandu », « X est moderne ») n'est pas recevable.

**Exemple :**  
L'ENF-2 (statut visible en moins de 5 s) écarte l'échange par fichiers et l'orchestration centrale ; la taille de l'équipe (deux personnes) écarte le point à point.

## Décision
**Ce que doit contenir :**  
La solution retenue, formulée sans ambiguïté.

**Exemple :**  
Les échanges inter-applicatifs passent par un broker de messages publiant les événements métier ; les trois progiciels y sont raccordés par des connecteurs fichier ; les appels synchrones exposés à l'extérieur passent par l'API Gateway.

## Conséquences
**Ce que doit contenir :**  
Les impacts de la décision, **positifs et négatifs**. Les conséquences négatives doivent être assumées, et si possible accompagnées de la mesure qui les compense.

**Exemple :**
- Ajout d'une nouvelle application sans modifier les existantes (abonnement aux événements).
- Le portail peut afficher un statut en retard de quelques secondes : un horodatage de dernière mise à jour est affiché à l'utilisateur.
- Le broker devient un composant critique : il doit être redondé (voir vue infrastructure) et supervisé.
- Montée en compétence nécessaire de l'équipe d'intégration sur le broker retenu.
