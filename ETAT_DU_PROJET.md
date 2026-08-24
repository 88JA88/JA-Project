# État du projet

## Règles de travail

- Les règles permanentes sont consignées dans `AGENTS.md`.
- Aucune modification du programme ne doit être effectuée sans l’accord préalable de l’utilisateur.
- Le présent état a été établi par lecture de `index.html` et de `planning.json` dans l’emplacement actuel du projet. Le programme avait temporairement porté le nom `Reseau_PERT.html`.

## Fichiers principaux examinés

- `index.html` : application web autonome « Réseau PERT », composée d’un seul fichier HTML avec CSS et JavaScript intégrés (3 501 lignes, 122 048 octets après la suppression complète de la démonstration).
- `planning.json` : fichier de projet PERT au format JSON, syntaxiquement valide, déclaré au format `planning-reseau`, version 1.
- Aucun autre fichier du programme n’a été modifié lors de ce relevé.

## Fonctionnalités présentes dans `index.html`

- Création, édition, déplacement, sélection et suppression d’activités. Sur iPad, un appui long immobile de 0,7 seconde ouvre la fiche de description et de ressources.
- Création, sélection et suppression de liaisons entre activités, avec prévention des cycles. Sur écran tactile, un premier toucher sélectionne la flèche et un second toucher sur la flèche bleue propose sa suppression après confirmation.
- Calcul du planning à partir des dépendances et des contraintes de début : dates au plus tôt, dates au plus tard, marges, activités et liaisons critiques.
- Gestion d’un catalogue de ressources avec nom, discipline et coût unitaire.
- Affectation de ressources aux activités avec durée d’intervention et calcul des coûts.
- Résumé des ressources utilisées et tableau détaillé des affectations.
- Contrôle du budget mensuel avec seuil, répartition des coûts par mois et signalement des dépassements.
- Vérification de cohérence du projet : identifiants, durées, dates, ressources, liaisons, cycles, dépendances et chevauchements d’utilisation des ressources.
- Ouverture et enregistrement de projets JSON, création d’un nouveau projet et liaison directe à un fichier lorsque l’API du navigateur est disponible.
- Sauvegarde automatique du planning et du catalogue de ressources dans le stockage local du navigateur.
- Impression du réseau avec mise à l’échelle automatique.
- Mode d’emploi succinct accessible dans une fenêtre par un bouton placé à côté d’« Imprimer ».
- Sur écran tactile, la date de début est resserrée contre le calendrier et séparée de la liste des ressources.
- Au démarrage, l’application reprend uniquement le dernier projet personnel mémorisé ; en l’absence de sauvegarde, le planning reste vide. Aucun projet de démonstration n’est inclus ni chargé.

## État des données dans `planning.json`

- Unité : jour (`j`).
- Seuil de budget mensuel : 4 000 €.
- 3 ressources :
  - `r1` — Res 2, Discipline B, 400 €/j ; durée affectée totale 7 j ; coût total 2 800 €.
  - `r2` — Res 3, Discipline C, 800 €/j ; durée affectée totale 7,5 j ; coût total 6 000 €.
  - `r3` — Res 1, Discipline A, 550 €/j ; durée affectée totale 7,5 j ; coût total 4 125 €.
- 5 activités, représentant 23 jours de durée d’activité cumulée.
- 12 affectations de ressources, représentant 22 jours d’affectation cumulés.
- 6 liaisons : `1 → 4`, `4 → 2`, `3 → 2`, `1 → 3`, `1 → 5` et `5 → 2`.
- Coût total calculé des affectations : 12 925 €.
- Coût par activité :
  - activité 1, « Recueil des données existantes » : 2 700 € ; durée 5 j ; contrainte de début au 20 août 2026 ;
  - activité 2, « propositions des membres de l'équipe » : 2 800 € ; durée 3 j ;
  - activité 3, « Réunions sectorielles » : 2 175 € ; durée 8 j ; contrainte de début au 3 août 2026 ;
  - activité 4, « Répartition du travail » : 3 500 € ; durée 4 j ;
  - activité 5, « Appels à contribution » : 1 750 € ; durée 3 j.

