# Purpose
Present XML source code of the MemberOf dashboard, which breaks down the more descriptive user account attributes of users scored and with these risks.  Future auditors may replace the '|inputlookup file.csv' value with a cleaned, .csv of their own.

# Source XML
<dashboard version="1.1" theme="dark">
  <label>MemberOf</label>
  <description>Descriptive attributes of users scored as Privileged, Domain Admin, or Enterprise Admin (see bottom table for accounts with null values)</description>
  <row>
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
        <option name="colorMode">block</option>
        <option name="drilldown">none</option>
        <option name="rangeColors">["0x53a051","0x0877a6","0xf8be34","0xf1813f","0xdc4e41"]</option>
        <option name="useColors">1</option>
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
        <option name="colorMode">block</option>
        <option name="drilldown">none</option>
        <option name="rangeColors">["0x118832","0xcba700","0xf8be34","0xf1813f","0xdc4e41"]</option>
        <option name="useColors">1</option>
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
        <option name="colorMode">block</option>
        <option name="drilldown">none</option>
        <option name="rangeColors">["0x1182f3","0x1182f3","0xf8be34","0xf1813f","0xdc4e41"]</option>
        <option name="useColors">1</option>
      </single>
    </panel>
  </row>
  <row>
    <panel>
      <table>
        <title>Privleged 'Title' attribute count</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Privleged=1
| fillnull value=" " Title
| stats count by Title
| fields - values(identity)
| sort by - count
| replace " " with "null"</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="count">4</option>
        <option name="dataOverlayMode">heatmap</option>
        <option name="drilldown">none</option>
        <option name="totalsRow">true</option>
        <format type="color" field="count">
          <colorPalette type="minMidMax" maxColor="#D41F1F" minColor="#FFFFFF"></colorPalette>
          <scale type="minMidMax"></scale>
        </format>
      </table>
    </panel>
    <panel>
      <table>
        <title>Domain Admins 'Title' attribute count</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Domain_Admin=1
| fillnull value=" " Title
| stats count by Title
| fields - values(identity)
| sort by - count
| replace " " with "null"</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="count">4</option>
        <option name="dataOverlayMode">heatmap</option>
        <option name="drilldown">none</option>
        <format type="color" field="count">
          <colorPalette type="minMidMax" maxColor="#CBA700" minColor="#FFFFFF"></colorPalette>
          <scale type="minMidMax"></scale>
        </format>
      </table>
    </panel>
    <panel>
      <table>
        <title>Enterprise Admins 'Title' attribute count</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Enterprise_Admin=1
| fillnull value=" " Title
| stats count by Title
| fields - values(identity)
| sort by - count
| replace " " with "null"</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="count">4</option>
        <option name="dataOverlayMode">heatmap</option>
        <option name="drilldown">none</option>
        <format type="color" field="count">
          <colorPalette type="minMidMax" maxColor="#1182F3" minColor="#FFFFFF"></colorPalette>
          <scale type="minMidMax"></scale>
        </format>
      </table>
    </panel>
  </row>
  <row>
    <panel>
      <table>
        <title>Privileged 'Department' attribute count</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Privleged=1
| fillnull value=" " Department
| stats count by Department
| fields - values(identity)
| replace " " with "null"
| sort by - count</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="count">4</option>
        <option name="dataOverlayMode">heatmap</option>
        <option name="drilldown">none</option>
        <option name="refresh.display">progressbar</option>
        <option name="rowNumbers">false</option>
        <format type="color" field="count">
          <colorPalette type="minMidMax" maxColor="#D41F1F" minColor="#FFFFFF"></colorPalette>
          <scale type="minMidMax"></scale>
        </format>
      </table>
    </panel>
    <panel>
      <table>
        <title>Domain Admins 'Department' attribute count</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Domain_Admin=1
| fillnull value=" " Department
| stats count by Department
| fields - values(identity)
| sort by - count
| replace " " with "null"</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="dataOverlayMode">heatmap</option>
        <option name="drilldown">none</option>
        <format type="color" field="count">
          <colorPalette type="minMidMax" maxColor="#CBA700" minColor="#FFFFFF"></colorPalette>
          <scale type="minMidMax"></scale>
        </format>
      </table>
    </panel>
    <panel>
      <table>
        <title>Enterprise Admins 'Department' attribute count</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Enterprise_Admin=1
