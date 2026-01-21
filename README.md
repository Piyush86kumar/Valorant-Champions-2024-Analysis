# Valorant Champions 2024 Match Analysis

This project provides a comprehensive analysis of match data from the Valorant Champions 2024 tournament. It utilizes a rich dataset to explore player statistics, agent performance, map trends, and economic factors throughout the event. The analysis is presented through a series of Jupyter Notebooks, each focusing on a different aspect of the tournament.

## Dataset

The dataset for this analysis is located in the `VCT_2024_seoul_dataset/` directory and was sourced by scrapping the vlr.gg website and it is also available on [Kaggle](https://www.kaggle.com/datasets/piyush86kumar/valorant-champions-2024). It contains detailed information about matches, players, agents, and economy.

### Dataset Files

The dataset is composed of the following CSV files:

*   **`agents_stats.csv`**: Statistics for each agent, including utilization rates.
*   **`columns_description.csv`**: Descriptions for all columns in the dataset.
*   **`detailed_matches_maps.csv`**: Detailed information about each map played in a match.
*   **`detailed_matches_overview_processed.csv`**: Processed overview of detailed match data.
*   **`detailed_matches_overview.csv`**: Overview of detailed match data.
*   **`detailed_matches_player_stats.csv`**: Detailed player statistics for each match.
*   **`economy_data.csv`**: Data on team economies for each map.
*   **`event_info.csv`**: General information about the tournament.
*   **`maps_stats.csv`**: Statistics for each map, including win percentages for attack and defense.
*   **`matches.csv`**: Information about each match played.
*   **`performance_data.csv`**: Player performance data, including multi-kill rounds and clutches.
*   **`player_stats.csv`**: Overall player statistics for the tournament.

For a detailed description of each column in these files, please refer to the `VCT_2024_seoul_dataset/README.md` file.

## Notebooks

The analysis is divided into the following Jupyter Notebooks:

*   **`Agents_stats.ipynb`**: Analyzes agent popularity and performance across different maps.
*   **`Detailed_matches_maps.ipynb`**: Provides a deep dive into map-specific statistics and trends.
*   **`Detailed_player_stats.ipynb`**: Offers a granular look at individual player performance.
*   **`Economy_stats.ipynb`**: Examines the impact of economy on round outcomes.
*   **`Player_stats.ipynb`**: Presents an overview of player statistics throughout the tournament.

## Getting Started

To explore this analysis, you will need to set up a Python environment and install the required dependencies.

### Prerequisites

*   Python 3.12.11
*   `pip` (Python package installer) or `conda`

### Installation

Choose your preferred environment manager:



1.  **Clone the repository:**
    ```bash
    git clone https://github.com/Piyush86kumar/Valorant-Champions-2024-Analysis.git
    cd <repository-directory>
    ```

**Option 1: Using `venv`**

2.  **Create and activate a virtual environment:**
    ```bash
    python -m venv venv
    venv\Scripts\activate
    ```

**Option 2: Using `conda`**

2.  **Create and activate a conda environment:**
    ```bash
    conda create --name valorant-analysis python=3.12.11
    conda activate valorant-analysis
    ```

3.  **Install the required dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

## Key Dependencies

This project relies on several key Python libraries for data analysis and visualization, including:

*   `pandas`
*   `numpy`
*   `matplotlib`
*   `seaborn`
*   `scikit-learn`

A complete list of dependencies can be found in the `requirements.txt` file.
