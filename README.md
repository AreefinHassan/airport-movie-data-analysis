# Airport, Movie & Birth-Data Analysis in Python

Exploratory data analysis in Python (pandas, NumPy, Matplotlib, Seaborn, SciPy) that fits
candidate probability distributions to three real datasets and compares them against the
observed data. The question in each case: which distribution actually describes the data?

## Datasets

| Dataset | File | Rows | What it measures |
|---|---|---|---|
| Airport routes | `data/airport_routes.csv` | 3,409 airports | Number of routes per airport (`Airport`, `NumberOfRoutes`) |
| Movie ratings | `movie_votes.csv` *(not in repo yet)* | — | Average vote per movie (`AverageVote`) |
| Birth dates | `DoB.txt` *(not in repo yet)* | — | Dates of birth, used to derive ages 1–99 |

> `movie_votes.csv` and `DoB.txt` are not included yet — the notebooks reference them from
> their original locations. They will be added to `data/` when available.

## Findings

### Airport routes — a power law

Most airports serve only a handful of routes while a few hubs serve hundreds, so the
distribution is heavily right-skewed. Fitted parameters:

| Distribution | Parameter |
|---|---|
| Power law | α = 1.612 |
| Exponential | λ = 0.0504 |
| Uniform | [a, b] = [1, 915] |
| Normal | μ = 19.85, σ = 53.51 |

**Conclusion: the route counts follow a power-law distribution** — the classic hub-and-spoke
pattern, where a small number of airports carry most of the traffic.

### Movie ratings — a normal distribution

Average votes cluster around the middle of the scale with symmetric spread. Fitted parameters:

| Distribution | Parameter |
|---|---|
| Power law | α = 1.851 |
| Exponential | λ = 0.1606 |
| Uniform | [a, b] = [1.9, 8.5] |
| Normal | μ = 6.227, σ = 0.893 |

**Conclusion: the ratings follow a normal distribution** — most movies sit near the mean
rating of ~6.2, with fewer at the extremes.

### Birth dates — ages, first digits, last digits

Dates of birth are converted to ages (kept in the 1–99 range), then the first and last
digits of each age are examined separately:

| Series | Distribution |
|---|---|
| Ages | Normal |
| First digit of age | Normal |
| Last digit of age | Uniform |

The last digit is spread evenly across 0–9, while the ages themselves and their first
digits bunch around the middle — as expected when ages are roughly bell-shaped.

## Notebooks

| Notebook | Contents |
|---|---|
| `notebooks/HW_2_Airport_Data.ipynb` | Airport routes: summary statistics, power-law / exponential / uniform / normal fits, and a visual comparison of the observed data against the fitted power law |
| `notebooks/HW_2_Movie_Data.ipynb` | Movie votes: summary statistics, the same four distribution fits, and a comparison of the observed ratings against the fitted normal |
| `notebooks/HW_2_Problem_2.ipynb` | Birth dates: age calculation, 1–99 filtering, first/last digit extraction, and histograms of the age, first-digit, and last-digit distributions |
| `notebooks/i2ds_hw_2_movie.ipynb` | Earlier version of the movie-rating analysis |
| `notebooks/i2ds_hw_2_DoB.ipynb` | Earlier version of the birth-date analysis |

The notebooks were developed in Google Colab (`pandas`, `numpy`, `matplotlib`, `seaborn`,
`scipy`). The polished `HW_2_*` versions are the main ones; the `i2ds_hw_2_*` versions are
earlier drafts kept for reference.

## Project layout

```
├── README.md
├── data/
│   └── airport_routes.csv      # routes per airport (3,409 rows)
├── notebooks/
│   ├── HW_2_Airport_Data.ipynb
│   ├── HW_2_Movie_Data.ipynb
│   ├── HW_2_Problem_2.ipynb
│   ├── i2ds_hw_2_DoB.ipynb
│   └── i2ds_hw_2_movie.ipynb
└── report/
    └── Data_Analysis_Report.pdf
```

## How to run

```bash
pip install pandas numpy matplotlib seaborn scipy
jupyter notebook notebooks/HW_2_Airport_Data.ipynb
```

The airport notebook runs as-is with the bundled `data/airport_routes.csv`. The movie and
birth-date notebooks expect `movie_votes.csv` and `DoB.txt` — update the file paths at the
top of each notebook to point at your local copies.
