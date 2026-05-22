# Décisions de gouvernance - ALLOW / FLAG / BLOCK

## Version française de travail

Ce document présente une définition publique et méthodologique des décisions de gouvernance utilisées dans le cadre NeoMundi.

Il ne divulgue pas les seuils propriétaires, les pondérations internes, les règles décisionnelles complètes ni les mécanismes d’inférence utilisés dans le moteur NeoMundi.

## Principe général

Les décisions ALLOW, FLAG et BLOCK ne sont pas des jugements absolus de vérité.

Elles constituent des états de gouvernance produits à partir de signaux runtime, tels que G, ΔG, des signaux de risque, des métriques informationnelles ou des règles configurées par le système utilisateur.

Leur rôle est d’aider un système d’IA, une application ou un opérateur humain à décider comment traiter une génération ou un segment d’exécution.

## ALLOW

ALLOW indique qu’une génération ou un segment d’exécution est considéré comme suffisamment stable pour poursuivre le flux prévu.

Dans ce contexte, ALLOW ne signifie pas que la réponse est absolument vraie, parfaite ou exempte de risque.

ALLOW signifie que, selon les signaux disponibles et les seuils appliqués, aucun niveau d’instabilité suffisant n’a été observé pour déclencher une alerte ou une interruption.

ALLOW peut soutenir :

- la poursuite de la génération ;
- la transmission de la réponse à l’utilisateur final ;
- l’archivage du résultat comme état stable ;
- la documentation d’un passage sans alerte.

## FLAG

FLAG indique qu’une génération ou un segment d’exécution présente un signal d’instabilité, d’incertitude, de risque ou de transition qui mérite attention.

FLAG ne signifie pas nécessairement que la réponse est fausse.

FLAG signifie qu’un ou plusieurs signaux runtime suggèrent qu’une supervision, une vérification, une relance, une correction ou une décision humaine peut être nécessaire.

FLAG peut être associé à :

- une baisse de stabilité ;
- une variation significative de ΔG ;
- un risque sémantique ;
- une hallucination possible ;
- une densité informationnelle problématique ;
- un défaut de grounding ;
- une règle métier configurée par le client.

## BLOCK

BLOCK indique qu’une génération ou un segment d’exécution ne doit pas poursuivre le flux normal selon les règles de gouvernance appliquées.

BLOCK peut correspondre à une interruption, une mise en attente, une demande de validation humaine, une régénération ou une redirection vers un autre workflow.

BLOCK ne doit pas être compris comme une preuve absolue de danger ou d’erreur.

Il s’agit d’une décision opérationnelle prise dans un cadre de gouvernance donné, selon des seuils, des règles et un niveau de risque configurés.

## Différence entre signal et décision

G, ΔG, E, Di ou ESI sont des signaux ou des métriques.

ALLOW, FLAG et BLOCK sont des décisions ou des états de gouvernance produits à partir de ces signaux.

Un signal observe.

Une décision oriente l’action.

Cette distinction est essentielle : NeoMundi ne prétend pas transformer automatiquement une métrique en vérité universelle. Le système produit des signaux interprétables et des états de gouvernance configurables.

## Interprétation contextuelle

Les décisions ALLOW, FLAG et BLOCK doivent toujours être interprétées dans leur contexte :

- domaine d’usage ;
- niveau de risque ;
- seuils configurés ;
- criticité métier ;
- présence ou non d’un humain dans la boucle ;
- contraintes réglementaires ;
- politique de gouvernance du système utilisateur.

Une même valeur de signal peut produire des décisions différentes selon le contexte d’application.

## Non-revendications

Les décisions ALLOW, FLAG et BLOCK ne prétendent pas fournir :

- une preuve absolue de vérité ;
- une certification juridique automatique ;
- une garantie d’absence d’hallucination ;
- une reconstruction de la cognition interne du modèle ;
- une décision morale universelle ;
- une substitution complète à la responsabilité humaine.

## Position méthodologique

ALLOW, FLAG et BLOCK doivent être compris comme des artefacts de gouvernance runtime.

Ils sont conçus pour rendre les systèmes IA plus observables, plus auditables et plus gouvernables pendant leur exécution.

Ils permettent de documenter non seulement ce qu’un modèle a produit, mais aussi dans quel état de stabilité ou d’instabilité cette production a été observée.
