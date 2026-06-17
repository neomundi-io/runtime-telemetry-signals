# Signaux de télémétrie runtime

Notes méthodologiques publiques et définitions de signaux pour l’observabilité runtime des systèmes d’IA orientée gouvernance.

🇬🇧 English version available here: [README.md](README.md)

---

## Objet du dépôt

Ce dépôt documente la structure conceptuelle publique des signaux de télémétrie runtime NeoMundi, notamment :

* les états de stabilité orientés gouvernance ;
* les signaux de variation runtime ;
* les concepts d’observabilité comportementale ;
* les artefacts de télémétrie orientés gouvernance ;
* les limites méthodologiques d’interprétation.

Ce dépôt ne divulgue pas les implémentations internes propriétaires, les pondérations, ni les mécanismes d’inférence runtime de NeoMundi ControlTower.

Son objectif est de clarifier :

* ce que les signaux sont censés représenter ;
* ce qu’ils ne prétendent pas représenter ;
* comment ils peuvent être utilisés dans des systèmes d’observabilité et de gouvernance runtime.

---

## Familles initiales de signaux

### G

**État de stabilité normalisé orienté gouvernance.**

Le G-score est conçu pour représenter une condition normalisée de stabilité, de régularité ou de cohérence runtime associée à une génération ou à un état d’exécution d’un système d’IA.

Il doit être lu comme un **signal de stabilité runtime**, et non comme une preuve de vérité factuelle.

Un G-score élevé peut indiquer qu’une génération est stable, régulière ou cohérente du point de vue runtime. Toutefois, cette stabilité peut coexister avec une réponse factuellement incorrecte.

Ce cas est appelé **stabilité trompeuse**.

### ΔG

**Signal de variation runtime associé aux variations comportementales temporelles entre fenêtres d’exécution.**

ΔG est destiné à :

* l’observabilité runtime ;
* le suivi des variations comportementales ;
* la télémétrie de gouvernance ;
* la détection de zones d’instabilité ou de tension ;
* l’identification de ruptures locales ou de transitions comportementales.

ΔG n’est pas :

* un signal de vérité ;
* un mécanisme de reconstruction cognitive ;
* un système d’omniscience sémantique ;
* une preuve automatique d’erreur.

---

## Autres signaux associés

Selon les campagnes et les contextes d’intégration, les signaux suivants peuvent être associés à G et ΔG.

### FLAG

Signal d’alerte runtime indiquant qu’une sortie mérite une attention particulière, une vérification renforcée ou une escalade.

Un FLAG ne signifie pas automatiquement qu’une réponse est fausse.
Il doit être interprété comme un signal d’attention, non comme un rejet systématique.

### DROP

Profil ou événement indiquant une rupture, une chute, une variation forte ou une zone de tension dans le signal observé.

Un profil DROP doit être analysé avec G, ΔG, FLAG, le régime runtime et, lorsque c’est pertinent, une couche factuelle externe.

### Régime runtime

État synthétique décrivant le contexte runtime global d’une sortie ou d’une séquence observée.

Un régime `STABLE` ne suffit pas à conclure qu’un système est sûr, fiable ou factuellement correct.
Le régime doit toujours être croisé avec les autres signaux.

### Exactitude benchmark

Couche externe de validation factuelle utilisée dans certaines campagnes d’analyse.

Elle permet de distinguer :

* une sortie stable et correcte ;
* une sortie stable mais incorrecte ;
* une sortie instable mais éventuellement correcte ;
* une sortie nécessitant une vérification complémentaire.

L’exactitude benchmark n’est pas un signal runtime interne.
Elle sert de couche externe de comparaison et de validation factuelle.

---

## Lecture opérationnelle des signaux

Les signaux NeoMundi doivent être interprétés dans une logique **multi-signal**.

Aucun signal isolé ne suffit à caractériser le risque d’une sortie générative.

