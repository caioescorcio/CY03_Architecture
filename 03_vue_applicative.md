# 3. Vue applicative

> **Vue obligatoire.** Elle se déduit de la vue métier : **quelles applications supportent quelles fonctions, comment elles échangent, et où se trouve la référence de chaque donnée**. Le type d'architecture applicative doit être explicitement tranché, et les schémas doivent se trouver dans le dossier, pas seulement dans le support de présentation.

## 3.1 Cartographie applicative
> **Deux schémas obligatoires**, qui sont les deux premiers niveaux du modèle C4 (au moins une vue du dossier doit être formalisée en C4 : c'est ici qu'on l'attend) :
>
> - **Niveau 1 — contexte système** : le SI de l'entreprise vu comme un tout, les acteurs (§2.2) et les systèmes externes autour de lui. C'est le schéma d'ensemble lisible en une page, sans commentaire oral.
> - **Niveau 2 — conteneurs** : les applications importantes pour le métier, leurs flux, et les acteurs qui les utilisent.
>
> Le **niveau 3 (composants, l'intérieur d'une application) n'est pas attendu**, sauf si une application mérite d'être détaillée pour le scénario. Légende explicite et niveaux cohérents entre eux dans les deux cas.

Expliquez les schémas : comment les applications se répartissent les fonctions métier du §2.1, et quelles applications sont nouvelles, conservées ou remplacées.

## 3.2 Applications principales
Pour chaque application importante :

| Application | Fonctions métier couvertes | Usage et utilisateurs | Produit du marché / développement spécifique | Technologies |
|:-------- |:-------- |:-------- |:-------- |:-------- |
| *…* | *…* | *…* | *…* | *…* |

Pour au moins un composant important, le choix entre produit du marché et développement spécifique fait l'objet d'un **ADR obligatoire**.

## 3.3 Flux applicatifs
Les échanges entre acteurs et applications, et entre applications :

| Flux | Source → cible | Nature (synchrone / asynchrone / batch) | Protocole / format | Volume ou fréquence |
|:-------- |:-------- |:-------- |:-------- |:-------- |
| *…* | *…* | *…* | *…* | *…* |

> **Diagramme de séquence obligatoire**, sur un flux réellement intéressant du scénario (pas un simple CRUD), en UML ou en **C4 dynamique** (le diagramme dynamique de C4, qui numérote les échanges entre les conteneurs du niveau 2) :
> - au moins trois acteurs ou composants, sans omettre de participant clé ;
> - protocoles, messages échangés, URL (si API REST), topics (si messagerie) ;
> - au moins un cas d'erreur (timeout, rejet, indisponibilité d'un composant…).

## 3.4 Données et systèmes de référence
Pour les principaux objets métier manipulés par le SI (client, commande, produit, contrat, équipement…), indiquez **quelle application fait référence** pour cette donnée — c'est elle qui la crée et la met à jour — et comment elle est diffusée aux autres applications.

| Objet métier | Système de référence | Applications consommatrices | Mode de propagation (API, événement, réplication, batch) |
|:-------- |:-------- |:-------- |:-------- |
| *…* | *…* | *…* | *…* |

Signalez les données dupliquées et ce que cela implique (fraîcheur, risque d'incohérence), et le cas échéant le recours à un référentiel dédié (MDM). Les volumétries de ces données sont traitées en [§4.4](04_vue_infrastructure.md), leur sensibilité en [§5.1](05_vue_cybersecurite.md).

## 3.5 Choix d'architecture applicative
Le **type d'architecture retenu** (monolithe modulaire, n-tiers, microservices, événementielle, serverless…), le **mode d'intégration** entre applications (API, messagerie, bus d'entreprise ou ESB, échange de fichiers…) et les principaux patterns utilisés (API Gateway, cache, CQRS, circuit breaker…), y compris ceux qui servent la performance et la résilience attendues par les ENF du §2.3. Le mode d'intégration fait l'objet d'un **ADR obligatoire**.

## 3.6 Impact de l'évolution sur les applications et les flux
Ce que l'évolution ou l'innovation du scénario ajoute ou change : nouvelles applications, nouveaux flux, nouvelles données, nouvelles contraintes de volume ou de temps de réponse.
