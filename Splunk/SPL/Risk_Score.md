For easy reference, this SPL calculates the Risk_Score of all 13,800 identities with their individual 'RS' scores.  

| inputlookup Denton_AD_Final_Set.csv
| stats count values(identity) by Risk_Score, RS_Enabled, RS_Privleged, RS_Email, RS_Logon_Status, RS_Pwd_Status, RS_Enterprise_Admin, RS_Domain_Admin
| table count, RS_Enabled, RS_Privleged, RS_Email, RS_Logon_Status, RS_Pwd_Status, RS_Enterprise_Admin, RS_Domain_Admin, Risk_Score
| fields - values(identity)
| sort by -Risk_Score, count
| rename count as Users