| fillnull value=" " Department
| stats count by Department
| fields - values(identity)
| sort by - count
| replace " " with "null"</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="dataOverlayMode">heatmap</option>
        <option name="drilldown">none</option>
        <format type="color" field="count">
          <colorPalette type="minMidMax" maxColor="#1182F3" minColor="#FFFFFF"></colorPalette>
          <scale type="minMidMax"></scale>
        </format>
      </table>
    </panel>
  </row>
  <row>
    <panel>
      <table>
        <title>Priviliged 'Office' attribute count</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Privleged=1
| fillnull value=" " Office
| stats count by Office
| fields - values(identity)
| sort by - count
| replace " " with "null"</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="count">4</option>
        <option name="dataOverlayMode">heatmap</option>
        <option name="drilldown">none</option>
        <format type="color" field="count">
          <colorPalette type="minMidMax" maxColor="#D41F1F" midColor="#FFFFFF" minColor="#FFFFFF"></colorPalette>
          <scale type="minMidMax" midValue="30.5"></scale>
        </format>
      </table>
    </panel>
    <panel>
      <table>
        <title>Domain Admins Office</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Domain_Admin=1
| fillnull value=" " Office
| stats count by Office
| fields - values(identity)
| sort by - count
| replace " " with "null"</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="drilldown">none</option>
        <format type="color" field="count">
          <colorPalette type="minMidMax" maxColor="#CBA700" minColor="#FFFFFF"></colorPalette>
          <scale type="minMidMax"></scale>
        </format>
      </table>
    </panel>
    <panel>
      <table>
        <title>Enterprise Admins Office</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Enterprise_Admin=1
| fillnull value=" " Office
| stats count by Office
| fields - values(identity)
| sort by - count
| replace " " with "null"</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="drilldown">none</option>
        <format type="color" field="count">
          <colorPalette type="minMidMax" maxColor="#1182F3" minColor="#FFFFFF"></colorPalette>
          <scale type="minMidMax"></scale>
        </format>
      </table>
    </panel>
  </row>
  <row>
    <panel>
      <table>
        <title>Priviliged 'Description' attribute count</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Privleged=1
| fillnull value=" " Description
| stats count by Description
| fields - values(identity)
| sort by - count
| replace " " with "null"</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="count">4</option>
        <option name="dataOverlayMode">heatmap</option>
        <option name="drilldown">none</option>
        <format type="color" field="count">
          <colorPalette type="minMidMax" maxColor="#D41F1F" minColor="#FFFFFF"></colorPalette>
          <scale type="minMidMax"></scale>
        </format>
      </table>
    </panel>
    <panel>
      <table>
        <title>Domain Admins 'Description' attribute count</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Domain_Admin=1
| fillnull value=" " Description
| stats count by Description
| fields - values(identity)
| sort by - count
| replace " " with "null"</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="count">4</option>
        <option name="drilldown">none</option>
        <format type="color" field="count">
          <colorPalette type="minMidMax" maxColor="#CBA700" minColor="#FFFFFF"></colorPalette>
          <scale type="minMidMax"></scale>
        </format>
      </table>
    </panel>
    <panel>
      <table>
        <title>Enterprise Admin 'Description' attribute count</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Enterprise_Admin=1
| fillnull value=" " Description
| stats count by Description
| fields - values(identity)
| sort by - count
| replace " " with "null"</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="count">4</option>
        <option name="dataOverlayMode">heatmap</option>
        <option name="drilldown">none</option>
        <format type="color" field="count">
          <colorPalette type="minMidMax" maxColor="#1182F3" minColor="#FFFFFF"></colorPalette>
          <scale type="minMidMax"></scale>
        </format>
      </table>
    </panel>
  </row>
  <row>
    <panel>
      <table>
        <title>Privileged 'Company' attribute count</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Privleged=1
| fillnull value=" " Company
| stats count by Company
| fields - values(identity)
| sort by - count
| replace " " with "null"</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="count">4</option>
        <option name="dataOverlayMode">heatmap</option>
        <option name="drilldown">none</option>
        <format type="color" field="count">
          <colorPalette type="minMidMax" maxColor="#D41F1F" minColor="#FFFFFF"></colorPalette>
          <scale type="minMidMax"></scale>
        </format>
      </table>
    </panel>
    <panel>
      <table>
        <title>Domain Admins 'Company' attribute count</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Domain_Admin=1
