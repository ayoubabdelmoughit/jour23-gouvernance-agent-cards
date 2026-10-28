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