## État du dépôt constaté avant cette intervention

- `index.html` comportait déjà une modification locale non validée dans Git : réduction de l’espacement du tableau des affectations et ajout d’une hauteur de ligne.
- `planning-ESSAI.json` apparaissait déjà supprimé dans l’état Git.
- `planning-2026-08-13 (2).json` apparaissait déjà comme fichier non suivi par Git.
- Ces changements préexistants ont été conservés sans aucune modification.

## Vérifications effectuées

- Lecture complète des deux fichiers demandés.
- Validation de la syntaxe JSON avec `jq`.
- Contrôle statique de la structure, des ressources, activités, affectations et liaisons du JSON.
- Calcul indépendant des totaux de durées et de coûts indiqués ci-dessus.
- Test fonctionnel effectué le 14 août 2026 dans le navigateur intégré, via un serveur local temporaire.
- Ouverture de l’application et chargement de `planning-2026-08-13 (2).json` réussis, sans erreur ni avertissement dans la console du navigateur.
- Affichage des 5 activités, de leurs ressources, dates, marges et coûts confirmé.
- Le planning parallèle actuel s’étend du 20 août au 5 septembre 2026 ; le chemin critique principal est `1 → 3 → 2`.
- Tableau des affectations confirmé : 12 affectations, 22 j et 12 925 € au total.
- Budget mensuel du planning parallèle : 9 853,13 € en août 2026 et 3 071,87 € en septembre 2026 ; août dépasse le seuil de 4 000 €, septembre est conforme et la somme reste exactement égale à 12 925,00 €.
- Le premier test dans le navigateur signalait 9 avertissements : 4 ressources parasites ensuite corrigées et 5 chevauchements désormais supprimés par le séquencement des activités.
- Ouverture des formulaires de création, de modification et de détails d’une activité confirmée ; aucune donnée de test n’a été enregistrée.
- Un test complet a confirmé le fonctionnement du programme et l’absence d’erreur de console avant le retour au planning parallèle.
- Après restauration du parallélisme, le contrôle confirme 6 liaisons valides, aucune boucle et deux besoins consolidés de personnel décrits ci-dessous.

## Règle métier des ressources

- La durée affectée à une ressource représente une charge totale en jours-personne.
- La ressource organise librement cette charge à l’intérieur de la période de l’activité.
- Aucun effectif disponible n’est enregistré dans le projet : en phase de conception, le planning exprime les moyens estimés nécessaires et les communique aux intéressés.
- Le logiciel établit uniquement le diagnostic de charge et le besoin estimé en personnes. Le choix entre répartir la charge et agir sur le planning appartient aux responsables du projet et à la ressource concernée.
- Pour l’estimation, chaque charge est répartie uniformément dans la fenêtre de son activité. Les charges simultanées sont additionnées et arrondies au nombre entier supérieur lorsque leur moyenne dépasse une personne.
- Les ressources sans aucune affectation restent disponibles dans le catalogue, mais ne sont pas mentionnées dans le rapport de vérification.

## État des anomalies constatées pendant le test manuel

