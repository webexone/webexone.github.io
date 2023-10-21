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

# Overview of the Reporting Lab

This lab will provide you with foundational and advanced knowledge of **Webex Contact Center Data and Analytics**. You will learn about the key contact center personas and how Analyzer helps them extract key business and operational KPIs, along with actionable insights, to measure contact center efficiency, agent performance, and customer experience. The lab will guide you through the usage of the **Webex Contact Center Analyzer**, which serves as the main Contact Center Reporting application. You will gain an understanding of **utilizing stock reports and dashboards**, **personalizing your reporting by creating custom reports** and the available options when it comes to **extracting your data**.

## Objectives

This Lab has been split into four chapters.

1. First part of this Lab **introduces you to the current Analyzer User Interface as well as the New Analyzer User Interface (Analyzer UX Refresh).**
   > Note: **Important to point out** that the New Analyzer User Interface is in **Early Access phase** and has access only to Historical Stock Reports.
2. In the second part we will look **how key Contact Center persons (Administrators, Supervisors and Contact Center Analysts) can use Analyzer to extract some key Contact Center KPIs and actionable insights around Contact Center Operational Performance, Customer Experience and Agent Performance using the various Stock reports and dashboards.**
3. In the third part we will look into some new data insights and walk through how we can **create custom reports and dashboards to extract some real-time  Contact Center data insights**.
4. Last chapter covers key data and reporting capabilities like the **export of reporting data, report scheduling and the available Data APIs** to extract the data.
# Table of Contents

