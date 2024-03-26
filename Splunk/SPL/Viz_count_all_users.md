# Purpose

Single value count of all Denton users

# Query

| inputlookup Denton_AD_Final_Set.csv
| stats count
