<div align="center">
    <h1>League of Legends Analytics on Professional Teams</h1>
    <p>Objective Control and Win Rate Insights</p>
</div>
---

<div style="text-align: center;">
    <h3>League of Legends: Objectives and Their Importance for League Win-Rates</h1>
</div>
<p>
    League of Legends is a MOBA (Multiplayer Online Battle Arena) style game where teams of five fight each other in order to defeat the nexus (main objective) and win.
</p>
 
<div style="text-align: left;">
    <h1><strong>Introduction</strong></h2>
</div>
<p>
    This dataset originates from Oracle’s Elixir, covering match data from the 2022 professional League of Legends season. 
    It includes games from major competitive regions such as the LCS, LEC, LCK, LPL, PCS, CBLoL, and others.
</p>

<hr>

<div style="text-align: left;">
    <h3>Key Match Insights</h3>
</div>
<ul>
    <li>In League of Legends, <strong>Dragon control</strong> is often considered a critical objective that can significantly impact a team's chances of winning.</li>
    <li>Teams that secure more dragons have better late-game scaling, buffs, and map control, leading to a higher probability of success.</li>
    <li>Once four dragons have been secured by a team, that is the max amount a team can have. However, if there is a stalemate of dragon control, one team could acquire 3 versus the opposite team having 4.</li>
</ul>

<hr>

<div style="text-align: left;">
    <h3>Analysis Question</h3>
</div>
<div style="text-align: left;">
    <p>Does obtaining more dragons correlate with a higher win rate in (<strong>tier-one league</strong>) League of Legends matches?</p>
    <p>
        Dragon control is a key part of professional play, offering buffs that scale throughout the game. Investigating whether controlling more dragons aligns 
        with a higher win rate could reveal insights about team strategies, objective prioritization, and meta preferences.
        This analysis could help coaches make better choices as to whether dragons are an important factor in winning the game.
    </p>
</div>

<hr>

<div style="text-align: left;">
    <h3>Dataset Summary</h3>
</div>
<p>
    The dataset contains approximately <strong>150,000 rows</strong> of data. For this analysis, we will focus on the following columns:
</p>

| **Column**        | **Definition**                                                                                     |
|--------------------|---------------------------------------------------------------------------------------------------|
| **dragons**        | The number of dragons secured.                                                                    |
| **league**         | The tier-one league where the match took place (e.g., LCS, LEC, LCK, LPL).                        |
| **result**         | The outcome of the match, indicating whether the team won (1) or lost (0).                        |

<p>
    These columns are central to answering our question about the relationship between dragon control and win rates in professional matches.
</p>
<div style="text-align: left;">
    <h1>Data Cleaning and Exploratory Data Analysis</h1>
</div>
<p>
    In the data cleaning process, several steps were performed to prepare this dataset for analysis:
    <ul>
        <li>Loaded the dataset from the 2022 League of Legends Esports match data using Oracle’s Elixir.</li>
        <li>Filtered the dataset to retain only rows corresponding to team-level data by selecting rows where the <code>position</code> column equals "team".</li>
        <li>Converted the game length from seconds to minutes and stored the result in a new column, <code>gamelength_minutes</code>, rounded to two decimal places for better readability.</li>
        <li>Transformed the <code>result</code> column into a boolean format and stored it in a new column, <code>result_bool</code>, to facilitate binary classification analysis.</li>
    </ul>
</p>
| gameid                | datacompleteness | url                               | league | year | split  | playoffs | date                | game | patch | xpdiffat25 | csdiffat25 |killsat25 
|-----------------------|------------------|-----------------------------------|--------|------|--------|----------|---------------------|------|-------|------------|------------|----------
| ESPORTSTMNT01_2690210 | complete         | NaN                               | LCKC   | 2022 | Spring | 0        | 2022-01-10 07:44:08 | 1    | 12.01 | -3971.0    | -97.0      | 6.0      
| ESPORTSTMNT01_2690210 | complete         | NaN                               | LCKC   | 2022 | Spring | 0        | 2022-01-10 07:44:08 | 1    | 12.01 | 3971.0     | 97.0       | 7.0      
| ESPORTSTMNT01_2690219 | complete         | NaN                               | LCKC   | 2022 | Spring | 0        | 2022-01-10 08:38:24 | 1    | 12.01 | -7746.0    | -33.0      | 1.0      
| ESPORTSTMNT01_2690219 | complete         | NaN                               | LCKC   | 2022 | Spring | 0        | 2022-01-10 08:38:24 | 1    | 12.01 | 7746.0     | 33.0       | 8.0      
| 8401-8401_game_1      | partial          | https://lpl.qq.com/es/stats.shtml?bmid=8401 | LPL    | 2022 | Spring | 0        | 2022-01-10 09:24:26 | 1    | 12.01 | NaN        | NaN        | NaN       |