| fillnull value=" " Company
| stats count by Company
| fields - values(identity)
| sort by - count
| replace " " with "null"</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="count">4</option>
        <option name="dataOverlayMode">heatmap</option>
        <option name="drilldown">none</option>
        <format type="color" field="count">
          <colorPalette type="minMidMax" maxColor="#CBA700" minColor="#FFFFFF"></colorPalette>
          <scale type="minMidMax"></scale>
        </format>
      </table>
    </panel>
    <panel>
      <table>
        <title>Enterprise Admins 'Company' attribute count</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Enterprise_Admin=1
| fillnull value=" " Company
| stats count by Company
| fields - values(identity)
| sort by - count
| replace " " with "null"</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="count">4</option>
        <option name="dataOverlayMode">heatmap</option>
        <option name="drilldown">none</option>
        <format type="color" field="count">
          <colorPalette type="minMidMax" maxColor="#1182F3" minColor="#FFFFFF"></colorPalette>
          <scale type="minMidMax"></scale>
        </format>
      </table>
    </panel>
  </row>
  <row>
    <panel>
      <table>
        <title>Privileged 'Manager' attribute count</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Privleged=1
| fillnull value=" " Manager
| stats count by Manager
| fields - values(identity)
| sort by - count
| replace " " with "null"</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="count">4</option>
        <option name="dataOverlayMode">heatmap</option>
        <option name="drilldown">none</option>
        <format type="color" field="count">
          <colorPalette type="minMidMax" maxColor="#D41F1F" minColor="#FFFFFF"></colorPalette>
          <scale type="minMidMax"></scale>
        </format>
      </table>
    </panel>
    <panel>
      <table>
        <title>Domain Admins 'Manager' attribute count</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Domain_Admin=1
| fillnull value=" " Manager
| stats count by Manager
| fields - values(identity)
| sort by - count
| replace " " with "null"</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="count">4</option>
        <option name="dataOverlayMode">heatmap</option>
        <option name="drilldown">none</option>
        <format type="color" field="count">
          <colorPalette type="minMidMax" maxColor="#CBA700" minColor="#FFFFFF"></colorPalette>
          <scale type="minMidMax"></scale>
        </format>
      </table>
    </panel>
    <panel>
      <table>
        <title>Enterprise 'Admins' attribute count</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Enterprise_Admin=1
| fillnull value=" " Manager
| stats count by Manager
| fields - values(identity)
| sort by - count
| replace " " with "null"</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="count">4</option>
        <option name="dataOverlayMode">heatmap</option>
        <option name="drilldown">none</option>
        <format type="color" field="count">
          <colorPalette type="minMidMax" maxColor="#1182F3" minColor="#FFFFFF"></colorPalette>
          <scale type="minMidMax"></scale>
        </format>
      </table>
    </panel>
  </row>
  <row>
    <panel>
      <table>
        <title>identities with null details</title>
        <search>
          <query>| inputlookup Denton_AD_Final_Set.csv
| search RS_Enterprise_Admin=1 OR RS_Domain_Admin=1 OR RS_Privleged=1
| fillnull value="null" Manager
| fillnull value="null" Title
| fillnull value="null" Office
| fillnull value="null" Department
| fillnull value="null" Company
| fillnull value="null" Description
| search Manager="null" AND Title="null" AND Office="null" AND Department="null" AND Company="null" AND Description="null"
| table 
identity
DisplayName
RS_Enterprise_Admin
RS_Domain_Admin
RS_Privleged
Title
Office
Department
Description
Company
Manager</query>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </search>
        <option name="drilldown">none</option>
        <option name="refresh.display">progressbar</option>
        <format type="color" field="RS_Privleged">
          <colorPalette type="map">{"1":#D41F1F}</colorPalette>
        </format>
        <format type="color" field="RS_Domain_Admin">
          <colorPalette type="map">{"1":#D41F1F}</colorPalette>
        </format>
      </table>
    </panel>
  </row>
</dashboard>
