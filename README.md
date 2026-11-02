# Nepal Flood Comment Classifier

![Python](https://img.shields.io/badge/python-3.10--3.12-blue) ![Streamlit](https://img.shields.io/badge/built%20with-Streamlit-FF4B4B) ![scikit-learn](https://img.shields.io/badge/scikit--learn-1.6.1-F7931E) ![License: MIT](https://img.shields.io/badge/code-MIT-green)

A Streamlit app that classifies public comments about the Nepal flood into **seven themes** and shows, inline, which words drove each prediction.

## Features

- **TF-IDF + LinearSVC** classifier bundled with the app (no downloads needed).
- **LIME token contributions** shown inline for every prediction.
- **Twelve one-click sample comments** (two per theme) so you can try it without typing anything.

## Categories

1. Government, Infrastructure & Development Criticism
2. Climate Change & Natural Causes
3. Death/Damage Toll & Casualty Speculation
4. Reactions to Footage & Specific Moments
5. China / Dam & Conspiracy Theories
6. Prayers, Religious & Condolence Messages
7. Unrelated/Unintelligible

## Performance

Evaluated on a held-out 10% test split of 13,313 labelled comments (80/10/10 train/validation/test) in the accompanying research repository:

| Model | Test accuracy | Test macro F1 |
|---|---|---|
| TF-IDF + Linear SVM (**used here**) | 99.02% | 0.9895 |
| TF-IDF + Logistic Regression | 98.95% | 0.9887 |
| BERT (fine-tuned) | 97.22% | 0.9711 |

## Run locally

Use Python 3.10-3.12 to match the model's scikit-learn 1.6.1 serialization format.

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
streamlit run app.py
```

## A note on the scores

LinearSVC does not provide calibrated probabilities. The displayed normalized margins are **relative scores**, not probabilities, and LIME uses them to estimate local token contributions.

## Repository layout

| Path | Purpose |
|---|---|
| `app.py` | Streamlit application |
| `models/best_classical_model.pkl` | Trained TF-IDF + LinearSVC pipeline |
| `requirements.txt` | Pinned Python dependencies |

## Related work

Datasets, notebooks and the full results bundle (classical, deep-learning and transformer baselines, plus LIME figures) are in the companion research repository `amrita-sail-lab/nepal-flood-analysis`, which is private until the accompanying paper is released.

## License

Code is released under the [MIT License](LICENSE).
