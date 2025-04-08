# DA401
# 🎵 Vibe-Based Music Recommendation System

This repository contains the code, data processing pipelines, and model training scripts for a music recommendation system that suggests tracks based on intrinsic musical characteristics and lyrical themes. The system is designed to identify and recommend songs with a similar *vibe*—capturing mood, energy, and style—while promoting discovery of underrepresented artists alongside popular hits.

---

## 🚀 Project Goals

- Build a hybrid music recommendation system that combines:
  - **Audio embeddings**: derived from musical properties (e.g., tempo, harmony, timbre).
  - **Lyrical embeddings**: extracted using Large Language Models (LLMs).
- Train clustering models to group songs with similar sonic and lyrical characteristics.
- Balance recommendations between popular tracks and lesser-known songs to encourage exploration.

---

## 🧠 Methodology Overview

### 1. **Dataset**

- **Million Song Dataset (MSD)**: Base dataset containing metadata and precomputed features.
- Audio not provided: Using **YouTube** to download full audio tracks.
- Sample size: Starting with 100–200 tracks for development, scaling up to ~100,000 songs.

### 2. **Audio Processing**

- Extract most replayed segment of each song using YouTube replay data.
- Use **Librosa** for preprocessing:
  - Mel spectrograms
  - Chroma features
  - MFCCs
  - Tempo & rhythm profiles
- Preprocessed features are stored as serialized vectors to save time.

### 3. **Lyrical Embeddings**

- Lyrics are extracted via online APIs or scraped, where available.
- Processed using LLMs (e.g., GPT or HuggingFace transformers) to create semantic embeddings that capture emotional tone, narrative structure, and thematic content.

### 4. **Modeling**

- Ensemble clustering: Combine different clustering models (e.g., K-means, DBSCAN, Agglomerative) using weighted voting.
- Dimensionality reduction via PCA or t-SNE for visualization and performance optimization.

### 5. **Recommendation Strategy**

- Input: a user’s favorite song or playlist
- Output: songs from the same cluster with similar audio/lyrical embeddings
- Optional: inject low-streamed or lesser-known tracks to increase discovery

---

## 🧰 Tools & Technologies

- Python, NumPy, Pandas, Scikit-learn
- Librosa, pydub for audio processing
- HuggingFace Transformers, OpenAI for LLM-based lyric embedding
- YouTube API / yt-dlp for audio scraping
- Supercomputer / HPC cluster for large-scale processing
- (Optional) Streamlit for building a simple frontend

---

## 📁 Repository Structure
