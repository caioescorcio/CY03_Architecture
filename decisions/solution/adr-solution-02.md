# ADR-SOLUTION-02 — Mode d'intégration : REST pour l'immédiat, événements pour le reste

## Statut
Acceptée

## Contexte
Une dizaine d'applications doivent échanger des données (§3.3). Certains échanges demandent une réponse immédiate : une place est-elle libre, le paiement est-il accepté (EF-1). D'autres peuvent attendre quelques secondes : statistiques (EF-3), listes de titres pour Access (EF-2). Les échanges secondaires ne doivent pas ralentir la vente en période de pointe (ENF-1). L'équipe compte 12 développeurs (ENF-3).

## Options envisagées
- **Tout en REST point à point.** C'est simple, mais chaque achat appellerait aussi Statistiques et Access : une lenteur de l'un d'eux ralentirait la vente, ce qui est inacceptable pendant un pic.
- **ESB central.** Il centralise les échanges, mais c'est un produit lourd à exploiter, qui demande une compétence rare et ajoute un point de passage unique : incompatible avec ENF-3.
- **REST pour les échanges qui demandent une réponse immédiate + bus d'événements managé pour le reste.** La vente reste rapide et les consommateurs se branchent sans modifier la vente ; en contrepartie, les copies ont quelques secondes de retard.

## Critère décisif
ENF-1 : pendant un pic, la vente ne doit attendre que l'Inventaire et le paiement. ENF-3 : un bus managé n'ajoute aucun serveur à exploiter.

## Décision
Les échanges qui demandent une réponse immédiate (réservation, paiement, revente) passent en **REST/JSON**. Tous les autres sont publiés comme **événements** sur un bus managé (topics `commande.payee`, `billet.emis`, `billet.invalide`, `acces.scan`), avec le pattern outbox.

## Conséquences
- Ajouter un consommateur (ex. Statistiques) ne change pas la vente.
- Les données copiées (statistiques, listes Access) ont quelques secondes de retard : Studio affiche l'heure de mise à jour.
- Les consommateurs doivent ignorer les messages reçus en double (idempotence).
