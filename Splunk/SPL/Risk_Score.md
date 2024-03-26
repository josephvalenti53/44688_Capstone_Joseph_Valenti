# Purpose
For easy reference, this SPL calculates the Risk_Score of all 13,800 identities with their individual 'RS' scores.  

http://desktop-cmiqhij:8000/en-US/app/search/report?s=%2FservicesNS%2Fnobody%2Fsearch%2Fsaved%2Fsearches%2FDenton%253A%2520User%2520Risk_Scores&sid=1711490446.991&dispatch.sample_ratio=1&display.page.search.mode=smart&workload_pool=&q=%7C%20inputlookup%20Denton_AD_Final_Set.csv%0A%7C%20stats%20count%20values(identity)%20by%20Risk_Score%2C%20RS_Enabled%2C%20RS_Privleged%2C%20RS_Email%2C%20RS_Logon_Status%2C%20RS_Pwd_Status%2C%20RS_Enterprise_Admin%2C%20RS_Domain_Admin%0A%7C%20table%20count%2C%20RS_Enabled%2C%20RS_Privleged%2C%20RS_Email%2C%20RS_Logon_Status%2C%20RS_Pwd_Status%2C%20RS_Enterprise_Admin%2C%20RS_Domain_Admin%2C%20Risk_Score%0A%7C%20fields%20-%20values(identity)%0A%7C%20sort%20by%20-Risk_Score%2C%20count%0A%7C%20rename%20count%20as%20Users&earliest=-24h%40h&latest=now

# Query
| inputlookup Denton_AD_Final_Set.csv
| stats count values(identity) by Risk_Score, RS_Enabled, RS_Privleged, RS_Email, RS_Logon_Status, RS_Pwd_Status, RS_Enterprise_Admin, RS_Domain_Admin
| table count, RS_Enabled, RS_Privleged, RS_Email, RS_Logon_Status, RS_Pwd_Status, RS_Enterprise_Admin, RS_Domain_Admin, Risk_Score
| fields - values(identity)
| sort by -Risk_Score, count
| rename count as Users
