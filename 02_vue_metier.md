# 2. Vue métier

> **Vue obligatoire**, présentée au point d'étape de la séance 4. Elle décrit **ce que le SI doit permettre à l'entreprise de faire** et **qui l'utilise**. On attend une analyse du besoin, pas un résumé de l'histoire de l'entreprise.

## 2.1 Fonctions métier principales
> **Schéma obligatoire** : cartographie des fonctions métier que le SI doit supporter, avec leurs principaux enchaînements (par exemple : vendre → planifier → produire → livrer → facturer).
>
> Formalisme libre (blocs fonctionnels, BPMN pour un processus) : **le modèle C4 ne s'applique pas à ce niveau**, il commence au chapitre 3.

Une **fonction métier** est une capacité que l'entreprise doit exercer, indépendamment des applications qui la supportent. Décrivez chaque fonction en quelques lignes : son rôle dans le métier de l'entreprise, les informations qu'elle manipule, les fonctions dont elle dépend. Si un **processus** particulier du scénario est structurant (un enchaînement d'activités entre plusieurs fonctions et plusieurs acteurs), représentez-le en complément.

Concentrez-vous sur les fonctions **propres au métier de l'entreprise**. Les fonctions support communes à toutes les entreprises (RH, paie, comptabilité générale, messagerie…) ne sont pas à détailler : elles peuvent apparaître sur le schéma comme un simple bloc.

## 2.2 Acteurs du SI
Les acteurs majeurs du système d'information, internes et externes : collaborateurs, clients, partenaires, fournisseurs, systèmes externes.

| Acteur | Interne / externe | Rôle | Fonctions métier utilisées |
|:-------- |:-------- |:-------- |:-------- |
| *…* | *…* | *…* | *…* |

## 2.3 Exigences
Reprenez les exigences fonctionnelles (EF) et non fonctionnelles (ENF) du scénario, numérotez-les (EF-1, ENF-1…) et **classez-les par priorité**. Si vous ajoutez des exigences au scénario, signalez-les comme telles et justifiez-les dans un ADR du répertoire `decisions/metier/`.

## 2.4 Impact de l'évolution sur les fonctions et les acteurs
Les changements introduits par l'évolution ou l'innovation souhaitée par l'entreprise : **fonctions nouvelles ou transformées, acteurs nouveaux ou dont le rôle change**. Faites-les apparaître sur le schéma du §2.1 (couleur ou légende).
