# UAE Trade Diversification: Machine Learning Framework & Dual-Tab Streamlit Web App

## 📺 Live Web App Walkthrough Video
👉 **https://drive.google.com/file/d/1nzFeu8Wn08Gy2K4b-xrVBs-OawhKx8Qz/view?usp=sharing**

*(Click the link above to view a screen recording of the live web interface, showing both the Export Growth Predictor tab and the HS Chapter Analysis dashboard running in real time).*

---

## 📊 Project Overview
I analyzed 12 years of public trade data from the World Bank (2012-2023) across 97 industrial categories (HS-2 chapters) to support UAE non-oil economic diversification. Using Python, I engineered a multi-stage data pipeline that identifies structural trade deficits, groups industries using K-Means clustering, and trains a Gradient Boosting Regressor to forecast future export growth. I then combined all these insights into a custom-styled, two-tab Streamlit web application.

---

## 🛠️ The Tech Stack
- **Web App & UI Styling:** Streamlit, Custom HTML/CSS, Base64 Background Rendering, Pyngrok
- **Data Engineering & Models:** Python (Pandas, NumPy, Scikit-Learn, Joblib)
- **Algorithms Used:** K-Means Clustering, Gradient Boosting Regressor, Random Forest, XGBoost

---

## 📁 Repository Structure
- `/scripts/FPimbalance analysis.ipynb` -> Pivoting raw trade flows, computing deficit years, and classifying transit hubs.
- `/scripts/FPclustering.ipynb` -> Calculating growth/volatility features, running K-Means ($k=3$), and exporting `clustering_results.csv`.
- `/scripts/FPPredictive.ipynb` -> Time-series lag engineering, model comparisons, and exporting `uae_gb_non_oil_exports_model.joblib`.
- `/scripts/Hybrid_Model.ipynb` -> Master deployment script assembling the dual-tab Streamlit interface (`app.py`).
- `/visuals/` -> Folder containing the demo video recording of the live interface.

---

## 🧼 How the Data Was Processed
- **Pivoting Trade Flows:** Aggregated raw World Bank records by year and product code, separating Imports, Exports, and Re-exports into distinct columns to calculate Total Exports, Net Trade Balance, and Re-export Intensity %.
- **Outlier Filtering:** Excluded Mineral Fuels (HS-27) during predictive training because its massive multi-billion dollar scale distorted the non-oil growth patterns.
- **Time-Series & Volatility Features:** Engineered 6 clustering indicators (including CAGR, Growth Consistency, and Trend Slope) alongside lagged variables and rolling averages for forecasting.

---

## 💡 Key Analytical Findings
- **Embedded Deficits:** 84.4% of product chapters show persistent trade deficits over the 12-year timeline, proving these imbalances are structural rather than temporary dips.
- **Shipping Hubs vs. Local Reliance:** 48% of chapters act as pass-through transit nodes. Machinery (HS-84, 91.1% re-export ratio) and Electrical Equipment (HS-85, 92.6% re-export ratio) show huge deficits alongside massive re-export activity. Conversely, Iron & Steel (HS-72, 20.2% re-export ratio) and processed foods (HS-19/20) represent true local import dependency.
- **Sector Clusters:** K-Means clustering ($k=3$, Silhouette Score = 0.497) grouped the product landscape into **Stable Sectors (61 chapters)** with low volatility, **Developing Sectors (28 chapters)** with high growth momentum, and **Declining Sectors (7 chapters)** facing negative trend slopes.
- **Export Forecasting:** Tested multiple models on a chronological split (2012–2017 train, 2020–2022 test). The **Gradient Boosting Regressor** yielded the strongest ML test performance ($R^2 = 0.678$), outperforming Random Forest ($0.566$) and XGBoost ($0.470$). It projected top 2023 growth opportunities in **Knitted Fabrics (HS-60, +101.1%)** and **Raw Hides & Skins (HS-41, +96.9%)**.

---

## 🌐 Inside the Dual-Tab Web Application (`Hybrid_Model.ipynb`)
To make the analysis usable for policy teams, I deployed a unified, custom-styled web interface divided into two interactive tabs:

### Tab 1: UAE Non-Oil Export Growth Predictor
- **Dynamic History Inputs:** Users enter an HS-2 chapter code and input between 3 to 12 years of historical export values (in kUSD).
- **Live Model Inference:** On click, the app dynamically computes lagged features, feeds them into the loaded Gradient Boosting model, and displays side-by-side KPI metrics for current vs. predicted exports.
- **Automated Categorization & Export:** Classifies the prediction into visual growth tiers (e.g., *HIGH GROWTH 🚀*, *MODERATE GROWTH 📈*) and includes a one-click **Download Prediction as CSV** button.

### Tab 2: UAE Trade Dynamics — HS Chapter Analysis
- **Sidebar Search & Filtering:** Allows users to search by product description keywords or select any HS chapter code from a dropdown menu.
- **Visual Status Badges:** Uses custom HTML/CSS cards to display color-coded status tags for **Deficit Severity**, **Dependency Type**, **Category**, and **Cluster Label**.
- **KPIs & Re-Export Progress Bar:** Displays total deficit years, mean net trade in USD, average re-export ratio, and a visual intensity progress bar, paired with automated bulleted interpretations and a CSV download option.
