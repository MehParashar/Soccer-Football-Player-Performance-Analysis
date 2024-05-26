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

OUTPUTS

            Player_misc Nation_misc Pos_misc   Squad_misc Age_misc Born_misc  \
0            Liel Abada      il ISR       FW    Charlotte   22-236      2001   
1  Jose Casas de Abadal      us USA    FW,DF  Inter Miami   23-341      2000   
2            Luis Abram      pe PER       DF  Atlanta Utd   28-089      1996   
3        Lalas Abubakar      gh GHA    DF,MF       Rapids   29-153      1994   
4         Kellyn Acosta      us USA       MF         Fire   28-307      1995   

  90s_misc        Player_passing Nation_passing Pos_passing  ... Int_misc  \
0      4.0            Liel Abada         il ISR          FW  ...        1   
1      0.3  Jose Casas de Abadal         us USA       FW,DF  ...        0   
2      7.5            Luis Abram         pe PER          DF  ...        6   
3      1.2        Lalas Abubakar         gh GHA       DF,MF  ...        2   
4     12.2         Kellyn Acosta         us USA          MF  ...       20   

  TklW_misc PKwon_misc PKcon_misc OG_misc Recov_misc Won_misc Lost_misc  \
0         3          0          0       0         10        0         8   
1         0          0          0       0          0        0         0   
2         3          0          0       0         27       10        10   
3         0          0          0       0          7        5         3   
4        13          0          0       0         64        7         5   

  Won%_misc       position_group  
0       0.0             Forwards  
1         0            Wing-Back  
2      50.0             Defender  
3      62.5             Defender  
4      58.3  Central Midfielders  

---------------------------------------------------------------------------------------

Top GKs
           Player_misc   Squad_misc  Rank  TklW_misc  Recov_misc
574       Zack Steffen       Rapids  15.5          0          31
88           Alex Bono  D.C. United  14.5          0          29
455       Maarten Paes    FC Dallas  14.0          0          28
387          Tim Melia  Sporting KC  13.5          0          27
306  Kristijan Kahlina    Charlotte  12.0          0          24






