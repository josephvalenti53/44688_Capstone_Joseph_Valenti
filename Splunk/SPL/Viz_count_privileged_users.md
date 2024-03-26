# Purpose

Count of Denton's privileged users where their adminCount attribute = 1
# Query

| inputlookup Denton_AD_Final_Set.csv
| search RS_Privleged=5
| stats count
