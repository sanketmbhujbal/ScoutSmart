# ScoutSmart: Advanced Football Talent Analytics ⚽📊

![Power BI](https://img.shields.io/badge/Power%20BI-Data%20Viz-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Python](https://img.shields.io/badge/Python-Data%20Eng-3776AB?style=for-the-badge&logo=python&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-Data%20Warehousing-4479A1?style=for-the-badge&logo=postgresql&logoColor=white)

> [**Live Dashboard**](https://app.powerbi.com/view?r=eyJrIjoiN2I3NTczNTItOTlhOC00YjQyLWI0OWEtM2EzMWVjZWVjOTgzIiwidCI6IjYwOTU2ODg0LTEwYWQtNDBmYS04NjNkLTRmMzJjMWUzYTM3YSIsImMiOjF9)  

## 📖 Project Overview
**ScoutSmart** is an end-to-end analytics pipeline designed to modernize football scouting. Unlike traditional analysis that relies on surface-level metrics (Goals & Assists), this tool leverages advanced underlying metrics—such as **Expected Goals (xG)**, **xGChain**, and **xGBuildup**—to identify undervalued talent across Europe's Top 5 Leagues.

This project simulates a real-world Business Intelligence workflow: **Ingesting** raw unstructured data, **Transforming** it into a relational schema, and **Visualizing** actionable insights for a non-technical end-user (e.g., a Club Scout or Director of Football).

---

## 💡 Motivation: Why This Topic?
As a data scientist and football enthusiast, I noticed that "counting stats" (Goals/Assists) are often noisy and result-oriented rather than process-oriented. A player can have a "lucky" season by overperforming their xG, or a creative midfielder might be undervalued because their teammates miss easy chances (high xA, low Assists).

**I chose this project to answer three specific questions:**
1.  **Sustainability:** Is a player's goal-scoring form sustainable, or are they statistically overperforming (Luck vs. Skill)?
2.  **Hidden Value:** Who are the most creative playmakers whose output is masked by poor finishing from their strikers?
3.  **Buildup Contribution:** Which wingers contribute most to possession phases (pre-assist actions) even if they don't take the final shot?

---

## 🛠️ Tech Stack & Workflow

The project follows a standard **ETL (Extract, Transform, Load)** pipeline:

| Stage | Tool | Description |
| :--- | :--- | :--- |
| **Data Collection** | **Python (BeautifulSoup)** | Built a custom scraper to harvest player performance data (2014-2024) from Understat/FBref. |
| **Data Cleaning** | **Pandas / NumPy** | Handled missing values, normalized player names, and standardized per-90 metrics. |
| **Storage** | **SQL** | Structured the data into a relational schema (fact tables for stats, dimension tables for players/teams). |
| **Visualization** | **Microsoft Power BI** | Developed the interactive dashboard, including DAX measures for dynamic benchmarking. |

---

## 📊 Data Dictionary
The dataset (`topwingers_teams.csv`) contains over 11,000 player-season records. Key features used in the analysis include:

| Metric | Definition | Why it matters for Scouting |
| :--- | :--- | :--- |
| **xG (Expected Goals)** | Probability of a shot resulting in a goal (0-1). | Measures the quality of chances a player gets, independent of finishing ability. |
| **xA (Expected Assists)** | The xG value of a shot resulting from a pass. | Measures creativity/passing quality, independent of the striker's finish. |
| **xGChain** | Total xG of every possession the player is involved in. | Identifies players involved in dangerous attacks, even if they didn't shoot or assist. |
| **xGBuildup** | xGChain minus shots and key passes. | Highlights "pre-assist" contributors—vital for scouting deep-lying playmakers. |
| **Key Passes** | Passes that lead directly to a shot. | A direct measure of chance creation volume. |

---

## 🚀 Dashboard Features
The Power BI dashboard is designed with a **"Widescreen F-Pattern"** layout for optimal user experience:

* **🔍 Fuzzy Player Search:** Instantly retrieve historical data for any player in the database (2,000+ entities).
* **🔦 Dynamic Spotlight:** Selecting a player highlights their data point across all scatter plots, while fading the rest of the league.
* **⚖️ Per 90 Normalization:** All comparison charts automatically adjust to "Per 90 Minutes" to fairly compare starters vs. impact substitutes.
* **📈 Efficiency Scatter Plots:**
    * *Finishing Efficiency:* **Goals vs. xG** (Top Left)
    * *Creative Output:* **Assists vs. xA** (Top Right)
    * *Playmaking Quality:* **Key Passes vs. xA** (Bottom Right)

---

## 🧪 Analytical Insights (The "Data Scientist" Perspective)
* **Regression to the Mean:** Scatter plots reveal that players who significantly overperform their xG (Goals > xG) in one season often regress in the following season. This is a critical signal for teams to *sell high*.
* **The "Playmaker's Curse":** By analyzing the delta between **Assists** and **xA**, we identified several wingers who created high-quality chances (high xA) but had low assist totals due to poor team finishing—marking them as prime "buy low" targets.
* **Metric Independence:** Correlation analysis shows that **xGChain** and **Goals** are not perfectly correlated, proving that valuable buildup players are often ignored by traditional scouting methods.

---

## 🔮 Future Improvements
* **Predictive Modeling:** Train a Machine Learning model (XGBoost) to predict future xG based on historical progression.
* **Similarity Search:** Implement a KNN (K-Nearest Neighbors) algorithm in Python to suggest "Similar Players" based on vector proximity.

---

