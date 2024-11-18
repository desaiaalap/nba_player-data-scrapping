
# NBA Players Data Scraping

This Python script is designed to scrape NBA player statistics data from the official NBA stats website using the `requests` library. The data includes various statistics for players across multiple seasons and season types (Regular Season and Playoffs). The script retrieves the data, processes it, and saves it in an Excel file for further exploratory data analysis (EDA).

---

## Features

1. **Data Collection**:
   - Retrieves player statistics for seasons ranging from 2015-16 to 2022-23.
   - Supports both **Regular Season** and **Playoff** data.
   
2. **Dynamic Column Naming**:
   - Automatically extracts column names from the API response to ensure consistency.

3. **Data Organization**:
   - Adds additional columns (`Year`, `Season_type`) to provide context for each dataset.
   - Combines data from all specified seasons and season types into a single DataFrame.

4. **Data Export**:
   - Saves the final dataset in `.xlsx` format for further analysis.

---

## Dependencies

The script requires the following Python libraries:
- `pandas` for data manipulation.
- `numpy` for numerical operations (though not actively used in the current script).
- `requests` for API calls.

To install the required libraries, run:
```bash
pip install pandas numpy requests
```

---

## How It Works

### Workflow

1. **Setup**:
   - The script begins by defining the URL for the NBA stats API and fetching headers for column names.
   
2. **Data Iteration**:
   - Loops through multiple seasons and season types (Regular Season and Playoffs).
   - Dynamically constructs the API URL for each combination of season and season type.

3. **Data Aggregation**:
   - Retrieves data in JSON format and converts it into a tabular DataFrame using `pandas`.
   - Adds metadata (`Year` and `Season_type`) for better context.

4. **Export**:
   - Concatenates all collected data into a single DataFrame and saves it as an Excel file named `NBA_players.xlsx`.

### Key Components
- **API URL Construction**:
   ```python
   url = 'https://stats.nba.com/stats/leagueLeaders?LeagueID=00&PerMode=Totals&Scope=S&Season='+y+'&SeasonType='+s+'&StatCategory=PTS'
   ```
   This dynamically constructs the URL for each season and season type combination.
   
- **Column Handling**:
   ```python
   headers = r['resultSet']['headers']
   ```
   Fetches column headers from the API response to dynamically adapt to the data structure.

- **DataFrame Merging**:
   ```python
   temp_df3 = pd.concat([temp_df2, temp_df1], axis=1)
   df = pd.concat([df, temp_df3], axis=0)
   ```
   Combines metadata and player statistics into a unified DataFrame.

---

## Output

- **File Name**: `NBA_players.xlsx`
- **Content**:
   - Comprehensive statistics for NBA players from 2015-16 to 2022-23.
   - Data categorized by year and season type (Regular Season or Playoffs).

---

## Usage

1. Clone the repository or copy the script to your local machine.
2. Ensure Python and the required libraries are installed.
3. Run the script:
   ```bash
   python nba_player_scraping.py
   ```
4. Open the `NBA_players.xlsx` file for analysis.

---

## Potential Enhancements

- Add error handling for API rate limits or network interruptions.
- Extend functionality to include other stat categories (e.g., REB, AST).
- Implement multithreading to speed up data collection.

---

## Notes

- This script relies on the availability of the NBA stats API and may require updates if the API structure changes.
- Ensure a stable internet connection when running the script.
