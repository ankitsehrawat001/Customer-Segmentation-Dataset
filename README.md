# Retail Intelligence Dashboard

A Streamlit dashboard for exploring the **Online Retail** transaction dataset. It summarizes sales by market and month, assigns invoice-level RFM clusters, and lets you search and export filtered transaction rows.

## Features

- Interactive filters for market, date range, and RFM cluster
- Sales value, average invoice value, invoice count, and market KPIs
- Market revenue and monthly revenue charts
- Invoice cluster share, frequency/value analysis, and cluster profiles
- Searchable transaction explorer with pagination and CSV export
- Uses the saved clustering model and transformer when compatible; otherwise fits a fallback KMeans model

## Data and analysis

The project includes `Online Retail.xlsx.zip`, which contains the real `Online Retail.xlsx` workbook. The app searches the project folder and its `data/` subfolder for local Excel, ZIP, or CSV data. Keep the provided ZIP in the project folder to use the included dataset.

The workbook contains transaction fields such as `InvoiceNo`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `UnitPrice`, `CustomerID`, and `Country`. The dashboard removes rows with missing required values and excludes returns, zero quantities, and non-positive prices or sales.

**Segments are calculated per invoice, not per customer.** The RFM inputs are recency in days, number of transaction lines on the invoice, and total invoice value. `CustomerID` is present in the source workbook but is not used to aggregate the dashboard's clusters.

## Requirements

- Python 3.10 or newer
- The packages listed in `requirements.txt`

## Setup and run (Windows PowerShell)

From the project folder:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
streamlit run app.py
```

If PowerShell blocks environment activation, run the app directly without activating the environment:

```powershell
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\streamlit.exe run app.py
```

Open the local URL printed by Streamlit, usually `http://localhost:8501`.

## Project files

- `app.py` — dashboard, data preparation, and segmentation pipeline
- `Online Retail.xlsx.zip` — included real transaction data
- `kmeans_clustering_model.pkl` — saved KMeans model
- `powertransformer_model.pkl` — saved feature transformer
- `requirements.txt` — Python dependencies
- `Customer_Segmentation_Dataset_git2.ipynb` — analysis notebook

## Notes

The saved model files were serialized with scikit-learn. If the installed scikit-learn version differs from the version used to create them, a compatibility warning may appear; the app attempts to use the saved artifacts and falls back to a fresh clustering fit if loading or prediction fails.
