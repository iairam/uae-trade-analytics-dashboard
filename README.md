# UAE Trade Diversification: Machine Learning Framework & Streamlit Web App

## 📺 Live Dashboard Demo Video
👉 **https://drive.google.com/file/d/1nzFeu8Wn08Gy2K4b-xrVBs-OawhKx8Qz/view?usp=sharing**

*(Click the link above to watch a quick video of the interface running live, showing how the sidebar filters, scenario sliders, and data tables respond in real time).*

---

## 📊 Project Overview
I analyzed 12 years of public trade data from the World Bank (2012-2023) covering 97 different industrial product categories (HS-2 chapters). The goal of this project was to separate normal re-export shipping hub activity from true domestic import reliance, map out growth patterns using K-Means clustering, and use Gradient Boosting to find hidden export opportunities. I then built a clean Streamlit app to host the interactive dashboard online.

---

## 🛠️ The Tech Stack
- **Languages & Frameworks:** Python, Streamlit (for the web app dashboard page)
- **Libraries:** Pandas, NumPy, Scikit-Learn, Statsmodels, Plotly
- **Models Used:** K-Means Clustering, Gradient Boosting Regressor, Random Forest, XGBoost

---

## 📁 Repository Structure
- `/scripts/FPimbalance analysis.ipynb` -> SQL-style data pivoting, deficit tracking, and hub analysis
- `/scripts/FPclustering.ipynb` -> K-Means model training, data scaling, and Silhouette optimization
- `/scripts/FPpredictive.ipynb` -> Testing and evaluating time-series forecasting models
- `/scripts/Hybrid_Model.ipynb` -> Fine-tuning model parameters and validating code scripts
- `/scripts/app.py` -> The Python script that runs the interactive Streamlit dashboard web page
- `/visuals/` -> Folder containing the master walkthrough video file

---

## 🧼 Cleaning the Data & Engineering Features
The dataset consists of 3,492 systematically structured panel records from the World Bank (WITS database). I used Python to process and transform the data:
- **Pivoting & Aggregating:** Grouped over 100,000 raw bilateral lines to aggregate rows cleanly by year and product type, splitting records into unique columns for Imports, Exports, and Re-exports.
- **New Calculations:** Created three core business metrics: *Total Exports* (Exports + Re-Exports), *Net Trade Balance*, and *Re-Export Intensity %*.
- **Outlier Removal:** Filtered out Mineral Fuels (HS-27) during predictive modeling because its multi-billion dollar scale skewed the non-oil growth analysis.

---

## 💡 Key Business & Economic Insights

### Deficit and Re-Export Analysis
- **Embedded Deficits:** 84.4% of all product categories show long-term trade deficits, proving these imbalances are a permanent part of the trade landscape rather than temporary drops.
- **Shipping Hub Hubs:** 48% of categories act as pass-through transit nodes. Large areas like Machinery (HS-84) and Electrical Equipment (HS-85) show multi-billion dollar deficits but have massive re-export ratios (>85%). This indicates high-velocity trading hub velocity, not domestic failure.
- **Absolute Dependence:** Iron & Steel (HS-72) and processed food imports (HS-19/20) show heavy deficits with almost zero re-export activity (≤30%), flagging real areas of local domestic reliance.

### Machine Learning Clustering Results
Using K-Means clustering ($k=3$, optimized with a Silhouette Score of 0.497), the models cleanly separated the product space into three distinct sectors to help guide trade investments:
- **Developing Sectors (28 Chapters):** High-velocity growth paths (Mean Growth = 33.74%) but high volatility (99.34). These are prime targets for export growth grants.
- **Stable Sectors (61 Chapters):** The steady baseline of UAE trade. Shows low, predictable volatility (44.95%) and reliable performance—perfect for stable trade credit insurance.
- **Declining Sectors (7 Chapters):** Downside trajectories with shrinking trend lines (Trend Slope = -13.43). High commercial risk zones.

### Export Forecasting Predictions
I tested multiple models on a chronological timeline split (Training on 2012-2017, Testing on 2020-2022). The **Gradient Boosting Regressor** yielded the best test accuracy ($R^2 = 0.678$), outperforming Random Forest and XGBoost. The model successfully isolated two major high-potential niche growth categories:
- **HS-60 (Knitted Fabrics):** Projected Export Growth of +101.1%
- **HS-41 (Raw Hides & Skins):** Projected Export Acceleration of +96.9%

---

## 🌐 How the Dashboard Works
The Streamlit web application dashboard provides an intuitive, interactive interface:
- **Control Sidebar:** Allows users to pick specific timelines and filter indicators instantly by individual HS-2 commodity codes.
- **Real-Time KPI Cards:** Displays running totals for Imports, Exports, and Net Balances instantly based on user selections.
- **Future Scenario Sliders:** Features an on-the-fly percentage slider so policy teams can change target parameters and simulate 2027 export projections on the fly.
- **Integrated Data Grid:** Embeds a clean, scrollable data frame at the bottom so operators can drill into raw sorted data records without leaving the page.