| Signal observé                    | Interprétation                                                    | Risque principal                                                    | Action recommandée                                                                  |
| --------------------------------- | ----------------------------------------------------------------- | ------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| G-score élevé seul                | Génération stable, régulière ou cohérente du point de vue runtime | Confusion possible entre stabilité et vérité factuelle              | Ne pas utiliser G seul pour valider une réponse ; croiser avec une couche factuelle |
| G-score élevé + exactitude faible | Stabilité trompeuse : réponse stable mais incorrecte              | Forte confiance apparente malgré une erreur factuelle               | Déclencher une validation factuelle externe ou une revue renforcée                  |
| G-score faible ou instable        | Fragilité runtime, irrégularité ou comportement moins stable      | Sortie potentiellement sensible au contexte, au modèle ou au prompt | Examiner la question, le provider et les variations associées                       |
| ΔG élevé ou profil DROP           | Variation forte, rupture locale ou zone de tension                | Transition runtime, instabilité ponctuelle ou dégradation locale    | Classer comme zone d’attention prioritaire                                          |
| FLAG                              | Alerte runtime indiquant qu’une sortie mérite vérification        | Surinterprétation comme erreur automatique                          | Utiliser comme signal d’escalade, pas comme rejet systématique                      |
| FLAG + DROP                       | Zone de risque runtime plus forte                                 | Risque accru d’instabilité ou de comportement problématique         | Prioriser l’analyse, envisager une revue humaine ou un second passage               |
| Régime STABLE seul                | Contexte synthétique globalement stable                           | Pouvoir discriminant limité si STABLE est dominant                  | Ne jamais utiliser le régime seul ; croiser avec G, ΔG, FLAG et exactitude          |
| ALLOW + exactitude faible         | Cas non détecté par le signal runtime                             | Faux négatif potentiel dans la logique de gouvernance               | Renforcer la couche factuelle ou benchmark                                          |
| Forte saturation de G-score       | Concentration du score autour d’un plafond observé                | Ambiguïté entre stabilité réelle et effet de saturation             | Tester la robustesse sur plusieurs providers, prompts et répétitions                |

---

## Règles d’interprétation actionnables

Ces règles constituent une première grammaire exploratoire pour l’observabilité et la gouvernance runtime.

Elles ne doivent pas être comprises comme des seuils définitifs.

| Règle | Condition                                  | Interprétation                          | Action recommandée                       |
| ----- | ------------------------------------------ | --------------------------------------- | ---------------------------------------- |
| R1    | G élevé + exactitude faible                | Stabilité trompeuse                     | Ajouter une validation factuelle externe |
| R2    | G élevé seul                               | Stabilité runtime, pas preuve de vérité | Ne jamais utiliser G seul pour valider   |
| R3    | FLAG + DROP                                | Zone de risque runtime prioritaire      | Escalade ou revue humaine                |
| R4    | G faible + ΔG élevé                        | Rupture ou tension potentielle          | Investiguer comme zone de transition     |
| R5    | FLAG + réponse correcte                    | Alerte sans erreur factuelle directe    | Lire comme attention, pas rejet          |
| R6    | Régime STABLE seul                         | Signal synthétique insuffisant          | Croiser avec G, ΔG, FLAG et exactitude   |
| R7    | G stable + faible FLAG + faible exactitude | Profil stable mais factuellement faible | Ajouter une couche factuelle             |
| R8    | Forte saturation de G                      | Stabilité forte ou effet de plafond     | Analyser variabilité, ΔG, FLAG et DROP   |
| R9    | Forte variabilité de G entre providers     | Sensibilité au modèle ou au contexte    | Utiliser comme cas de test prioritaire   |
| R10   | Signal unique utilisé seul                 | Base décisionnelle insuffisante         | Utiliser une lecture multi-signal        |

---

## Classification OBS/GOV-ready

Pour une première intégration externe, les signaux doivent être consommés selon leur rôle dans une architecture d’observabilité ou de gouvernance.

| Signal               | Catégorie              | Usage recommandé                                                         |
| -------------------- | ---------------------- | ------------------------------------------------------------------------ |
| G-score              | Obligatoire            | Signal central de stabilité runtime, à croiser avec une couche factuelle |
| ΔG / dg_variation    | Obligatoire            | Détection de rupture, tension ou transition locale                       |
| FLAG / taux de FLAG  | Obligatoire            | Signal d’alerte, d’escalade ou de vérification renforcée                 |
| Exactitude benchmark | Obligatoire hors ligne | Couche externe de validation factuelle                                   |
| Régime               | Recommandé             | Lecture synthétique du contexte runtime, non suffisante seule            |
| dg_profile           | Recommandé             | Profil simplifié de variation, utile pour des règles interprétables      |
| G-score seul         | À éviter seul          | Risque de confusion entre stabilité et factualité                        |
| Régime seul          | À éviter seul          | Trop synthétique pour servir de déclencheur isolé                        |

