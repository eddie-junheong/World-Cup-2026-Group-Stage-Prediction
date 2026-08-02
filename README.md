# World-Cup-2026-Group-Stage-Prediction
This is a data analysis project aims to explore whether a team strength based on FIFA official ELO can predict football match outcomes.

With the 2026 World Cup just around the corner, I thought a fun way to celebrate would be to tackle a real-world data project and learn some new skills along the way. This project uses descriptive statistics to break down how each country performed in the group stage, calculates win probabilities using the Elo rating system, and evaluates expected goals (xG) for every group stage match. This is a personal learning project where I used Claude to help brainstorm ideas and clean up the data. I hope you enjoy it!


# 1. Get data

There is a free dataset of all of the international football matches starting way back from the very first official match to the present (1872 - 2026) and still updates till present. But for this report, only data from the 2014 to 2022 World Cup tournament will be used.

Dataset link: https://www.kaggle.com/datasets/martj42/international-football-results-from-1872-to-2017

To capture the Elo rating data, official website from FIFA is the place I visit. Using some simple python function, I can scrape through website api and got the datasets of each team Elo (update till June 10, 2026).

Dataset link: https://inside.fifa.com/fifa-world-ranking/men

# 2. Analysis

To get every group of 48 teams in the group stage. I prompted a line in Claude that process the Elo team file to generate table contains match group of 48 nations that qualified for the World Cup 2026. 

Here is the prompt:

```text
Clean the data table which pick only the nation that is qualified in the world cup 2026 and add a ELO raing column next to it
```

Here is the file returned by Claude:

...

```text
Question: Which group in the WC2026 is the hardest/easiest to compete in?
```

I calculate the mean and median ELO of each group using the "average" and "median" fomular in Excel.

| Group | Average ELO | Median ELO |
|---|---|---|
| A | 1553.31 | 1548.68 |
| B | 1511.77 | 1504.90 |
| C | 1579.35 | 1629.22 |
| D | 1590.41 | 1592.54 |
| E | 1542.48 | 1569.70 |
| F | 1600.34 | 1585.68 |
| G | 1549.94 | 1590.98 |
| H | 1585.69 | 1548.48 |
| I | 1639.62 | 1620.76 |
| J | 1608.36 | 1584.22 |
| K | 1599.42 | 1586.39 |
| L | 1606.99 | 1627.02 |

Chart

<img width="1262" height="643" alt="Image" src="https://github.com/user-attachments/assets/39ae604c-0736-4bb9-922b-9ad478c66491" />

The chart above gives some insight about mean and median ELO by each group.

- If a group with mean and median are the same,it means that means that group is ELO balance between all team in the same group (Group A, Group B,etc)
- If a group with median higher than mean, it means that there is a very low ranking team that pull the whole average ELO down (Outliners). The other three in that group is a very strong individuals.
- If a group with mean higher than median, it means that there is a very high ranking team pull the whole average ELO up. Which makes them a very high favor to qualify for the next round.

From the chart, we also see group I (France, Senegal, Norway, Iraq) is the group with the highest mean and median which means that this group is the hardest to compete in. On the other hand, group B (Switzerland, Canada, Qatar, Bosnia and Herzegovina) has the lowest ELO which makes it statistically the easiest group to compete in. 

```text
Question: Do Elo really predict the outcome of the match? Will smaller Elo team always lose to higher Elo team?
```

By using the same Elo calculation to evaluate chess Elo of these chess master.

Fomular:

```text
P(A wins) = 1 / (1 + 10^(−ΔElo / 400)) or 1/(1+10^(-(A2-B2)/400))
```
I prompted Claude to clean up the data in the results file only use 3 latest tournament of the 2014, 2018 and 2022 WC tournament. The table shows the ELO diff, goals, and the results between two competitors of the whole tournament. 

... file ***

Chart

<img width="1053" height="630" alt="Image" src="https://github.com/user-attachments/assets/8e8591da-a576-4482-b524-3c7a2cc1480e" />

By looking at this chart, we can confirm that Higher ELO team win most of the time, but the chance that lower ELO can make some magical outcome is high like in the 2018 tournament where it got up to 25% of all 64 matches. Aside from winning and losing, draw is a big factor in football. Where the drawing probabilities is approximately one in every four game which is around 25% of the time.

