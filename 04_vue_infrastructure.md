# 4. Vue infrastructure

> **Vue obligatoire.** Elle montre **où et comment s'exécute le SI** : lieux d'hébergement, réseaux, modes d'exécution, stockage, continuité, exploitation. Le dimensionnement fin des machines (CPU, RAM) n'est pas attendu ; les ordres de grandeur qui pèsent sur l'architecture — volumétries de stockage, débits réseau — le sont quand le scénario les justifie.

## 4.1 Hébergement et répartition du SI
> **Schéma obligatoire** : les lieux d'hébergement (datacenter on-premise, cloud public ou privé, sites locaux, edge…) et, pour chacun, les parties du SI qui s'y trouvent.
>
> Le **diagramme de déploiement C4** convient bien ici : il place les conteneurs du §3.1 sur les nœuds où ils s'exécutent. Un schéma d'infrastructure classique est également accepté, à condition qu'on retrouve les applications du chapitre 3.

Expliquez pourquoi chaque partie du SI est hébergée à cet endroit. Le modèle de déploiement retenu fait l'objet d'un **ADR obligatoire**, qui montre en quoi il découle du contexte de l'entreprise.

## 4.2 Réseaux et interconnexions
Comment les sites, le cloud, les utilisateurs et les partenaires sont reliés (Internet, VPN, liaisons dédiées, SD-WAN…), la segmentation principale, et ce qui se passe en cas de perte d'une liaison.

Quand un flux du §3.3 est volumineux ou contraint en temps de réponse, donnez l'**ordre de grandeur du débit nécessaire** et vérifiez qu'il est compatible avec la liaison prévue.

## 4.3 Modèle de service et mode d'exécution
Pour les composants importants, précisez **qui opère quoi** et **comment le composant s'exécute** :

- modèle de service : matériel et logiciel gérés en propre, infrastructure louée, plateforme managée ou logiciel en service — soit, dans le cas du cloud, IaaS, PaaS ou SaaS ;
- mode d'exécution : serveur physique, machine virtuelle, conteneur, exécution sans serveur.

Pour chaque produit ou service cité, montrez que ce partage est compris : ce qui reste à la charge de l'entreprise et ce qui revient au fournisseur.

## 4.4 Stockage et volumétries
Les principaux jeux de données du §3.4, leur volume (actuel et prévu), et la technologie de stockage retenue (base relationnelle, NoSQL, stockage objet, fichiers…) **avec la raison du choix**. Le choix de persistance d'au moins un jeu de données important fait l'objet d'un **ADR obligatoire**.

## 4.5 Sauvegarde et continuité de service
Ce qui est sauvegardé et où, les objectifs de reprise (RTO / RPO) pour les applications critiques, et les dispositifs de continuité (redondance, site de secours, fonctionnement en mode dégradé).

## 4.6 Exploitation
**Qui exploite chaque partie du SI** (équipe interne, infogérant, éditeur, hébergeur), comment elle est supervisée, et quels engagements de service (SLA) sont attendus.

## 4.7 Impact de l'évolution sur l'infrastructure
Ce que l'évolution ou l'innovation du scénario change : nouveaux sites, nouvelles volumétries ou débits, nouveaux besoins de disponibilité ou de latence.
