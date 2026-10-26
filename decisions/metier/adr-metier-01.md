# ADR-METIER-01 — Ajout de l'exigence ENF-7 : protection des données personnelles et des flux financiers

## Statut
Acceptée

## Contexte
Le scénario cite parmi les enjeux la protection « des données personnelles et des flux financiers pour le compte de tiers », mais n'en fait pas une exigence numérotée. Or la plateforme a les caractéristiques suivantes :
- elle traite les données de millions de spectateurs (6,2 M de billets en 2025, puis × 3 en deux ans), pour le compte de 1 400 organisateurs ;
- elle encaisse des fonds qui appartiennent aux organisateurs, via BilletLive Pay ;
- elle s'ouvre à trois nouveaux pays de l'UE.

Sans exigence explicite, aucune vue n'est tenue de justifier ses mesures de protection.

## Options envisagées
- **Ne pas ajouter d'exigence** et laisser la protection à la vue cybersécurité. C'est plus simple, mais la vue métier ne trace alors aucune obligation et les choix des vues applicative et infrastructure ne s'y rattachent pas.
- **Une exigence générique « le SI est sécurisé »**. Elle n'est ni vérifiable ni rattachée à une réglementation, donc elle ne guide aucun choix.
- **Une exigence ENF-7 explicite** qui cite le RGPD, la DSP2 et PCI-DSS, avec l'engagement qu'aucune donnée de carte ne passe par BilletLive. Elle est vérifiable et oriente les choix : prestataire de paiement agréé, minimisation des données.

## Critère décisif
Le chiffre d'affaires repose sur la confiance des organisateurs. Les obligations RGPD (BilletLive agit comme sous-traitant), DSP2 (authentification forte) et PCI-DSS s'imposent dès aujourd'hui. Avec une équipe de 12 développeurs (ENF-3), le seul moyen réaliste de tenir PCI-DSS est de ne jamais manipuler de données de carte. Cette contrainte doit donc être écrite noir sur blanc.

## Décision
Ajout de l'exigence **ENF-7 (priorité 1 - Critique)** : les données personnelles des spectateurs et les flux financiers pour compte de tiers sont protégés selon le RGPD, la DSP2 et PCI-DSS. Aucune donnée de carte n'est stockée ni traitée par BilletLive.

## Conséquences
- Le paiement est entièrement délégué au prestataire agréé, avec une page ou un composant de paiement hébergé chez lui, ce qui réduit fortement le périmètre PCI-DSS.
- La vue cybersécurité (chapitre 5) doit rattacher ses mesures à ENF-7.
- Les contrats avec les organisateurs doivent préciser les rôles RGPD (responsable de traitement et sous-traitant).
- BilletLive dépend davantage du prestataire de paiement, ce qui est compensé par le choix d'un prestataire européen qui couvre les 4 pays.
