# Purpose

Best represented in circle graph.  Shows the number of users of each overall 'Risk_Score' of 5 - 13 points

# Query

| inputlookup Denton_AD_Final_Set.csv
| stats count values(identity) by Risk_Score
| fields - values(identity)
| sort by -Risk_Score, count
| rename count as Users
