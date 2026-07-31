# World-Cup-2026-Group-Stage-Prediction
This is a data analysis project aims to explore whether a team strength based on FIFA official ELO can predict football match outcomes.

With the 2026 World Cup just around the corner, I thought a fun way to celebrate would be to tackle a real-world data project and learn some new skills along the way. This project uses descriptive statistics to break down how each country performed in the group stage, calculates win probabilities using the Elo rating system, and evaluates expected goals (xG) for every group stage match. This is a personal learning project where I used Claude to help brainstorm ideas and clean up the data. I hope you enjoy it!


# 1. Get data

There is a free dataset of all of the international football matches starting way back from the very first official match to the present (1872 - 2026) and still updates till present. But for this report, only data from the 2014 to 2022 World Cup tournament will be used.

Dataset links: https://www.kaggle.com/datasets/martj42/international-football-results-from-1872-to-2017

To capture the Elo rating data, official website from FIFA is the place I visit. Using some simple python function, I can scrape through website api and got the datasets of each team Elo (update till June 10, 2026).
