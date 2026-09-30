# SLM Quality Prediction & Parameter Optimization

Prédiction data-driven de la **densité** et de la **rugosité de surface (Ra)** en
**fusion laser sur lit de poudre (SLM)** d'acier inoxydable **316L**, dans un
contexte de **données rares**, puis sélection des paramètres procédé par
optimisation multi-objectifs à base de modèles de substitution (surrogates).

Ce dépôt contient le code de recherche associé à l'article :

> **Data-driven prediction and surrogate-based parameter selection for density and
> surface roughness in SLM of 316L SS under data scarcity**
> Abbas Hodroj, Hadj Habib Rouabah, Zakariya Ghalmane, Mourad Zghal.
> *The International Journal of Advanced Manufacturing Technology*, Springer, 2026.
> DOI : [10.1007/s00170-026-18908-7](https://doi.org/10.1007/s00170-026-18908-7)

## Contexte

En fabrication additive métallique, les campagnes expérimentales sont coûteuses :
les jeux de données sont donc petits. L'objectif est de construire des modèles
prédictifs fiables malgré cette rareté, puis de les utiliser comme substituts pour
proposer des paramètres procédé (puissance laser, vitesse de balayage, espacement
des vecteurs, épaisseur de couche…) atteignant des cibles de densité et de rugosité.

## Approche

1. **Augmentation de données** pour compenser la rareté :
   - mélanges gaussiens (**GMM**),
   - **cGAN** (Conditional GAN),
   - **CTGAN** (données tabulaires, via SDV).
2. **Modélisation prédictive** de Ra et de la densité :
   - modèles à base d'arbres (**XGBoost**, **AdaBoost**, Random Forest),
   - **stacking** de régresseurs,
   - **réseaux de neurones** (Keras/TensorFlow), y compris une architecture
     multi-sorties (Ra + densité).
3. **Analyse statistique** des facteurs (**ANOVA**) et de l'énergie volumique (VED).
4. **Sélection de paramètres** par optimisation multi-objectifs sur les surrogates :
   - **NSGA-II** (DEAP),
   - **évolution différentielle** (SciPy).

## Résultats (voir l'article)

- R² de ~0,73 à ~0,95 selon la cible pour les modèles simples.
- Réseau multi-sorties atteignant R² > 0,98.
- Paramètres proposés par l'optimisation à moins de ~1 % d'écart des cibles.

## Contenu du dépôt

| Fichier | Rôle |
|---|---|
| `data_remplissage.ipynb` / `data-remplissage.ipynb` | Préparation et complétion des données |
| `GMM.ipynb`, `cGAN.ipynb`, `ctgan.ipynb` | Augmentation de données |
| `models_*.ipynb`, `PVHT_GMM_models.ipynb` | Entraînement et comparaison des modèles |
| `2_aims_*.ipynb`, `models_pvht_anova_gmm_gan.ipynb` | Modèles multi-cibles (Ra + densité) |
| `optimisation_para.ipynb` | Optimisation multi-objectifs (NSGA-II, DE) |
| `affichage.ipynb` | Visualisations des résultats |
| `best_RN_Ra_dens_model.h5` | Réseau multi-sorties entraîné |
| `adaboost_model.pkl` | Modèle AdaBoost entraîné |
| `data - Copie.xlsx` | Jeu de données utilisé |

## Stack technique

Python · scikit-learn · TensorFlow / Keras · XGBoost · PyTorch · SDV / CTGAN ·
DEAP (NSGA-II) · SciPy · Pandas · NumPy · Matplotlib · Seaborn

## Installation

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter lab
```

## Citation

```bibtex
@article{hodroj2026slm,
  title   = {Data-driven prediction and surrogate-based parameter selection for density and surface roughness in SLM of 316L SS under data scarcity},
  author  = {Hodroj, Abbas and Rouabah, Hadj Habib and Ghalmane, Zakariya and Zghal, Mourad},
  journal = {The International Journal of Advanced Manufacturing Technology},
  year    = {2026},
  doi     = {10.1007/s00170-026-18908-7},
  publisher = {Springer}
}
```
