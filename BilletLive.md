#### Scénario 1 : BilletLive — Plateforme de Billetterie Événementielle

**Contexte de l'entreprise**

BilletLive est une entreprise nantaise créée en 2019 par deux anciens responsables de salles de spectacle. Elle édite une plateforme de billetterie en marque blanche utilisée par 1 400 organisateurs : salles de concert, festivals, clubs sportifs, théâtres et musées. En 2025, 6,2 millions de billets ont été vendus au travers de la plateforme, pour un chiffre d'affaires de 14 millions d'euros généré par une commission moyenne de 4 % sur le prix du billet.

L'entreprise compte 38 collaborateurs : douze développeurs, un ingénieur plateforme, neuf commerciaux chargés du recrutement et du suivi des organisateurs, huit personnes au support client et huit aux fonctions support. Il n'existe ni équipe d'exploitation, ni astreinte système constituée, ni service informatique interne distinct de l'équipe produit. L'équipe technique est jeune et à l'aise avec les pratiques d'ingénierie modernes — intégration et déploiement continus, infrastructure décrite sous forme de code, observabilité — mais n'a aucune compétence en administration de matériel et revendique de ne jamais avoir possédé de serveur.

L'offre repose sur quatre produits. BilletLive Shop _(avec mention manuscrite : B2B2C)_ est la boutique de vente en ligne, déclinée aux couleurs de chaque organisateur. BilletLive Studio est le back-office par lequel l'organisateur construit son plan de salle, définit ses catégories tarifaires, ses quotas et ses filières de distribution. BilletLive Access est l'application de contrôle d'accès, utilisée sur smartphone par les bénévoles de festivals comme sur des douchettes professionnelles. BilletLive Pay assure l'encaissement, via un prestataire de paiement agréé, puis le reversement aux organisateurs.

Le profil de charge de la plateforme est extrême et parfaitement irrégulier. Lors d'une mise en vente de festival, 180 000 personnes se présentent en trois minutes et la plateforme doit encaisser des pointes de 40 000 requêtes par seconde ; le reste de l'année, elle en traite environ 200. Une douzaine de mises en vente critiques ponctuent l'année, dont les dates sont connues plusieurs semaines à l'avance.

**Enjeux de l'entreprise**

Absorber des pics de charge deux cents fois supérieurs à la normale sans jamais survendre une place, garantir le contrôle d'accès sur des sites parfois dépourvus de réseau, protéger des données personnelles et des flux financiers pour le compte de tiers, et maintenir un coût d'infrastructure compatible avec une commission de 4 %.

**Vision et évolution**

BilletLive prépare son ouverture à la Belgique, à l'Espagne et au Portugal, avec un objectif de triplement du volume de billets en deux ans. L'entreprise vise également un segment nouveau pour elle : la billetterie de grands stades de 60 000 places, où le contrôle d'accès doit traiter plusieurs dizaines de milliers d'entrées en moins d'une heure, sur une quarantaine de tourniquets simultanés.

Un nouveau produit, BilletLive Resale, doit permettre la revente encadrée entre particuliers : un billet remis en vente est invalidé et un nouveau titre nominatif est émis à l'acheteur, l'organisateur conservant la maîtrise du prix plafond et du nombre de reventes autorisées. Ce service crée une exigence de cohérence forte, un même billet ne pouvant en aucun cas exister deux fois.

Les organisateurs réclament par ailleurs un accès en temps réel à leurs ventes et à leurs entrées pendant l'événement, ainsi qu'un état de reversement plus détaillé que le récapitulatif mensuel actuel.

Enfin, la direction veut faire disparaître le billet lui-même. Sur les grands stades, où quarante tourniquets doivent absorber 60 000 personnes en une heure, elle envisage de proposer au spectateur qui le souhaite de s'enregistrer à l'avance avec une photographie et de franchir ensuite le tourniquet par reconnaissance faciale, sans billet ni téléphone. Le service serait facultatif et réservé aux spectateurs qui l'acceptent explicitement, les autres continuant à passer par le scan. Personne dans l'entreprise n'a encore tranché la question de savoir ce qui serait conservé, où, pendant combien de temps, ni comment un spectateur pourrait revenir sur son accord.

#### Exigences structurantes

**Exigences fonctionnelles**

- **File d'attente équitable et unicité de la place :** À l'ouverture d'une mise en vente, le système doit ordonner les acheteurs dans une file d'attente, leur restituer leur position, et garantir qu'une même place ne peut jamais être vendue deux fois, y compris en situation de revente.

- **Contrôle d'accès en environnement dégradé :** Le système doit valider un billet en moins de 300 millisecondes sur le lieu de l'événement, y compris lorsque celui-ci ne dispose d'aucune connectivité, puis réconcilier les scans a posteriori sans jamais accepter deux fois le même titre.

- **Reversement traçable aux organisateurs :** Le système doit produire pour chaque organisateur un état de reversement détaillé à la transaction, rapprochable avec les mouvements constatés chez le prestataire de paiement.

**Exigences non fonctionnelles**

- **Absorption des pics de charge :** La plateforme doit supporter un facteur deux cents entre sa charge nominale et sa charge de pointe, sur des créneaux connus à l'avance, sans intervention manuelle de mise à l'échelle et sans que cette capacité soit immobilisée le reste de l'année.

- **Coût à la transaction mesurable :** Le coût d'infrastructure par billet vendu doit rester inférieur à 0,04 euro et être mesurable par organisateur et par événement.

- **Exploitabilité par une petite équipe :** La plateforme doit être exploitable par une équipe de douze développeurs sans astreinte système dédiée 24 heures sur 24, ce qui impose de limiter au strict nécessaire le nombre de composants dont l'entreprise assure elle-même le maintien en condition opérationnelle.
