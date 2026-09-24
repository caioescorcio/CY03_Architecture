# 5. Vue cybersécurité

> **Vue obligatoire.** Il s'agit de protéger le SI **au bon niveau** : des mesures proportionnées à la sensibilité des données et aux risques réels du scénario, et réalistes au regard de la taille de l'entreprise. Empiler des technologies hors contexte ne rapporte pas de points.

## 5.1 Sensibilité des données et des flux
Les objets métier du §3.4 et les flux du §3.3, classés selon leur sensibilité (données personnelles, données de paiement, secrets industriels, données de sûreté…), les obligations qui s'y attachent (RGPD, contrats…) et les principales menaces qui les visent.

## 5.2 Identités et accès
Comment les utilisateurs (internes, clients, partenaires) s'authentifient et comment leurs droits sont gérés, et **comment les applications s'authentifient entre elles**. Ce mécanisme fait l'objet d'un **ADR obligatoire**, qui couvre les deux cas.

## 5.3 Mécanismes de protection

> Pas de schéma obligatoire ici. Si un schéma aide (zones de confiance, exposition sur Internet, chemins d'accès), reprenez le schéma du §3.1 ou du §4.1 en y ajoutant les mesures, plutôt que d'en dessiner un nouveau.
Les mécanismes importants à mettre en place, rattachés aux données et aux flux du §5.1 qu'ils protègent : chiffrement, segmentation réseau, filtrage, gestion des secrets, journalisation et détection…

## 5.4 Maintien en condition de sécurité (MCS)
Qui assure le **maintien en condition de sécurité** du SI (équipe interne, prestataire, éditeurs, hébergeur), au regard de la structure de l'entreprise : mises à jour de sécurité, surveillance, réponse aux incidents.

## 5.5 Impact de l'évolution sur les risques
Les risques nouveaux introduits par l'évolution ou l'innovation du scénario, et les mesures qui y répondent.
