# Purpose
Present XML source code of the Risk Score dashboard.  Future auditors may replace the '|inputlookup file.csv' value with a cleaned, .csv of their own.

# Source Code
<dashboard version="1.1" theme="dark">
  <label>Risk Scores</label>
  <description>Overall Risk Score calculation for the 7 risk categories analyzed</description>
  <row>
    <panel>
      <title>All Users</title>
      <single>
        <title>All Denton Users</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| stats count</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="drilldown">all</option>
        <drilldown>
          <link target="_blank">search?q=%7C%20inputlookup%20Denton_AD_Final_Set.csv%0A%7C%20table%0Aidentity%0ADisplayName%0ATitle%0AOffice%0ADepartment%0ADescription%0ACompany%0AManager%0AMemberOf%0A%7C%20sort%20by%20identity&amp;earliest=-24h@h&amp;latest=now</link>
        </drilldown>
      </single>
    </panel>
    <panel>
      <title>Privileged</title>
      <single>
        <title>Users who are Privileged (adminCount=1)</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Privleged=1
| stats count</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="drilldown">all</option>
        <option name="refresh.display">progressbar</option>
        <drilldown>
          <link target="_blank">search?q=%7C%20inputlookup%20Denton_AD_Final_Set.csv%0A%7C%20search%20RS_Privleged%3D1%0A%7C%20table%0Aidentity%0ADisplayName%0ATitle%0AOffice%0ADepartment%0ADescription%0ACompany%0AManager%0AMemberOf%0A%7C%20sort%20by%20identity&amp;earliest=-24h@h&amp;latest=now</link>
        </drilldown>
      </single>
    </panel>
    <panel>
      <title>Domain Admins</title>
      <single>
        <title>Users who are MemberOf the Domain Admins AD group</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Domain_Admin=1
| stats count</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="drilldown">all</option>
        <drilldown>
          <link target="_blank">search?q=%7C%20inputlookup%20Denton_AD_Final_Set.csv%0A%7C%20search%20RS_Domain_Admin%3D1%0A%7C%20table%0Aidentity%0ADisplayName%0ATitle%0AOffice%0ADepartment%0ADescription%0ACompany%0AManager%0AMemberOf%0A%7C%20sort%20by%20identity&amp;earliest=-24h@h&amp;latest=now</link>
        </drilldown>
      </single>
    </panel>
    <panel>
      <title>Enterprise Admins</title>
      <single>
        <title>Users who are MemberOf the Enterprise Admins AD group</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Enterprise_Admin=1
| stats count</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="drilldown">all</option>
        <drilldown>
          <link target="_blank">search?q=%7C%20inputlookup%20Denton_AD_Final_Set.csv%0A%7C%20search%20RS_Enterprise_Admin%3D1%0A%7C%20table%0Aidentity%0ADisplayName%0ATitle%0AOffice%0ADepartment%0ADescription%0ACompany%0AManager%0AMemberOf%0A%7C%20sort%20by%20identity&amp;earliest=-24h@h&amp;latest=now</link>
        </drilldown>
      </single>
    </panel>
  </row>
  <row>
    <panel>
      <chart>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| chart count values(identity) by Risk_Score
| eval Risk_Score=Risk_Score." points"</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="charting.axisY.scale">linear</option>
        <option name="charting.chart">area</option>
        <option name="charting.chart.nullValueMode">gaps</option>
        <option name="charting.chart.showDataLabels">all</option>
        <option name="charting.chart.sliceCollapsingThreshold">0.0001</option>
        <option name="charting.chart.stackMode">default</option>
        <option name="charting.drilldown">none</option>
        <option name="charting.layout.splitSeries">0</option>
        <option name="charting.legend.placement">none</option>
        <option name="refresh.display">progressbar</option>
      </chart>
    </panel>
    <panel>
      <table>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| eval RS_Enabled="Whether account is enabled and can access Denton.com"	
| eval RS_Privleged = "Whether account is classified with privileged AD access"
| eval RS_Email = "Whether account is provisioned with a Microsoft Email"
| eval RS_Logon_Status	= "Whether account has successfully logged in the last -90d"
| eval RS_Pwd_Status = "Whether account has reset their pwd in the last -90d"
| eval RS_Enterprise_Admin	="Whether account is MemberOf the Enterprise Admin AD group"
| eval RS_Domain_Admin = "Whether account is MemberOf the Domain Admin AD group"
| table RS_Enabled	RS_Privleged	RS_Email	RS_Logon_Status	RS_Pwd_Status	RS_Enterprise_Admin	RS_Domain_Admin
| head 1
| transpose
| rename column as Metric, "row 1" as Description</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="drilldown">none</option>
      </table>
    </panel>
    <panel>
      <chart>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| chart count values(identity) by Risk_Score
| eval Risk_Score=Risk_Score." points"</query>
          <earliest>@d</earliest>
          <latest>now</latest>
        </search>
        <option name="charting.chart">pie</option>
        <option name="charting.drilldown">none</option>
      </chart>
    </panel>
  </row>
  <row>
    <panel>
      <title>Risk Score</title>
      <table>
        <title>Risk Score</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv 
| stats count values(identity) by Risk_Score, RS_Enabled, RS_Privleged, RS_Email, RS_Logon_Status, RS_Pwd_Status, RS_Enterprise_Admin, RS_Domain_Admin 
| table Risk_Score,count, RS_Enabled, RS_Privleged, RS_Email, RS_Logon_Status, RS_Pwd_Status, RS_Enterprise_Admin, RS_Domain_Admin, 
| fields - values(identity) 
| sort by -Risk_Score, count 
| rename count as Users</query>
          <earliest>@d</earliest>
          <latest>now</latest>
        </search>
        <option name="count">40</option>
        <option name="dataOverlayMode">none</option>
        <option name="drilldown">none</option>
        <option name="percentagesRow">false</option>
        <option name="rowNumbers">false</option>
        <option name="totalsRow">false</option>
        <format type="color" field="Risk_Score">
          <colorPalette type="list">[#118832,#CBA700,#D94E17,#D41F1F,#D41F1F]</colorPalette>
          <scale type="threshold">3,5,6,100</scale>
        </format>
        <format type="color" field="RS_Enabled">
          <colorPalette type="map">{"1":#D41F1F}</colorPalette>
        </format>
        <format type="color" field="RS_Privleged">
          <colorPalette type="map">{"1":#D41F1F}</colorPalette>
        </format>
        <format type="color" field="RS_Email">
          <colorPalette type="map">{"1":#D41F1F}</colorPalette>
        </format>
        <format type="color" field="RS_Logon_Status">
          <colorPalette type="map">{"2":#9E2520}</colorPalette>
        </format>
        <format type="color" field="RS_Pwd_Status">
          <colorPalette type="map">{"2":#9E2520}</colorPalette>
        </format>
        <format type="color" field="RS_Enterprise_Admin">
          <colorPalette type="map">{"1":#D41F1F}</colorPalette>
        </format>
        <format type="color" field="RS_Domain_Admin">
          <colorPalette type="map">{"1":#D41F1F}</colorPalette>
        </format>
        <format type="color" field="Users">
          <colorPalette type="minMidMax" maxColor="#D41F1F" minColor="#FFFFFF"></colorPalette>
          <scale type="minMidMax"></scale>
        </format>
      </table>
    </panel>
  </row>
</dashboard>
