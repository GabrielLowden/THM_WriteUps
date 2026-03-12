# Challenge Write-Up: <Introduction to Phishing>

## Platform / Event
<TryHackMe SOC Simulator>

## Difficulty
<Easy>

## Date Completed
<2026-03-11>

---

# 1. Objective

"
- Monitor and analyze real-time alerts
- Identify and document critical events such as suspicious emails and attachments
- Create detailed case reports based on your observations to help your team understand the full scope of alerts and malicious activity
"

---

# 2. Challenge Description

"Learn how to use SOC Simulator by completing your first scenario. Close all True Positive alerts to pass!"

---

# 3. Files / Artifacts Provided

- Alert queue
- Access to Elastic SIEM Tool


---

# 4. Initial Recon / Observations

## First look at the SOC Sim Dashboard.
![Dashboard.png did not load](/IntroductionToPhishing/screenshots/dashboard.png)
- 4 Alerts entered the queue at sparatic times over the course of the simulation

## First Alert == ID 8814
![alertqueue.png did not load](/IntroductionToPhishing/screenshots/alert-queue.png)
- The rule triggered from an external link inside an inbound email
- The rule description gives good direction by suggesting to investigate whether the links were clicked or not
- The alert gives us the email content & inside the link: [<a href="https://hrconnex.thm/onboarding/15400654060/j.garcia">Set Up My Profile</a>]
    - VirusTotal & DNSDumpster tell us the domain is invalid...it was made up for the scenario

## For Reference
![datasources.png not loaded](/IntroductionToPhishing/screenshots/datasources.png)
- As alerts come in it is good to know they will come from either firewall logs or email logs
- And that there is 87 unique documents to sift through

---

# 5. Analysis

## ID 8814

Steps I took:
+ Review firewall logs for web-browsing to URL inside alert
    + KQL Query [datasource : "firewall" and URL : "https://hrconnex.thm/onboarding/15400654060/j.garcia"]
    + This gave no results...the user (and other users) did not click the link --> close case
+ Duediligence
    + KQL Query [sender: "onboarding@hrconnex.thm"]
        + 2 emails total from this sender to the same recipient
Conclusion:
+ Close Case and report as False Positive

## ID 8815

![alert8815.png did not load](/IntroductionToPhishing/screenshots/alert8815.png)
Steps Taken:
+ Review firewall logs for web-browsing to URL inside alert
    + KQL Query [datasource : "firewall" and URL: "http://bit.ly/3sHkX3da12340"]
    ![firewallBlock8815.png did not load](/IntroductionToPhishing/screenshots/firewallBlock8815.png)
    + User clicked link, but was blocked by firewall --> User Awareness Training... 
    + Only 1 result from firewall, so no other user clicked link
Conclusion:
+ Close case and report as True Positive

## ID 8816

![alert8816.png did not load](/IntroductionToPhishing/screenshots/alert8816.png)
Steps Taken:
+ Recognise this is related to ID 8815 --> same URL, source/destinations IPs, ports, etc
    + Already know that this alert is a True positive from previous alert 8815
Conclusion:
+ Close case and report as True Positive

## ID 8817

![alert8817.png did not load](/IntroductionToPhishing/screenshots/alert8817.png)
Steps Taken:
+ Review firewall logs for web-browsing to URL inside alert
    + KQL Query: [datasource : "firewall" and URL: "https://m1crosoftsupport.co/login"]
    + The user clicked the link and the website was not blocked! --> Investigate website/URL/IP more
        + Use Virus Total to check reputation...
        ![maliciousIP.png did not load](/IntroductionToPhishing/screenshots/maliciousIP.png)
        + **The user clicked a link that is malicious!**
        
Conclusion:
+ Close case and report as True Positive

## ID 8818

![alert8818.png did not load](/IntroductionToPhishing/screenshots/alert8818.png)
Steps Taken:
+ Because I did my duediligence in analysis of alert 8814, I know that the email was sent twice.
    + Our rules just alerted again for a repeated email
Conclusion:
+ Close case and report as False Positive

---

# Stats/Results

## ID 8814 - Correct
Answer: False Positive
My Submission: False Positive
## ID 8815 - Incorrect
Answer: False Positive
My Submission: True Positive
## ID 8816 - Correct
Answer: True Positive
My Submission: True Positive
## ID 8817 - Correct
Answer: True Positive
My Submission: True Positive
## ID 8818 - Correct
Answer: False Positive
My Submission: False Positive

# Other Opinions/Observations
+ In a real world scenario some proactive measures to take not available in the sim:
    + Use VirusTotal & DNSDumpster (Some links/domains were not real)
    + Review Email headers for possible spoofing
    + Update a blocklist as malicious IPs/emails/URLs are identified
    + Microsoft has a safelink feature 
+ I did not prioritize by severity....