1. **Corrigée le 14 août 2026.** À l’ouverture d’un projet JSON, l’application charge désormais une copie exacte des ressources contenues dans le projet au lieu de les fusionner avec le catalogue local. Le test avec `planning-2026-08-13 (2).json` confirme la présence des 3 seules ressources attendues et la disparition des 4 avertissements parasites.
2. **Diagnostic initial invalidé le 14 août 2026.** L’activité 4 est bien enregistrée avec `y = 2`, mais sa date, son cadre et son titre sont entièrement visibles à l’ouverture lorsque la zone est à son défilement initial (`scrollTop = 0`). La capture qui semblait montrer un masquage avait été réalisée après un défilement automatique provoqué par une interaction de test. Aucune correction du programme n’est nécessaire sur ce point.
3. **Corrigée le 14 août 2026.** Le texte d’aide décrit désormais les interactions réelles : double-clic dans le vide pour créer une activité, clic gauche sur une activité pour la sélectionner, double-clic gauche pour la modifier et clic droit pour renseigner ses détails.
4. **Corrigée le 14 août 2026.** Les coûts mensuels sont désormais répartis en centimes selon la méthode des plus forts restes. Leur somme affichée est garantie égale au coût daté total arrondi : 9 853,13 € + 3 071,87 € = 12 925,00 € avec le planning actuel.
5. **Corrigée le 14 août 2026 après clarification métier.** Les cinq anciens avertissements de chevauchement par paire sont remplacés par deux diagnostics consolidés : 2 personnes du 25 au 28 août 2026 pour « Res 1 — Discipline A » (charge moyenne maximale 1,15 personne) et 2 personnes sur la même période pour « Res 3 — Discipline C » (charge moyenne maximale 1,08 personne). Le rapport ne formule aucune proposition d’action.

6. **Corrigée le 24 août 2026.** Sur GitHub Pages, le chargement asynchrone de `planning.json` pouvait se terminer après l’ouverture d’un JSON personnel et remplacer celui-ci par la démonstration intégrée. Toute ouverture, liaison ou création volontaire annule désormais définitivement ce chargement initial.
7. **Solution intermédiaire retirée le 24 août 2026.** La démonstration avait été séparée dans `planning-demo.json` et rendue accessible par un bouton « Démo ».
8. **Corrigée le 24 août 2026.** À la demande de l’utilisateur, `planning-demo.json`, le bouton « Démo » et tout le code associé sont supprimés. La clé de sauvegarde GitHub Pages est renouvelée afin que toute ancienne démo déjà mémorisée soit également ignorée, sans modifier la sauvegarde utilisée par le fichier HTML ouvert directement sur l’ordinateur.

## Fait lors de cette intervention

- Création de `AGENTS.md` à partir des règles permanentes de référence.
- Création et renseignement de `ETAT_DU_PROJET.md` d’après l’état réel des fichiers examinés.
- Exécution du test manuel autorisé et ajout de ses résultats au présent document.
- Correction validée dans `index.html` : suppression de la fusion automatique entre les ressources d’un projet ouvert et le catalogue local.
- Test de non-régression ciblé réussi : 3 ressources attendues, aucune erreur bloquante, 5 avertissements de chevauchement réels et aucune erreur de console.
- Contrôle géométrique ciblé de l’activité 4 : date à 2 px du haut de la zone, cadre à 36 px et titre à 46 px ; le masquage supposé n’est pas reproductible à l’ouverture.
- Correction du texte d’aide pour le rendre conforme aux interactions réellement programmées.
- Correction de la répartition des arrondis mensuels et test ciblé réussi : somme mensuelle égale au total général, écarts au seuil cohérents et aucune erreur de console.
- Ajout validé des liaisons `4 → 3` et `3 → 5` dans `planning-2026-08-13 (2).json` ; contrôle réussi de la structure, de l’absence de cycle, des nouvelles dates et de l’absence de chevauchement.
- Test fonctionnel final réussi dans le navigateur avec le programme et les données à jour ; aucune nouvelle anomalie détectée et aucune donnée de test enregistrée.
- Après clarification métier, retrait validé des liaisons artificielles `4 → 3` et `3 → 5` et restauration du planning parallèle initial ; JSON valide, sans cycle, avec cinq sollicitations simultanées attendues.
- Remplacement validé des avertissements de chevauchement par l’estimation des besoins en personnel à partir des charges en jours-personne ; test réussi avec 0 erreur, 2 propositions consolidées et aucune erreur de console.
- Contrôle de non-régression réussi : total des affectations inchangé à 22 j et 12 925,00 €, budget inchangé à 9 853,13 € en août et 3 071,87 € en septembre.
- Suppression validée de l’avertissement concernant les ressources sans affectation. Test réussi avec une ressource temporaire non utilisée : elle reste dans le catalogue, n’apparaît pas dans le rapport et les deux seules alertes restent les besoins estimés de personnel. La session de test a ensuite été restaurée avec les 3 ressources du JSON.
- Allègement validé du libellé des besoins estimés : « organisation à confirmer avec la ressource », sans le mot « manuellement ».
- Suppression validée de toute proposition dans les avertissements de charge. Le rapport conserve uniquement le diagnostic compact afin de laisser davantage de place à un planning plus long.
- Ajout validé dans `Reseau_PERT.html` d’un bouton « Mode d’emploi » à côté d’« Imprimer ». Il ouvre une fenêtre d’aide centrée sur les manipulations, avec contenu défilable et bouton de fermeture ; le test dans le navigateur confirme son ouverture et sa fermeture. `planning.json` n’a pas été modifié.

