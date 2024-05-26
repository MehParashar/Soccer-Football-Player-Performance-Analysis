# Soccer-Football-Player-Performance-Analysis
This repository contains a set of functions to scrape, process, and analyze soccer player performance data from FBRef. The analysis covers various performance metrics across different player positions.

Table of Contents
         Overview
         Setup
         Functions
         scrape_fbref_data
         rename_duplicate_columns
         create_full_stats_db
         position_grouping
         per_90fi
         key_stats_db
         rank_players
         plot_player_attributes
         plot_top_players
         Usage
         Example Outputs

Overview
The provided code extracts player performance data from FBRef, processes the data, normalizes it, and performs analysis to rank players based on key performance indicators (KPIs). It also generates visualizations of player attributes and rankings.

Setup
To use this code, ensure you have the following Python packages installed:

requests
pandas
beautifulsoup4
numpy
matplotlib
You can install these packages using pip:
----------------------------------------------------------------------------------
      pip install requests pandas beautifulsoup4 numpy matplotlib
----------------------------------------------------------------------------------
Functions
scrape_fbref_data
Scrapes data from a given FBRef URL and returns a DataFrame.

Parameters:
url (str): The URL of the FBRef page to scrape.
Returns:
DataFrame: The scraped data.
---------------------------------------------------------------------------------
    df = scrape_fbref_data('https://fbref.com/en/comps/22/passing/Major-League-Soccer-Stats')
---------------------------------------------------------------------------------
rename_duplicate_columns
Renames duplicate columns in a DataFrame by adding a suffix.

Parameters:
df (DataFrame): The DataFrame with potential duplicate columns.
suffix (str): The suffix to add to duplicate columns.
Returns:
DataFrame: The DataFrame with renamed columns.
----------------------------------------------------------------------------------
    df = rename_duplicate_columns(df, '_passing')
----------------------------------------------------------------------------------
create_full_stats_db
Creates a comprehensive database of player statistics by scraping multiple FBRef pages and merging the data.

Returns:
DataFrame: The full statistics database.
----------------------------------------------------------------------------------        
    full_stats_db = create_full_stats_db()
----------------------------------------------------------------------------------
position_grouping
Classifies players into specific positions based on their position data.

Parameters:
x (str): The position data for a player.
Returns:
str: The classified position.
----------------------------------------------------------------------------------
      full_stats_db['position_group'] = full_stats_db['Pos_misc'].apply(position_grouping)
----------------------------------------------------------------------------------
per_90fi
Normalizes statistics per 90 minutes played.

Parameters:
dataframe (DataFrame): The DataFrame containing the data to be normalized.
Returns:
DataFrame: The DataFrame with normalized statistics.
----------------------------------------------------------------------------------
    normalized_df = per_90fi(full_stats_db)
----------------------------------------------------------------------------------

key_stats_db
Extracts key statistics for a specific position.

Parameters:
df (DataFrame): The full statistics database.
position (str): The position to extract key statistics for.
Returns:
DataFrame: The DataFrame with key statistics for the specified position.
----------------------------------------------------------------------------------
    key_stats = key_stats_db(full_stats_db, 'Defender')
----------------------------------------------------------------------------------

rank_players
Ranks players based on their key statistics.

Parameters:
df (DataFrame): The DataFrame containing the player data.
key_stats (list): The list of key statistics to rank players by.
Returns:
DataFrame: The DataFrame with ranked players.
----------------------------------------------------------------------------------
     ranked_players = rank_players(df, key_stats)
----------------------------------------------------------------------------------

plot_player_attributes
Plots a radar chart of a player's attributes.

Parameters:

position (str): The player's position.
player_name (str): The player's name.
players_df (DataFrame): The DataFrame containing player data.
key_stats (list): The list of key statistics to plot.

----------------------------------------------------------------------------------
    plot_player_attributes('Defender', 'Vitor Costa', players_df, key_stats)
----------------------------------------------------------------------------------




