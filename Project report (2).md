# Valorant Champions 2024 Seoul
# Comprehensive Data Analysis Report

**Author:** [Your Name]  
**Domain:** Esports Analytics (Competitive FPS – Valorant)  
**Tools:** Python, Pandas, NumPy, Matplotlib, Seaborn

## Table of Contents
1. [Executive Summary](#1-executive-summary)
2. [Project Objective & Business Context](#2-project-objective--business-context)
3. [Data Sources & Project Structure](#3-data-sources--project-structure)
4. [Data Engineering & Preparation](#4-data-engineering--preparation)
5. [Exploratory Data Analysis Overview](#5-exploratory-data-analysis-overview)
6. [Pillar 1: Player Performance & Efficiency](#6-pillar-1-player-performance--efficiency)
7. [Pillar 2: Agent Meta & Map Strategy](#7-pillar-2-agent-meta--map-strategy)
8. [Pillar 3: Economy & Round Win Impact](#8-pillar-3-economy--round-win-impact)
9. [Key Insights & Business Value](#9-key-insights--business-value)
10. [Technical Toolkit](#10-technical-toolkit)
11. [Limitations](#11-limitations)
12. [Future Scope](#12-future-scope)

## 1. Executive Summary

This comprehensive analysis examines data from the Valorant Champions 2024 (VCT Seoul) tournament to identify the key factors that contribute to winning at the highest level of professional play. Using match, player, agent, map, and economy datasets, the analysis focuses on player performance, strategic agent and map selection, and economic decision-making rather than raw kill counts alone. The findings reveal that metrics such as KAST% and ADR are stronger indicators of impact, effective agent-map synergies outperform meta popularity, and efficient economy management provides a measurable competitive advantage. This project demonstrates strong data engineering, exploratory analysis, and insight-driven storytelling skills.

## 2. Project Objective & Business Context

### Objective
The primary objective of this project was to build a structured and repeatable analytical framework capable of explaining why certain teams consistently win at the highest level of competitive Valorant. Rather than relying on surface-level indicators such as total kills or highlight performances, the analysis was designed to uncover underlying performance drivers across three dimensions:

- Identifying the key statistical differences between winning and losing teams
- Determining which player-level metrics (e.g., KAST%, ADR) best represent true in-round impact
- Evaluating how strategic decisions, including agent composition and economy management, influence match outcomes

This approach ensures that insights are grounded in efficiency, consistency, and decision quality rather than isolated events.

### Business Context & Relevance
From a business and analytics perspective, this project closely mirrors real-world data analysis challenges:
- Data is fragmented across multiple sources, requiring careful integration and validation
- Raw or headline metrics can be misleading without proper context and normalization
- Stakeholders require actionable insights that support strategic decisions, not just descriptive dashboards

By transforming complex tournament data into clear, decision-oriented insights, this project demonstrates how data analytics can be used to support strategy evaluation, performance optimization, and predictive decision-making—skills directly transferable to professional Data Analyst and Data Science roles.

## 3. Data Sources & Project Structure

### Data Sources
The dataset is composed of multiple structured CSV files, each representing a specific analytical layer of the Valorant Champions 2024 (VCT Seoul) tournament. This modular structure enables flexible joins and supports both high-level and granular analysis across matches, maps, players, agents, and economy.

#### Core Reference & Metadata Files
- **event_info.csv**: Contains general information about the tournament, including event name, location, and format
- **columns_description.csv**: Provides detailed descriptions of all columns across the dataset

#### Match & Map-Level Data
- **matches.csv**: Stores match-level information such as match identifiers, participating teams, and match outcomes
- **detailed_matches_maps.csv**: Contains map-specific data for each match, including map names, results, and team performance
- **maps_stats.csv**: Aggregated statistics for each map, including win percentages for attack and defense sides

#### Player-Level Performance Data
- **player_stats.csv**: Provides overall player statistics for the tournament, offering a high-level view of individual performance
- **detailed_matches_player_stats.csv**: Contains granular, match-level player statistics, including ACS, ADR, KAST%, and K/D ratios
- **performance_data.csv**: Includes advanced performance indicators such as multi-kill rounds and clutch scenarios

#### Agent & Strategic Data
- **agents_stats.csv**: Contains statistics for each agent, including pick rates and win rates

#### Economy Data
- **economy_data.csv**: Captures team economy information at the map and round level, including credits spent and buy types

### Analytical Value
The separation of data into specialized CSV files reflects a normalized data design, similar to real-world production systems. This structure required deliberate data engineering effort to reconstruct meaningful analytical views, reinforcing skills in multi-table joins, data validation, and building scalable analytical pipelines.

### Data Collection Methodology
The data was collected through a custom-built web scraping pipeline from vlr.gg, one of the most authoritative sources for professional Valorant esports statistics. The scraper was implemented as a separate data engineering project, demonstrating ownership of the full data lifecycle.

### Project Structure
```
VCT 2024/
├── VCT_2024_seoul_dataset/          # Dataset storage
│   ├── agents_stats.csv            # Agent utilization and win rates
│   ├── detailed_matches_maps.csv   # Map-specific data per match
│   ├── detailed_matches_player_stats.csv # Match-by-match player performance
│   ├── economy_data.csv           # Team economy and buy-type stats
│   ├── player_stats.csv           # Overall player statistics
│   └── [additional dataset files]
├── Player_stats.ipynb              # Player performance analysis
├── Agents_stats.ipynb              # Agent utilization analysis
├── Detailed_matches_maps.ipynb     # Map strategy analysis
├── Detailed_player_stats.ipynb     # Advanced player metrics
├── Economy_stats.ipynb             # Economic impact analysis
└── CHAMPIONS_2024_REPORT.md        # Final comprehensive report
```

## 4. Data Engineering & Preparation

Handling real-world data requires a robust data engineering strategy to ensure accuracy and consistency across multiple analytical layers.

### Merging Strategy
The datasets were designed to be interoperable, with `match_id` and `player_id` serving as primary keys. For instance, `detailed_matches_player_stats` and `economy_data` can be linked via `match_id`, enabling cross-domain analysis such as correlating a player's performance with their team's economic status.

### Preprocessing Techniques
- **Handling Percentages**: Columns like `kast` and `hs_percent` were stored as strings (e.g., "83%"). Custom scripts strip the '%' symbol and convert these to float datatypes for numerical analysis.
- **Parsing Complex Strings**: In the `economy_data` dataset, round information was stored in condensed format like "2 (2)". These were parsed to create separate columns for rounds played and rounds won for each buy category.
- **Dictionary Parsing**: In `agents_stats`, the `map_utilizations` column (stringified dictionary) was parsed using `ast.literal_eval` to expand map-specific agent pick rates into individual columns.
- **Null Value Handling**: Null values in `map_name` and `map_winner` were addressed by filtering DataFrames for map-specific analyses.

### Feature Engineering
- **Kills Per Round (KPR)**: Engineered by dividing total kills by rounds played to normalize statistics across matches of varying lengths.
- **Composite Performance Scores**: Created weighted metrics combining multiple performance indicators for holistic player evaluation.
- **Economic Efficiency Metrics**: Derived features calculating economic win rates and momentum indicators.

## 5. Exploratory Data Analysis Overview

The analytical framework follows a systematic approach to uncover patterns in professional Valorant performance:

### Statistical Foundations
- **Distribution Analysis**: Examined metric distributions to identify outliers and performance clusters
- **Correlation Analysis**: Investigated relationships between performance metrics and match outcomes
- **Normalization Techniques**: Adjusted metrics for match length, map complexity, and team composition

### Visualization Strategy
- **2×2 subplot grids** for metric comparison and trend identification
- **Horizontal bar charts** with value labels for ranking displays
- **Heatmaps** for agent-map effectiveness and strategic patterns
- **Distribution plots** for outlier detection and performance clustering

Each visualization was designed to answer specific analytical questions, focusing on insight generation rather than aesthetic presentation.

## 6. Pillar 1: Player Performance & Efficiency
*(Sources: Player_stats.ipynb, Detailed_player_stats.ipynb)*

### Analysis Focus
- Individual player statistical profiles and consistency metrics
- Performance differentiation between winning and losing teams
- Advanced metrics including KAST%, ADR, ACS, and composite scoring

### Key Findings
- **KAST%** emerges as a stronger indicator of winning impact than raw K/D ratios
- Elite players distinguish themselves through consistency across multiple metrics
- High ACS alone does not guarantee map wins without supporting efficiency metrics

### Performance Metrics Analysis
- **Top Performers**: Players achieving 1.20+ rating with ACS scores exceeding 250
- **Consistency Indicators**: KAST% above 75% and ADR scores above 140
- **Clutch Performance**: Success rates above 25% in high-pressure 1v2/1v3 scenarios

## 7. Pillar 2: Agent Meta & Map Strategy
*(Sources: Agents_stats.ipynb, Detailed_matches_maps.ipynb)*

### Analysis Focus
- Agent pick rate vs. win rate effectiveness
- Map-specific agent utilization patterns
- Strategic composition vs. meta imitation

### Key Findings
- Popular agents are not always the most effective performers
- Strong agent-map synergies exist beyond general meta trends
- Top teams prioritize situational compositions over meta imitation

### Strategic Insights
- **Map-Specific Adaptations**: Agents like Viper show increased effectiveness on multi-site maps
- **Role Distribution**: Duelists (35-40%), Controllers (20-25%), Initiators/Sentinels (45-50%)
- **Veto Strategy**: Teams ban Haven in 45% of sequences, indicating its strategic importance

## 8. Pillar 3: Economy & Round Win Impact
*(Sources: Economy_stats.ipynb)*

### Analysis Focus
- Team credits vs. round win correlations
- Economic momentum and recovery patterns
- Buy-type effectiveness analysis

### Key Findings
- Higher spending shows diminishing returns beyond optimal thresholds
- Thrifty round wins significantly improve future round win probability
- Efficient teams consistently win with lower average economic expenditure

### Economic Metrics
- **Full-Buy Win Rate**: 60%+ across tournament vs. Eco win rate <20%
- **Pistol Round Impact**: 35% increased match victory probability
- **Economic Recovery**: Teams winning 55%+ of semi-eco rounds demonstrate strong adaptation

## 9. Key Insights & Business Value

### Strategic Insights
- **Efficiency beats aggression**: Consistent performance metrics outweigh highlight moments
- **Economy discipline amplifies momentum**: Thrifty wins create sustainable competitive advantages
- **Contextual meta understanding**: Map-specific strategies outperform general trends

### Business Value
This analysis framework can support:
- **Team strategy planning**: Data-driven agent selection and map preparation
- **Player evaluation**: Comprehensive performance assessment beyond basic statistics
- **Predictive match modeling**: Foundation for forecasting based on pre-match indicators
- **Tournament analysis**: Understanding championship-level decision patterns

## 10. Technical Toolkit

### Languages & Libraries
- **Python**: Primary programming language for analysis and automation
- **Pandas**: Data manipulation and analysis framework
- **NumPy**: Numerical computing and array operations
- **Matplotlib**: Statistical visualization and plotting foundation
- **Seaborn**: Advanced statistical visualization with enhanced aesthetics

### Techniques & Methodologies
- **Exploratory Data Analysis (EDA)**: Systematic data investigation and pattern discovery
- **Feature Engineering**: Creation of derived metrics and normalized indicators
- **Metric Normalization**: Adjusting statistics for contextual factors (match length, map complexity)
- **Outlier Detection**: Statistical methods for identifying exceptional performances
- **Analytical Storytelling**: Transforming data insights into actionable narratives

### Data Processing Skills
- Multi-table joins using primary and foreign keys
- Data validation and schema understanding
- Building scalable, reusable analytical pipelines
- Handling semi-structured data formats and complex parsing

## 11. Limitations

- **No round-by-round positional data**: Limited ability to analyze spatial strategies and positioning
- **Limited temporal modeling**: Cannot fully capture momentum shifts within matches
- **External factors not captured**: Communication quality, psychological pressure, and team dynamics
- **Sample size constraints**: Tournament scope limits generalizability to broader competitive landscape
- **Data completeness**: Some advanced metrics may be unavailable for certain matches or players

## 12. Future Scope

### Predictive Modeling Development
Build a comprehensive win probability prediction model incorporating:
- **Agent Composition Features**: Team synergy analysis and counter-pick modeling
- **Economic Indicators**: Pre-round economic states and momentum factors
- **Historical Performance**: Map-specific player and team performance trends

### Advanced Analytics
- **Time-series Analysis**: Round-by-round momentum modeling and performance trajectories
- **Machine Learning Applications**: Classification models for match outcome prediction
- **Network Analysis**: Player collaboration patterns and team communication insights
- **Real-time Analytics**: Live tournament monitoring and strategic recommendations

### Expanded Data Integration
- **Broader Tournament Coverage**: Multi-event analysis across VCT seasons
- **Additional Data Sources**: Integration with player stream data and community analytics
- **Automated Reporting**: Real-time dashboard development for ongoing tournaments

This framework establishes a foundation for advanced esports analytics, with potential applications in team strategy optimization, talent evaluation, and competitive intelligence gathering.
