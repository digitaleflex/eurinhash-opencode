# EURINHASH — Mission UX Specification

> FR/EN — v1.0 — 2026-09-19

## FR

### Objectif UX

Faire du Command Center une interface de **contrôle de mission** plutôt qu'une simple interface de chat.

L'utilisateur doit pouvoir répondre à tout moment :

1. Quelle mission suis-je en train d'accomplir ?
2. Que fait le système maintenant ?
3. Quelles ressources sont utilisées ?
4. Pourquoi ont-elles été choisies ?
5. Qu'est-ce qui a réellement été validé ?
6. Qu'est-ce qui reste non vérifié ?
7. Quelles preuves établissent la complétion ?

### Architecture d'écran

```text
┌──────────────┬─────────────────────────────┬──────────────┐
│ WORKSPACE    │ CHAT / MISSION              │ AGENT        │
│ files / git  │ objective / plan / chat     │ state/model  │
│ issue / task │ execution / verification   │ tools/risk   │
├──────────────┴─────────────────────────────┴──────────────┤
│ ACTIVITY / EVENTS / EXECUTION / EVIDENCE                  │
├───────────────────────────────────────────────────────────┤
│ COMMAND / INPUT                                           │
└───────────────────────────────────────────────────────────┘
```

### États

```text
REQUESTED
→ RUNNING
→ EXECUTING
→ VALIDATING
→ VERIFYING
→ VERIFIED
```

Branches : `BLOCKED`, `FAILED`, `PAUSED`, `CANCELLED`, `UNVERIFIED`, `NEEDS_REVIEW`.

### Règles d'affichage

- aucune métrique sans source, unité et signification ;
- `UNKNOWN` n'est jamais affiché comme zéro ;
- une estimation est distinguée d'une observation ;
- l'agent peut déclarer une réussite, mais l'UI ne la transforme pas automatiquement en preuve ;
- les permissions et changements sensibles sont visibles ;
- l'activité est dérivée d'événements réels ;
- les panneaux ne créent pas de deuxième source de vérité.

### Explainability

Le panneau de routage doit pouvoir expliquer :

- capacités requises ;
- candidats considérés ;
- candidats exclus et raison ;
- ressource sélectionnée ;
- contraintes de coût/quota/latence ;
- niveau de confiance ou qualité des données lorsque défini.

### Verification panel

Chaque critère doit présenter :

`criterion → status → evidence → validation → unresolved conditions`.

### Modes de densité

`MINIMAL | STANDARD | DEVELOPER | OBSERVER | DEBUG`

Ils modifient la densité d'information, jamais les règles métier.

### Responsive terminal

Sur petit terminal : conserver mission, session/chat et input ; replier/repositionner les panneaux contextuels ; ne pas supprimer la preuve ou les erreurs importantes.

---

## EN

### UX goal

Make the Command Center a **mission-control interface**, not merely a chat interface.

At any moment the user should know the mission, current activity, resources, selection rationale, validated work, remaining uncertainty and proof of completion.

### Screen architecture

Persistent zones: Workspace, Chat/Mission, Agent.

Contextual zones: Activity, Tasks, Git, MCP/LSP, diagnostics and evidence.

Overlays: command palette, permissions, routing explanation, error details and verification.

### State and truth

The UI must distinguish requested, running, executing, validating, verifying and verified, with blocked/failed/paused/cancelled/unverified/review branches.

No metric without source and meaning. Unknown is not zero. Estimated data is distinct from observed data. Agent claims are not verification evidence.

### Explainability

Routing must expose requirements, candidates, exclusion reasons, selected resource and relevant cost/quota/latency constraints.

### Verification

Acceptance criteria are evaluated individually and linked to concrete evidence.

### Density and narrow terminals

Density modes alter information density only. Narrow terminals collapse contextual surfaces while preserving mission, session and input functionality.
