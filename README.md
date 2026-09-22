# 🎵 Emotion-Conditioned Piano Music Generation (CVAE-LSTM)

[![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-EE4C2C?style=flat&logo=pytorch&logoColor=white)](https://pytorch.org/)
[![Dataset](https://img.shields.io/badge/Dataset-EMOPIA-blue)](https://github.com/lucas2012/EMOPIA)

> **Université Paris-Dauphine — Projet de Deep Learning (Mai 2026)**  
> **Auteurs :** Éric CHEN & Léa YANG

---

## 🌐 Navigation / Language
- [Français](#-version-française)
- [English](#-english-version)

---

## 🇫🇷 Version Française

### 📌 Présentation du Projet
Ce projet explore la génération automatique de musique pour piano conditionnée par des émotions. Nous combinons le dataset **EMOPIA** et le **modèle circomplexe de Russell (1980)** pour classer les pièces musicales selon la **Valence** (positivité) et l'**Activation / Arousal** (énergie) :

* **Q1 (Haute Valence / Haute Activation) :** Joie, excitation
* **Q2 (Basse Valence / Haute Activation) :** Tension, colère
* **Q3 (Basse Valence / Basse Activation) :** Tristesse, mélancolie
* **Q4 (Haute Valence / Basse Activation) :** Calme, sérénité

Notre architecture retenue est un **Auto-Encodeur Variationnel Conditionnel couplé à un LSTM (CVAE-LSTM)**.

### 📊 Benchmark des Modèles
Représentation des données : Tokenisation **REMI** via `MidiTok` (vocabulaire de 268 tokens, $SEQ\_LEN = 512$).

| Modèle | Dim Latente ($d$) | Loss Val (ELBO) | Résultat |
| :--- | :---: | :---: | :--- |
| **VAE (MLP)** | 64 | 2346.0 | Overfitting massif, perte du contexte temporel. |
| **VAE (CNN 1D)** | 64 | 1885.4 | Bonnes structures locales, amnésie temporelle. |
| **VAE (LSTM)** | 64 | 1284.4 | Excellente cohérence, génération émotionnelle aléatoire[cite: 1]. |
| **C-VAE (LSTM)** | **64** | **1283.6** | **Haute qualité musicale + Séparation nette en 4 clusters**[cite: 1]. |

### 🛠️ Structure du Dépôt
```text
cvae-emopia-music/
├── data/              # Fichiers EMOPIA .mid (bruts et tokenisés)
├── models/            # Checkpoints des modèles (.pt)
├── notebooks/         # Visualisations latentes (PCA, t-SNE)
├── samples/           # Fichiers MIDI générés (Q1 à Q4)
├── src/               # Code source (dataset, architectures, train, generate)
├── rapport_deep.pdf   # Rapport de projet complet
├── requirements.txt   # Dépendances Python
└── README.md
