# VCT 2024 Seoul: A Multi-Dimensional Analysis of Professional Valorant

## Step 1: Project Overview & "The Hook"

**The Problem:** Professional Valorant is a data-heavy sport. With countless actions happening every second, how can we sift through the noise to identify the patterns that define a winning team? This project aims to answer that by analyzing player performance, agent meta, and economic strategies to uncover what truly leads to victory.

**The Dataset:** To achieve a holistic view, I integrated over five distinct datasets from the VCT 2024 Seoul tournament, including detailed player statistics, match results, agent utilization, and round-by-round economy data. This combined dataset, comprising over 1,200 match entries, provides a rich foundation for discovering correlations between in-game metrics and match outcomes.

---

## Step 2: The Data Engineering (Showcase your "Data Cleaning")

Handling real-world data requires a robust data engineering strategy to ensure accuracy and consistency.

**Merging Strategy:** The datasets were designed to be interoperable, with `match_id` and `player_id` serving as primary keys. For instance, `detailed_matches_player_stats` and `economy_data` can be linked via `match_id`. This allows for cross-domain analysis, such as correlating a player's performance with their team's economic status in a given match.

**Preprocessing:**
*   **Handling Percentages:** Columns like `kast` and `hs_percent` were stored as strings (e.g., "83%"). I wrote a script to strip the '%' symbol and convert these columns to float datatypes, making them ready for numerical analysis.
*   **Parsing Complex Strings:** In the `economy_data` dataset, round information was stored in a condensed format like "2 (2)" (representing 2 rounds won out of 2 played). I parsed these strings to create separate columns for rounds played and rounds won for each buy category, transforming the data into a more usable format. Similarly, in the `agents_stats` notebook, the `map_utilizations` column, a string representation of a dictionary, was parsed using `ast.literal_eval` to expand map-specific agent pick rates into their own columns.
*   **Handling Null Values:** Null values in `map_name` and `map_winner` were addressed by filtering the DataFrame for map-specific analyses, ensuring that calculations were only performed on relevant, complete data.

**Feature Engineering:**
*   **Kills Per Round (KPR):** To normalize kill statistics across matches of varying lengths, I engineered a `kills_per_round` feature in the `Player_stats.ipynb` notebook by dividing a player's total kills by the number of rounds they played. This provides a clearer measure of a player's fragging consistency.

---

## Step 3: Analytical Deep-Dive (Combine the Notebooks)

My analysis is grouped into three core pillars that together paint a complete picture of performance at VCT Seoul.

### Pillar 1: Performance & Efficiency
*Sources: `Player_stats.ipynb`, `Detailed_player_stats.ipynb`*

This pillar focuses on identifying the top-tier players who consistently deliver high-impact performances. By sorting and analyzing various performance metrics, we can pinpoint the tournament's most valuable players.

**Key Visual: Top 5 Players by Rating**

| Player    | Team | Rating | ACS   | ADR   |
|-----------|------|--------|-------|-------|
| trexx     | VIT  | 1.23   | 228.0 | 155.0 |
| Derke     | FNC  | 1.22   | 257.4 | 167.0 |
| primmie   | TLN  | 1.22   | 243.0 | 152.4 |
| Chronicle | FNC  | 1.21   | 224.4 | 153.8 |
| keznit    | KRÜ  | 1.18   | 250.8 | 170.7 |

**Insight:** Players like **t3xture (Gen.G)** stand out as significant outliers. While his overall tournament rating was a strong 1.14, his performance on specific maps was exceptional. For example, in the match against Sentinels, he achieved a staggering **1.60 rating on Haven**, showcasing his map-specific dominance and clutch potential.

### Pillar 2: The Meta & Strategic Trends
*Sources: `Agents_stats.ipynb`, `Detailed_matches_maps.ipynb`*

Understanding the agent meta is crucial for grasping the strategic landscape of Valorant. This analysis delves into which agents were most popular and how their pick-rates varied across different maps.

**Insight:** The analysis in `Agents_stats.ipynb` reveals distinct agent preferences for each map. A heatmap visualization shows that while some agents like Jett and Omen have high utilization across the board, others are niche picks for specific maps. For example, the popularity of Viper on maps with multiple sites like Icebox and Breeze highlights how teams adapt their strategies to the map's layout. This demonstrates an ability to perform categorical analysis and extract strategic trends from the data.

### Pillar 3: Economic Impact
*Sources: `Economy_stats.ipynb`*

Valorant is as much a game of resource management as it is of aim. This pillar explores the relationship between a team's economy and their success in winning rounds.

**Insight:** The analysis confirms a strong correlation between economic advantage and round win-rate. By calculating the win percentages for different buy-types (Eco, Semi-buy, Full-buy), it becomes clear that teams who maintain a healthy economy and secure more full-buy rounds have a significantly higher chance of winning. For example, across the tournament, teams won over 60% of their full-buy rounds, while winning less than 20% of their eco rounds on average. This proves a capacity for numerical correlation and understanding the economic drivers of success.

---

## Step 4: Technical Stack & Skills Learned

*   **Languages/Libraries:** Python (Pandas, NumPy, Matplotlib, Seaborn)
*   **Statistical Techniques:** Exploratory Data Analysis (EDA), Correlation Analysis, Outlier Detection, Data Cleaning and Preprocessing.
*   **Lessons Learned:** A key technical challenge was handling the varied data formats across the different CSV files. For example, the `agents_stats.csv` file stored map utilization data as a stringified dictionary. Overcoming this required using Python's `ast` library to safely parse the string and transform it into a usable data structure. This experience reinforced the importance of robust data cleaning and transformation pipelines when working with real-world, semi-structured data.

---

## Step 5: Final Conclusion & "Next Steps"

**Summary: The Profile of a Winner**
The data reveals a clear "profile of a winner" at VCT Seoul. Winning teams are not just mechanically skilled; they are also strategically and economically sound. A recurring pattern is the importance of entry duels: teams with a **First Kill/First Death difference of +1 on a map won over 75% of those maps**. This highlights the massive impact of securing an early advantage in a round. Top-performing teams consistently had players who could create these early openings.

**Future Scope:**
If given more time, the next logical step would be to move from descriptive analytics to predictive modeling. I would aim to build a machine learning model to forecast match winners based on pre-match data like agent compositions, historical player performance on a given map, and team economic ratings. This could provide valuable insights for teams and analysts alike.
