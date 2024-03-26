# Purpose

Count of Denton users who have 'Domain Marita' in their MemberOf AD attribute

# Query

| inputlookup Denton_AD_Final_Set.csv
| search RS_Domain_Admin=1
| stats count