| Topic                                                                                                                                                                    | Type        | Dificulty | Time   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------- | --------- | ------ |
| [Pre-Requisities](#pre-requisites)                                                                                                                                       | Activity    | EASY      | 5 min  |
| [Desktop Login Process](#desktop-login-process)                                                                                                                          | Activity    | EASY      | 5 min  |
| [Part 1: Webex Contact Center Analyzer User Interface](#part-1-webex-contact-center-analyzer-user-interface)                                                             | Exploration | EASY      | 5 min  |
| [1.1: Analyzer User Interface](#11-analyzer-user-interface)                                                                                                              | Activity    | EASY      | 5 min  |
| [1.2: NEW Analyzer User Interface](#12-new-analyzer-user-interface)                                                                                                      | Activity    | EASY      | 15 min  |
| [Part 2: Contact Center Insights with New Analyzer Stock reports](#part-2-contact-center-insights-with-new-analyzer-stock-reports)                                       | Exploration | EASY      | 20 min  |
| [2.1: High-level Contact Center Performance and Usage insights](#21-high-level-contact-center-performance-and-usage-insights)                                            | Exploration | EASY      | 5 min  |
| [2.2: Customer Experience and Queue Performance](#22-customer-experience-and-queue-performance)                                                                          | Exploration | EASY      | 10 min  |
| [2.3: Agent Performance](#23-agent-performance)                                                                                                                          | Exploration | EASY      | 5 min  |
| [Part 3: (BONUS) Contact Center Insights with Analyzer custom reports and Dashboards](#part-3-bonus-contact-center-insights-with-analyzer-custom-reports-and-dashboards) | Exploration | EASY      | 5 min  |
| [3.1: Realtime Contact In the Queue](#31-realtime-contact-in-the-queue)                                                                                                  | Exploration | EASY      | 10 min  |
| [3.2: Realtime Agent State](#32-realtime-agent-state)                                                                                                                    | Exploration | EASY      | 5 min  |
| [3.3: Realtime Dashboard](#33-realtime-dashboard)                                                                                                                        | Exploration | EASY      | 5 min  |
| [Part 4: (BONUS) Data extraction and scheduling Capabilities](#part-4-bonus-data-extraction-and-scheduling-capabilities)                                                 | Exploration | EASY      | 5 min  |
| [4.1: Export Data as Excel or CSV](#41-export-data-as-excel-or-csv)                                                                                                      | Exploration | EASY      | 5 min  |
| [4.2: Visualization Scheduler](#42-visualization-scheduler)                                                                                                              | Exploration | EASY      | 5 min  |
| [4.3: Search APIs](#43-search-apis)                                                                                                                                      | Exploration | EASY      | 10 min |



## Pre-Requisites

1. Ensure that you have received your tenant login credentials (Administrator, Supervisor and Agent)from the Lab proctors.
2. In this Lab, Part 1 and 2 already have historical data created to capture the key insights, hence no need to login Agent or make calls.
3. In Part 3, we will look into some Realtime data insights for which make sure you logged-in with your supervisor-agent or Agent and able to make and receive calls. 
- Agent and Supervisor user accounts are configured and ready for logins.
- As an agent, you're associated with two teams—designated by your Attendee ID—as "Team1" and "Team2".

	Example:
	
	> If your attendee ID is 100:
	>
	> 100_Team1
	>
	> 100_Team2
	
	**You Will Need**  **One additional device** (like your personal phone) to test inbound calls to the Webex Contact Center. You can use your cell phone for this purpose.

5.  A preset inbound Voice flow is available for test calls.

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

##  Analyzer  Login Process 


1.  Make sure you are able to login into Administrator Portal -  [admin.webex.com](https://admin.webex.com) using your Supervisor credentials
2. Once Logged-in Goto --> "Quick Links" --> Click "Analyzer" 
![analyzer](/assets/images/reporting/intro_CH.png)

3. For Part-3 of the Lab Login as an Supervisor-agent or Agent :

Note: If you are already logged-in as an Agent as part of other Labs, no action required. 

Login As Supervisor-Agent: 
to your agent you can use your Agent Credentials or Supervisor credentials with Role as : "Supervisor and Agent"


- Login with Supervisor Credentials   [admin.webex.com](https://admin.webex.com)
- Goto "Quick Links" --> Click "Desktop"
- Select the Role as : "Supervisor and Agent"
- Enter the Dialed number provided (If not pre-filled)
- Team should be pre-populated 
- Submit

Login as an Agent:  
- Use below link
	Agent Login Credentials for the Agent Desktop: [desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com).

	> We will use the new feature of Desktop telephony that uses the browser as a device to directly receive calls.
	
	- Notice that the voice option defaults to "Desktop".
	
	- Select Team1 from the list. Agents can belong to multiple teams, but they can only receive calls of 1 specific team. Your agent is configured for 2 teams.
	
	- Check the **Remember My Credentials** box to save your credentials for future sign-ins.
	
	- Click Sign in to be connected to telephony and complete the login process.

![agent-desktop](/assets/images/reporting/03-image.png)

> NOTE: Agents cannot access the Agent Desktop from multiple browsers or multiple tabs of the same browser window. In that case, a warning message will be displayed.

![agent-desktop](/assets/images/reporting/04-image.png)

> The video below shows a demo about the agent login process and the available options:

![agent-desktop](/assets/images/reporting/AgentLogin.gif)

---


# Part 1: Webex Contact Center Analyzer User Interface

## 1.1 Analyzer User Interface

This lab is designed to give you basic understanding of Analyzer, user interface features, access controls and permissions as well as the default dashboards available in the Admin Portal. In the following exercises, the goal is the familiarization with the product, interfaces and terminology.

1. At this point you should be already logged-in to the Analyzer

2. As you login you may see this pop-up prompting to “Explore New Analyser”.
   $${\color{red}“DO\space NOT\space LAUNCH”\space it\space at\space this\space time\space and\space Click\space `Cancel`.}$$
   ![refesh-popup](/assets/images/reporting/1_1_RefreshPopup.png)

3. Navigate around the home screen learning the different features available on this screen.

   - Make a note of sessions count for the four data repositories:
     - Customer Session
     - Customer Activity
     - Agent Session
     - Agent Activity <br>
       ![Repos](/assets/images/reporting/1_1_repos.png)

4. Click on the **Visualizations** tab on the left. <br>
   ![Visualizations](/assets/images/reporting/1_1_visualizations.png)

5. On the top in Search field, search for any key word like `agent`:

   - Click on **Agent Realtime** report and note down the path for this report. <br>
     ![Agent Path](/assets/images/reporting/1_1_agentpath.png)
   - Searched items can be further filtered to show Visualizations or Folders from the `Show` dropdown menu.
     ![Show](/assets/images/reporting/1_1_Show.png)

6. Then, navigate to the following path: <br>
   ![Path](/assets/images/reporting/1_1_path.png) <br>
   Click ![ListView](/assets/images/reporting/1_1_ListView.png) to change the view to List view.
   ![List](/assets/images/reporting/1_1_List.png)

   - Here you can sort the reports based on a specific header by clicking on it.
   - Notice the **Temporal Scope**, which can be either **Realtime, Compound** or **Historical**. (all of these will be **realtime**)
   - ID is <ins>unique</ins> for every report and a report can also be searched by its ID.

7. Click the ![Dots](/assets/images/reporting/1_1_dots.png) icon next to the report and then click on **Details**. <br>
   ![Details](/assets/images/reporting/1_1_Details.png) <br>
   ![DetailsInfo](/assets/images/reporting/1_1_DetailsInfo.png) <br>

   - Make a note of the **Date Range** and **Scheduled Jobs**.
   - Try the same for any Historical stock report. <br>

8. On the top, click on your **username** and then **Help** to open the help manual for Analyzer.

   - This provides you with an online version of the [Analyzer User Guide](https://www.cisco.com/c/en/us/td/docs/voice_ip_comm/cust_contact/contact_center/webexcc/Analyzer_2/b_analyzeronloinehelp/_b_analyzeronloinehelp_chapter_01.html), a great document that provides information about all the available <ins>stock reports</ins>, <ins>variables</ins> as well as <ins>functionalities</ins> of Analyzer.

9. Click on **Tenant Time zone** option on the header. Set it to the time-zone in which you want to Run Visualizations (**Tenant or Browser**).
   ![TimeZone](/assets/images/reporting/1_1_Timezone.png)

## 1.2 NEW Analyzer User Interface



# Part 2: Contact Center Insights with New Analyzer Stock reports

In this section, we will delve into how various personas within a contact center can leverage the Webex Contact Center Analyzer to capture Key Performance Indicators (KPIs) and glean insights that can measure and enhance customer experience, agent performance, and overall business outcomes. We will explore some of the pre-built stock reports with New Analyzer Interface, which can help you gather these key actionable insights from day one.

## 2.1 High-level Contact Center Performance and Usage insights

**Persona:** CC Administrator, Supervisors, CC Manager, Leadership
**Preferred View Type:** Chart, Trending

**Business Use Case:** Contact centre administrators play a crucial role in managing and optimizing contact centre operations. To effectively monitor and analyse the performance of the contact centre, it is essential for administrators to capture and track high-level contact centre state and usage data. This data provides valuable insights into various aspects, such as agent productivity, call volumes, customer satisfaction, and system performance. By capturing this information, administrators can make informed decisions, identify areas for improvement, and ensure efficient contact centre operations.

**A. Expected Insights and Actions:** Monthly trending of total inbound and outbound contacts over this year. Secondly, the usage of different communication channels, such as phone calls, emails, live chat, and social media interactions.

### Contact Center Overview – Historical

Search for the lable `Contact center Overview` and double click `Contact Center Overview – Historical` dashboard.

1. Make a note of: Average service level, Total handle contact, Total abandoned contacts, Average Handle Time.
2. Switch the Duration to `This Year` notice the change into these KPIs.
3. Select **Channel Type** and opt for digital channels only: Email, Chat and Social to observe the update KPI’s.

![OverviewHist](/assets/images/reporting/2_1_OverviewHist.png)

### Contact Volume Historical Dashboard

1. Search for `Contact Volume Historical Dashboard` and execute it.
2. You would notice all the dialed number and entry points in the contact centre across all the channels and respective contact volume.
3. Switch to the **Chart view**.
4. Duration to `This Year`.
5. Interval to `Monthly`, click `Apply`.
6. This provides you a trending view of contact volume for the year and comparison on monthly basis.
7. Update **Channel Type** filter to select `Telephony` and `Chat`. Observe the comparison data between these channels over the period of time.

![VolumeTable](/assets/images/reporting/2_1_VolumeTable.png)

**Action:** Administrators analyse this data to assess channel preferences, allocate resources effectively, and identify opportunities for improving customer service across different channels.

![VolumeDashboard](/assets/images/reporting/2_1_VolumeDashboard.png)

**B. Expected Insights and Actions:** Trend and detailed insight of Agent performance metrics like Max connected duration and Avg Connected duration across Agent Teams as well as Agent level break down optionally. This helps to identify any need of process improvements or additional agent training.

### Agent Performance Dashboard

1. By default, you would notice Chart view of the monthly data with “Max connected duration” and “Average connected Duration” with weekly interval.
2. You can try to switch the Duration and Interval to look for the data for longer or shorter period and trend.
3. Switch to the Table View ![TableView](/assets/images/reporting/2_1_TableView.png) and you would notice much more detailed data insights into each team and agent level.
4. Further filtering can be done based on Team, Channel and Agent Name, to gather insights around specific agent group.

**Action:** Look if the max connected duration is consistently high, it may indicate a need for process improvements or additional agent training. If the average connected duration is longer than desired, it may indicate the need to streamline processes, provide agents with additional resources or tools, or optimize call handling techniques. On the other hand, if the average connected duration is too short, it may indicate rushed interactions or missed opportunities for upselling or cross-selling.

![PerformanceDashboard](/assets/images/reporting/2_1_PerformanceDashboard.png)

## 2.2 Customer Experience and Queue Performance

**Persona:** CC Supervisors, CC Manager, Business Analyst
**Preferred View Type:** Table

**Business Use-Case:** Capturing and analysing customer experience analytics in a contact centre is essential for businesses to understand and improve customer satisfaction levels. By gathering key data insights across every stage of the Contact including:

1. IVR
2. Self-Service / Virtual Agent
3. Queue performance including Transfer Rate after connection to an Agent
4. Queue Opt-out / Callback

![VirtualAgentFlow](/assets/images/reporting/2_2_Flow.png)

**A. Expected Insights and Actions:** Understanding the virtual agent's resolution rate, and escalation rate to the Queue.

### IVR & CVA Dialog Flow Report

![DialogFlowTable](/assets/images/reporting/2_2_DialogFlowTable.png)

**Actions:** Refining the virtual agent's responses where escalation rate to the Queue is higher, training them on new issues.

**B. Expected Insights and Actions:** Supervisor looking for key performance metrics for their line of business (Queue), Percentage Handled, Abandonment Rate, Avg Abandoned Time and Service Level.

### CSQ All Fields Report

![CSQTable](/assets/images/reporting/2_2_CSQTable.png)

**Actions:** Adjusting staffing levels and/or call routing improvements to manage peak times and low service level. Implement callback options to reduce wait times and abandonment rate.

**C. Expected Insights and Actions:** Offering the callback to the customers when they are in IVR or waiting in the Queue is one of the most efficient ways to improve the customer experience. Capture the callback success rate and reasons for failure.

### Callback Report

![CallbackTable](/assets/images/reporting/2_2_CallbackTable.png)

**Actions:** For low Callback success rate review the Reason, one of the prime reasons for an unsuccessful callback request is that customers aren’t reachable or busy at callback time. Explore if offering the Callback Retry attempt ([CallbackFailed](https://www.cisco.com/c/en/us/td/docs/voice_ip_comm/cust_contact/contact_center/webexcc/SetupandAdministrationGuide_2/b_mp-release-2/wcc-flow-designer.html#Cisco_Concept.dita_2e773682-6129-4fb7-b857-4b56f57103bc)) for the callback would help improving the success rate and tweak it based on further review.

## 2.3 Agent Performance

**Business Use-Case:**

**Persona:** CC Supervisors, CC Manager, Business Analyst
**Preferred View Type:** Table

**Expected Insights and Actions:**

### Agent Call Summary Report

Actions:

# Part 3: (BONUS) Contact Center Insights with Analyzer custom reports and Dashboards

There are **4 key Data Repositories today**, which store all the customer and Agent related data for the Webex contact Center.

![ReposTable](/assets/images/reporting/3_ReposTable.png)

![ReposFlow](/assets/images/reporting/3_ReposFlow.png)

In this Lab we would create a custom report to monitor the calls waiting in Queue on realtime bases and Agents available to handle them and in which state they are.

Currently option to create custom report is not available in New Analyzer UX, hence we would use our Current Analyzer Interface for this Lab.

Before you continue with this exercise follow below:

1. Make a Call and select prompted options to get to an agent, with no agent available you would hear a wait music.
2. Make sure your agent is logged-in and currently in Idle state.

## 3.1 Realtime Contact in the Queue

## 3.2 Realtime Agent State

## 3.3 Realtime Dashboard

# Part 4: (BONUS) Data extraction and scheduling Capabilities

Similar to Lab Part-3 advance data extraction and scheduling capabilities are not avalaible in New Analyzer UX and is part of roadmap. Hence for this exercise we would use current Analyzer interface.

## 4.1 Export Data as Excel or CSV

- Open `Incoming, Short, IVR Time- Entry Point` report in separate browser tab and Export the Data as Excel.
- Now you can use this data, filter or share as needed.

![Export](/assets/images/reporting/4_1_Export.png)

## 4.2 Visualization Scheduler

In this exercise we will learn how to schedule visualizations within Analyzer. In Analyzer, you can schedule any historical visualization to be run and sent in a predefined time period to an email address. This is very handy for admins or supervisors who need to see reports on a scheduled daily, weekly or monthly basis.

1. Find the `CSQ All Fields Report`.

![CSQ](/assets/images/reporting/4_2_CSQ.png)

2. Next, in the right-hand corner of the report, select the three ellipsis and from the dropdown select the option **Schedule Job**.
   ![ScheduleOptions](/assets/images/reporting/4_2_ScheduleOptions.png)

3. Fill in the schedule information for the scheduled report.
   - Start with the **Job Name**. Let’s set this to run daily so we will give it the name **CSQ All Fields Report_Daily**.
   - Choose a start date and time. Select today’s date with a time of a few minutes ahead of your current time to give it time to trigger.
   - Next complete the details for the email notification by entering in your email address and a subject line.

![Schedule](/assets/images/reporting/4_2_Schedule.png)

4. Once **saved**, the scheduled job will show up under the `Jobs` list.

![Job](/assets/images/reporting/4_2_Job.png)

5. If everything was setup correctly, check your email for the report after the trigger time has passed.

6. If your job was only set to run once, once it runs, that job is deleted from the jobs list.
7. **Close** the job scheduling window. Go back to the folder structure and look at the Details of the report, it will show the number of jobs scheduled. You should see 1 scheduled job to reflect the job we just scheduled in this exercise.

![JobDetails](/assets/images/reporting/4_2_Details.png)

## 4.3 Search APIs

In this exercise, we are going to use the API to retrieve the LastAgentInteraction example from Github to find when a customer called in the last 7 days and which agent they reached.

1. Open Developer portal using this link:
   https://developer.webex-cx.com/documentation/search/v1/search-tasks

2. Login with your Admin user.

![APILogin](/assets/images/reporting/4_3_Login.png)

3. Click **Try Out -> Maximize Screen**.

![TryOut](/assets/images/reporting/4_3_TryOut.png) <br>
![MaximizeScreen](/assets/images/reporting/4_3_MaximizeScreen.png)

4. You can explore the schema by clicking on Docs to open the **Documentation Explorer**. On the explorer, click on **Query -> task -> TaskList**.

![Explorer](/assets/images/reporting/4_3_Explorer.png)

5. Now let’s execute a query and see what data you get. <ins>Update the Origin number highlighted in yellow in below query with the phone number you are using to make the test calls.</ins>

6. Go to the query window and **delete** the text first **before** you paste the new query with your number.

7. Then, paste the snippet in Query space and click Run ![Play](/assets/images/reporting/4_3_Play.png). You should see results similar to the following:

![Snippet](/assets/images/reporting/4_3_Snippet.png)

```
{
  #LAST AGENT INTERACTIONS: Usage of filters, aggregates, pagination and custom fields to find when the customer called last in a 7 day window and who they reached
  task(
    # NOTE: from and to are mandatory arguments that take the Epoch timestamp in milliseconds
    from: 1675638001000 #This can be set to Date.now() - (days * 24 * 60 * 60 * 1000) for lookback in days
    to: 1675782001000 #This can be set to Date.now() in millis
    timeComparator: createdTime #Filter by created Time only
      filter: {
      #Filter the type of Task
      and: [
        { channelType: { equals: telephony } } #Telephony calls only
        { origin: { equals: "XXXXXXXXXXXX" } } #Customer ANI
        { status: { equals: "ended" } } #Final Disposition
        { direction: { equals: "inbound" } } #Inbound call only
        { isActive: { equals: false } } #Resolved call only
        { owner: { notequals: { id: null } } } #Only calls that had an Owner
      ]
    }
    pagination: { cursor: "0" } #Display first page only
  ) {
    tasks {
      #Task Metadata
      id
      createdTime
      endedTime
      origin
      destination
      lastWrapupCodeName #Why the customer called
      totalDuration
      selfserviceDuration
      captureRequested
      #Treatment Details
      lastEntryPoint {
        #Entrypoint Details
        id
        name
      }
      lastQueue {
        #Queue Details
        id
        name
      }
      lastTeam {
        #Team Details
        id
        name
      }
      owner {
        #Agent Details
        name
        id
      }
    }
    #Pagination Information
    pageInfo {
      endCursor
      hasNextPage
    }
  }
}
```

### Congratulations, you have officially completed the Webex Contact Center Reporting Experience labs!