- Ajout validé dans `index.html` de la suppression tactile d’une liaison : appui long de 0,7 seconde sur la flèche, confirmation obligatoire, annulation si le doigt se déplace de plus de 10 px. Le toucher simple et la suppression au clavier restent inchangés. Le mode d’emploi a été actualisé et le JavaScript passe le contrôle de syntaxe. `planning.json` n’a pas été modifié.

- Ajout validé dans `index.html` de l’accès tactile à la fiche d’une activité : un appui long immobile de 0,7 seconde reproduit le clic droit, tandis qu’un déplacement de plus de 10 px annule l’ouverture et conserve le glisser-déposer. Les aides à l’écran ont été actualisées. Contrôle de syntaxe réussi et tests ciblés réussis pour l’ouverture et l’annulation sur déplacement. `planning.json` n’a pas été modifié.

- Correction validée dans `index.html` de la disposition sur iPad : la zone calendrier et date de début occupe 99 px, les ressources commencent à 108 px et ne la chevauchent plus. La présentation sur ordinateur reste inchangée. Contrôle de syntaxe et contrôle des dimensions réussis. `planning.json` n’a pas été modifié.

- Après le test réel sur iPad ayant montré que l’appui long sur une flèche SVG n’était pas fiable, remplacement validé dans `index.html` par une séquence explicite : premier toucher pour sélectionner la flèche en bleu, second toucher sur cette même flèche pour demander confirmation, puis suppression après accord. Les touches Suppr et Retour arrière restent disponibles avec un clavier. Le mode d’emploi a été actualisé et le contrôle de syntaxe est réussi. `planning.json` n’a pas été modifié.

- Correction validée dans `index.html` du conflit de chargement sur GitHub Pages : un JSON personnel ouvert pendant l’attente de `planning.json` ne peut plus être remplacé ensuite par la démonstration. Le même garde-fou s’applique à « Lier le fichier de travail » et « Nouveau projet ». Contrôle de syntaxe réussi et test asynchrone ciblé réussi avec retour 404 simulé. `planning.json` n’a pas été modifié.
- Suppression validée de tout chargement automatique de la démonstration. Ajout du bouton « Démo » et du fichier indépendant `planning-demo.json`, réactualisable séparément. Le projet personnel mémorisé est repris au démarrage ; sinon le planning reste vide. La consultation de la démonstration préserve la sauvegarde personnelle existante. Syntaxe JavaScript et JSON contrôlée.
- Suppression complète validée de la solution de démonstration : retrait du bouton et du code, suppression de `planning-demo.json` et neutralisation de toute copie antérieure mémorisée sur GitHub Pages. Le démarrage est désormais strictement limité à un projet personnel mémorisé ou à un planning vide.

## Prochaine étape proposée

- Aucune anomalie fonctionnelle ne reste ouverte dans le périmètre validé. Attendre une nouvelle demande de l’utilisateur avant toute autre modification.

## Reste à faire

- Attendre l’accord de l’utilisateur avant toute modification du programme.
- Ne traiter ensuite qu’une seule modification à la fois.
- Mettre à jour ce document après chaque modification validée.
