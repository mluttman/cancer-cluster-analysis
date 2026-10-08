# County-Level Cancer Incidence & Lifestyle/Risk-Factor Clustering

An exploratory, educational data science project clustering U.S. counties by publicly available lifestyle and healthcare-access indicators, and comparing those clusters against county-level cancer incidence rates.

**This is a portfolio/learning project, not epidemiological research.** It's intended to demonstrate applied data science skills (data acquisition, cleaning, unsupervised learning, visualization) using real public health data — not to establish what causes cancer. See [Limitations & Ethics](#limitations--ethics) before drawing any conclusions from the results.

## Why this project

Built as part of a transition from IBM's AI Engineering and Machine Learning Professional Certificates into applied, domain-relevant portfolio work — specifically aimed at cancer research / prevention contexts (e.g. volunteer or early-career work with organizations like Moffitt Cancer Center).

## Data Sources

| Source | What it provides | Access |
|---|---|---|
| [NCI State Cancer Profiles](https://statecancerprofiles.cancer.gov/incidencerates/) | Age-adjusted cancer incidence rates by county | Public, no login |
| [CDC PLACES](https://www.cdc.gov/places/) | County-level modeled estimates: obesity, physical inactivity, smoking, binge drinking, diabetes, high blood pressure, general health, healthcare access | Public Socrata API, no key required |

Both are pulled live in the notebook — no data files are committed to this repo (keeps it small and always current). If either source changes its URL/dataset ID, the notebook includes a manual-download fallback.

## Method

1. Pull both datasets by county FIPS code
2. Clean, join, and drop counties with suppressed/missing values
3. Standardize lifestyle/risk-factor features
4. K-Means clustering (k chosen via elbow method + silhouette score)
5. Profile each cluster and compare cancer incidence rates across clusters
6. PCA for 2D visualization of cluster separation

## Repo structure

```
cancer-cluster-analysis/
├── README.md
├── requirements.txt
└── notebooks/
    └── county_cancer_cluster_analysis.ipynb
```

## Running it

**Recommended: Google Colab** (no local setup needed)
1. Go to [colab.research.google.com](https://colab.research.google.com)
2. File → Upload notebook → select `notebooks/county_cancer_cluster_analysis.ipynb`
3. Run all cells top to bottom (Runtime → Run all)

**Or locally:**
```bash
git clone <your-repo-url>
cd cancer-cluster-analysis
pip install -r requirements.txt
jupyter lab notebooks/county_cancer_cluster_analysis.ipynb
```

## Limitations & Ethics

- **Ecological analysis, not individual-level.** County-level correlations don't tell you anything about individual people — this is the well-known "ecological fallacy." No individual causal claims can be made from this data.
- **Correlation ≠ causation.** Observed patterns may reflect confounders not controlled for here: age distribution, screening/diagnosis rates, income, insurance coverage, occupational exposure, and environmental factors.
- **PLACES indicators are modeled small-area estimates** derived from survey data (BRFSS), not direct county censuses — they carry their own estimation uncertainty.
- **Low-population counties with suppressed cancer data are dropped**, which likely biases the remaining sample toward larger, more urban counties.
- **Not peer-reviewed, not clinical guidance.** This should not be cited as evidence about the causes of cancer in any real population.

## Possible extensions

- Multi-year PLACES data to look at trends, not a single snapshot
- Add EPA environmental quality data by county
- Add TCGA tumor-level genomic data for a complementary individual-level analysis
- Try hierarchical clustering / Gaussian mixture models and compare to K-Means
- Control for age distribution and screening rates to reduce confounding

## License

MIT (or your preference — update before publishing)
