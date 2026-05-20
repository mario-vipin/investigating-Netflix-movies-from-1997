# 🎬 Netflix 1990s Movie Analysis

> Exploratory data analysis of Netflix's catalog focused on movies from the 1990s — built to help a nostalgic-style production company understand the decade's cinematic trends.

---

## 📌 Project Overview

This project dives into Netflix's movie catalog to uncover patterns in 1990s films. Using Python, we filter, clean, and analyse the data to answer two key business questions:

1. **What was the most frequent movie duration in the 1990s?**
2. **How many short Action movies (< 90 minutes) were released in the 1990s?**

---

## 📁 Dataset

**File:** `netflix_data.csv`

| Column | Description |
|---|---|
| `show_id` | Unique ID for the show |
| `type` | Type of content (Movie / TV Show) |
| `title` | Title of the show |
| `director` | Director of the show |
| `cast` | Cast of the show |
| `country` | Country of origin |
| `date_added` | Date added to Netflix |
| `release_year` | Year of release |
| `duration` | Duration in minutes |
| `description` | Description of the show |
| `genre` | Show genre |

---

## 🛠️ Tech Stack

- **Python 3**
- **pandas** — data loading, filtering, and analysis
- **matplotlib** — visualisation (duration distribution histogram)

---

## 🚀 Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/your-username/netflix-1990s-eda.git
cd netflix-1990s-eda
```

### 2. Install dependencies
```bash
pip install pandas matplotlib
```

### 3. Add the dataset
Place `netflix_data.csv` in the root project directory.

### 4. Run the analysis
```bash
python netflix_1990s_eda.py
```

---

## 🔍 Methodology

### Step 1 — Filter for 1990s Movies
```python
movies_90s = netflix_df[
    (netflix_df["type"] == "Movie") &
    (netflix_df["release_year"] >= 1990) &
    (netflix_df["release_year"] < 2000)
]
```

### Step 2 — Most Frequent Duration
The `duration` column is stored as a string (e.g. `"94 min"`). We extract the numeric value using regex, then use `.mode()` to find the most common duration.

```python
movies_90s["duration_int"] = movies_90s["duration"].str.extract(r"(\d+)").astype(int)
duration = int(movies_90s["duration_int"].mode()[0])
```

### Step 3 — Short Action Movie Count
Filter for Action films under 90 minutes and count them.

```python
short_movie_count = len(movies_90s[
    (movies_90s["genre"] == "Action") &
    (movies_90s["duration_int"] < 90)
])
```

---

## 📊 Outputs

| Variable | Description |
|---|---|
| `duration` | Most frequent movie duration in the 1990s (integer, minutes) |
| `short_movie_count` | Number of short Action movies (< 90 min) from the 1990s |

A histogram of 1990s movie duration distribution is also saved as `duration_distribution.png`.

---

## 📂 Project Structure

```
netflix-1990s-eda/
│
├── netflix_data.csv              # Source dataset (not included in repo)
├── netflix_1990s_eda.py          # Main analysis script
├── duration_distribution.png     # Output chart (generated on run)
└── README.md                     # Project documentation
```

---

## 💡 Potential Extensions

- Analyse genre trends across the full decade year-by-year
- Compare 1990s movie durations to other decades
- Identify the most prolific directors of the 1990s on Netflix
- Visualise country-of-origin breakdowns for 1990s content

---

## 📄 License

This project is for educational and analytical purposes. Dataset sourced from Netflix public data.
