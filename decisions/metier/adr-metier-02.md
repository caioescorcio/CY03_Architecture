# ADR-METIER-02 — Ajout de l'exigence EF-7 : maîtrise des données biométriques

## Statut
Acceptée

## Contexte
La direction envisage l'entrée par reconnaissance faciale dans les grands stades (EF-4) : 60 000 personnes en une heure sur 40 tourniquets. Le scénario précise que « personne n'a encore tranché ce qui serait conservé, où, pendant combien de temps, ni comment un spectateur pourrait revenir sur son accord ». Les données biométriques sont une catégorie particulière au sens de l'article 9 du RGPD. Elles exigent :
- un consentement explicite ;
- une analyse d'impact (AIPD) ;
- une stricte minimisation des données.

## Options envisagées
- **Ne rien ajouter** et traiter la question en phase de réalisation. L'architecture risquerait alors d'être construite sur un stockage centralisé et durable des visages, incompatible avec le RGPD et coûteux à corriger.
- **Interdire la reconnaissance faciale** et retirer EF-4. C'est sûr juridiquement, mais cela contredit la vision de la direction et ferme le segment des grands stades.
- **Ajouter une exigence EF-7** qui encadre EF-4 : consentement explicite et séparé de l'achat, retrait possible à tout moment avec effacement, conservation limitée à l'événement, scan toujours disponible.

## Critère décisif
L'article 9 du RGPD n'autorise la biométrie qu'avec un consentement explicite, libre (le scan doit donc rester une vraie alternative) et retirable. Le scénario laisse précisément ces points ouverts. Les fixer dès la vue métier conditionne les choix de stockage et d'hébergement des vues suivantes.

## Décision
Ajout de l'exigence **EF-7 (priorité 1 - Critique si EF-4 est réalisée)** :
- le consentement est explicite et distinct de l'achat ;
- il est retirable à tout moment, et son retrait entraîne l'effacement des données biométriques ;
- les données ne sont conservées que pendant la durée strictement nécessaire à l'événement ;
- le scan reste disponible pour tous.

## Conséquences
- La photo et le gabarit facial sont rattachés à un billet et à un événement, et non à un profil permanent. Ils sont effacés après l'événement.
- Le Shop doit proposer un parcours de retrait du consentement, et le support doit savoir le traiter.
- Une AIPD est un préalable à toute mise en service de EF-4, ce qui peut retarder ou bloquer le service.
- La complexité du service augmente pour une fonction facultative. C'est cohérent avec la priorité 3 de EF-4 : la fonction n'est lancée que si EF-7 est tenue.
