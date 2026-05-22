# Runtime Telemetry Signals

## Version française de travail

Ce dépôt documente la structure publique des signaux de télémétrie runtime NeoMundi.

Il ne divulgue pas les formules propriétaires, les pondérations internes, les mécanismes d’inférence, ni les règles décisionnelles complètes utilisées dans le moteur NeoMundi.

Son objectif est de clarifier :

- ce que les signaux représentent ;
- ce qu’ils ne prétendent pas représenter ;
- comment ils peuvent être interprétés dans un cadre de gouvernance runtime ;
- quelles sont leurs limites méthodologiques.

## G - État de stabilité de gouvernance

G est un analogue de stabilité de type Lyapunov, orienté gouvernance, qui permet d’observer si une génération reste dans une zone de stabilité opérationnelle ou s’en éloigne.

G est un signal normalisé de stabilité de gouvernance associé à une génération IA ou à un segment d’exécution.

Il peut être compris comme un analogue de stabilité inspiré des raisonnements de type Lyapunov appliqués aux systèmes dynamiques.

Il ne s’agit pas d’une fonction de Lyapunov canonique, ni d’une preuve formelle de stabilité du modèle.

G aide à observer si une génération reste dans une zone de stabilité opérationnelle, s’approche d’une zone de transition, ou présente des signes d’instabilité.
