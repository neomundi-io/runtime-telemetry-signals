> **Référence historique — 25 octobre 2026.** Le sens actuel des mesures se lit dans [Metric Contract](https://github.com/neomundi-io/neomundi-metric-contract) et la [documentation API](https://github.com/neomundi-io/neomundi-runtime-measurement). Les définitions ci-dessous restent conservées pour leur contexte et leurs citations ; elles ne constituent pas une spécification actuelle de production.

# Signaux de télémétrie runtime

Définitions publiques des signaux et recommandations méthodologiques pour l’observabilité runtime des IA orientée gouvernance.

🇬🇧 Version anglaise : [README.md](README.md)

---

## Ce que ce dépôt explique

NeoMundi produit des signaux de télémétrie runtime qui aident les organisations à observer le comportement d’une génération d’IA pendant qu’elle est produite.

Ces signaux sont conçus pour soutenir des décisions de gouvernance telles que :

- poursuivre une génération ;
- demander une vérification factuelle ;
- régénérer une réponse ;
- rediriger la requête vers un autre modèle ;
- soumettre la sortie à une revue humaine ;
- documenter un événement runtime ;
- appliquer une politique d’arrêt définie par le client.

Les signaux NeoMundi ne prennent pas les décisions de gouvernance à la place de l’organisation.

Ils fournissent des informations mesurables qui peuvent être interprétées dans le cadre d’une politique de gouvernance définie par l’opérateur du système, l’intégrateur ou l’organisation utilisatrice.

En pratique :

> NeoMundi mesure le comportement runtime.  
> L’organisation définit l’action.

---

## Finalité du dépôt

Ce dépôt documente la structure conceptuelle publique des signaux de télémétrie runtime NeoMundi, notamment :

- les états de stabilité orientés gouvernance ;
- les signaux de variation runtime ;
- les concepts d’observabilité comportementale ;
- les artefacts de télémétrie orientés gouvernance ;
- les principes de lecture multi-signaux ;
- les usages possibles en gouvernance ;
- les limites méthodologiques et opérationnelles.

Son objectif est de clarifier :

- ce que les signaux sont censés représenter ;
- ce qu’ils ne prétendent pas représenter ;
- comment ils peuvent être interprétés ensemble ;
- comment ils peuvent soutenir des processus d’observabilité et de gouvernance ;
- quelles limites doivent être prises en compte avant de définir une politique opérationnelle.

Ce dépôt ne divulgue pas les implémentations propriétaires, les pondérations internes, les mécanismes d’inférence ni les composants protégés de NeoMundi ControlTower.

---

## Familles principales de signaux

### G-score

**État normalisé de stabilité runtime orienté gouvernance.**

Le G-score représente une condition normalisée associée à la stabilité, à la régularité ou à la cohérence comportementale d’une génération d’IA ou d’un état d’exécution.

Il doit être interprété comme un signal de stabilité runtime.

Il ne constitue pas une preuve qu’une réponse est factuellement correcte.

Un G-score élevé peut indiquer qu’une génération est stable, régulière ou cohérente du point de vue runtime. Toutefois, une génération stable peut malgré tout contenir une réponse incorrecte.

Cette situation est appelée :

**stabilité trompeuse**

La stabilité trompeuse apparaît lorsqu’une sortie semble stable du point de vue runtime, mais échoue à une validation factuelle, scientifique, juridique ou métier externe.

---

### ΔG

**Signal de variation runtime associé aux changements de stabilité au cours du temps.**

ΔG représente l’évolution ou la variation de la condition de stabilité runtime au fil de la séquence de génération ou entre différents points de mesure.

Il peut contribuer à :

- l’observabilité runtime ;
- la surveillance des variations comportementales ;
- la détection de ruptures locales ;
- l’identification de zones de transition ;
- la détection de zones d’instabilité ou de tension ;
- la télémétrie de gouvernance ;
- des politiques d’intervention configurables.

ΔG n’est pas :

- un score de vérité ;
- une preuve automatique d’erreur ;
- une reconstruction de la cognition interne du modèle ;
- un mécanisme universel de validation sémantique ;
- une instruction automatique d’arrêter une génération.

Un ΔG négatif ou fortement variable peut indiquer une dégradation ou une transition dans la condition runtime observée. Sa signification opérationnelle dépend du contexte, des signaux associés et de la politique de gouvernance appliquée.

---

## Signaux et artefacts associés

Selon la campagne, le mode API et le contexte d’intégration, les signaux suivants peuvent être associés à G et ΔG.

### FLAG

Signal d’attention runtime indiquant qu’une sortie ou une génération mérite une vérification, une analyse ou une escalade supplémentaire.

Un FLAG ne signifie pas automatiquement qu’une réponse est fausse.

Il doit être interprété comme un signal d’attention, et non comme un rejet automatique.

Les usages possibles incluent :

- une vérification renforcée ;
- une seconde passe de validation ;
- une régénération ;
- un reroutage ;
- une escalade ;
- la documentation d’un incident.

---

### ALLOW

Statut de gouvernance indiquant qu’aucune condition de blocage n’a été identifiée par la politique runtime configurée.

ALLOW ne constitue pas une certification factuelle.

Une sortie peut recevoir le statut ALLOW tout en nécessitant une validation factuelle, juridique, scientifique, de sécurité ou métier externe.

---

### DROP

Profil ou événement de variation runtime indiquant une baisse, une rupture, une forte variation ou une zone de tension dans le signal observé.

Un profil DROP doit être interprété avec :

- le G-score ;
- ΔG ;
- FLAG ou ALLOW ;
- le régime runtime ;
- les signaux de cohérence ;
- une validation factuelle ou benchmark, lorsque cela est pertinent.

DROP peut aider à identifier des zones d’attention prioritaires, mais ne prouve pas à lui seul qu’une sortie est incorrecte.

---

### FLAT

Profil de variation indiquant un mouvement visible limité du signal de stabilité runtime observé.

Un profil FLAT peut correspondre à une forme de régularité ou de saturation du signal.

Il ne doit pas être interprété seul comme une preuve de correction, de sécurité ou de fiabilité.

---

### V_SHAPE

Profil de variation indiquant une baisse observée suivie d’une récupération partielle ou plus importante.

Ce profil peut refléter une tension runtime temporaire, une transition ou une dynamique de récupération.

Son interprétation dépend de l’amplitude, du moment d’apparition, de la décision associée et des autres signaux disponibles.

---

### Régime runtime

État synthétique décrivant le contexte runtime global d’une sortie observée ou d’une séquence d’exécution.

Les exemples peuvent inclure des régimes stables, transitionnels ou instables.

Un régime `STABLE` ne suffit pas pour conclure qu’un système est :

- sûr ;
- fiable ;
- factuellement correct ;
- conforme ;
- prêt pour une exécution automatique.

Le régime runtime doit toujours être croisé avec les autres signaux.

---

### Exactitude benchmark

Couche externe de validation factuelle utilisée dans certaines campagnes d’analyse.

L’exactitude benchmark aide à distinguer des situations telles que :

- sortie stable et factuellement correcte ;
- sortie stable mais factuellement incorrecte ;
- sortie instable mais potentiellement correcte ;
- faiblesse factuelle non détectée par la télémétrie runtime ;
- sortie nécessitant une validation externe renforcée.

L’exactitude benchmark n’est pas un signal runtime interne de NeoMundi.

Il s’agit d’une couche externe de comparaison ou de validation factuelle.

---

### Signaux de cohérence et de risque factuel

Selon l’implémentation ou la campagne, les observations runtime peuvent également inclure des signaux liés à :

- la cohérence sémantique ;
- des indicateurs de risque factuel ;
- des indicateurs liés aux hallucinations ;
- la densité informationnelle ;
- la latence ;
- l’usage des tokens ;
- des estimations d’énergie ou de coût.

Ces signaux associés apportent un contexte supplémentaire, mais doivent rester interprétés dans les limites de leur mesure.

---

## Des signaux runtime aux actions de gouvernance

Les signaux NeoMundi sont conçus pour rendre le comportement runtime interprétable dans un système de gouvernance.

Ils n’imposent pas une décision universelle.

Un même signal peut conduire à des actions différentes selon :

- le cas d’usage ;
- la politique de risque de l’organisation ;
- le domaine ;
- la criticité de la sortie ;
- les exigences juridiques ou de conformité applicables ;
- la disponibilité d’une revue humaine ;
- la présence de couches factuelles externes ou de retrieval.

Le tableau suivant présente des interprétations possibles en vue d’une gouvernance.

Il ne s’agit pas d’une table de décision automatique et il ne définit pas de seuils universels de production.

| Signaux observés | Interprétation possible | Risque ou limite principale | Action de gouvernance possible |
| --- | --- | --- | --- |
| G-score élevé seul | Génération stable, régulière ou cohérente du point de vue runtime | Risque de confondre stabilité et vérité factuelle | Croiser avec une couche factuelle ou métier |
| G-score élevé + forte exactitude factuelle | Sortie stable et validée extérieurement dans le contexte testé | La validation peut rester limitée au benchmark ou au domaine testé | Poursuivre selon la politique applicable |
| G-score élevé + faible exactitude factuelle | Stabilité trompeuse : sortie stable mais factuellement incorrecte | Apparence de fiabilité malgré une faiblesse factuelle | Déclencher une vérification factuelle, du grounding ou une revue renforcée |
| G-score faible ou instable | Fragilité runtime, irrégularité ou stabilité plus faible | Sensibilité possible au prompt, au fournisseur, au modèle ou au contexte | Examiner, régénérer ou appliquer une seconde passe de validation |
| ΔG élevé | Forte variation ou transition runtime | Une dégradation locale peut être surinterprétée comme une erreur | Examiner G, le profil, la décision et le contexte associés |
| Profil DROP | Baisse, rupture ou zone de tension persistante | DROP seul ne prouve pas un échec factuel | Classer comme zone d’attention prioritaire |
| FLAG | La sortie nécessite une attention supplémentaire | FLAG peut être confondu avec un rejet automatique | Vérifier, régénérer, rerouter ou escalader selon la politique |
| FLAG + DROP | Zone d’attention runtime renforcée | Risque accru de comportement instable ou problématique | Prioriser l’analyse, la revue humaine ou une intervention configurable |
| FLAG + sortie factuellement correcte | Signal d’attention sans erreur factuelle démontrée | Supposer à tort que chaque FLAG correspond à une réponse incorrecte | Traiter comme une alerte, pas comme un rejet |
| ALLOW + faible exactitude factuelle | La politique runtime n’a pas identifié la faiblesse factuelle | Faux négatif potentiel si les signaux runtime sont utilisés seuls | Renforcer la validation factuelle externe |
| Régime STABLE seul | Contexte runtime synthétique globalement stable | Valeur discriminante limitée lorsqu’il est utilisé seul | Croiser avec G, ΔG, FLAG, cohérence et validation factuelle |
| Forte saturation du G-score | Concentration autour d’un plafond observé | Ambiguïté entre stabilité réelle et effet de saturation | Tester sur plusieurs prompts, fournisseurs, répétitions et configurations |
| Signal de variation runtime précoce | Une intervention peut être techniquement possible avant la fin | L’action appropriée n’est pas déterminée par le signal seul | Continuer, vérifier, régénérer, rerouter, escalader ou arrêter selon la politique |

---

## Règles exploratoires d’interprétation

Les règles suivantes forment une première grammaire publique pour l’observabilité runtime et la gouvernance.

Elles ne doivent pas être comprises comme :

- des seuils définitifs de production ;
- des classifications universelles du risque ;
- des instructions automatiques d’exécution ;
- des règles de certification.

| Règle | Condition | Interprétation exploratoire | Réponse de gouvernance possible |
| --- | --- | --- | --- |
| R1 | G élevé + faible exactitude factuelle | Stabilité trompeuse | Ajouter une validation factuelle externe |
| R2 | G élevé seul | Stabilité runtime, pas preuve de vérité | Ne jamais utiliser G seul pour valider |
| R3 | FLAG + DROP | Zone d’attention runtime prioritaire | Escalade, reroutage ou revue humaine |
| R4 | G faible + ΔG élevé | Rupture ou transition potentielle | Examiner la séquence runtime locale |
| R5 | FLAG + réponse correcte | Alerte sans erreur factuelle démontrée | Traiter comme une attention, pas comme un rejet automatique |
| R6 | Régime STABLE seul | Signal synthétique insuffisant | Croiser avec G, ΔG, FLAG et preuves factuelles |
| R7 | G stable + faible exactitude factuelle | Profil stable mais factuellement faible | Ajouter une validation factuelle ou fondée sur le retrieval |
| R8 | Forte saturation de G | Stabilité réelle ou possible effet plafond | Analyser la variabilité, les répétitions et les signaux associés |
| R9 | Forte variation entre fournisseurs | Sensibilité au fournisseur, au modèle ou au contexte | Utiliser comme cas de test comparatif prioritaire |
| R10 | Un signal isolé | Base de décision insuffisante | Appliquer une lecture multi-signaux |
| R11 | Dégradation précoce de ΔG | Point d’intervention potentiel | Appliquer une politique définie par le client, pas un arrêt universel automatique |
| R12 | Taux de FLAG élevé dans une campagne | Résultat dépendant du corpus ou de la configuration | Ne pas généraliser sans réplication |

---

## Classification OBS/GOV-ready

Pour une intégration externe, les signaux peuvent être consommés selon leur rôle dans une architecture d’observabilité ou de gouvernance.

| Signal ou artefact | Catégorie suggérée | Usage recommandé |
| --- | --- | --- |
| G-score | Signal runtime principal | Signal central de stabilité, à interpréter avec d’autres signaux |
| ΔG / dg_variation | Signal runtime principal | Détection d’une variation locale, d’une rupture ou d’une transition |
| FLAG / taux de FLAG | Signal de gouvernance principal | Attention, escalade, vérification renforcée ou entrée d’intervention |
| ALLOW | Statut de gouvernance | Indique l’absence de condition de blocage selon la politique configurée, sans certification factuelle |
| Exactitude benchmark | Couche externe hors ligne | Validation factuelle ou benchmark comparatif |
| Régime runtime | Signal contextuel | Lecture synthétique du contexte runtime |
| dg_profile | Signal contextuel | Résumé interprétable de l’évolution de ΔG |
| Score de cohérence | Signal associé | Contextualiser la régularité ou la dégradation sémantique |
| Indicateur de risque factuel | Signal associé | Soutenir une revue factuelle renforcée |
| Position du token | Télémétrie opérationnelle | Identifier quand un événement runtime survient pendant la génération |
| G-score seul | À éviter seul | Risque de confusion entre stabilité et factualité |
| Régime seul | À éviter seul | Trop synthétique pour piloter une décision isolée |
| Taux de FLAG seul | À éviter seul | Forte dépendance au corpus et aux conditions expérimentales |

---

## Exemples de lecture multi-signaux

### Cas 1 — Sortie stable et validée extérieurement

```text
G-score élevé
ΔG faible
Aucun FLAG
Régime STABLE
Forte exactitude benchmark
```

Lecture possible :

La sortie semble stable et cohérente du point de vue runtime et elle est validée factuellement dans le contexte du benchmark testé.

Réponse de gouvernance possible :

Poursuivre selon la politique applicable de l’organisation.

---

### Cas 2 — Stabilité trompeuse

```text
G-score élevé
ΔG faible
Aucun FLAG
Régime STABLE
Faible exactitude benchmark
```

Lecture possible :

La sortie semble stable du point de vue runtime, mais échoue à une validation factuelle externe.

Réponse de gouvernance possible :

Déclencher une vérification externe, du grounding, du retrieval ou une revue renforcée.

---

### Cas 3 — Zone de tension runtime

```text
G-score faible
ΔG élevé
FLAG présent
Profil DROP
Régime transitionnel ou instable
```

Lecture possible :

La sortie est associée à une tension runtime, une rupture ou une zone de transition.

Réponse de gouvernance possible :

Régénérer, rerouter, escalader vers une revue humaine, appliquer une seconde passe de validation ou invoquer un mécanisme de contrôle configuré.

---

### Cas 4 — Signal d’attention sans échec factuel

```text
FLAG présent
Profil DROP ou V_SHAPE
Réponse correcte selon une validation externe
```

Lecture possible :

Le signal runtime a identifié une variation ou une zone d’attention, mais aucune erreur factuelle directe n’a été démontrée.

Réponse de gouvernance possible :

Documenter l’événement, examiner la séquence runtime et éviter de traiter le FLAG comme un rejet automatique.

---

### Cas 5 — Signal runtime insuffisant pour détecter une faiblesse factuelle

```text
ALLOW
G-score élevé
Régime STABLE
Faible exactitude factuelle
```

Lecture possible :

Les signaux runtime n’ont pas identifié la faiblesse factuelle.

Réponse de gouvernance possible :

Maintenir une couche externe de validation factuelle, scientifique, juridique ou métier.

---

## Actionnabilité des signaux runtime

Un signal runtime est actionnable lorsqu’il est disponible suffisamment tôt et de manière suffisamment cohérente pour soutenir une intervention possible avant ou immédiatement après la génération.

Les interventions possibles incluent :

- poursuivre la génération ;
- arrêter la génération ;
- demander une régénération ;
- rerouter vers un autre modèle ;
- déclencher une vérification factuelle ;
- escalader vers une revue humaine ;
- enregistrer un incident ou un artefact d’audit.

Une étude exploratoire conduite par Fatima Ezzahrae Gouarab a examiné si le premier point ΔG négatif observé pouvait soutenir une politique d’arrêt anticipé côté client.

Dans les conditions spécifiques étudiées, le signal a été détecté avant la fin de la génération dans la majorité des cas, ce qui suggère qu’une intervention runtime peut être techniquement envisageable.

Cependant :

- le critère de détection utilisé dans l’étude était exploratoire ;
- `ΔG < 0` n’est pas un seuil officiel universel NeoMundi ;
- les tokens théoriquement évitables ne sont pas équivalents à des économies de coût validées ;
- l’étude n’a pas établi que la réponse était incomplète, inutilisable ou incorrecte au point de détection ;
- l’étude n’établit pas que l’arrêt est toujours l’action appropriée.

La conclusion principale est donc :

> Les signaux runtime peuvent rendre une intervention techniquement possible.  
> Ils ne déterminent pas quelle intervention est appropriée.

L’organisation utilisatrice reste responsable de la définition de la politique de gouvernance applicable.

Note exploratoire sur l’actionnabilité :

- [Actionnabilité du signal runtime NeoMundi ControlTower](https://doi.org/10.5281/zenodo.21499295)

---

## Reproductibilité et dépendance au contexte

L’actionnabilité n’a de valeur opérationnelle que si le signal sous-jacent est suffisamment caractérisé dans des conditions répétées et variées.

Une étude exploratoire de réplication a évalué les signaux NeoMundi à travers :

- plusieurs campagnes d’exécution ;
- plusieurs fournisseurs ;
- différentes températures de génération ;
- des corpus classiques ;
- des corpus de stress-test ciblés ;
- des catégories de prompts élargies.

L’étude a montré que la fréquence observée des décisions FLAG variait sensiblement selon le corpus expérimental et, dans une certaine mesure, selon le fournisseur.

Les corpus classiques ont produit de faibles taux de FLAG dans les configurations testées.

Les corpus de stress-test ciblés ont produit des taux de FLAG plus élevés, avec des différences entre fournisseurs.

Dans les conditions étudiées, la température ne semblait pas être le principal facteur déterminant.

L’étude a également rapporté une relation cohérente entre les profils DROP et les décisions FLAG dans les configurations testées.

Ces observations conduisent à une distinction importante :

### Prévalence du signal

Fréquence à laquelle un signal apparaît dans une campagne donnée.

### Cohérence du signal

Maintien d’une relation cohérente entre les signaux associés et les décisions dans les configurations testées.

Un signal peut rester cohérent dans sa structure interne même lorsque sa prévalence observée varie selon le corpus ou le fournisseur.

Note exploratoire sur la reproductibilité :

- [Stabilité et reproductibilité du signal runtime NeoMundi ControlTower](https://doi.org/10.5281/zenodo.21499715)

---

## Limite de contexte et de reproductibilité

La fréquence observée d’un signal runtime peut dépendre :

- de la composition du corpus de prompts ;
- de la nature des situations testées ;
- du fournisseur ;
- de la version du modèle ;
- des paramètres de génération ;
- de la période d’exécution ;
- du protocole de mesure ;
- des critères de détection ou d’agrégation choisis.

Un taux de FLAG observé dans une campagne expérimentale ne doit pas être interprété comme :

- un taux d’échec universel ;
- un score général de sécurité du modèle ;
- un niveau global de fiabilité du fournisseur ;
- un taux d’incident à l’échelle d’une population ;
- une estimation directe du risque en production.

Les résultats de stress-test doivent être interprétés comme des mesures obtenues dans des conditions volontairement exigeantes.

Les politiques de production doivent être calibrées à partir :

- de cas d’usage représentatifs ;
- de fenêtres d’exécution répétées ;
- de contrôles positifs et négatifs connus ;
- de conditions métier pertinentes ;
- du suivi des fournisseurs et des versions de modèles ;
- d’une validation factuelle ou experte externe lorsque cela est nécessaire.

---

## Limite d’actionnabilité

La détection runtime peut rendre une intervention techniquement possible avant la fin de la génération.

Elle ne détermine pas automatiquement si le système doit :

- arrêter ;
- poursuivre ;
- régénérer ;
- rerouter ;
- vérifier ;
- escalader ;
- documenter l’événement.

Ces actions restent des choix de gouvernance configurables.

Une politique d’intervention en production doit tenir compte :

- de la criticité du cas d’usage ;
- du coût des faux positifs ;
- du coût des faux négatifs ;
- du niveau de complétude de la réponse ;
- des exigences métier ;
- des contraintes de latence ;
- de la disponibilité d’une revue humaine ;
- des modèles ou systèmes de repli ;
- des exigences de conservation des preuves.

Un signal peut donc être techniquement actionnable sans que la politique d’intervention associée soit universellement validée.

---

## Position méthodologique

Les signaux de télémétrie runtime NeoMundi sont des artefacts d’observabilité orientés gouvernance.

Ils sont conçus pour soutenir :

- la supervision runtime ;
- l’observabilité comportementale ;
- les processus de gouvernance ;
- l’auditabilité ;
- l’analyse de télémétrie ;
- les systèmes d’orchestration ;
- l’analyse comparative de modèles ;
- la détection de zones de tension ;
- la détection de ruptures locales ;
- la détection de stabilité trompeuse ;
- des politiques d’intervention configurables côté client.

Ils ne sont pas destinés à :

- reconstruire la cognition interne d’un modèle ;
- établir une vérité sémantique universelle ;
- certifier automatiquement une réponse ;
- remplacer l’expertise juridique, médicale, scientifique, de sécurité ou métier ;
- produire un classement universel des modèles ;
- définir un seuil universel d’arrêt ;
- imposer automatiquement une action de gouvernance.

La lecture minimale recommandée combine, lorsque ces éléments sont disponibles :

- le G-score ;
- ΔG ou dg_variation ;
- FLAG ou ALLOW ;
- le régime runtime ;
- le profil ΔG ;
- les indicateurs de cohérence ou de risque factuel ;
- une couche externe factuelle ou métier lorsque le cas d’usage l’exige.

---

## Limites d’interprétation

Un G-score élevé ne signifie pas qu’une réponse est vraie.

Un G-score faible ne signifie pas automatiquement qu’une réponse est fausse.

Un FLAG ne signifie pas automatiquement qu’une réponse est fausse ou inutilisable.

Un statut ALLOW ne constitue pas une certification factuelle.

Un régime STABLE ne suffit pas pour conclure qu’un système est sûr ou fiable.

Un ΔG élevé ne prouve pas une erreur.

Un profil DROP ne justifie pas automatiquement le blocage d’une sortie.

Un point ΔG négatif ne constitue pas, à lui seul, un seuil universel d’arrêt.

Un taux de FLAG mesuré dans une campagne ne doit pas être généralisé sans réplication.

Aucun signal isolé ne suffit pour caractériser l’ensemble du risque associé à une sortie générative.

Les signaux doivent être interprétés ensemble :

- dans leur contexte d’usage ;
- avec les preuves disponibles ;
- dans le cadre d’une politique documentée ;
- avec une connaissance du protocole de mesure ;
- avec la validation métier appropriée.

---

## Intégration dans les systèmes de gouvernance

Dans une architecture d’observabilité, les signaux NeoMundi peuvent être utilisés pour :

- tracer les exécutions génératives ;
- comparer les comportements entre fournisseurs ou modèles ;
- identifier des zones de tension runtime ;
- surveiller les variations comportementales ;
- détecter des changements entre fenêtres d’exécution ;
- produire des artefacts d’audit ;
- alimenter des tableaux de bord de gouvernance ;
- documenter des événements critiques.

Dans une architecture de gouvernance, ils peuvent contribuer à des décisions configurables telles que :

- autoriser une sortie ;
- demander une vérification factuelle ;
- demander une régénération ;
- rerouter vers un autre modèle ;
- appliquer une politique d’arrêt anticipé ;
- escalader vers une revue humaine ;
- ouvrir une anomalie ou un incident ;
- conserver des preuves pour l’audit ;
- lancer un processus de replay ou de retest.

NeoMundi fournit la couche de mesure et de télémétrie.

L’organisation utilisatrice définit :

- les seuils applicables ;
- les règles de décision ;
- la politique de risque ;
- la stratégie d’intervention ;
- la frontière d’autorisation ;
- l’action opérationnelle finale.

---

## Études exploratoires externes

L’interprétation publique des signaux runtime NeoMundi a été enrichie par des études exploratoires conduites par des contributeurs externes.

Ces études constituent des contributions méthodologiques.

Elles ne constituent pas :

- une validation mathématique définitive ;
- une certification produit ;
- des affirmations universelles de performance ;
- une approbation réglementaire ;
- une preuve d’adéquation à tous les environnements de production.

### Interprétation multi-signaux

Une première revue exploratoire externe a été conduite par Pape Malick Diop, Data Scientist et ML Researcher.

La revue a examiné :

- le G-score ;
- ΔG ;
- FLAG ;
- le régime runtime ;
- l’exactitude benchmark ;
- la stabilité trompeuse ;
- l’interprétation multi-signaux ;
- l’intégration OBS/GOV-ready.

Analyse associée :

- [Signaux temps réel, stabilité trompeuse et importance de la lecture multi-signaux](https://neomundi.org/observatoire-ia/signaux-temps-reel-stabilite-trompeuse-et-importance-lecture-multi-signaux)

### Actionnabilité des signaux

Fatima Ezzahrae Gouarab a évalué la faisabilité technique exploratoire de l’utilisation des signaux runtime NeoMundi comme entrées d’une politique de gouvernance côté client pendant la génération.

Étude :

- [Actionnabilité du signal runtime NeoMundi ControlTower](https://doi.org/10.5281/zenodo.21499295)

### Reproductibilité des signaux

Fatima Ezzahrae Gouarab a également conduit une étude comparative de réplication multi-fournisseurs, multi-corpus et multi-configurations.

Étude :

- [Stabilité et reproductibilité du signal runtime NeoMundi ControlTower](https://doi.org/10.5281/zenodo.21499715)

Ensemble, ces contributions documentent trois dimensions complémentaires :

1. comment les signaux peuvent être interprétés ;
2. comment ils peuvent soutenir des actions de gouvernance ;
3. dans quelles conditions méthodologiques leur interprétation doit être répliquée et contextualisée.

---

## Licence

Ce dépôt est publié sous licence Apache-2.0.

---

## À propos

Définitions publiques des signaux de télémétrie runtime et recommandations méthodologiques pour l’observabilité des IA orientée gouvernance et la gouvernance runtime configurable.
