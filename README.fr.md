# Signaux de télémétrie runtime

Notes méthodologiques publiques et définitions de signaux pour l’observabilité runtime des systèmes d’IA orientée gouvernance.

Ce dépôt documente la structure conceptuelle publique des signaux de télémétrie runtime de NeoMundi, notamment :

- les états de stabilité de gouvernance ;
- les signaux de variation runtime ;
- les concepts d’observabilité comportementale ;
- les artefacts de télémétrie orientés gouvernance ;
- les frontières méthodologiques.

Ce dépôt ne divulgue pas les implémentations internes propriétaires, les pondérations, ni les mécanismes d’inférence runtime.

Son objectif est de clarifier :

- ce que ces signaux sont censés représenter ;
- ce qu’ils ne prétendent pas représenter ;
- et comment ils peuvent être utilisés dans des systèmes de gouvernance runtime.

## Familles initiales de signaux

### G

État de stabilité normalisé orienté gouvernance.

G est conçu pour représenter une condition de stabilité de gouvernance normalisée associée à une génération ou à un état d’exécution d’un système d’IA.

### ΔG

Signal de variation runtime associé aux variations comportementales temporelles entre différentes fenêtres d’exécution.

ΔG est destiné à :

- l’observabilité runtime ;
- la surveillance des variations comportementales ;
- la télémétrie de gouvernance ;
- la mise en évidence de signaux d’instabilité.

ΔG n’est pas :

- un signal de vérité ;
- un mécanisme de reconstruction de la cognition ;
- ni un système d’omniscience sémantique.

## Position méthodologique

Les signaux de télémétrie runtime de NeoMundi sont des artefacts d’observabilité orientés gouvernance.

Ils sont conçus pour soutenir :

- la supervision runtime ;
- les workflows de gouvernance ;
- l’auditabilité ;
- l’analyse télémétrique ;
- les systèmes d’orchestration.

Ils ne visent pas à revendiquer une reconstruction exhaustive de la cognition interne des modèles, ni une vérité sémantique universelle.
