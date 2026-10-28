# Runbook d'Incident — jour 23 (FAQ Bot CTPES)

## Objectif
Ce document décrit les actions à suivre si l'agent "jour 23" présente un comportement
inattendu ou incorrect (ex : il invente des informations, répond hors de son rôle,
ou donne des conseils financiers/juridiques qu'il ne devrait pas donner).

---

## 1. Détection
Signes qu'un incident est en cours :
- L'agent répond à une question hors du périmètre CTPES au lieu de refuser poliment
  (ex : il donne un vrai conseil financier personnalisé au lieu de rediriger vers l'équipe)
- L'agent invente des informations non présentes dans le Prompt Template (hallucination)
- L'agent répond dans une langue ou un ton inapproprié
- Une personne de l'équipe ou un porteur de projet signale une réponse incorrecte

## 2. Contention (limiter les dégâts immédiatement)
- Désactiver temporairement le flow sur la plateforme Agentic AI (Pause/Disable du flow,
  ou retirer l'accès au lien partagé du Chat) — équivalent du "Kill Switch"
- Si déployé derrière un endpoint public : couper ou restreindre l'accès à l'endpoint
- Prévenir l'équipe/le propriétaire (Ayoub Abdelmoughit) de l'incident en cours

## 3. Remédiation (comprendre et corriger)
- Consulter l'historique des conversations dans le Playground pour identifier la question
  exacte qui a causé le problème
- Comparer le comportement actuel avec la version taguée précédente pour voir si un
  changement récent du Prompt Template est en cause :
  ```
  git diff v1.0.0 v1.1.0
  ```
- Corriger le Prompt Template (préciser davantage le périmètre, renforcer la consigne de
  refus hors-sujet, etc.)
- Si la correction est incertaine ou complexe : **revenir (rollback)** à la dernière
  version stable taguée. Deux méthodes :

  **Méthode A — `git revert` (recommandée, sûre)**
  Crée un nouveau commit qui annule les changements, sans effacer l'historique :
  ```
  git revert <sha_du_commit_problematique>
  git push
  ```

  **Méthode B — `git reset --hard` + force push (rapide mais destructive)**
  Revient directement à un tag stable, en effaçant les commits suivants :
  ```
  git reset --hard v1.0.0
  git push --force
  ```
  ⚠️ À utiliser uniquement sur un projet personnel / hors production. Sur un projet
  d'équipe ou en production, toujours préférer `git revert`.

## 4. Rétablissement (retour à la normale)
- Tester la correction dans le Playground avec le(s) même(s) cas qui avaient posé problème,
  plus les 3 questions de test standard (2 dans le périmètre, 1 hors périmètre)
- Réactiver le flow / rouvrir l'accès
- Mettre à jour l'Agent Card (section "Quelles sont ses limites" si une nouvelle limite a
  été découverte) et créer un nouveau tag (ex. `v1.1.1` si c'est un correctif / Patch)
- Documenter l'incident brièvement ci-dessous pour référence future

---

## Historique des incidents
*(aucun incident réel à ce jour — ce runbook a été rédigé de manière préventive)*
