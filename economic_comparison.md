# Comparatif économique 3 approches — PCB Defect

> Document remis à **Inès Tabet** (Mistral) qui relaie à **TechniMatic**.
> Auteurs : `Tom` × `Franck` — Date : `08/07/2026`

## Méthodologie

- **Option A et B implémentées** : mesures **réelles**, obtenues respectivement sur les branches `tom/option-a` (CNN from scratch) et `franck/transfert_learning` (ResNet-18 transfer learning), sur le même dataset (2100 images, split train/val/test identique, seed 42).
- **option C non implémentée** : estimation argumentée via sources publiques (voir section dédiée). 

## Tableau

| Critère | Option A (CNN scratch) | Option B (Transfer ResNet-18) | Option C (Zero-shot CLIP) |
|---|---|---|---|
| **Données d'entraînement requises** | 1470 (train) | 1470 (train) | **0** |
| **Temps train (CPU)** | 9,6 s (8 epoches) | 610,8 s (10 epochs) | **0** (pas d'entraînement) |
| **Latence inférence / image (CPU)** | 0,41 ms | 56,53 ms | 80-150 ms (estimé) |
| **Mémoire modèle (Mo)** | 2,09 Mo (548k paramètres) | 42,65 Mo (11,18M paramètres) | ~150 Mo (poids CLIP, non ré-entraînés) |
| **Accuracy attendue** | 57,5% (mesuré) | 56,2% (mesuré) | 20-40% (estimé, dépend de la qualité du prompt) |
| **Coût € (training cloud)** |  ~$0 (temps négligeable) | ~$0 (temps négligeable) | $0 (aucun entraînement) |
| **Coût € (API)** | $0 (modèle local) | $0 (modèle local) | $0 (modèle local) |
| **Maintenance** | Réentraîner si dérive (10s, rapide) | Réentraîner si dérive (10 min, plus coûteux en temps) | Aucune (prompts à raffiner) |

**Légende** :
- **Mesuré** : valeur obtenue dans notre implémentation
- **Estimé** : valeur extrapolée de sources publiques (citée ci-dessous)

## Sources des estimations

- **Accuracy attendue faible sur domaine spécialisé** : le papier original CLIP (Radford et al., 2021, "Learning Transferable Visual Models From Natural Language Supervision") montre que les performances zero-shot chutent nettement sur des domaines visuels éloignés de la distribution d'entraînement (photos web) — les défauts PCB (rayures, soudures froides) sont visuellement subtils et hors distribution, contrairement aux objets du quotidien sur lesquels CLIP excelle.
- **Poids du modèle (~150 Mo)** : cf. `README.md` du repo, section "Bloqué·e·s" : *"Sur CLIP : ~150 Mo de téléchargement au 1ᵉʳ appel"*.
- **Latence estimée** : par extrapolation, un forward pass CLIP ViT-B/32 sur CPU tourne typiquement entre 50 et 150 ms par image selon la taille d'image et le nombre de prompts comparés (7 classes ici) — cohérent avec les temps d'inférence CPU habituellement documentés pour ce modèle sur des tâches de classification zero-shot à faible nombre de classes.

## Comparaison qualitative

| Aspect | Option A | Option B | Option C |
|---|---|---|---|
| **Quand préférer** | Volume modeste, contrainte CPU forte, besoin d'un modèle léger à déployer | Besoin de robustesse "standard" sans trop de risque projet, si le budget compute est disponible | Absence totale de données labellisées, besoin d'un POC rapide sans entraînement |
| **Quand éviter** | Si la précision doit être maximisée à tout prix | Si le budget temps d'entraînemebt/latence est très contraint | Si la précision est critique - les défauts PCB sont hors distribution CLIP |
| **Domaine adapté** | POC industriel, contrôle qualité léger avec réentraînement fréquent | Cas nécessitant un existant "safe" mais où la latence n'est pas critique | Preuve de concept rapide, avant collecte de données labellisées |

---

*Comparatif produit en binôme — `08/07/2026`.*
