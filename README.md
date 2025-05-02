 DA401

**Vibe-Based Music Recommendation System**

This repository implements a three-stage pipeline to build a hybrid music recommendation system that captures both audio and lyrical characteristics to suggest songs with a similar “vibe”—mood, energy, and style—while promoting discovery of underrepresented artists alongside popular hits.

---

## 🚀 Quick Start

1. **Clone the repo**
   ```bash
   git clone https://github.com/Banguyen13/DA401.git
   cd DA401
2. **Create a virtual environment & install dependencies**

  ```bash
  python3 -m venv env
  source env/bin/activate
  pip install -r requirements.txt
  ```
3. **Data Preparation**

- Run notebooks/GeneratedPlaylists.ipynb to sample songs from the Million Song Dataset and generate labeled subsets (genre, era, mood).

- Download audio files into data/audio/ (filenames like <song_title> - <artist>.mp3). You can use yt_dlp or the provided helper script.

4. **Extract Audio Embeddings**

- Open notebooks/embeddings_extraction.ipynb

- Set input/output paths at the top

- Run all cells to compute features (MFCCs, chroma, spectral contrast, tempo, etc.) and save to output/embeddings.parquet

5. **Cluster & Visualize**

- Open notebooks/Songs_clustering.ipynb

- Adjust clustering parameters (e.g., n_clusters, algorithm choice)

- Run all cells to generate cluster labels and PCA/t-SNE plots in output/figures/

📂 **Repository Structure**
```bash
DA401/
├── data/
│   ├── audio/                     # Raw audio files (.mp3, .wav)
│   ├── sampled_df.csv             # Initial playlist sample from MSD
│   ├── hiphop_country.csv         # Genre-labeled subset
│   ├── hiphop_country.parquet
│   ├── old_new.csv                # Era-labeled subset
│   ├── old_new.parquet
│   ├── sad_bright.csv             # Mood-labeled subset
│   └── sad_bright.parquet
├── notebooks/
│   ├── GeneratedPlaylists.ipynb   # Sampling & playlist generation
│   ├── embeddings_extraction.ipynb# Audio feature extraction
│   └── Songs_clustering.ipynb     # Clustering & visualization
├── output/
│   ├── processed_sample.parquet   # Combined sample metadata
│   ├── embeddings.parquet         # Extracted audio embeddings
│   ├── cluster_labels.csv         # Song↔cluster mapping
│   └── figures/                   # PCA & silhouette plots
├── requirements.txt               # Python dependencies
└── README.md                      # Project overview & instructions
```
🔍 **Pipeline Overview**
1. **Sampling (GeneratedPlaylists.ipynb)**

- Draw a representative sample from the Million Song Dataset (MSD).

- Split and label by genre, era (old vs. new), and mood (sad vs. bright).

- Export sample metadata to CSV/Parquet.

2. **Embedding Extraction (embeddings_extraction.ipynb)**

- Load sampled metadata.

- Extract audio features using librosa: MFCCs, chroma, spectral contrast, tempo, zero-crossing rate, etc.

- Flatten and save embeddings in Parquet format for fast I/O.

3. **Clustering & Visualization (Songs_clustering.ipynb)**

- Load audio embeddings (and merge optional lyrical embeddings).

- Experiment with clustering algorithms (K-Means, Agglomerative, DBSCAN).

- Evaluate clusters with silhouette scores and elbow methods.

- Reduce dimensionality (PCA or t-SNE) for 2D visualization.

- Save cluster assignments and publish plots under output/figures/.

⚙️ **Customization**
Feature Parameters: In embeddings_extraction.ipynb, tweak hyperparameters (e.g., n_mfcc, hop_length, FFT window) to capture different aspects of the audio.

Clustering Strategy: In Songs_clustering.ipynb, adjust n_clusters, distance metrics, or ensemble multiple algorithms for robust groupings.

Lyrical Embeddings: Integrate HuggingFace transformers or OpenAI API calls in the clustering notebook to fuse semantic lyric features.

🛠 **Dependencies**
Python ≥ 3.8

numpy, pandas, scikit-learn, librosa, matplotlib, pyarrow

yt_dlp or youtube_dl (optional for audio downloads)

openai, transformers (optional for lyrical embeddings)

🤝 **Contributing**
Contributions are welcome! Please:

Open an Issue to report bugs or propose enhancements.

Submit a Pull Request to add features or improve documentation.

Suggest new audio features or clustering methods.

