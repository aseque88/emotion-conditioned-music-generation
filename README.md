
# 🎵 Emotion-Conditioned Piano Music Generation (CVAE-LSTM)

> **Université Paris-Dauphine — Deep Learning (Mai 2026)**
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

Ce projet explore la génération automatique de musique pour piano conditionnée par une intention émotionnelle. En combinant le dataset [**EMOPIA**](https://zenodo.org/records/5090631#.YPPo-JMzZz8) et le **modèle circomplexe de Russell (1980)**, nous classons les pièces selon la **Valence** (positivité) et l'**Activation / Arousal** (énergie) :

* **Q1 (Haute Valence / Haute Activation) :** Joie, excitation


* **Q2 (Basse Valence / Haute Activation) :** Tension, colère


* **Q3 (Basse Valence / Basse Activation) :** Tristesse, mélancolie


* **Q4 (Haute Valence / Basse Activation) :** Calme, sérénité



Notre architecture retenue est un **Auto-Encodeur Variationnel Conditionnel couplé à un LSTM (CVAE-LSTM)**.

### 📊 Benchmark des Modèles

Représentation des données : Tokenisation **REMI** via `MidiTok` (vocabulaire de 268 tokens, $SEQ\_LEN = 512$).

| Étape | Modèle           | Dim Latente ($d$) | Loss Val (ELBO) | Résultat & Observations                                         |
| ----: | ---------------- | ----------------: | --------------: | --------------------------------------------------------------- |
| **1** | **VAE (MLP)**    |                64 |          2450 | Overfitting massif, perte du contexte temporel.                 |
| **2** | **VAE (CNN 1D)** |                64 |          2200 | Motifs locaux appris, amnésie temporelle.                       |
| **3** | **VAE (LSTM)**   |                64 |          1284.4 | Excellente cohérence, génération émotionnelle aléatoire.        |
| **4** | **C-VAE (LSTM)** |            **64** |      **1283.6** | **Qualité musicale optimale + Séparation nette en 4 clusters.** |


### 🛠️ Structure du Dépôt

* `docs/` : Rapports de projet (FR / EN) et diapos de présentation.


* `models/checkpoints/` : Poids `.pt` sauvegardés pour chaque modèle.


* `notebooks/` : Pipeline complet de génération de musique pour piano conditionnée par des émotions à l'aide de la tokenisation MIDI et de différents modèles (VAE MLP, VAE CNN, VAE LSTM, CVAE) + Analyses statistiques et visualisations (PCA, t-SNE).


* `samples/` : Fichiers MIDI générés (MLP, CNN, VAE-LSTM, CVAE-LSTM par quadrant).





---

## English Version

### 📌 Project Overview

This repository presents an end-to-end framework for emotion-conditioned piano music generation. Utilizing the [**EMOPIA**](https://zenodo.org/records/5090631#.YPPo-JMzZz8) dataset and **Russell's circumplex model (1980)**, our goal is to generate music guided by four distinct emotion quadrants based on **Valence** and **Arousal**:

* **Q1 (High Valence / High Arousal):** Joy, excitement


* **Q2 (Low Valence / High Arousal):** Tension, anger


* **Q3 (Low Valence / Low Arousal):** Sadness, melancholy


* **Q4 (High Valence / Low Arousal):** Calmness, serenity



Our primary model architecture is a **Conditional Variational Autoencoder paired with LSTMs (CVAE-LSTM)**.

### 📊 Model Benchmark

Data Representation: **REMI** tokenization via `MidiTok` (vocabulary size of 268 tokens, fixed $SEQ\_LEN = 512$).

|  Step | Model            | Latent Dim ($d$) | Val Loss (ELBO) | Performance Summary                                              |
| ----: | ---------------- | ---------------: | --------------: | ---------------------------------------------------------------- |
| **1** | **VAE (MLP)**    |               64 |          2450 | Severe overfitting, loss of temporal order.                      |
| **2** | **VAE (1D-CNN)** |               64 |          2200 | Learns local patterns, suffers from short-term memory.           |
| **3** | **VAE (LSTM)**   |               64 |          1284.4 | High musical coherence, unguided emotion generation.             |
| **4** | **C-VAE (LSTM)** |           **64** |      **1283.6** | **Best musical grammar + Clear 4-cluster emotional separation.** |


### 🛠️ Repository Structure

* `docs/`: Project reports (FR / EN) and slides.


* `models/checkpoints/`: Saved `.pt` weights for each evaluated model.


* `notebooks/`: Complete pipeline for emotion-conditioned piano music generation using MIDI tokenization and various models (MLP VAE, CNN VAE, LSTM VAE, CVAE), including statistical analysis and visualizations (PCA, t-SNE).


* `samples/`: Generated MIDI audio files for each model.




