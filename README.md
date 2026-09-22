# 🎵 Emotion-Conditioned Piano Music Generation (CVAE-LSTM)

> **Université Paris-Dauphine — Projet de Deep Learning (Mai 2026)**
> 
> **Auteurs :** Éric CHEN & Léa YANG
> 
> 

---

## 🌐 Navigation / Language
- [Français](#version-française)
- [English](#english-version)
---

## Version Française

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
| --- | --- | --- | --- |
| **VAE (MLP)** | 64 | 2346.0 | Overfitting massif, perte du contexte temporel.

 |
| **VAE (CNN 1D)** | 64 | 1885.4 | Bonnes structures locales, amnésie temporelle.

 |
| **VAE (LSTM)** | 64 | 1284.4 | Excellente cohérence, génération émotionnelle aléatoire.

 |
| **C-VAE (LSTM)** | **64** | **1283.6** | **Haute qualité musicale + Séparation nette en 4 clusters**.

 |

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

```

### 🚀 Démarrage Rapide

```bash
# 1. Cloner le projet et installer les dépendances
git clone https://github.com/votre-username/cvae-emopia-music.git
cd cvae-emopia-music
pip install -r requirements.txt

# 2. Entraîner le CVAE-LSTM
python src/train.py --model cvae_lstm --latent_dim 64 --epochs 100

# 3. Générer un morceau selon une émotion (ex: Q1 - Joie)
python src/generate.py --emotion Q1 --temperature 0.6 --output samples/joy.mid

```

---

## English Version

### 📌 Project Overview

This repository presents an end-to-end framework for emotion-conditioned piano music generation. Utilizing the **EMOPIA** dataset and **Russell's circumplex model (1980)**, our goal is to generate music guided by four distinct emotion quadrants based on **Valence** and **Arousal**:

* **Q1 (High Valence / High Arousal):** Joy, excitement


* **Q2 (Low Valence / High Arousal):** Tension, anger


* **Q3 (Low Valence / Low Arousal):** Sadness, melancholy


* **Q4 (High Valence / Low Arousal):** Calmness, serenity



Our primary model architecture is a **Conditional Variational Autoencoder paired with LSTMs (CVAE-LSTM)**.

### 📊 Model Benchmark

Data Representation: **REMI** tokenization via `MidiTok` (vocabulary size of 268 tokens, fixed $SEQ\_LEN = 512$).

| Model | Latent Dim ($d$) | Val Loss (ELBO) | Performance Summary |
| --- | --- | --- | --- |
| **VAE (MLP)** | 64 | 2346.0 | Severe overfitting, loss of temporal order.

 |
| **VAE (1D-CNN)** | 64 | 1885.4 | Learns local patterns, suffers from short-term memory.

 |
| **VAE (LSTM)** | 64 | 1284.4 | High musical coherence, unguided emotion generation.

 |
| **C-VAE (LSTM)** | **64** | **1283.6** | **Best musical grammar + Clear 4-cluster emotional separation**.

 |

### 🛠️ Repository Structure

```text
cvae-emopia-music/
├── data/              # EMOPIA dataset (.mid & processed tokens)
├── models/            # Saved PyTorch checkpoints (.pt)
├── notebooks/         # Latent space analysis (PCA & t-SNE)
├── samples/           # Generated MIDI samples (Q1 through Q4)
├── src/               # Source code (dataset, models, train, generate)
├── rapport_deep.pdf   # Complete project report
├── requirements.txt   # Python dependencies
└── README.md

```

### 🚀 Quickstart

```bash
# 1. Clone & Install
git clone https://github.com/votre-username/cvae-emopia-music.git
cd cvae-emopia-music
pip install -r requirements.txt

# 2. Train CVAE-LSTM
python src/train.py --model cvae_lstm --latent_dim 64 --epochs 100

# 3. Generate a track conditioned on emotion (e.g., Q3 - Sadness)
python src/generate.py --emotion Q3 --temperature 0.6 --output samples/sadness.mid

```
