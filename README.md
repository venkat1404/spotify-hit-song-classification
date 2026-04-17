# Spotify Hit Song Classification

Group project for BUDT704 — Group 8 (Brenda Ngaba, Venkat Gollangi, Anish Rao Tumla, Rohith Kumar Tappa).

We had a simple question: can you predict whether a song will be a hit just from its audio features? Spotify tracks things like how energetic a song is, how loud, how vocal-heavy. We wanted to know if those numbers actually tell you anything useful about chart success.

---

## Dataset

[30,000 Spotify Songs](https://www.kaggle.com/datasets/joebeachcapital/30000-spotify-songs) from Kaggle — tracks released between 1957 and 2020, each with audio features pulled from the Spotify API.

| Feature | What it measures |
|---|---|
| `valence` | How positive/happy the track sounds (0–1) |
| `energy` | Intensity — loud, fast, noisy = high energy |
| `danceability` | How well it works for dancing |
| `instrumentalness` | Likelihood the track has no vocals |
| `loudness` | Overall loudness in dB |
| `tempo` | BPM |
| `speechiness` | Amount of spoken word content |
| `acousticness` | Whether the track is acoustic |

---

## Mood Trends

Spotify uses `valence` and `energy` together to put songs into four mood buckets: Happy, Angry, Sad, and Relaxed. We tracked how hit songs broke down across those buckets over time.

A few things stood out. Happy-sounding music dominated in the 80s and early 2010s. Around 2020, sad music spiked sharply — the same period happy music dipped. Genre matters too: EDM leans angry, Latin leans happy, R&B and rap lean sad or relaxed.

---

## Models

**Logistic Regression** got ~84% accuracy. Sounds good until you realize the dataset is heavily imbalanced — most songs aren't hits. The model learned to just call everything a non-hit. It correctly identified 2 out of 933 actual hits.

**Random Forest (tuned with grid search)** was a lot better:

- Precision: **0.83** — when it calls something a hit, it's right 83% of the time
- Recall: **0.59** — catches 59% of actual hits in the test set
- Lift: **3.4x** in the top 10% of predictions vs. random selection

---

## What the Model Actually Cares About

The top predictors were `instrumentalness`, `loudness`, and `energy` — not `valence`, not `tempo`, not `danceability`.

The implication: how a song is produced matters more than how it makes you feel. Vocal-heavy tracks are far more likely to be hits than instrumental ones, and raw sonic punch (loudness + energy) outweighs emotional texture.

---

## Repo Structure

```
spotify-hit-song-classification/
├── data/
│   └── spotify_songs-1.csv
├── notebooks/
│   └── Spotify_Songs_Analysis.ipynb
└── README.md
```

## Setup

```bash
git clone https://github.com/yourusername/spotify-hit-song-classification
cd spotify-hit-song-classification
pip install pandas scikit-learn matplotlib
jupyter notebook notebooks/Spotify_Songs_Analysis.ipynb
```
