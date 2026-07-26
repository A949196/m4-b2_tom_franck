# Verdict — Recommandation TechniMatic via Mistral

> 8 lignes maximum.
> Auteurs : `Tom` × `Franck` — Date : `08/07/2026`

**Recommandation** : Option A (CNN scratch) en production, avec collecte de données supplémentaires en parallèle.

**Raison principale (chiffrée)** : à accuracy quasi identitque (57,5% vs 56,2%), Option A entraîne 60 fois plus vite (9,6s vs 610,8s) et infère 100 fois plus vite (0,41 ms vs 56,53 ms) qu'Option B, pour un modèle 20 fois plus léger (2,09 Mo vs 42,65 Mo) - sans bénéfice mesurable du transfer learning sur ce volume de données.

**Condition de changement d'avis** : si le volume de données devient important, ou si un domaine plus proche d'ImageNet est ciblé, alors je proposerais de réévaluer Option B (le transfer learning devrait alors montrer son avantage habituel).

---

*Verdict binôme — `08/07/2026`.*
