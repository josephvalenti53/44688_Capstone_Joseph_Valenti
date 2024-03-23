# 44688 Capstone Joseph Valenti

# Welcome! 

Hello, my name is Joseph Valenti, I'm a cybersecurity analyst specializing in Identity & Access Management (IAM), Privileged Access Management (PAM), and Vulnerability Management.  I have a strong love of Splunk, creating my own connections to databases, simply all things manipulating data!  Data is only the fifth form of matter!

# Purpose: 

This repository aims to assist cybersecurity analysts, identity management admins, and others affiliated in the domain of cybersecurity governance with a streamlined, automated approach to collecting data on their organization's greatest asset, (and greatest risk), their Employees!

We will be exploring a single, fictitious company named Denton Insurance, specifically the account security and vulnerabilities within the company's Microsoft Active Directory.

With this Splunk Enterprise instance, we'll evaluate, hunt in the SPL (search processing language), and create dashboards helpful to executive staff in remediating vulnerabilities, the vulnerabilities discussed include:

- Enabled Users with a password older than 90 days
- Enabled Privileged Users that have not logged in the domain the last 90 days
- Enabled Users created over one year ago and have never logged in
- Enabled Users who have access (memberOf) to Domain Admin & Enterprise Admin and drilling down into their specific vulnerabilities

# Attributes

This folder explains all AD attributes pulled for each user/identity employed at Denton Insurance, or if a service user (non-human identity) exisiting.  Of these 141 initial attributes, 30 are necessary in evaluating Denton's Identity & Priviliged Access Management governance and risk.  

# Overleaf Document
https://www.overleaf.com/read/zzqpmvmrzmbc#653a71
