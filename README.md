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
    style="border: none; margin-bottom: 20px;">
</iframe>

<p>
    Looking at the data, it seems most professional teams acquire between 2-4 dragons every game. 
    These higher numbers indicate dragon stalemates, as having any more than 4 dragons in a game would 
    mean both teams are having even fights to obtain dragons.
</p>

<iframe 
    src="assets/avg_dragons.html" 
    width="800" 
    height="600" 
    frameborder="0" 
    style="border: none; margin-top: 20px; margin-bottom: 20px;">
</iframe>

<p>
    Most leagues averaged about 2.2 dragons this season (2022). However, the highest average is in the 
    LCK, which could be telling of their strategy for prioritizing dragons compared to other teams.
</p>

<div style="text-align: left;">
    <h3>Bivariate Analysis</h3>
    <p>The following plots show the relationships between two columns in the data:</p>
</div>

<iframe 
    src="assets/vspm_v_kills.html" 
    width="800" 
    height="600" 
    frameborder="0" 
    style="border: none; margin-top: 20px; margin-bottom: 20px;">
</iframe>

<p>
    Teams with a higher VSPM tend to be more active in creating map pressure and securing kills. This correlation 
    is seen in the plot showing the importance of vision control in facilitating aggressive plays and securing objectives.
</p>

<div style="text-align: left;">
    <h3>Interesting Aggregates</h3>
    <p>The following plot show the relationship between win rate and the number of dragons secured after aggregating the data:</p>
</div>

<iframe 
    src="assets/agg_wr.html" 
    width="800" 
    height="600" 
    frameborder="0" 
    style="border: none; margin-top: 20px; margin-bottom: 20px;">
</iframe>
<p>
    After <code>groupby</code>-ing the win rate by the number of dragons secured, the analysis reveals a clear positive correlation. 
    This means that as teams secure more dragons during a match, their likelihood of winning increases significantly. 
    The positive correlation shows the importance of dragon control as a strategic objective in professional play, 
    as it provides advantages that translate into higher success rates in matches.
</p>
<div style="text-align: left;">
    <h1>Assessment of Missingness</h1>
</div>

<div style="text-align: left;">
    <h3>NMAR Analysis</h3>
</div>
<p>
    Based on the dataset, I believe that the <code>result<code/> column (indicating whether the team won or lost) is Not Missing at Random (NMAR). This means the missingness of the result     column is directly related to the outcome of the matches themselves, and the probability of a missing value is influenced by factors tied to the column's content. <code>result</code>     could be missing more often in matches that were forfeited, abandoned, or had technical issues. For instance, if a match ends prematurely, its result may not be recorded, and technical     issues have happened in professional matches before.
<p/>

<div style="text-align: left;">
    <h3>Missingness Dependency</h3>
    <p>
        The analysis aimed to determine if <code>gamelength</code> is Missing at Random (MAR) on the <code>barons</code> column, 
        based on a permutation test using the Kolmogorov-Smirnov (KS) statistic.
    </p>
    <ul>
        <li><strong>Observed KS Statistic</strong>: 0.0412</li>
        <li><strong>Permutation P-value</strong>: 0.0</li>
    </ul>
    <iframe
      src="assets/ks_dist.html"
      width="800"
      height="600"
      frameborder="0"
    ></iframe>
    <h4>Interpretation of Results</h4>
    <ul>
        <li><strong>Observed KS Statistic</strong>: 
            The KS statistic measures the difference between the distributions of <code>gamelength</code> for rows 
            where <code>barons</code> is missing versus not missing. A higher value indicates more significant differences 
            between the two distributions.
        </li>
        <li><strong>Permutation P-value</strong>: 
            The p-value quantifies the likelihood of observing a KS statistic at least as extreme as 0.0412 under the null 
            hypothesis that the missingness of <code>barons</code> is independent of <code>gamelength</code>. A p-value of 0.0 
            indicates that this result is extremely unlikely under the null hypothesis.
        </li>
    </ul>
    <h4>Conclusion</h4>
    <p>
        The <strong>p-value of 0.0</strong> suggests strong evidence to reject the null hypothesis. This implies that the missingness 
        of <code>barons</code> is not independent of <code>gamelength</code>. Therefore, <code>gamelength</code> is likely 
        <strong>MAR on `barons`</strong>, as the distribution of game length depends on whether the <code>barons</code> data is missing 
        or not.
    </p>
</div>
