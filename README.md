# mlb-fan-experience-analytics
A statistical analysis of MLB fan experience using Python, feature engineering, and predictive modeling.

Overview:
This project develops a statistical index that combines affordability, game quality, player star power, and concession pricing to identify the games that provide the highest overall fan experience.

Motivation:
Fans often choose games based on ticket prices or team popularity, but these don't necessarily lead to the best overall experience. This project explores whether publicly available baseball data can identify games that maximize entertainment while minimizing cost.

Data:
The data for this project was collected from two main types of sources. MLB game, player, lineup, weather, timing, and award data came from MLB StatsAPI. Concession prices were collected from public secondary sources that reported MLB beer and hot dog prices by team or ballpark.
Current Data Cleaning Notes
Unit of analysis is a team-game.
Team names were standardized.
Postponed/incomplete games were removed.
Concession prices were merged by team-season.
Actual starting lineups were used for the superstar factor.
Current-season leader variables are lagged through the day before the game to avoid leakage.


Methods: 
The project builds a weighted normalized index rather than trying to predict MLB wins directly. Each completed MLB game is represented twice, once for each team. Raw variables are standardized using 2024 as the baseline season. This makes variables with different units comparable.
Index Formula
raw index =
0.35(game quality z)
0.15(lineup superstar factor z)
0.10(current-season leader factor z)
0.25(concession cost z)
0.15(staleness z)
Final Normalization
final index = 100 + 10(raw index z-score)
With this scale, 100 represents the 2024 average game-team experience and 10 points represents about one standard deviation. The project also includes a 2025 holdout check using pre-game available variables.


Variables:
Variable:				Meaning
concession_999_cost:			Total cost of 9 beers and 9 hot dogs
game_quality_raw:			    Measures how exciting/successful the game was for that team
lineup_superstar_factor_raw:	Measures star power from actual starting lineups	current_season_leader_factor_raw	Rewards players currently near league leads in HRs, hits, strikeouts, or saves
staleness_raw:            Measures late-game waiting time after the 7th inning 
999_optimality_index:			Final normalized 9/9/9 score


Results
Final 9/9/9 Index Results
2025 Game And Team Rankings
2025 Experience Value Per Dollar
Index Stability Across Seasons
Pre-Game Holdout Check
Component Relationships
Key Results To Include
2024 mean index: 100.000
2024 standard deviation: 10.001
2025 mean index: 99.833
2025 standard deviation: 10.172
2026 mean index: 99.946
2026 standard deviation: 9.843
2025 AUC for above-average index games: about 0.825
Section 13 Value-Per-Dollar Teams
Top 5:
New York Yankees
Detroit Tigers
Arizona Diamondbacks
Miami Marlins
Atlanta Braves
Bottom 5:
Chicago White Sox
Texas Rangers
St. Louis Cardinals
Los Angeles Dodgers
Washington Nationals

From our results we can target some of the teams to show what factors cause the overall 9/9/9 rankings. First is the New York Yankees, this team has a lot of star players and keeps the prices low to be able to rank first place. On the other hand the LA Dodgers have a lot of talented players but choose to have really expensive hot dogs and beers. Teams like the Atlanta Braves, Detroit Tigers, and the Arizona Diamondbacks have two-three exciting players while having good price items. Lastly, teams that don’t perform well and don’t have stars have either make up with the 9/9/9 index by making their beer and hot dogs super cheap, in this case, the Miami Marlins,  or they still continue with high price items the Washington Nationals which makes them the worst team to participate in this challenge for. 