---

## Exemple de lecture multi-signal

Une intégration simple peut lire les signaux de la manière suivante :

```text
Cas 1 :
G-score élevé
ΔG faible
Aucun FLAG
Régime STABLE
Exactitude benchmark élevée

Lecture :
sortie stable, cohérente et factuellement validée dans le cadre du benchmark.
```

```text
Cas 2 :
G-score élevé
ΔG faible
Aucun FLAG
Régime STABLE
Exactitude benchmark faible

Lecture :
stabilité trompeuse.
La sortie paraît stable du point de vue runtime, mais elle échoue à la validation factuelle.
Action recommandée : validation externe, revue renforcée ou couche de grounding.
```

```text
Cas 3 :
G-score faible
ΔG élevé
FLAG présent
Profil DROP
Régime instable ou transitionnel

Lecture :
zone de tension runtime.
Action recommandée : escalade, revue humaine, second passage ou routage vers un mécanisme de contrôle.
```

---

## Position méthodologique

Les signaux runtime NeoMundi sont des **artefacts d’observabilité orientés gouvernance**.

Ils sont conçus pour soutenir :

* la supervision runtime ;
* les workflows de gouvernance ;
* l’auditabilité ;
* l’analyse télémétrique ;
* les systèmes d’orchestration ;
* la détection de zones de tension, de rupture ou de stabilité trompeuse.

Ils ne prétendent pas :

* reconstruire exhaustivement la cognition interne d’un modèle ;
* établir une vérité sémantique universelle ;
* certifier automatiquement une réponse ;
* remplacer une validation métier, juridique, scientifique ou factuelle.

La recommandation minimale est de combiner au moins :

* G-score ;
* ΔG ou dg_variation ;
* FLAG ;
* régime ;
* couche factuelle ou benchmark externe lorsque l’usage le requiert.

---

## Limites d’interprétation

Un G-score élevé ne signifie pas qu’une réponse est vraie.

Un FLAG ne signifie pas automatiquement qu’une réponse est fausse.

Un régime STABLE ne suffit pas à conclure qu’un système est sûr.

Un ΔG élevé ne prouve pas une erreur, mais signale une variation ou une tension qui mérite attention.

Les signaux doivent être interprétés ensemble, dans leur contexte d’usage, avec les données disponibles et les limites du protocole de mesure.

---

## Intégration dans des systèmes de gouvernance

Dans une architecture d’observabilité, les signaux peuvent être utilisés pour :

* tracer des sorties génératives ;
* comparer des comportements entre providers ou modèles ;
* identifier des zones de tension ;
* produire des artefacts d’audit ;
* surveiller des variations runtime ;
* alimenter des dashboards de gouvernance.

Dans une architecture de gouvernance plus avancée, ils peuvent contribuer à des décisions configurables, par exemple :

* laisser passer une sortie ;
* déclencher une vérification factuelle ;
* demander une régénération ;
* router vers un autre modèle ;
* escalader vers une revue humaine ;
* documenter un événement critique.

Ces usages doivent rester configurables, contextualisés et adaptés au niveau de risque du domaine concerné.

---

## Référence externe

Une première lecture exploratoire externe des signaux runtime NeoMundi a été réalisée par Pape Malick DIOP, Data Scientist / ML Researcher.

Le rapport analyse notamment :

* G-score ;
* ΔG ;
* FLAG ;
* régime runtime ;
* exactitude benchmark ;
* stabilité trompeuse ;
* lecture OBS/GOV-ready.

Ce rapport est exploratoire.
Il ne constitue ni une validation mathématique définitive, ni une certification du produit.
Il propose une première grammaire d’interprétation et des règles actionnables pour l’intégration externe.

Analyse contributeur associée :

* [Signaux temps réel, stabilité trompeuse et importance d’une lecture multi-signaux](https://neomundi.org/observatoire-ia/signaux-temps-reel-stabilite-trompeuse-et-importance-lecture-multi-signaux)

---

## Licence

Ce dépôt est publié sous licence Apache-2.0.

---

## À propos

Définitions publiques des signaux de télémétrie runtime et notes méthodologiques pour l’observabilité des IA orientée gouvernance.