We can also from the table, find out and sort out the matches that the win probabilities is higher than 70% but results in a draw or upset. Using the FILTER function in Excel, I fill out the 3 tournaments within table. This is the table I got from that. 

| Date | Year | Higher ELO Team | Lower ELO Team | Higher ELO | Lower ELO | ELO Diff | Win Prob (Higher %) | Goals (Higher ELO) | Goals (Lower ELO) | Result |
|---|---|---|---|---|---|---|---|---|---|---|
| 2014-06-14 | 2014 | Uruguay | Costa Rica | 1954 | 1789 | 166 | 72.2% | 1 | 3 | Upset |
| 2014-06-17 | 2014 | Brazil | Mexico | 2162 | 1918 | 244 | 80.3% | 0 | 0 | Draw |
| 2014-06-21 | 2014 | Germany | Ghana | 2127 | 1790 | 337 | 87.4% | 2 | 2 | Draw |
| 2014-06-28 | 2014 | Brazil | Chile | 2146 | 1995 | 152 | 70.5% | 1 | 1 | Draw |
| 2014-07-05 | 2014 | Netherlands | Costa Rica | 2128 | 1875 | 253 | 81.1% | 0 | 0 | Draw |
| 2018-06-16 | 2018 | Argentina | Iceland | 2027 | 1822 | 205 | 76.5% | 1 | 1 | Draw |
| 2018-06-17 | 2018 | Germany | Mexico | 2093 | 1935 | 158 | 71.3% | 0 | 1 | Upset |
| 2018-06-17 | 2018 | Brazil | Switzerland | 2189 | 1927 | 261 | 81.8% | 1 | 1 | Draw |
| 2018-06-19 | 2018 | Colombia | Japan | 1983 | 1782 | 202 | 76.2% | 1 | 2 | Upset |
| 2018-06-25 | 2018 | Spain | Morocco | 2099 | 1787 | 313 | 85.8% | 2 | 2 | Draw |
| 2018-06-27 | 2018 | Germany | South Korea | 2069 | 1756 | 314 | 85.9% | 0 | 2 | Upset |
| 2018-07-01 | 2018 | Spain | Russia | 2082 | 1757 | 324 | 86.6% | 1 | 1 | Draw |
| 2018-07-06 | 2018 | Brazil | Belgium | 2203 | 2055 | 148 | 70.1% | 1 | 2 | Upset |
| 2018-07-07 | 2018 | Croatia | Russia | 1983 | 1771 | 212 | 77.2% | 2 | 2 | Draw |
| 2022-11-22 | 2022 | Denmark | Tunisia | 2018 | 1826 | 192 | 75.2% | 0 | 0 | Draw |
| 2022-11-22 | 2022 | Argentina | Saudi Arabia | 2173 | 1749 | 423 | 92.0% | 1 | 2 | Upset |
| 2022-11-25 | 2022 | Netherlands | Ecuador | 2109 | 1935 | 174 | 73.1% | 1 | 1 | Draw |
| 2022-11-27 | 2022 | Belgium | Morocco | 2068 | 1870 | 198 | 75.7% | 0 | 2 | Upset |
| 2022-11-28 | 2022 | South Korea | Ghana | 1893 | 1677 | 215 | 77.6% | 2 | 3 | Upset |
| 2022-11-28 | 2022 | Serbia | Cameroon | 1940 | 1707 | 233 | 79.2% | 3 | 3 | Draw |
| 2022-11-30 | 2022 | France | Tunisia | 2074 | 1811 | 263 | 81.9% | 0 | 1 | Upset |
| 2022-12-01 | 2022 | Spain | Japan | 2112 | 1898 | 213 | 77.4% | 1 | 2 | Upset |
| 2022-12-02 | 2022 | Brazil | Cameroon | 2253 | 1722 | 531 | 95.5% | 0 | 1 | Upset |
| 2022-12-02 | 2022 | Portugal | South Korea | 2091 | 1854 | 237 | 79.6% | 1 | 2 | Upset |
| 2022-12-09 | 2022 | Brazil | Croatia | 2217 | 1997 | 220 | 78.0% | 1 | 1 | Draw |

