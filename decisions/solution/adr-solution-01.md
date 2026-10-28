# ADR-SOLUTION-01 — File d'attente virtuelle : produit du marché

## Statut
Acceptée

## Contexte
Lors d'une mise en vente, 180 000 personnes arrivent en 3 minutes (40 000 req/s, soit 200 fois la charge normale, ENF-1). Les acheteurs doivent être servis dans l'ordre et connaître leur position (EF-1). L'équipe compte 12 développeurs, sans astreinte (ENF-3). La douzaine de mises en vente critiques est connue à l'avance.

## Options envisagées
- **Pas de file, uniquement de l'autoscaling.** Pas de composant en plus ; mais aucune base ne passe de 200 à 40 000 req/s en quelques secondes, l'ordre d'arrivée n'est pas garanti et il faut payer une forte capacité pendant les pics (ENF-4).
- **File développée en interne.** Contrôle total ; mais c'est le composant le plus exposé de toute la plateforme, à construire, tester en charge et surveiller par 12 développeurs sans astreinte.
- **File d'attente SaaS du marché** (ex. Queue-it, Cloudflare Waiting Room). Elle absorbe le pic chez le fournisseur et laisse passer les acheteurs au débit que la plateforme supporte ; en contrepartie, BilletLive dépend d'un fournisseur et paie un abonnement.

## Critère décisif
ENF-3 : l'équipe ne peut pas exploiter elle-même le composant qui reçoit le pic le plus fort. ENF-1 : avec la file SaaS, la plateforme ne voit qu'un débit choisi, et non 40 000 req/s.

## Décision
La file d'attente est un **produit SaaS du marché**, placé devant Shop Web. Il remet à chaque acheteur un jeton signé que l'API Vente vérifie.

## Conséquences
- La plateforme n'est dimensionnée que pour le débit choisi en sortie de la file.
- L'abonnement entre dans le coût par billet (ENF-4) et doit être comparé entre fournisseurs.
- Dépendance au fournisseur : prévoir un mode dégradé (fermeture temporaire de la vente) en cas de panne de la file.
