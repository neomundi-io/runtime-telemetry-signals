# ΔG = variation de G entre deux fenêtres runtime

## Version française de travail

Ce document présente une définition publique et méthodologique du signal ΔG utilisé dans le cadre NeoMundi.

Il ne divulgue pas les formules propriétaires, les pondérations internes, les mécanismes d’inférence, ni les règles décisionnelles complètes utilisées dans le moteur NeoMundi.

## Définition

ΔG représente la variation observée du signal G entre plusieurs fenêtres d’exécution runtime.

Il permet de suivre l’évolution d’un état de stabilité de gouvernance pendant une génération IA ou un segment d’exécution.

Dans cette lecture, G représente un état normalisé de stabilité, tandis que ΔG représente le déplacement ou la variation de cet état au cours du temps.

## Rôle du signal

ΔG est conçu pour faire apparaître les changements de stabilité pendant l’exécution.

Il peut contribuer à identifier :

- une stabilisation progressive ;
- une dégradation de stabilité ;
- une rupture comportementale ;
- une transition entre régimes ;
- une dérive observable dans la génération.

## Ce que ΔG ne prétend pas mesurer

ΔG ne prétend pas mesurer :

- la vérité sémantique absolue ;
- la certitude factuelle ;
- la cognition interne du modèle ;
- la cause profonde du changement observé ;
- une hallucination universelle ou exhaustive.

## Position méthodologique

ΔG est un signal d’observabilité runtime.

Il ne cherche pas à expliquer pourquoi un modèle change de comportement.  
Il vise à rendre observable le moment où un changement de stabilité apparaît dans la génération.

ΔG est donc particulièrement utile dans les systèmes de gouvernance où l’enjeu n’est pas seulement de connaître l’état final d’une réponse, mais aussi de suivre son évolution pendant l’exécution.

## Usage gouvernance

Dans un système de gouvernance runtime, ΔG peut servir à :

- détecter une variation significative de stabilité ;
- déclencher une alerte ;
- alimenter une timeline de stabilité ;
- soutenir une décision ALLOW / FLAG / SIGNAL ;
- documenter une trajectoire de génération ;
- fournir un signal exploitable à un système d’orchestration.

## Limites

ΔG doit toujours être interprété avec le contexte de génération.

Une variation de ΔG ne constitue pas, à elle seule, une preuve d’erreur ou d’hallucination.

Elle indique qu’un changement de stabilité a été observé entre plusieurs fenêtres d’exécution.

L’interprétation finale dépend du contexte, du niveau de risque, des seuils choisis et du système de gouvernance dans lequel le signal est utilisé.
