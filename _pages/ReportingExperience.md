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

This Lab has been split into four parts.

1. First part of this Lab **introduces** you to the **current Analyzer User Interface** as well as the **New Analyzer User Interface (Analyzer UX Refresh).**

   > Note: **Important to point out** that the New Analyzer User Interface is in **Early Access phase** and has access only to Historical Stock Reports.
   > {: .block-warning }

2. In the second part we will look how **key Contact Center personas (Administrators, Supervisors and Contact Center Analysts) can use Analyzer** to extract some key Contact Center KPIs and actionable insights around **Contact Center Operational Performance, Customer Experience and Agent Performance** using the various **Stock** reports and dashboards.
3. In the third part we will walk through how we can **create custom reports** to extract key Contact Center data insights.
4. Last chapter covers key data and reporting capabilities like the **export of reporting data, report scheduling and the available Data APIs** to extract the data.

# Table of Contents

| Topic                                                                                                                                             | Type        | Dificulty    | Time   |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ------------ | ------ |
| [Pre-Requisites](#pre-requisites)                                                                                                                 | Activity    | EASY         | 5 min  |
| [Analyzer and Desktop Login Process](#analyzer-login-process)                                                                                     | Activity    | EASY         | 5 min  |
| [Part 1: Webex Contact Center Analyzer User Interface](#part-1-webex-contact-center-analyzer-user-interface)                                      | Exploration | EASY         | 15 min |
| [1.1: Analyzer User Interface](#11-analyzer-user-interface)                                                                                       | Exploration | EASY         |        |
| [1.2: NEW Analyzer User Interface](#12-new-analyzer-user-interface)                                                                               | Activity    | EASY         |        |
| [Part 2: Contact Center Insights with New Analyzer Stock reports](#part-2-contact-center-insights-with-new-analyzer-stock-reports)                | Activity    | EASY         | 15 min |
| [2.1: High-level Contact Center Performance and Usage insights](#21-high-level-contact-center-performance-and-usage-insights)                     | Activity    | EASY         |        |
| [2.2: Customer Experience and Queue Performance](#22-customer-experience-and-queue-performance)                                                   | Activity    | INTERMEDIATE |        |
| [Part 3: Contact Center Insights with Analyzer custom reports](#part-3-bonus-contact-center-insights-with-analyzer-custom-reports-and-dashboards) | Activity    | INTERMEDIATE | 15 min |
| [3.1: Create Custom Realtime Agent Report](#31-create-custom-realtime-agent-report)                                                               | Activity    | INTERMEDIATE |        |
| [Part 4: (BONUS) Data extraction and scheduling Capabilities](#part-4-bonus-data-extraction-and-scheduling-capabilities)                          | Activity    | EASY         | 20 min |
| [4.1: Export Data as Excel or CSV](#41-export-data-as-excel-or-csv)                                                                               | Activity    | EASY         |        |
| [4.2: Visualization Scheduler](#42-visualization-scheduler)                                                                                       | Activity    | EASY         |        |
| [4.3: Search APIs](#43-search-apis)                                                                                                               | Activity    | INTERMEDIATE |        |

## Pre-Requisites

1. Ensure that you have received your tenant login credentials (Administrator, Supervisor and Agent) from the Lab proctors.
2. Make sure you are able to login into [Admin Portal](https://admin.webex.com) & [Analyzer](https://analyzer-v2.wxcc-us1.cisco.com/analyzer/home).
3. In this Lab, Part 1 and 2 already have historical data created to capture the key insights, hence no need to login Agent or make calls to complete those parts.
4. In Part 3, we will look into some Realtime data insights for which make sure you are logged-in with your Supervisor-Agent or Agent.

### You Will Need

1. **One additional device** (like your personal phone) to test inbound calls to the Webex Contact Center. You can use your cell phone for this purpose.

   - Administrator credentials for the Control Hub: admin.webex.com.
   - Agent Login Credentials for the Agent Desktop: desktop.wxcc-us1.cisco.com.

2. The items listed below have been pre-configured for you:
   - Agent and Supervisor user accounts are configured and ready for login.
   - You can access the Agent Desktop via the URL: [https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com).
   - As an agent, you're associated with two teams —designated by your Attendee ID— as "Team1" and "Team2".

Example:

> If your attendee ID is 100:
>
> 100_Team1
>
> 100_Team2

3. Agents will use browsers for voice calls using WebRTC (Web Real-time Communication) endpoints. Additionally, Webex Calling extensions have been assigned to users (both agents and supervisors) to facilitate alternate device experiences. Webex Contact Center agents and supervisors can opt for any mix of these devices, encompassing PSTN endpoints and mobile phones.

4. A preset inbound Voice flow is available for test calls.

## Lab Configuration

> Please submit the form below with your Attendee ID in 3 digits long format (e.g. if your attendee ID is 51, please enter 051). All configuration items in the lab guide will be renamed with that prefix.

<script>
document.forms["attendee-form"][1].value = localStorage.getItem("attendeeID") || "Your Attendee ID" 
update()
</script>
<form id="attendee-form">
  <label for="attendee">Attendee ID:</label>
  <input type="text" id="attendee" name="attendee" onChange="update()"><br>
<br>
  <button onclick="update()">Save</button>
</form>
<script>
document.forms["attendee-form"][1].value = localStorage.getItem("attendeeID") || "Your Attendee ID"
update()
</script>

The following Administration entities have been configured for you via [Webex Control Hub](https://admin.webex.com){:target="\_blank"}.

Please note, that to proceed to the next section, you will need to use the accounts shown below.

| **Entity**    | **Name**                                                            |
| ------------- | ------------------------------------------------------------------- |
| Agent 1       | wxcclabs+agent_ID<w class = "attendee_out">AttendeeID</w>@gmail.com |
| Supervisor 1  | wxcclabs+supvr_ID<w class = "attendee_out">AttendeeID</w>@gmail.com |
| Administrator | wxcclabs+admin_ID<w class = "attendee_out">AttendeeID</w>@gmail.com |

# Analyzer Login Process

1.  Make sure you are able to login into Administrator Portal ([admin.webex.com](https://admin.webex.com) using your Supervisor credentials.
2.  Once logged-in, go to `Quick Links` on the right and click on `Analyzer`.
    ![analyzer](/assets/images/reporting/intro_CH.png)
    ![analyzer](/assets/images/reporting/analyzerLogin.gif)
3.  For Part 3 of the Lab, login as an Supervisor-agent or Agent :

> Note: If you are already logged-in as an Agent as part of other Labs, no action is required.
> {: .block-tip }

You have 2 options to login as an Agent:

1.  Supervisor credentials with Role as `Supervisor and Agent`
2.  Using your Agent Credentials

### Login As Supervisor-Agent

> Note: Currently supervisors can not login via Desktop/WebRTC. If you want to test a login with WebRTC, make sure to sign in as an agent, as per the steps on the next chapter.

| **User Role** | **User email**                                                   | **Endpoint**        |
| ------------- | ---------------------------------------------------------------- | ------------------- |
| Supervisor    | wxcclabs+supvr\_<w class="attendee_out">AttendeeID</w>@gmail.com | Webex App/Extension |

- Login with Supervisor Credentials [admin.webex.com](https://admin.webex.com).
- Go to `Quick Links` --> Click on `Desktop`.
- Select the Role as : `Supervisor and Agent`.
- Enter the Dialed number provided (if it is not pre-filled).
- Team should be pre-populated.
- Click `Submit`.

![analyzer](/assets/images/reporting/supervisorlogin.gif)

### Login in the Webex app for PC or Mac

> In this lab, we can use the Webex app for PC or Mac to login to the Desktop with the **supervisor** account.
> {: .block-warning }

- Download Link: **[https://www.webex.com/downloads.html](https://www.webex.com/downloads.html){:target="\_blank"}**

![Webex App](/assets/images/Lab1-AD-1.png)

- Install the application on your PC/Mac.

- Open Webex app and сlick **Sign In**. Enter the provided supervisor credentials.

### Agent Desktop Login

| **User Role** | **User email**                                                   | **Endpoint**   |
| ------------- | ---------------------------------------------------------------- | -------------- |
| Agent         | wxcclabs+agent\_<w class="attendee_out">AttendeeID</w>@gmail.com | WebRTC/Desktop |

> **Note**: To log in to the agent desktop, use either a different web browser or a new incognito web page. This will prevent the browser caching issues with admin and agent credentials.
>
> {: .block-tip }

- Navigate to **[Desktop](https://desktop.wxcc-us1.cisco.com/){:target="\_blank"}** in the chrome browser with the incognito mode.

- Enter the agent’s **email ID**.

- Enter the **Password** for the appropriate username.

- In the **_Station Credentials_** pane, select **"Desktop"**.

- Select the team **<w class="attendee_out">Your_Attendee_ID</w>\_Team1**.

- Click the **_Submit_** button. The browser may ask you to confirm the use the microphone from the browser.

- Make sure that you are successfully logged in to the Agent Desktop.

![Agent Sign In](/assets/images/AG-2.gif)

# Part 1: Webex Contact Center Analyzer User Interface

## 1.1 Analyzer User Interface

This lab is designed to give you **basic understanding of Analyzer, user interface features** as well as the default dashboards available in the Admin Portal. In the following exercises, the goal is the **familiarization** with the product, interfaces and terminology.

![analyzer](/assets/images/reporting/old_ux_intro.gif)

1. At this point, you should be already logged-in to Analyzer. If not, use the steps above to login to [Analyzer](https://analyzer-v2.wxcc-us1.cisco.com/analyzer/home).

2. As you login, you may see this pop-up prompting to “Explore New Analyser”.
   $${\color{red}DO\space NOT\space LAUNCH\space it\space at\space this\space time\space and\space Click\space Cancel.}$$
   ![refesh-popup](/assets/images/reporting/1_1_RefreshPopup.png)

3. Navigate around the home screen to learn the different features available on this screen.

   - Make a note of the sessions count for the four data repositories:
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
   Click ![ListView](/assets/images/reporting/1_1_ListView.png) to change the view to `List` view.
   ![List](/assets/images/reporting/1_1_List.png)

   - Here you can sort the reports based on a specific header by clicking on the header.
   - Notice the **Temporal Scope**, which can be either **Realtime, Compound** or **Historical**.
   - ID is <ins>unique</ins> for every report and a report can also be searched by its `ID` besides the name.

7. Click the ![Dots](/assets/images/reporting/1_1_dots.png) icon next to the report and then click on **Details**. <br>
   ![Details](/assets/images/reporting/1_1_Details.png) <br>
   ![DetailsInfo](/assets/images/reporting/1_1_DetailsInfo.png) <br>

   - Make a note of the **Date Range** and **Scheduled Jobs**.
   - Try the same for any Historical stock report. <br>

8. On the top, click on your **username** and then **Help** to open the help manual for Analyzer.

   - This provides you with an online version of the [Analyzer User Guide](https://www.cisco.com/c/en/us/td/docs/voice_ip_comm/cust_contact/contact_center/webexcc/Analyzer_2/b_analyzeronloinehelp/_b_analyzeronloinehelp_chapter_01.html), a great document that provides information about all the available <ins>stock reports</ins>, <ins>variables</ins> as well as <ins>functionalities</ins> of Analyzer.

9. Click on **Tenant Time zone** option on the header. Set it to the time-zone in which you want to Run Visualizations (You have two possible options: **Tenant or Browser**).
   ![TimeZone](/assets/images/reporting/1_1_Timezone.png)

## 1.2 NEW Analyzer User Interface

The **New Webex Contact Center Analyzer (Analyzer UX Refresh)** offers an enhanced and intuitive user interface that enables you to manage stock historical dashboards. It provides faster, more efficient, and focused views of historical analytics for Webex Contact Center, enhancing the integrated experience. The stock historical dashboards offer ready-to-use metrics, allowing you to generate metrics related to entry points, queues, teams, contacts, and agents for strategic decision-making.

> Note: The New Analyzer today does not currently provide custom dashboards. To access custom dashboards, you can use the existing Analyzer. Extending custom reporting support and adding real-time reports to New Analyzer UX is in our roadmap.
> {: .block-warning }

1. Login into the **New Analyzer**:

   - Click `Try Now` on the current Analyzer page.
     ![TryNow](/assets/images/reporting/1_2_TryNow.png)
     - New Analyzer will be cross-launched.
     - It may ask you to enter your supervisor username again.
     - You can also navigate between the new Analyzer and existing Analyzer using the browser tabs.

   ![NewLogin](/assets//images/reporting/1_2_login_new_ux.gif)

   You can see a new home page with centralized dashboards and reports. You'll see a new search bar to search through the various dashboards.

   ![New UX Home Page analyzer](/assets/images/reporting/1_2_UX_UI.gif)

2. Report Tabs: Reports and Dashboards are grouped under following `Tabs`:

   - **All:** Lists all the dashboards and reports.
   - **Recent:** Lists the most recent dashboards that you viewed.
   - **Favorite:** Lists the dashboards that you have marked as favorite.
   - **Stock:** Lists the predefined stock historical dashboards provided by Cisco.

   Click on each Tab and make a **note of the number of reports** in each Tab.

   ![Tabs](/assets//images/reporting/1_2_Tabs.png)

3. Click on `star` icon next to the `Abandoned Call Detail Activity Report` to mark it as your **Favorite**.

   ![Favourite](/assets//images/reporting/1_2_Favourite.png)

   This allows you to access your favorite dashboards easily under the dedicated `Favorite` tab.

4. Next, view the `Agent Call Summary Report`, for this **double-click** on the dashboard name or select **View** under the **Actions** tab.

   ![View](/assets//images/reporting/1_2_View.png)
   ![New UX Stock Report UI](/assets/images/reporting/1_2_New_UX.gif)

5. Next, review again the count of the reports in each tab and also if your **recently executed** report and **favorite marked** reports are visible under the respective tabs.

   ![Tabs](/assets//images/reporting/1_2_Tabs.png)

6. Use the `Sort By` drop-down menu to filter stock dashboards by options such as **Name, Created By,** and **Last Edited By**. This enables easy organization and navigation based on your preferred sorting criteria.

   ![LastEditedBy](/assets//images/reporting/1_2_LastEditedBy.png)

7. Switch to **Card View** by cliking ![CardIcon](/assets//images/reporting/1_2_CardIcon.png).

   ![CardView](/assets//images/reporting/1_2_CardView.png)

   The **List View** is the default view and allows easy navigation and quick access to the entire collection of stock dashboards.

   The **Card View** provides a compact and visual representation of the stock dashboards, displaying snapshots of 15 dashboards in a single view.

8. Next, switch back to the List view and make a note of the `Labels` column.

   We've replaced folder-based navigation with `labels`. The **predefined labels** help you find and sort stock historical dashboards. The labels are color-coded to enhance the user experience. You can search for dashboards using labels.

   - All stock reports by default are marked with label `Stock`. <br>
     ![Labels](/assets//images/reporting/1_2_Labels.png)

9. Next, use the search box to find a stock dashboard using different criteria or comma separated words. For this example, search the word `transition`. <br>
   ![TransitionSearch](/assets//images/reporting/1_2_TransitionSearch.png)

   This would list all the **Transition reports**, which are built for easy reporting insights for customers migrated from UCCX but also useful for any customer.

   ![TransitionReports](/assets//images/reporting/1_2_TransitionReports.png)

   Customize your search selecting criteria such as **Name, Labels, Created By,** or **Last Edited By** from the drop-down menu.

10. Next, click on the user profile icon on the top right of the user interface provides user information. The time zone settings and dark mode options are available in the user profile settings.

    - **Time Zone**

      By default, the new Analyzer shows the tenant time zone. You can update the browser settings if necessary. <ins>Scheduled jobs always run in the tenant time zone.</ins>

    - **Dark Mode**

      You have the option to switch between dark and light screen modes to suit your viewing experience.

11. Next, let's take a look at **key functions** for a stock report. Go to the `Agent Call Summary Report`, which you viewed in **step #3**.

12. By default, data is displayed in `Table View` for `Last week`. Change it to `This month` and click **Apply**.
    What you see here is the Agent summary data for all the agents for this month.

    > Note: In the Table view of a dashboard, Analyzer supports a maximum of 100 columns and up to 100,000 rows.

13. Click on `Agent Endpoint (DN)` filter and make a note of device types used by the users (Agent and Supervisors). You would notice a **mix** of Dial numbers and WebRTC devices.

14. **Pin Column**

    You can **pin columns** or **move columns** of a dashboard to the right and left of the table based on your requirements.

    - On the dashboard, on the `Total Onbound` column, click the hamburger menu next to the column header. <br>
      ![Hamburger](/assets//images/reporting/1_2_Hamburger.png)
    - Go to `Pin Column` and click `Pin Left`. <br>
      ![PinLeft](/assets//images/reporting/1_2_PinLeft.png) <br>
      This would move the **Total Inbound** column to the left of the table. <br>
      ![MovedLeft](/assets//images/reporting/1_2_MovedLeft.png)

15. **Autosize Column**

    Next, let's autosize all the columns as data in some columns is not clearly visible because of last textual size. To do so:
    On the dashboard column, click the **hamburger** menu next to the column header.

    1. Click `Autosize This Column`.
    2. For all columns, click `Autosize All Columns`.

    ![AutosizeColumn](/assets//images/reporting/1_2_AutosizeColumn.png)

    This would allow you to see all the data points clearly.

16. **Advanced Filtering**

    We already saw how you can use predefined filters on the reports. Beyond that, you can also filter the data data for other columns in the reports.
    In the current `Agent Call summary` report, let's filter the data to identify any agents which handled low number of calls.

    For this, click on Hamburger sign ![HambSign](/assets//images/reporting/1_2_HambSign.png) next to the `Total Inbound` Column --> Click on the Filter ![FilterSign](/assets//images/reporting/1_2_FilterSign.png) option and select **“0”** and **“1”**. Data will be updated immediately (No need to click Apply).

    ![FilterDone](/assets//images/reporting/1_2_FilterDone.png)

17. **Column View**

    You can customize the visibility of columns in the table. On the dashboard column, click the hamburger menu next to the column header. Click on **Column view** icon ![ColumnIcon](/assets//images/reporting/1_2_ColumnIcon.png) and uncheck all `Time` field columns to exclude them and have a simpler count only view.

    ![ColumnView](/assets//images/reporting/1_2_ColumnView.png)

18. Switch the view of the report from `Table` to `Chart` by clicking ![ChartIcon](/assets//images/reporting/1_2_ChartIcon.png) on top right corner of the report.

    ![ChartView](/assets//images/reporting/1_2_ChartView.png)

    You would notice a graphical view of the data for the number of `Total Inbound Contact` each agent handled during this month along with a trend line.

#### Trend Line

In **Chart** view, the new Analyzer introduces `Trend Line`, which is a visual representation of trends with data points. When viewing a dashboard, the presence of a trend line allows users to quickly identify and understand the underlying trend or pattern within the data.

![TrendLine](/assets//images/reporting/1_2_TrendLine.png)

Similarly you can try filter the data based on `Agent Name` and `Agent Endpoint (DN)`.

**Congratulations, you have completed this lab! You can continue with the next one.**

# Part 2: Contact Center Insights with New Analyzer Stock reports

In this section, we will delve into how various personas within a contact center can leverage the Webex Contact Center Analyzer to capture Key Performance Indicators (KPIs) and glean insights that can measure and enhance customer experience, agent performance, and overall business outcomes. We will explore some of the pre-built stock reports with New Analyzer Interface, which can help you gather these key actionable insights from day one.

## 2.1 High-level Contact Center Performance and Usage Insights

**Persona:** CC Administrator, Supervisors, CC Manager, Leadership
**Preferred View Type:** Chart, Trending

**Business Use Case:** Contact centre administrators play a crucial role in managing and optimizing contact centre operations. To effectively monitor and analyse the performance of the contact centre, it is essential for administrators to capture and track high-level contact centre state and usage data. This data provides valuable insights into various aspects, such as agent productivity, call volumes, customer satisfaction, and system performance. By capturing this information, administrators can make informed decisions, identify areas for improvement, and ensure efficient contact centre operations.

### **A. Expected Insights and Actions**

Monthly trending of total inbound and outbound contacts over this year. Secondly, the usage of different communication channels, such as phone calls, emails, live chat, and social media interactions.

### Contact Center Overview – Historical

Search for the label `Contact Center Overview` and double click on the `Contact Center Overview – Historical` dashboard.

1. Make a note of the following cards: Average Service Level, Total Handled, Total Abandoned Contacts, Average Handle Time.
2. Switch the Duration to `This Year` notice the change into these KPIs.
3. Select **Channel Type** and opt for digital channels only: Email, Chat and Social to observe the update KPI’s.
4. Scroll Down the dashboard to the review "Contact Details in Queue" Report.
5. On right upper corner of the "Contact Details in Queue" Chart View
6. Observe the historical Queue volume and trending across last 7 days.

#### **Field Description**

**Contact Center Overview – Historical** dashboard displays displays contact statistics for a specified duration and time interval. Users can filter data using drop-down lists. The available information includes:

- Average Service Level: Shows the percentage of contacts handled within the set service level.
- Total Contacts Handled: Displays the total number of contacts handled across various communication channels.
- Total Contacts Abandoned: Shows the total number of contacts that were abandoned.
- Average Handled Time: Indicates the average time taken to handle a contact.
- Longest Contact in Queue: Displays the waiting time for the contact with the longest queue time.
- Contact Details in Queue: Shows the details of contacts (voice, email, social, and chat)

![OverviewHist](/assets/images/reporting/2_1_OverviewHist.png)
![OverviewHist](/assets/images/reporting/CCOverview2.png)

### Contact Volume Historical Dashboard

1. Search for `Contact Volume Historical Dashboard` and execute it.
2. You would notice all the dialed number and entry points in the contact centre across all the channels and respective contact volume.
3. Switch to the **Chart view**.
4. Duration to `This Year`.
5. Interval to `Monthly`, click `Apply`.
6. This provides you a trending view of contact volume for the year and comparison on monthly basis.
7. Update **Channel Type** filter to select `Telephony` and `Chat`. Observe the comparison data between these channels over the period of time.

#### **Field Description**

The parameters in this dashboard include DNIS (Dialed Number), Entry Point Name, Interval, Channel Type, and Contacts.

- DNIS is a service from the phone company delivering a number indicating the digits dialed by the caller. It's used as a row segment, but it doesn't appear for chat contacts.
- The entry point name is the name of a particular entry point, also used as a row segment.
- Interval refers to a time period, specifically the last 7 days in this context.
- Channel Type denotes the media type of contact, like telephony, email, or chat, and it's used as a row segment.
- Finally, Contacts is a parameter that refers to the count of contact session IDs, serving as a unique identifier for each contact.

**Action:** Administrators analyse this data to assess channel preferences, allocate resources effectively, and identify opportunities for improving customer service across different channels.

![VolumeDashboard](/assets/images/reporting/2_1_VolumeDashboard.png)

### **B. Expected Insights and Actions**

Trend and detailed insight of Agent performance metrics like `Max Connected Duration` and `Avg Connected Duration` across Agent Teams as well as Agent level break down optionally. This helps to identify any need of process improvements or additional agent training.

### Agent Performance Dashboard

1. Search for `performance` in the search bar. Look for `Agent Performance Dashboard` and double click to view it.
2. By default, you would notice Chart view of the monthly data with “Max connected duration” and “Average connected Duration” with weekly interval.
3. You can try to switch the Duration and Interval to look for the data for longer or shorter period and trend.
4. Switch to the Table View ![TableView](/assets/images/reporting/2_1_TableView.png) and you would notice much more detailed data insights into each team and agent level.
5. Further filtering can be done based on Team, Channel and Agent Name, to gather insights around specific agent group.

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

### **A. Expected Insights and Actions:**

Understanding the virtual agent's resolution rate, and escalation rate to the Queue.

To extract expected insights we can leverage stock report "IVR & CVA Dialog Flow Report"

### IVR & CVA Dialog Flow Report

This report displays the Self-service operational metrics. Which consist of:

- The total number of IVR calls handled by the virtual agent.
- Number of abandoned calls in Self-service.
- Number of IVR calls that were escalated to a queue.
- Percentage of IVR calls that were escalated to a queue.

Steps:

1. Search for label `selfservice`.
2. Look for `IVR & CVA Dialog flow` Report --> Double click to view it.

**Actions:** Refining the virtual agent's responses where escalation rate to the Queue is higher, training them on new issues.

![DialogFlowTable](/assets/images/reporting/cvaimage2.png)
![IVRCVAFields](/assets/images/reporting/2_2_IVRCVAFields.png)

### **B. Expected Insights and Actions**

Supervisor looking for key performance metrics for their line of business (Queue), Percentage Handled, Abandonment Rate, Avg Abandoned Time and Service Level.

### CSQ All Fields Report

The CSQ All Fields Report presents the queue-related data such as call statistics, service level, and key fields like Average Queue Time, Average Speed of Answer, Calls Handled, and Calls Abandoned under service level. This report combines the fields of all queue-related reports.

This report is also part of Transitions reports built in Webex Contact Center to deliver the look and feel of Key Contact Center Express (UCCX) reports to help customers who transitions to Cloud Webex Contact Center.

Steps:

1. Search for Label `Transition`.
2. Look for `CSQ ALL Fields Report` and double click it to view.

**Actions:** Adjusting staffing levels and/or call routing improvements to manage peak times and low service level. Implement callback options to reduce wait times and abandonment rate.

![CSQTable](/assets/images/reporting/CSQallreport2.png)

![CSQTable](/assets/images/reporting/2_2_CSQTable.png)

### **C. Expected Insights and Actions**

Offering the callback to the customers when they are in IVR or waiting in the Queue is one of the most efficient ways to improve the customer experience. Capture the callback success rate and reasons for failure.

### Callback Report

The contact center customer can opt to receive a callback from an agent while in IVR or waiting in a queue. The courtesy callback flow is configured by the flow developer.

![CSQAllfield](/assets/images/reporting/callback.png)

![CallbackTable](/assets/images/reporting/callback1.png)

**Actions:** For low Callback success rate review the Reason, one of the prime reasons for an unsuccessful callback request is that customers aren’t reachable or busy at callback time. Explore if offering the Callback Retry attempt ([CallbackFailed](https://www.cisco.com/c/en/us/td/docs/voice_ip_comm/cust_contact/contact_center/webexcc/SetupandAdministrationGuide_2/b_mp-release-2/wcc-flow-designer.html#Cisco_Concept.dita_2e773682-6129-4fb7-b857-4b56f57103bc)) for the callback would help improving the success rate and tweak it based on further review.

**Congratulations, you have completed this lab! You can continue with the next one.**

# Part 3: Contact Center Insights with Analyzer custom reports

In this lab, we will create a custom report to monitor the calls waiting in the queue in real-time, along with the available agents and their respective states. Since the option to create a custom report is currently unavailable in the New Analyzer UX, we will be using our current Analyzer interface for this lab.

In Webex Contact Center, there are four primary data repositories that store critical customer and agent-related information. These repositories are structured as follows:

1. **Customer Activity Record**

- **Description**: This type of record represents individual, atomic steps within the customer's workflow. It captures key moments in the customer journey, providing insights into their interactions with the contact center.
- **Examples**:

  - Customer in IVR or queue, talking to an agent, or on hold.
  - Customer on specific web pages, such as the home page, product page, or checkout page.

2. **Customer Session Record**

   - **Description**: Customer Session Records are more comprehensive, encapsulating the entire customer workflow. They consist of a sequence of customer activities, providing a holistic view of the customer's engagement with the contact center.

- **Examples**:

  - Customer calls the contact center for assistance.
  - Customer visits a website and explores its content.
  - Customer interacts with the website and engages in a chat with an agent.
  - Customer initiates contact by sending an email, and an agent responds.

3. **Agent Activity Record**

   **Description**: This record type focuses on individual actions within the agent's workflow. It logs every significant step an agent takes, shedding light on their interactions and status throughout their workday.

   **Examples**:

   - Agent's status transitions, such as idle, available, talking, or wrapping up.
   - Agent's offline activities, including dialing, note-taking, and reading emails.
   - Agent's involvement in chats with customers and the subsequent wrap-up process.

4. **Agent Session Record**

   **Description**: Agent Session Records provide a comprehensive overview of an agent's work. They encompass a sequence of agent activities, offering insights into the agent's handling of tasks and interactions.

   **Examples**:

   - An agent manages a service call, logging an incident or request.
   - An agent initiates an outbound call and schedules a meeting for a customer.
   - An agent engages in chat interactions with customers, providing answers and assistance.
   - An agent reads and responds to customer emails, ensuring effective communication.

These data repositories play a crucial role in capturing, organizing, and analysing the wealth of information generated within the Webex Contact Center, ultimately supporting informed decision-making and enhancing customer and agent experiences.

![CSR](/assets/images/reporting/CSR.png)

Before you continue with this exercise follow below:

1. Make a Call and select prompted options to get to an agent, with no agent available you would hear a wait music.
2. Make sure your agent is logged-in and currently in `Idle` state.

## 3.1 Create Custom Realtime Agent Report

In this Lab, we will create a **custom visualization** to showcase the **state of agents on a Realtime basis**.

**Objective:** Create an Agent Real-time state report with following data insights:

1. State of Agents on real-time basis for Telephony channel.
2. Capture key metrics:

   - Agent Team
   - Agent Name
   - Agent State
   - Idle Code
   - Total number of agents logged-in
   - Number of Agents in Available and idle state for each team
   - Duration in the State

3. Create a high-level view, based on line of business (Group or Teams).
4. Have Data summarize based on each Line of Business (LOB).
5. Have options to filter the data based on LOB and Idle code.
6. Create some visual indication when certain agents in Idle state for long duration.

While completing this Exercise, you will be able to understand and use some **key capabilities** like:

- Fields and Measures
- Enhanced Fields
- Formulas
- Drill-down
- Group Summary
- On the Fly-filter
- Filtering

1. Create a new **visualization** in Analyzer as an **Agent Activity Record**.

   - Set **Start Time** as `Realtime`.
   - Set **Duration** as `None (Snapshot)`.
   - **Refresh duration** as `3 Seconds`.

   ![TimeSettings](/assets/images/reporting/3_1_TimeSettings.png)

2. Next, we will begin adding variables to the visualization. Click on **Row Segment** and add:

   - Team Name
   - Agent Name
   - Activity State
   - Idle Code Name

   ![RowSegments](/assets/images/reporting/3_1_RowSegments.png)

3. Next, click on **Profile Variables** and add `Agent Session ID (Count)` and rename the name as `#Total`.

![AgentTotal](/assets/images/reporting/3_1_AgentTotal.png)

4. To capture **Available Agent Count** add `Agent Session ID`. Name it as `#Available`.

   - Drag `Activity State` as **Filter** with value `available`. <br>
     ![AvailFilter](/assets/images/reporting/3_1_AvailFilter.png)

5. Repeat step 4 to add **Idle Agent Count**, this time with filter value `idle`. Name it as `#Idle`.

![IdleFilter](/assets/images/reporting/3_1_IdleFilter.png)

6. Next, we need to capture the **State Duration**. We will achieve this by using a **formula** to subtract the **activity start time** from **current time**, which will give us the **activity duration**.

   - Search for Measure Profile variable `Activity Start Timestamp`.
   - Under formula, select `Minimum Activity Start Timestamp` and save it. <br>
     ![MinActivity](/assets/images/reporting/3_1_MinActivity.png)
   - **Right click** on the field and click **New Formula** After, right click on the created field and click on `New Formula`. <br>
     ![NewFormula](/assets/images/reporting/3_1_NewFormula.png)
   - Name it **Duration** and swap the fields by clicking ![Swap](/assets/images/reporting/3_1_Swap.png).
   - **Click** ![Dropdown](/assets/images/reporting/3_1_Dropdown.png) on the empty field and select `Current Timestamp`.
   - Select ![Subtract](/assets/images/reporting/3_1_Subtract.png) **Subtraction operator**, as shown below. <br>
     ![SubtractionFormula](/assets/images/reporting/3_1_SubtractionFormula.png).
   - Right click the `Duration` profile variable, and set the **Duration Number Format** as `Duration > MM:SS`. <br>
     ![DurationFormat](/assets/images/reporting/3_1_DurationFormat.png).
   - Hide `Minimum Activity Start Timestamp` by clicking on the **eye** icon. <br>
     ![Hide](/assets/images/reporting/3_1_Hide.png).

7. **Re-order** the variables by dragging and dropping the variables in the order that you wish to see them in the report.

![Reorder](/assets/images/reporting/3_1_Reorder.png)

8. Save the report as `3.1_AAR_RT_AgentState_<YourStudentID>` (e.g. _3.1_AAR_RT_AgentState_101_) in your folder and click `Preview`.

![AAR_RT](/assets/images/reporting/3_1_AAR_RT.png)

9. Notice that the `#Total` count for each agent is **“10”**.

   - This is because each agent is a multi-channel agent (with Total 10 channels, 1 voice, and 3 Chat, 3 Email, 3 Social ones).
   - In this case we want to capture data for Telephony channel only so let’s add a Channel Filter for Telephony.
   - Go Back to the report edit mode and Add Filter with Channel Type as Telephony.

   ![FilterTelephony](/assets/images/reporting/3_1_FilterTelephony.png)

10. Save the visualization and click on Preview to run it again.

![SavedVisualization](/assets/images/reporting/3_1_SavedVisualization.png)

11. We are still missing below asks:

![MissingAsks](/assets/images/reporting/3_1_MissingAsks.png)

12. Update the **Output Type** to `Column Heatmap`.

![Heatmap](/assets/images/reporting/3_1_Heatmap.png)

13. To create a LOB group:

    - Right click on the Team name and then `Create Enhanced Field`.
      ![EnhancedField](/assets/images/reporting/3_1_EnhancedField.png)
    - Name the Field **LOB_Grouping{{StudentID}}**, replacing {{StudentID}} with your provided ID.

    **Add 2 groups** containing the following teams:
    CL_G1x : Seach for “Team1” Select from 51_Team1 to 59_Team1
    CL_G2x : Seach for “Team2” Select from 51_Team2 to 59_Team2

    ![LOBGrouping](/assets/images/reporting/3_1_LOBGrouping.png)

    Save it.

    ![Lob](/assets/images/reporting/3_1_Lob.png)

    - Make this Enhanced Field **global** so it can be used for any other visualizations with need of creating it again.

      Right click LOB_Grouping{{StudentID}} --> Click Save --> When prompted, click Save again.

      ![SaveLOB](/assets/images/reporting/3_1_SaveLOB.png)
      ![SaveLOB2](/assets/images/reporting/3_1_SaveLOB2.png)

    - Field is now saved and can be used in any other report.
    - Move LOB_Grouping{{StudentID}} as top row segment.

    ![LOBRow](/assets/images/reporting/3_1_LOBRow.png)

14. To create a **Summary** at LOB level:

    - Click `Show Summary` Option and select **LOB_Grouping**.
      ![LOBSummary](/assets/images/reporting/3_1_LOBSummary.png)
    - Click `Customize` --> Go to **LOB_Grouping** level.
      ![LOBCustomize](/assets/images/reporting/3_1_LOBCustomize.png)
    - Select `SUM` for **#Total**, **#Idle**, **#Avaliable** --> Save it.
      ![ReportSummary](/assets/images/reporting/3_1_ReportSummary.png)

15. Lastly, add the **on-the fly filters** for the **LOB Grouping** and **Idle Code Name**.

    - Click on `Show Filter On Run Mode`.
      ![ShowRunMode](/assets/images/reporting/3_1_ShowRunMode.png)
    - Select **LOB_Grouping** and **Idle Code Name**.
      ![Select](/assets/images/reporting/3_1_Select.png)

16. **Save** visualizations and check the `Preview`.

![Preview](/assets/images/reporting/3_1_Preview.png)

**Congratulations, you have completed this lab! You can continue with the next one.**

# Part 4: (BONUS) Data extraction and scheduling Capabilities

Similar to Lab Part-3, advanced data extraction and scheduling capabilities are not avalaible in New Analyzer UX and are part of the roadmap. Hence, for this exercise, we will use the current Analyzer interface.

## 4.1 Export Data as Excel or CSV

Although Analyzer offers a lot of functionalities for users, Contact Center administrators and analysts often need to work with the data offline, modify them via Excel or even share the transformed information with other parties. In this exercise we will see how Analyzer allows users to easily download the report results from within the Analyzer interface.

1. Open `Incoming, Short, IVR Time- Entry Point` report in separate browser tab (or use any other open report in current Analyzer if you prefer).
2. Click on `Export` on the top and you have the option to `Export as Excel` or `Export as CSV`. Select to export the data as Excel.
3. File will be downloaded to your computer.
4. Now you can use this data offline, perform advanced calculations from Excel or share with your colleagues as needed.

![Export](/assets/images/reporting/4_1_Export.png)

## 4.2 Visualization Scheduler

In this exercise we will learn how to schedule visualizations within Analyzer. In Analyzer, you can schedule any historical visualization to be run and sent in a predefined time period to an email address. This is very handy for admins or supervisors who need to see reports on a scheduled daily, weekly or monthly basis.

1. Find the report `CSQ All Fields Report`.

![CSQ](/assets/images/reporting/4_2_CSQ.png)

2. Next, in the right-hand corner of the report, select the three ellipsis and from the dropdown select the option **Schedule Job**. <br>
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

## **Congratulations, you have officially completed the Webex Contact Center Reporting Experience labs!**
