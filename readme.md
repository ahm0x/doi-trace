<img src="https://upload.wikimedia.org/wikipedia/commons/e/e5/NASA_logo.svg" alt="NASA Logo" width="120">
<h1 align="center">🌍 DOI Trace
</h1><b>Creating and updating a collection of EOSDIS dataset citing publication citations</b>
Part of NASA's Earth Science Data and Information System (EOSDIS)

<br>
<a href="https://github.com/nasa/doi-trace/actions"><img src="https://img.shields.io/github/actions/workflow/status/nasa/doi-trace/ci.yml?label=CI&amp;logo=github"></a> <a href="https://pypi.org/project/doi-trace/"><img src="https://img.shields.io/pypi/v/doi-trace?color=blue&amp;logo=pypi"></a> <a href="https://www.python.org/"><img src="https://img.shields.io/badge/Python-3.9+-blue.svg?logo=python"></a> <a href="LICENSE"><img src="https://img.shields.io/github/license/nasa/doi-trace"></a>

- - -

## 📖 Overview

**DOI Trace** is a command-line tool that automates the discovery and aggregation of **citations for EOSDIS datasets** across multiple scholarly data sources, including:

* 🌐 Web of Science
* 🔬 Scopus
* 🔎 Crossref
* 📘 DataCite
* 🎓 Google Scholar

It enables NASA and the scientific community to **track the usage and impact of Earth science datasets** efficiently.

- - -

## ⚙️ Installation

1. **Clone the repository**

``` bash
git clone https://github.com/nasa/doi-trace.git
cd doi-trace
```

2. **Install the package**

``` bash
python -m pip install .
```

3. **Set up configuration**
    * Copy the example config file:

    ``` bash
    cp config.toml.example config.toml
    ```

    * Add your API keys and customize parameters as needed.

- - -

## 🚀 Usage

### 🔧 Pre-setup

Obtain the latest dataset DOIs from the [EOSDIS DOI Server](https://doiserver.eosdis.nasa.gov/ords/f?p=100:8:::NO:::)
Place the downloaded CSV file into the `eosdis_csv_files/` directory.

Keep **the two most recent `.csv` files** for accurate comparison.

- - -

### 🌐 Web of Science Citations

1. Execute a *Cited Reference Search* for prefixes `10.5067`, `10.7927`, and `10.3334` at [Web of Science](https://www.webofscience.com/wos/woscc/cited-reference-search).
2. Export results as **BibTeX** (`Full Record and Cited References`) into the `WoS/` directory.
3. Run the processor:

``` bash
python -m doi_trace wos --start-date YYYY-MM-DD --end-date YYYY-MM-DD
```

- - -

### 🔬 Scopus Citations

1. Create an API key from [Elsevier Developer Portal](https://dev.elsevier.com/).
2. Add it to your `config.toml` under `scopus_api_key`.
3. Run:

``` bash
python -m doi_trace scopus --start-date YYYY-MM-DD --end-date YYYY-MM-DD
```

- - -

### 🔎 Crossref Citations

``` bash
python -m doi_trace crossref --start-date YYYY-MM-DD --end-date YYYY-MM-DD
```

- - -

### 📘 DataCite Citations

``` bash
python -m doi_trace datacite --start-date YYYY-MM-DD --end-date YYYY-MM-DD
```

- - -

### 🎓 Google Scholar Citations

1. Get a SerpAPI key from [serpapi.com](https://serpapi.com/).
2. Add it under `serp_api_key` in `config.toml`.
3. Run:

``` bash
python -m doi_trace google-scholar --start-date YYYY-MM-DD --end-date YYYY-MM-DD
```

- - -

### 🔗 Combine Citations

Merge results from multiple sources:

``` bash
python -m doi_trace combine
# or specific sources
python -m doi_trace combine -s wos -s scopus -s google-scholar
```

**Combiner features:**

* Detects most recent citation files
* Removes duplicates
* Creates a unified citation dataset in `data/combined_citations_YYYYMMDD.json`

- - -

### 🧩 Run All Processors

To execute all processors sequentially:

``` bash
python -m doi_trace all --start-date YYYY-MM-DD --end-date YYYY-MM-DD
```

- - -

## 📦 Output

Generated output files contain:

* Citation metadata (title, authors, year, etc.)
* Dataset DOIs and their links
* Validation results
* Processing logs and metadata

Output examples:

```
data/wos_citations_20251026.json
data/scopus_citations_20251026.json
data/combined_citations_20251026.json
```

- - -

## 📚 Example Workflow

``` bash
# Update config and place CSVs
cp config.toml.example config.toml

# Process citations from all sources
python -m doi_trace all --start-date 2024-01-01 --end-date 2024-12-31

# Combine results
python -m doi_trace combine
```

- - -

## 🛰️ About EOSDIS

The **Earth Observing System Data and Information System (EOSDIS)** provides end-to-end capabilities for managing NASA’s Earth science data — from satellite collection to distribution for global researchers.

For more info, visit:
🔗 [https://earthdata.nasa.gov/eosdis](https://earthdata.nasa.gov/eosdis)
