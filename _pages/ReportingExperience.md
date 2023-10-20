---
title: Reporting Experience
author: Krishna Tyagi & George Kovanis
date: 2023-10-20
layout: post
---

<script>
    function update(){them = Array.from(document.querySelectorAll("input")).reduce((acc, input) => ({...acc, [input.id + "_out"] : input.value}),{});
	Object.entries(them).forEach((entry) => {
    Array.from(document.getElementsByClassName(entry[0])).forEach((element,index) => 
    {
      console.log(document.getElementsByClassName(entry[0])[index].innerHTML); 
      document.getElementsByClassName(entry[0])[index].innerHTML = entry[1];
    })})

  event.preventDefault()
   if(document.forms["attendee-form"][1].value != "Your Attendee ID"){
    localStorage.setItem("attendeeID",document.forms["attendee-form"][1].value)
  }  
  }
</script>

# Table of Contents

| Topic                                                                             | Type          | Dificulty    | Time   |
| --------------------------------------------------------------------------------- | ------------- | ------------ | ------ |
| [Part 0: Overview of the Reporting Lab](#overview-of-the-reporting-lab)           | Exploration   | EASY         | 5 min  |
| [Objectives](#objectives)                                                         | Activity      | EASY         | 5 min  |
| [Pre-Requisities](#pre-requisites)                                                | Activity      | EASY         | 5 min  |
| [Desktop Login Process](#desktop-login-process)                                   | Activity      | EASY         | 5 min  |
| [Part 1: Agent Desktop Experience](#agent-desktop-overview)                       | Exploration   | EASY         | 5 min  |
| [1.1: Make an Inbound Call](#desktop-login-process)                               | Activity      | EASY         | 5 min  |
| [1.2: Make an Outdial Call]()                                                     | Activity      | EASY         | 5 min  |
| [1.2: Extend the Agent Desktop Experience](#desktop-administration)               | Activity      | INTERMEDIATE | 10 min |
| [1.2: Desktop Administration](#desktop-administration)                            | Exploration   | INTERMEDIATE | 10 min |
| [Part 2: Supervisor Experience](#supervisor-experience)                           | Exploration   | EASY         | 5 min  |
| [2.1: Exploring Supervisor Roles](#supervisor-experience)                         | Exploration   | EASY         | 5 min  |
| [2.2: Team Performance - Team Messaging - Changing State](#supervisor-experience) | Exploration   | EASY         | 10 min |
| [2.3: Quality Management Recordings](#supervisor-experience)                      | Exploration   | EASY         | 5 min  |
| [2.4: Supervisor Administration](#supervisor-administration)                      | Practical Lab | INTERMEDIATE | 10 min |
| [2.5: Supervisor Licensing](#supervisor-licensing)                                | Practical Lab | EASY         | 5 min  |
| [BONUS: Customizations & Programmability](#custom-desktop)                        | Practical Lab | ADVANCED     | 30 min |

# Overview of the Reporting Lab

This lab will provide you with foundational and advanced knowledge of **Webex Contact Center Data and Analytics**. You will learn about the key contact center personas and how Analyzer helps them extract key business and operational KPIs, along with actionable insights, to measure contact center efficiency, agent performance, and customer experience. The lab will guide you through the usage of the **Webex Contact Center Analyzer**, which serves as the main Contact Center Reporting application. You will gain an understanding of **utilizing stock reports and dashboards**, **personalizing your reporting by creating custom reports** and the available options when it comes to **extracting your data**.

## Objectives

This Lab has been split into four chapters.

1. First section **introduces you to the current Analyzer User Interface as well as the New Analyzer User Interface (Analyzer UX Refresh).**
   > Note: **Important to point out** that the New Analyzer User Interface is in **Early Access phase** and has access only to Historical Stock Reports.
2. In the second section we will look **how key Contact Center persons (Administrators, Supervisors and Contact Center Analysts) can use Analyzer to extract some key Contact Center KPIs and actionable insights around Contact Center Operational Performance, Customer Experience and Agent Performance using the various Stock reports and dashboards.**
3. In the third section we will walk through how we can **create custom reports and dashboards to extract key Contact Center data insights**.
4. Last chapter covers key data and reporting capabilities like the **export of reporting data, report scheduling and the available Data APIs** to extract the data.

## Pre-Requisites

1. Ensure that you have received your tenant login credentials from the Lab proctors.
2. Make sure you are able to login into Administrator Portal & Analyzer.
3. For this Lab, Part 1 and 2 already have historical data created to capture the key insights.
4. In Part 3, we will look into some Realtime data insights for which make sure you can login your agent and make a call according to the steps below.

**You Will Need**

1. **One additional device** (like your personal phone) to test inbound calls to the Webex Contact Center. You can use your cell phone for this purpose.

- Administrator credentials for the Control Hub: [admin.webex.com](https://admin.webex.com).
- Agent Login Credentials for the Agent Desktop: [desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com).

1. The items listed below have been pre-configured for you:

- Agent and Supervisor user accounts are configured and ready for logins.
- You can access the Agent Desktop via the URL: [https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com).
- As an agent, you're associated with two teams—designated by your Attendee ID—as "Team1" and "Team2".

Example:

> If your attendee ID is 100:
>
> 100_Team1
>
> 100_Team2

1. Agents will use browsers for voice calls using WebRTC (Web Real-time Communication) endpoints. Additionally, Webex Calling extensions have been assigned to users (both agents and supervisors) to facilitate alternate device experiences. Webex Contact Center agents and supervisors can opt for any mix of these devices, encompassing PSTN endpoints and mobile phones.

2. A preset inbound Voice flow is available for test calls.

## Lab Configuration

> Please submit the form below with your Attendee ID. All configuration items in the lab guide will be renamed with that prefix.

<div class="alert"></div>
<form id="attendee-form">
      <label for="attendee-id">Attendee ID</label>
      <input type="text" name="attendee-id" id="attendee-id" onChange="update()"/>
      <button onclick="update()">SAVE</button>
      
</form>
<script src="/assets/gitbook/form.js"></script>

<script>
document.forms["attendee-form"][1].value = localStorage.getItem("attendeeID") || "Your Attendee ID" 
update()
</script>

The following Administration entities have been configured for you via [Webex Control Hub](https://admin.webex.com){:target="\_blank"}

Please note, that to proceed to the next section, you will need to use the accounts shown in the top 3 rows.

| **Entity**    | **Name**                                                              |
| ------------- | --------------------------------------------------------------------- |
| Agent 1       | wxcclabs+agent_ID<w class = "attendee-class">attendeeID</w>@gmail.com |
| Supervisor 1  | wxcclabs+supvr_ID<w class = "attendee-class">attendeeID</w>@gmail.com |
| Administrator | wxcclabs+admin_ID<w class = "attendee-class">attendeeID</w>@gmail.com |

## Desktop Login Process

- To Login to the Agent Desktop, launch Google Chrome and navigate to the URL: [https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com).

> **Note: Please use Google Chrome as the browser to take advantage of the all new WebRTC Voice Option.**

> Tip: You can also find this link under Control Hub: [admin.webex.com](https://admin.webex.com) > Contact Center > Settings.

- Once you're in the login page, enter the agent credentials (username and password).

> In this example, please use the specific login for your attendee ID, as per above.

![agent-desktop](/assets/images/agent/01-image.png)

![agent-desktop](/assets/images/agent/02-image.png)

- This is the station Login Screen. Agents may input the number where they need to receive incoming and outdial calls.

> We will use the new feature of Desktop telephony that uses the browser as a device to directly receive calls.

- Notice that the voice option defaults to "Desktop".

- Select Team1 from the list. Agents can belong to multiple teams, but they can only receive calls of 1 specific team. Your agent is configured for 2 teams.

- Check the **Remember My Credentials** box to save your credentials for future sign-ins.

- Click Sign in to be connected to telephony and complete the login process.

![agent-desktop](/assets/images/agent/03-image.png)

> NOTE: Agents cannot access the Agent Desktop from multiple browsers or multiple tabs of the same browser window. In that case, a warning message will be displayed.

![agent-desktop](/assets/images/agent/04-image.png)

> The video below shows a demo about the agent login process and the available options:

![agent-desktop](/assets/images/agent/AgentLogin.gif)

---

**NOTE:**

> The login device and DN can be enforced on the Desktop Profile as follows:

- If your administrator configures the default Dial Number (DN), the default DN is prepopulated in the Dial Number and Extension fields.
- If your administrator restricts the DN to the default DN, you cannot edit the prepopulated DN when signing in to the Agent Desktop.

- Users can choose between Dial Number or Extension or Desktop.

  - Extension: Just in case the agent is using Webex Calling or some other softphone as calling endpoint

  - Dial Number: E.164 format phone number
    - If you check the **International Dialing Format** box, you can choose the country code based on your geographical location from the drop-down list. You can also enter a country code or country name to filter the list. Dial numbers are validated based on the country code
