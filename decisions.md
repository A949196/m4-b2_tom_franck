# Décisions du binôme — M4-B2 (PCB Defect)

## 1. Option choisie pour l'implémentation

**Choix** : Option A (CNN scratch)

**Argument** :
- Volume modeste (~2k images, ~300/classe) : suffisant pour un CNN simple sans overfitting sur 5-10 epochs.
- Objectif pédagogique : comprendre l'architecture de bout en bout (utile pour argumenter le comparatif face à des boîtes noires transfer/CLIP).
- CPU-only imposé par le brief : CNN scratch reste le plus léger à entraîner et à faire tourner rapidement.

## 2. Répartition des tâches binôme

| Tâche | Membre 1 (`Tom`) | Membre 2 (`Carpentier`) | Modalité |
|---|---|---|---|
| Setup repo + EDA | Repo, template, branch | EDA | aync |
| Implémentation option | Option A | Option B | async |
| Comparatif économique | Comparatif économique | rien | async |
| README + restitution | README | restitution | aync README + sync restitution |

## 3. Coordination Discord

- **Matin** (~9h) : check-in MP — qui fait quoi aujourd'hui ?
- **Midi** : point d'étape — qu'est-ce qui est mergé ?
- **Soir** : ce qui reste pour demain
- **Vendredi 11h** : test croisé du repo (chacun clone et teste le code de l'autre)

## 4. Branches Git

- Convention : `tom/option-a` 
- Merge sur `main` après revue MP

## 5. Restitution duo mardi 1ᵉʳ sept (rentrée M5)

- **Franck** présente : (démo technique 3 min)
- **Tom** présente : (argumentation économique 2 min)
- 5 min total + 5 min discussion

## 6. Points négociés (à expliciter en cas de désaccord)

---

*Décisions tracées par le binôme `Tom` × `Franck` — `08/07/2026`.*
