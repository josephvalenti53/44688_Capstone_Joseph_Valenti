# 44688 Capstone Joseph Valenti

# Welcome! 

Hello, my name is Joseph Valenti, I'm a cybersecurity analyst specializing in Identity & Access Management (IAM), Privileged Access Management (PAM), and Vulnerability Management.  I have a strong love of Splunk, creating my own connections to databases, simply all things manipulating data aka the fifth form of matter!

# Purpose: 

This repository aims to assist cybersecurity analysts, identity management admins, and others affiliated in the domain of cybersecurity governance with a streamlined, automated approach to collecting data on their organization's greatest asset, (and greatest risk), their Employees! (and nonemployee contractors)

We will be exploring a single, fictitious company named Denton Insurance, specifically the account security and vulnerabilities within the company's Microsoft Active Directory.

With a Splunk Enterprise instance, we'll evaluate, hunt in the SPL (search/splunk processing language), and create dashboards helpful to executive staff in remediating identity based vulnerabilities, the vulnerabilities discussed include:

- Enabled Users with a password older than 90 days
- Enabled Privileged Users that have not logged in the domain the last 90 days
- Enabled Users created over one year ago and have never logged in
- Enabled Users who have access (memberOf) to Domain Admin & Enterprise Admin and drilling down into their specific vulnerabilities

# Attributes

This folder explains all AD attributes pulled for each user/identity employed at Denton Insurance.  Of these 141 initial attributes, 30 are necessary in evaluating Denton's Identity & Priviliged Access Management governance and risk.  

# Final Results

Because these rely on timestamp values, the final results are dynamic.  Therefore, after the auditor pulls their initial Active Directory user data, leverage the file 'Final_Results' to see the final tally of accounts falling into the four vulnerability metrics.  

For this particular analysis, the results of vulnerable accounts out of 13,800 is below:

- Enabled Users with a password older than 90 days: 5,241 accounts
- Enabled Privileged Users that have not logged in the domain the last 90 days: 57 accounts
- Enabled Users created over one year ago and have never logged in: 962 accounts
- Enabled Users who have access (memberOf) to Domain Admin & Enterprise Admin and drilling down into their specific vulnerabilities: 12 accounts

# Overleaf Document

https://www.overleaf.com/read/zzqpmvmrzmbc#653a71





