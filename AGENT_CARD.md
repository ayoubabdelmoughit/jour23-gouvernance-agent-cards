# Agent Card — jour 23 (FAQ Bot CTPES)

## Que fait l'agent ?
Répond aux questions des porteurs de micro-projets sur les services du Centre des Très
Petites Entreprises Solidaires (CTPES) : financement, formation, accompagnement
administratif. Refuse poliment toute question hors de ce périmètre (pas d'invention
d'information).

## Qui en est responsable ?
- Propriétaire : Ayoub Abdelmoughit
- Responsable technique : Ayoub Abdelmoughit

## Quels outils utilise-t-il ?
- Modèle : Ollama (gpt-oss:120b)
- Orchestration : Plateforme Agentic AI (flow visuel, 4 nœuds)
- Composants : Chat Input → Prompt Template → Agent → Chat Output

## Sources de données
- Contexte statique injecté dans le Prompt Template (informations CTPES rédigées en dur,
  pas de base de données externe à ce stade)
- Depuis v1.1.0 : inclut aussi les horaires d'accueil du centre

## Quelles sont ses limites ?
- Répond UNIQUEMENT sur la base du contexte écrit dans le Prompt Template — aucune
  recherche web, aucune base de données connectée
- Ne gère pas l'historique multi-session (pas de mémoire entre deux conversations)
- Si le contexte CTPES change dans la réalité, il faut mettre à jour le Prompt Template
  manuellement (pas de source live)
- Pas de garde-fou contre un prompt-injection avancé dans la question utilisateur

## Mode de déploiement (Jour 24)
- **Mode utilisé : Temps Réel (API)** — l'agent est exposé via l'interface chat/API de
  la plateforme Agentic AI et répond à chaque question à la demande, instantanément.
- **Pourquoi ce mode** : chaque requête est une question isolée d'un porteur de projet
  qui attend une réponse immédiate — exactement le cas d'usage du déploiement temps réel
  (par opposition à un traitement par lots programmé).
- **Pourquoi pas les autres modes** :
  - *Batch* — non pertinent, il n'y a pas de gros volume à traiter à intervalles réguliers.
  - *Streaming* — non pertinent, il n'y a pas de flux continu d'événements à consommer.
  - *Edge* — non pertinent, l'agent n'est pas embarqué sur un appareil local ; il s'exécute
    côté plateforme (cloud), accessible via navigateur.

## KPI & Métriques
- Taux de réponses pertinentes (dans le périmètre CTPES)
- Taux de refus corrects (hors périmètre → refus poli, pas d'hallucination)
- (pas encore de dashboard/mesure automatisée sur ce flow — à ajouter si mis en prod)

## Version & Revue
- Version actuelle : v1.1.0
- Date de création : 28/10/2026
- Dernière revue : 28/10/2026

### Historique des versions
- **v1.0.0** (28/10/2026) : version initiale — FAQ sur services, financement, formation, accompagnement
- **v1.1.0** (28/10/2026) : ajout d'une information (horaires d'accueil) — pas de changement de comportement, compatible avec v1.0.0
