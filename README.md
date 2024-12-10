<div style="text-align: center;">
    <h1>League of Legends Analytics on Professional Teams</h1>
    <p>Objective Control and Win Rate Insights</p>
</div>

<hr>

<div style="text-align: center;">
    <h3>League of Legends: Objectives and Their Importance for League Win-Rates</h3>
</div>
<p style="text-align: center;">
    League of Legends is a MOBA (Multiplayer Online Battle Arena) style game where teams of five fight each other in order to defeat the nexus (main objective) and win.
</p>

<hr>

<div style="text-align: left;">
    <h3>Key Match Insights</h3>
</div>
<ul>
    <li>In League of Legends, <strong>Dragon control</strong> is often considered a critical objective that can significantly impact a team's chances of winning.</li>
    <li>Teams that secure more dragons have better late-game scaling, buffs, and map control, leading to a higher probability of success.</li>
    <li>Once four dragons have been secured by a team, that is the maximum number a team can have. However, if there is a stalemate of dragon control, one team could acquire 3 versus the opposite team having 4.</li>
</ul>

<hr>

<div style="text-align: left;">
    <h3>Analysis Question</h3>
</div>
<p>
    Does obtaining more dragons correlate with a higher win rate in (<strong>tier-one league</strong>) League of Legends matches?
</p>
<p>
    Dragon control is a key part of professional play, offering buffs that scale throughout the game. Investigating whether controlling more dragons aligns 
    with a higher win rate could reveal insights about team strategies, objective prioritization, and meta preferences.
    This analysis could help coaches make better choices as to whether dragons are an important factor in winning the game.
</p>

<hr>

<div style="text-align: left;">
    <h3>Dataset Summary</h3>
</div>
<p>
    The dataset contains approximately <strong>150,000 rows</strong> of data. For this analysis, we will focus on the following columns:
</p>

<table>
    <thead>
        <tr>
            <th><strong>Column</strong></th>
            <th><strong>Definition</strong></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><strong>dragons</strong></td>
            <td>The number of dragons secured.</td>
        </tr>
        <tr>
            <td><strong>league</strong></td>
            <td>The tier-one league where the match took place (e.g., LCS, LEC, LCK, LPL).</td>
        </tr>
        <tr>
            <td><strong>result</strong></td>
            <td>The outcome of the match, indicating whether the team won (1) or lost (0).</td>
        </tr>
    </tbody>
</table>

<p>
    These columns are central to answering our question about the relationship between dragon control and win rates in professional matches.
</p>

<hr>

<div style="text-align: left;">
    <h1>Data Cleaning and Exploratory Data Analysis</h1>
</div>
<p>
    In the data cleaning process, several steps were performed to prepare this dataset for analysis:
</p>
<ul>
    <li>Loaded the dataset from the 2022 League of Legends Esports match data using Oracle’s Elixir.</li>
    <li>Filtered the dataset to retain only rows corresponding to team-level data by selecting rows where the <code>position</code> column equals "team".</li>
    <li>Converted the game length from seconds to minutes and stored the result in a new column, <code>gamelength_minutes</code>, rounded to two decimal places for better readability.</li>
    <li>Transformed the <code>result</code> column into a boolean format and stored it in a new column, <code>result_bool</code>, to facilitate binary classification analysis.</li>
</ul>
<p>
    The first few rows and columns are shown below:
</p>

<table>
    <thead>
        <tr>
            <th><strong>gameid</strong></th>
            <th><strong>datacompleteness</strong></th>
            <th><strong>url</strong></th>
            <th><strong>league</strong></th>
            <th><strong>year</strong></th>
            <th><strong>split</strong></th>
            <th><strong>playoffs</strong></th>
            <th><strong>date</strong></th>
            <th><strong>game</strong></th>
            <th><strong>patch</strong></th>
            <th><strong>xpdiffat25</strong></th>
            <th><strong>csdiffat25</strong></th>
            <th><strong>killsat25</strong></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>ESPORTSTMNT01_2690210</td>
            <td>complete</td>
            <td>NaN</td>
            <td>LCKC</td>
            <td>2022</td>
            <td>Spring</td>
            <td>0</td>
            <td>2022-01-10 07:44:08</td>
            <td>1</td>
            <td>12.01</td>
            <td>-3971.0</td>
            <td>-97.0</td>
            <td>6.0</td>
        </tr>
        <tr>
            <td>ESPORTSTMNT01_2690210</td>
            <td>complete</td>
            <td>NaN</td>
            <td>LCKC</td>
            <td>2022</td>
            <td>Spring</td>
            <td>0</td>
            <td>2022-01-10 07:44:08</td>
            <td>1</td>
            <td>12.01</td>
            <td>3971.0</td>
            <td>97.0</td>
            <td>7.0</td>
        </tr>
        <tr>
            <td>ESPORTSTMNT01_2690219</td>
            <td>complete</td>
            <td>NaN</td>
            <td>LCKC</td>
            <td>2022</td>
            <td>Spring</td>
            <td>0</td>
            <td>2022-01-10 08:38:24</td>
            <td>1</td>
            <td>12.01</td>
            <td>-7746.0</td>
            <td>-33.0</td>
            <td>1.0</td>
        </tr>
        <tr>
            <td>ESPORTSTMNT01_2690219</td>
            <td>complete</td>
            <td>NaN</td>
            <td>LCKC</td>
            <td>2022</td>
            <td>Spring</td>
            <td>0</td>
            <td>2022-01-10 08:38:24</td>
            <td>1</td>
            <td>12.01</td>
            <td>7746.0</td>
            <td>33.0</td>
            <td>8.0</td>
        </tr>
        <tr>
            <td>8401-8401_game_1</td>
            <td>partial</td>
            <td><a href="https://lpl.qq.com/es/stats.shtml?bmid=8401">Link</a></td>
            <td>LPL</td>
            <td>2022</td>
            <td>Spring</td>
            <td>0</td>
            <td>2022-01-10 09:24:26</td>
            <td>1</td>
            <td>12.01</td>
            <td>NaN</td>
            <td>NaN</td>
            <td>NaN</td>
        </tr>
    </tbody>
</table>

<div style="text-align: left;">
    <h3>Univariate Analysis</h3>
    <p>The following plot shows the distribution of dragons secured in professional League of Legends matches:</p>
</div>
<iframe 
        src="assets/dragons_plot.html" 
        width="800" 
        height="600" 
        frameborder="0" 
        style="border: none;">
</iframe>
