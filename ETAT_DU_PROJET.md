# État du projet

## Règles de travail

- Les règles permanentes sont consignées dans `AGENTS.md`.
- Aucune modification du programme ne doit être effectuée sans l’accord préalable de l’utilisateur.
- Le présent état a été établi par lecture de `index.html` et de `planning.json` dans l’emplacement actuel du projet. Le programme avait temporairement porté le nom `Reseau_PERT.html`.

## Fichiers principaux examinés

- `index.html` : application web autonome « Réseau PERT », composée d’un seul fichier HTML avec CSS et JavaScript intégrés (4 732 lignes, 170 620 octets après le remplacement des confirmations natives de suppression sur iPad).
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
- Le nom du fichier actif est affiché après « Réseau PERT — », actualisé après ouverture, liaison, création ou enregistrement, puis mémorisé pour la reprise automatique. Les noms longs sont tronqués visuellement sans perdre leur intitulé complet dans l’infobulle.
- À droite des ressources utilisées, un résumé affiche la durée réelle du projet entre sa première date de début et sa dernière date de fin, ainsi que le coût total des affectations. Les intitulés sont en gras et le résumé passe sous les ressources lorsque la largeur disponible est insuffisante.
- Sous chaque activité, le coût total est placé à gauche et la date de fin est alignée à droite afin de la distinguer clairement de la date de début affichée au-dessus.
- Un bouton « Tableau des activités », placé à côté du tableau des affectations, ouvre un récapitulatif consultatif recalculé à chaque ouverture : activité, durée, prédécesseurs, successeurs, dates au plus tôt, marge totale, fin au plus tard et coût total. Les dépendances sont indiquées par leurs noms, le nom des activités du chemin critique est en gras et le tableau défile horizontalement sur écran étroit.
- Un bouton « Diagramme de Gantt » ouvre une visualisation consultative reconstruite à partir des dates du PERT : une ligne resserrée et une barre par activité, unité de temps affichée, échelle temporelle automatique dont chaque ligne verticale fine et contrastée correspond à la date indiquée, chemin critique en rouge et en gras, marge totale prolongée par une zone blanche bordée, libellés maintenus à gauche pendant le défilement horizontal et signalement des activités sans dates calculables. Le Gantt ne permet aucune modification du projet.
- Un bouton « Calendrier » ouvre le calendrier du projet. Le mode par défaut est « jours ouvrés » avec exclusion du samedi et du dimanche ; l’utilisateur peut choisir les jours calendaires et ajouter ou retirer des dates non travaillées.
- Le calendrier officiel « France métropolitaine » est appliqué par défaut et peut être désactivé. La fenêtre affiche séparément, avec leur nom et leur date, les onze jours fériés officiels de chaque année couverte par le projet et les dates particulières ajoutées manuellement. Les fêtes mobiles sont calculées à partir de Pâques.
- Le calendrier est enregistré dans le JSON ; les anciens JSON sans calendrier sont interprétés en jours ouvrés avec le calendrier officiel France métropolitaine.
- Le même calendrier commande les calculs au plus tôt et au plus tard, les marges, les dépendances, la vérification des durées, le résumé global, la répartition mensuelle du budget, le diagnostic de charge et le Gantt. Les périodes non travaillées sont grisées dans le Gantt.
- L’unité du projet est choisie dans un menu limité à Jour, Heure et Semaine. Une semaine représente 5 jours en mode ouvré et 7 jours en mode calendaire. Les anciens libellés équivalents sont normalisés lors de l’ouverture d’un JSON.

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
- Modification validée du nom produit par « Enregistrer » : format `planning-JJ-MM-HHhMM.json`, sans année et selon l’heure locale de l’ordinateur. Contrôle réussi avec `planning-24-08-18h42.json`.
- Amélioration validée de « Enregistrer » : les navigateurs compatibles demandent le fichier de destination lors du premier enregistrement et le réutilisent ensuite pendant la session ; les autres affichent un avertissement indiquant le nom exact de la copie et le rôle du dossier de téléchargement avant de poursuivre. Les deux parcours ont été testés avec succès.
- Ajout validé du nom du fichier actif à côté de « Réseau PERT — ». Le nom est actualisé et mémorisé pour « Ouvrir », « Lier le fichier de travail », « Nouveau projet », « Enregistrer » et la reprise automatique. Tests réussis d’affichage, de mémorisation et de restauration. Publication GitHub autorisée le 25 août 2026.
- Ajout validé du résumé global à droite de « Ressources utilisées » : durée totale entre la première date de début et la dernière date de fin, dates au format français et coût total des affectations. Les titres « Ressources utilisées », « Durée totale » et « Coût total » sont en gras ; la disposition revient à la ligne sur écran étroit. Tests réussis pour un projet daté, des dates incomplètes et le total des coûts.
- Inversion validée sous chaque activité : coût total à gauche, date de fin à droite, avec largeur resserrée et alignement explicite de la date. Le contrôle de structure et de syntaxe est réussi. Publication GitHub autorisée le 25 août 2026.
- Ajout validé et publié du tableau consultatif des activités et de leurs dépendances, avec neuf colonnes et défilement horizontal sur écran étroit. Le mode d’emploi est actualisé. Syntaxe JavaScript, structure HTML et test fonctionnel ciblé réussis : recalcul à l’ouverture, deux activités liées, noms du prédécesseur et du successeur, dates, marges, coûts et neuf cellules par ligne. Publication GitHub effectuée le 25 août 2026 dans le commit `fbcac32`.
- Mise en gras validée localement du nom des activités du chemin critique dans le tableau des activités. Le test ciblé confirme qu’une activité critique est marquée et qu’une activité non critique reste en caractères normaux. Cette seule retouche n’est pas encore publiée.
- Le 25 août 2026, l’utilisateur considère ce stade de l’application comme opérationnel.
- Ajout local d’une première visualisation Gantt strictement consultative. Le test ciblé confirme l’ouverture, le tri, la position et la largeur des barres, la distinction entre activité critique et ordinaire et le traitement d’une activité sans dates. La syntaxe JavaScript et la structure passent les contrôles ; cette version d’essai n’est pas encore publiée.
- Ajustement local validé techniquement du Gantt : lignes ramenées à 28 px pour rapprocher les barres, affichage explicite de l’unité de temps et ligne verticale fine à chaque passage du dimanche au lundi. Le test sur une période de seize jours confirme deux séparateurs hebdomadaires cohérents. Ces ajustements ne sont pas encore publiés.
- Retrait local des séparateurs hebdomadaires, jugés ambigus : les seules lignes verticales restantes correspondent désormais exactement aux dates de l’échelle. Ajout d’un prolongement blanc bordé représentant la marge totale à droite de la barre colorée. Le test confirme l’alignement des graduations, une marge visuelle de 2 j sur une activité non critique et l’absence de prolongement pour une activité critique. Cette correction n’est pas encore publiée.
- Renforcement local du contraste des lignes verticales datées après constat visuel de leur manque de visibilité. Leur épaisseur reste limitée à 1 px et leur alignement avec les dates demeure inchangé. Cette correction n’est pas encore publiée.
- Ajout local du calendrier de projet et remplacement des additions calendaires directes par un moteur de temps travaillé. Tests réussis : vendredi + 1 j = lundi ; jeudi + 5 j = jeudi suivant ; vendredi + 1 j avec lundi exclu = mardi ; calcul inverse au plus tard exact ; 1 semaine ouvrée = 5 j ; mode calendaire conservé ; durée fractionnaire de 1,5 j du vendredi au lundi midi ; ancien JSON sans calendrier normalisé en jours ouvrés ; calendrier JSON sauvegardé et dates exclues dédoublonnées.
- Test ciblé du réseau PERT réussi avec deux activités liées : exclusion du week-end, décalage d’un lundi non travaillé, dépendance respectée, dates au plus tard cohérentes et chemin critique inchangé. Syntaxe JavaScript, structure de la fenêtre Calendrier et contrôle des différences réussis. Cette évolution n’est pas encore publiée.
- Ajout local du calendrier officiel France métropolitaine, vérifié d’après la liste officielle de Service-Public.fr. Test 2026 réussi : onze jours fériés, lundi de Pâques le 6 avril, Ascension le 14 mai, lundi de Pentecôte le 25 mai et fête nationale le 14 juillet ; un jour d’activité débutant le vendredi 3 avril finit le mardi 7 avril. La désactivation du calendrier officiel et sa persistance JSON sont également testées. Cette évolution n’est pas encore publiée.
- Correction locale de l’enregistrement d’une affectation : lorsque celle-ci est sélectionnée dans la fiche d’activité, le bouton général « Enregistrer » applique automatiquement la ressource et la durée actuellement saisies. Test réussi avec passage de 2 à 3 unités et refus d’une durée supérieure à celle de l’activité. Le bouton redondant « Modifier » a ensuite été supprimé avec toutes ses références d’interface, sans retirer l’enregistrement automatique. Cette correction n’est pas encore publiée.
- Ajout local de l’unité après la durée inscrite dans chaque barre du Gantt, avec singulier et pluriel. Les premiers tests couvraient également les unités libres avant leur remplacement par le menu limité décrit ci-dessous. Cette correction n’est pas encore publiée.
- Remplacement local de la saisie libre « Unité » par un menu proposant uniquement Jour, Heure et Semaine ; l’unité Mois a été écartée. Le mode d’emploi est actualisé et le test confirme les trois seules options, leur branchement au recalcul et la normalisation des anciens JSON. Cette correction n’est pas encore publiée.
- Clarification du mode d’emploi : remplacement du planning affiché par « Nouveau projet », geste exact de création d’une liaison, suppression d’une liaison au clavier ou sur iPad, modification et suppression des ressources, portée de « Vérifier le projet », contenu du tableau des affectations et comparaison du budget mensuel quelle que soit l’unité de temps. Publication GitHub autorisée le 26 août 2026.
- Corrections pour iPad : un toucher bref sélectionne désormais explicitement une activité sans déclencher son déplacement ; un bouton « Supprimer la liaison » devient disponible lorsqu’une flèche est sélectionnée et la zone tactile des liaisons est élargie ; les ressources affectées sont remplacées par des lignes tactiles visibles, sans modifier leurs données ni le calcul des coûts. La fiche ne donne plus automatiquement le focus à la description sur écran tactile, afin de ne pas ouvrir le clavier devant les ressources. Syntaxe JavaScript, structure HTML et différences Git contrôlées. Publication GitHub autorisée le 26 août 2026 ; un essai réel dans Safari sur iPad doit suivre la mise en ligne.
- Correction du bouton « Ouvrir » sur iPad : le champ JSON n’est plus entièrement masqué ni déclenché par un clic JavaScript artificiel. Un véritable sélecteur de fichier transparent recouvre désormais le bouton visuel et reçoit directement le toucher, ce qui permet à iPadOS d’afficher son sélecteur de documents. Le chargement, la validation et les données du JSON restent inchangés. Contrôles réussis : syntaxe JavaScript, sélecteur unique sans attribut `hidden`, suppression de l’ancien `fichierProjet.click()` et absence d’identifiants HTML dupliqués. Publication GitHub autorisée le 26 août 2026 ; un essai réel dans Safari sur iPad doit suivre la mise en ligne.
- Après essai réel dans Safari sur iPad, la sélection des activités et des liaisons fonctionne, mais les boutons de suppression ne produisent pas leur événement `click` et aucune confirmation n’apparaît. Correction : « Supprimer l’activité » et « Supprimer la liaison » déclenchent aussi directement leur commande sur `pointerup` pour les pointeurs tactiles, avec conservation du clic sur ordinateur, de la confirmation obligatoire et des garde-fous contre une double suppression. Syntaxe JavaScript, branchement des deux commandes et différences Git contrôlés. Publication GitHub autorisée le 26 août 2026.
- Le nouvel essai réel sur iPad montre que le déclenchement direct ne suffit pas : les éléments sont bien sélectionnés en bleu, mais aucune confirmation native n’apparaît. Nouvelle correction : les deux boutons ne reposent plus sur l’attribut natif `disabled` et utilisent un état visuel avec `aria-disabled` ; `window.confirm()` est remplacé par une fenêtre de confirmation intégrée à l’application, avec boutons Annuler et Supprimer eux-mêmes compatibles avec `pointerup`. La confirmation reste obligatoire et l’action est effacée avant exécution pour empêcher toute double suppression. Syntaxe JavaScript, structure HTML, absence de confirmation native résiduelle pour les activités et liaisons, et différences Git contrôlées. Publication GitHub autorisée le 26 août 2026.

## Prochaine étape proposée

- Faire contrôler visuellement le calendrier et le planning recalculé par l’utilisateur avec son projet réel, puis corriger un seul point à la fois avant toute publication.

## Reste à faire

- Attendre l’accord de l’utilisateur avant toute nouvelle modification du programme ou publication.
- Ne traiter ensuite qu’une seule modification à la fois.
- Mettre à jour ce document après chaque modification validée.
