<div align="center">
    <h1>League of Legends Analytics on Professional Teams</h1>
    <p>Objective Control and Win Rate Insights</p>
</div>
---

<div style="text-align: center;">
    <h1>League of Legends: Objectives and Their Importance for League Win-Rates</h1>
</div>
<p>
    League of Legends is a MOBA (Multiplayer Online Battle Arena) style game where teams of five fight each other in order to defeat the nexus (main objective) and win.
</p>
 
<div style="text-align: center;">
    <h2>Introduction</h2>
</div>
<p>
    This dataset originates from Oracle’s Elixir, covering match data from the 2022 professional League of Legends season. 
    It includes games from major competitive regions such as the LCS, LEC, LCK, LPL, PCS, CBLoL, and others.
</p>

<hr>

<div style="text-align: center;">
    <h2>Key Match Insights</h2>
</div>
<ul>
    <li>In League of Legends, <strong>Dragon control</strong> is often considered a critical objective that can significantly impact a team's chances of winning.</li>
    <li>Teams that secure more dragons have better late-game scaling, buffs, and map control, leading to a higher probability of success.</li>
    <li>Once four dragons have been secured by a team, that is the max amount a team can have. However if there is a stale-mate of dragon control then one team could acquire 3 versus the opposite team having 4</li>
</ul>

<hr>

<div style="text-align: center;">
    <h2>Analysis Question</h2>
</div>
<p style="text-align: center;">
    Does obtaining more dragons correlate with a higher win rate in (<strong>tier-one league</strong>) League of Legends matches?  
</p>
<p>
    Dragon control is a key part of professional play, offering buffs that scale throughout the game. Investigating whether controlling more dragons aligns 
    with a higher win rate could reveal insights about team strategies, objective prioritization, and meta preferences.
</p>

<hr>

<div style="text-align: center;">
    <h2>Dataset Summary</h2>
</div>
<p>
    The dataset contains approximately <strong>150,000 rows</strong> of data. For this analysis, we will focus on the following columns:
</p>
<ul>
| **Columns** | **Definition**                                                                 |
|--------------|---------------------------------------------------------------------------------|
| dragons      | The number of dragons secured                                                  |
| elders       | The number of elder dragons secured                                            |
| barons       | The number of barons secured                                                   |
| firsttothree | The first team to destroy three towers                                         |
    towers      
| league       | The tier-one league where the match took place (e.g., LCS, LEC, LCK, LPL).     |
| result       | The outcome of the match, indicating whether the team won (1) or lost (0).     | 
</ul>
<p>
    These columns are central to answering our question about the relationship between dragon control and win rates in professional matches.
</p>