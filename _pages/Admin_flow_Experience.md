---
title: Admin and Flow Experience
author: Bhushan Suresh
date: 2023-10-15
layout: post
---

<script>
 function update () {
    const form = document.forms['attendee-form'];
    if (form) {
      form.addEventListener('submit', function (event) {
        event.preventDefault();
        const inputs = Array.from(form.querySelectorAll('input'));
        const values = inputs.reduce((acc, input) => {
          acc[input.id + '_out'] = input.value;
          return acc;
        }, {});

        Object.entries(values).forEach(([id, value]) => {
          const elements = document.getElementsByClassName(id);
          Array.from(elements).forEach(element => {

            console.log(element.innerHTML);
            if(Number(element.innerHTML) > 99 ){
               console.log(`Got a 99+ attendee: ${element.innerHTML}`);
               element.innerHTML = value;
             }
            else{
               console.log(`Got a sub 99 attendee: ${element.innerHTML}`);
               if(element.innerHTML.includes('gmail.com'))
               {
                element.innerHTML = `0${value}`;
                }
               else{
                element.innerHTML = value;
               }
                }
          });
        });
        const attendeeIDInput = form.elements['attendeeID'];
       if (attendeeIDInput && attendeeIDInput.value !== 'Your_Attendee_ID') {
          localStorage.setItem('attendeeID', attendeeIDInput.value);
        }
      });
    }
  };
</script>

# Table of Contents

| Topic                                                                                                | Lab Type    | Difficulty Level | Estimated length |
| ---------------------------------------------------------------------------------------------------- | ----------- | ---------------- | ---------------- |
| [Part 1: Introduction to the new Admin Experience](#part-1-introduction-to-the-new-admin-experience) | Exploration | EASY             | 10 min           |
| [ 1.1: Control Hub User Management Tasks](#11-control-hub-user-management-tasks)                     | Activity    | EASY             | 10 min           |
| [ 1.2: Contact Center User Configuration](#12-contact-center-user-configuration)                     | Activity    | EASY             | 10 min           |
| [ 1.3: Bulk Operations](#13-bulk-operations)                                                         | Activity    | EASY             | 5 min            |
| [ 1.4: Access to the Agent Desktop](#14-access-to-the-agent-desktop)                                 | Activity    | EASY             | 10 min           |
| [Part 2: Introduction to Flow Designer](#part-2-introduction-to-flow-designer)                       | Exploration | EASY             | 10 min           |
| [ 2.1: Configuring tenant for Call Delivery](#21-configuring-tenant-for-call-delivery)               | Activity    | EASY             | 10 min           |
| [ 2.2: Adding Text-To-Speech to the flow](#22-adding-text-to-speech-to-the-flow)                     | Activity    | EASY             | 8 min            |
| [ 2.3: Adding Callback functionality to the flows](#23-adding-callback-functionality-to-the-flows)   | Activity    | EASY             | 8 min            |
| [ 2.4: Business Hours Configuration](#24-business-hours-configuration)                               | Exploration | EASY             | 8 min            |
| [ 2.6: Bringing it all together: Advanced Flow configuration ](#24-business-hours-configuration)                               | Exploration | EASY             | 8 min            |
| [Part 3: Introduction to Flow Debugger](#part-3-introduction-to-flow-debugger)                       | Activity    | EASY             | 15 min           |
| [Part 4: Introduction to Flow Versioning](#part-4-introduction-to-flow-versioning)                   | Exploration | EASY             | 15 min           |
| [Part 5: Flow Error Handling](#part-5-flow-error-handling)                                           | Exploration | EASY             | 15 min           |
| [Part 6: Workflow in Outdial Entry Point](#part-6-introduction-to-the-new-admin-experience)          | Activity    | EASY             | 15 min           |
| [Bonus: Experience Management](#bonus-experience-management)                                         | Exploration | EASY             | 15 min           |
| [Bonus: Other Flow Enhancements](#bonus-other-flow-enhancments)                                      | Exploration | EASY             | 5 min            |

# Part 1: Introduction to the new Admin Experience

In this Lab, we will go through Admin UI by completing the tasks that are required for the general pre-configuration of a tenant. These tasks are to be undertaken by a customer administrator. By following each of the steps, you would have prepared your tenant to begin configuring different services offered by the platform. At the end of the lab, you should be able to log in to an agent interface with the configured user extension.
You can do the tasks from the lab guide either on the **Lab Tenant** (you need to request access from the lab support team).

### Objective

- This lab is designed to help you do the initial setup and configuration of the tenant.
- The lab contains multiple exercises on Control Hub (Admin Portal) to make you comfortable with the Webex Contact Center application.

### Pre-requisites

(0) **Lab Credentials and Attendee ID** - Provided to you over email.

> Please **`submit the form below with your Attendee ID`**. All configuration items in the lab guide will be renamed with that prefix.
> {: .block-warning }

<script>
document.forms["attendee-form"][1].value = localStorage.getItem("attendeeID") || "Your Attendee ID" 
</script>
<form id="attendee-form">
  <label for="attendee">Attendee ID:</label>
  <input type="text" id="attendee" name="attendee" onChange="update()"><br>
<br>
  <button onclick="update()">Save</button>
</form>

<br/>

(2) Administrator access to Control Hub

Your Administrator ID is in the format
**wxcclabs+admin_ID<w class = "attendee_out">attendeeID</w>@gmail.com**

(3) PSTN number (dialed number) registered on the Control Hub

> This is sent over email as the DN (Dialed Number)

(4) The items listed below have been pre-configured for you:

- Agent and Supervisor user accounts are configured and ready for logins.
- You can access the Agent Desktop via the URL: [https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com).
- As an agent, you're associated with two teams—designated by your Attendee ID—as "Team1" and "Team2".

Example:

> If your attendee ID is 100:
>
> 100_Team1
>
> 100_Team2

(5) Agents will use browsers for voice calls using WebRTC (Web Real-time Communication) endpoints. Additionally, Webex Calling extensions have been assigned to users (both agents and supervisors) to facilitate alternate device experiences. Webex Contact Center agents and supervisors can opt for any mix of these devices, encompassing PSTN endpoints and mobile phones.

(6) A preset inbound Voice flow is available for test calls.

### Quick Links

> Control Hub: **[https://admin.webex.com](https://admin.webex.com){:target="\_blank"}**\
> Agent Desktop: **[https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com){:target="\_blank"}**\

### Lab Section

> The overall aim of admin consolidation is to provide a single pane of glass (SPOG) experience for administrators so that admins need not have frequent context switch by having to traverse different applications.
>
> The following steps outlines the new features of a new admin experience.
>
> This introduces the new left navigation panel for Webex Contact Center in Control Hub as well as other configuration settings which were migrated from the Management Portal.

![Admin_Experience](/assets/images/AE_image1.png)

## 1.1: Control Hub User Management Tasks

> The following section describes the process of managing different types of users. You will use the steps to add new users and verify the Calling extensions for Supervisors. While adding the user, we will see how to select user roles.

> **Note: Agents will use WebRTC endpoints (Desktop Telephony)** > **Supervisors will use Webex Calling App (as Telephony Device)**
> {: .block-warning }

### 1. Verify the configuration parameters

The following Administration entities have been configured for you via [Webex Control Hub](https://admin.webex.com){:target="\_blank"}.

Please note, that to proceed to the next section, you will need to use the accounts shown below.

| **Entity**         | **Name**                                                            |
| ------------------ | ------------------------------------------------------------------- |
| Administrator      | wxcclabs+admin_ID<w class = "attendee_out">attendeeID</w>@gmail.com |
| Agent 1            | wxcclabs+agent_ID<w class = "attendee_out">attendeeID</w>@gmail.com |
| Supervisor 1       | wxcclabs+supvr_ID<w class = "attendee_out">attendeeID</w>@gmail.com |
| Desktop Profile    | WebexOne Desktop Profile                                            |
| Inbound EP         | <w class = "attendee_out">attendeeID</w>\_EP                        |
| Queue              | <w class = "attendee_out">attendeeID</w>\_Q                         |
| Team 1             | <w class = "attendee_out">attendeeID</w>\_team1                     |
| Team 2             | <w class = "attendee_out">attendeeID</w>\_team2                     |
| Site               | <w class = "attendee_out">attendeeID</w>\_Site                      |
| Multimedia Profile | <w class = "attendee_out">attendeeID</w>\_MMP                       |
| Outdial EP         | WebexOne_Outdial_EP                                                 |
| Outdial ANI        | WebexOneOutdial ANI                                                 |
| Address Book       | WebexOne Address Book                                               |
| Inbound Flow       | QtoA_WebexOne_InboundFlow                                           |
| Outbound Flow      | WebexOne_OutdialFlow                                                |

### 2. Verify agents, supervisors and telephony settings

- Login to the [Control Hub](https://admin.webex.com){:target="\_blank"} with the admin account.

- In the left navigation pane go to **_Contact Center Users_** under **Management**.

- Click on **_Manage Users_** button.

- Select **_Manually add users_**.

- Check the agent's **First name**, **Last name** and input the **Email addresses** of the agent.

- Click on **`+`** sign and add the supervisor in the same way.

- For consistency, verify that the **Email addresses** are same as in the table above and click **_Next_**.

- Next **Assign license for users** and select **_Webex Calling (Professional)_** & **_Contact Center (Premium Agent)_**.

- On the next page, make sure that the **_Location_** is selected under **_Assign Numbers_**. The correct value should be already selected by default.

- The **_Phone Number_** left as **None**.

- On the same page, Enter the correct **`Extension`** under **_Assign Numbers_**. The correct Extensions should be provided to you with the admin credentials.

- In step **Step 4: Review** verify the data and Click **_Add users_**.

- On the next page, you should get confirmation **"2 users added"**. Confirm the same by pressing **_Close_**.

- Now select the supervisor user and modify his role to **_Premium Agent - Supervisor Role_** by clicking the **_Edit Licenses_** button in the **_Licenses_** section.

- Click **_Save_** and **_Close_** to confirm the changes.

- Validate the users by going to the email account. Open the Control Hub validation email and follow the **Cisco Webex** instructions to activate the both accounts.

- Refresh the **_Users_** page in the Control Hub, make sure that both users are in **Active** status.

## 1.2: Contact Center User Configuration

> The following section outlines how to verify the Site, Team, and Multimedia Profile that will be assigned to the Contact Center users. We will also learn how to navigate to the Webex Contact Center admin section and how to associate newly created Sites, Teams, and Multimedia Profiles with new users.

![Admin_Experience](/assets/images/admin_exp_1.gif)

| **Entity**          | **Name**                                      |
| ------------------- | --------------------------------------------- |
| Multimedia Profiles | <w class="attendee_out">attendeeID</w>\_MMP   |
| Site                | <w class="attendee_out">attendeeID</w>\_Site  |
| Team1               | <w class="attendee_out">attendeeID</w>\_Team1 |

> **NOTE:** Here, the configuration is created with your **Attendee ID** and should be used as the prefix for all your configurations.
> {: .block-tip }

### 1. Verify the Multimedia Profile

- Login with admin credentials to Control Hub by accessing [https://admin.webex.com](https://admin.webex.com){:target="\_blank"}.

- In the left pane navigate to **_Contact Center_** card.

- Scroll down in the left navigation panel to the **_DESKTOP EXPERIENCE_** section and click on **_Multimedia Profiles_**.

- Click on **`Create Multimedia Profile`** button.

- Input Name as **<w class="attendee_out">attendeeId</w>\_MMP**.

- In the Media Details section, leave the **Blended** mode and input **`1`** for **_Voice_**, **`3`** for **_Chat_**, **`3`** for **_Email_**, **`3`** for **_Social_**, and click **_Create_** button in the lower right corner.

### 2. Verify the Site

- Navigate to **_USER MANAGEMENT_** in the left navigation panel and select **_Sites_**.

- Click on **`Create Site`** button and provide the Name as **<w class="attendee_out">attendeeId</w>\_Site**.

- Select your MMP in the **_Multimedia profile_** drop down list and hit **_Create_**.

### 3. Verify the Teams

- Navigate to **_Teams_** under the **_USER MANAGEMENT_**.

- Click on the **`Create Team`**.

- Input _Name_ as **<w class="attendee_out">attendeeId</w>\_Team1**.

- Select your site from the **_Parent Site_** drop-down.

- Select the **_team type_** **`Agent Based`**.

- Select your **_Multimedia profile_**.

- Left as a default value **_Global Layout_** in the **_Desktop layout_** drop-down and click on **_Create_** button.

### 4. Activating the Contact Center Settings for users

- On Webex Control Hub, navigate to **_Contact Center Users_** under the **_USER MANAGEMENT_**.

- Find your and select the agent, to launch the **_Edit_** view for a particular User configuration.

- Click on **_Contact Center Enabled_** toggle to move it to **_On_**.

- In the **_Agent Settings_** section, select your site in the **_Site_** drop-down.

- Click the **_Teams_** area and select your team

- Select the default **_Agent-Profile_** in the **_Desktop Profile_** drop-down list.

- Choose the **_Multimedia Profile_** and hit **_Save_**.

- In the User's table make sure that the agent is now shown with the **_Contact Center Enabled_** flag as **`Yes`** and **_Status_** as **`Active`**.

- Repeat the steps above for the supervisor.

## 1.3: Bulk Operations

> In this section you will learn how to use the Bulk Configuration in Control Hub by creating a third team. As an administrator, you can use Bulk Operations to create, modify, import, or export configuration objects in Webex Contact Center. This feature provides greater speed and efficiency to deploy and configure Webex Contact Center systems.

Bulk Operations are available for the following configuration object types:

| ------------------- | -------------------- |
| ------------------- | -------------------- |
| Entry Point         | Auxiliary Code       |
| Queue               | Agent Profile        |
| Outdial Entry Point | Address Book         |
| Outdial Queue       | Outdial ANI          |
| Site                | Skill Definition     |
| Team                | Skill Profile        |
| Users               | Entry Point Mappings |
| User Profiles       | Audio Files          |
| Work Types          | Global Variable      |

### Create the third Team

- Go to the Control Hub by accessing [https://admin.webex.com](https://admin.webex.com){:target="\_blank"}.

- In the left pane navigate to **_Contact Center_** card.

- Select **_Bulk Operations_** in the Webex CC navigation pane from the left.

- Click **_Create Bulk Operations_** button in the right upper corner.

![Bulk Menu](/assets/images/Bulk-1.gif)

- In Step 1 select the configuration object **_Team_** in the drop-down list.

- In the Export section enter the **MyTeam** as the file name and click **Next** button.

- Once the task is **Completed** click on **_Download export file_** button under the **Action** and open the csv file in the notepad.

- The first line is the headers, it is mandatory to have it during the import process. Remove all lines from the CSV file except the first line with headers and the line with **<w class="attendee_out">attendeeId</w>\_Team3**.

```csv
NAME,SITE,TYPE,MULTIMEDIA PROFILE,SKILL PROFILE,DN,CAPACITY,DESKTOP LAYOUT
###_Team1,###_Site,AGENT,###_MMP,,,,Default Desktop Layout
```

- Rename the Team1 to **<w class="attendee_out">attendeeId</w>\_Team2** and save the file. You should have only 2 rows in the file.
  Example:

```csv
NAME,SITE,TYPE,MULTIMEDIA PROFILE,SKILL PROFILE,DN,CAPACITY,DESKTOP LAYOUT
###_Team3,###_Site,AGENT,###_MMP,,,,Default Desktop Layout
```

- Go back to the **Bulk Operations** menu and click **_Create Bulk Operations_** button again.

- In step 1, select the **_Team_** configuration object from the drop-down list and **import** the CSV file by dragging it into the Import section.

- Click **Next** button and wait the results. The status should be shown as **Completed**.

- On Webex Control Hub, navigate to **_Teams_** under the **_USER MANAGEMENT_** tab and verify that the **<w class="attendee_out">attendeeId</w>\_Team3** is created.


## 1.4: Access to the Agent Desktop

> We will now log in to the Agent Desktop with your credentials and use Desktop (WebRTC) as the telephony device.

> **Note: Please use Google Chrome as the browser to take advantage of the all new WebRTC Voice Option.**
> {: .block-warning }

### 1. Download and Login in the Webex app for PC or Mac

> For the supervisor user, **Lab Tenant** you would need Webex app for placing calls to Entry Point and sign in as supervisor.
> {: .block-warning }

- Download the Webex app from **[https://www.webex.com/downloads.html](https://www.webex.com/downloads.html){:target="\_blank"}**.

![Webex App](/assets/images/Lab1-AD-1.png)

- Install the application on your PC/Mac.

- Open Webex app and сlick **Sign In**. Specify the supervisor credentials.

### 2. Agent Desktop Login

> **Note**: To log in to the agent desktop, we will use Chrome profiles so that we can use the same browser for Admins, Agents and Supervisors without clearing the cache.
> {: .block-tip }

- Here is how you create a Chrome profile so you can login the Agent on the same browser

  - Select **`Profiles`** on Chrome
  - Select **`Add Profile`**
  - Select **`continue without an account`**
  - Give it a name .i.e **`supervisor`**
  - Click **`done`**

![CH-Desktop-Call-In-Accepted](/assets/images/agent/Chrome-Create-Profile.gif)

---

- After you create a new Chrome Profile, navigate to **[https://desktop.wxcc-us1.cisco.com/](https://desktop.wxcc-us1.cisco.com/){:target="\_blank"}** in the chrome browser with the incognito mode.

- Enter the agent’s **email ID** which you created in the previous task.

- Enter the **Password** for the appropriate username.

- In the **_Station Credentials_** pane, select **"Desktop"**.

- Select the team **<w class="attendee_out">attendeeId</w>\_Team1**.

- Click **_Submit_** button. The browser may ask you to confirm use the microphone from the browser.

- Make sure that you are successfully logged in to the Agent Desktop.

![Agent Sign In](/assets/images/AG-2.gif)

# Part 2: Introduction to Flow Designer

Flow designer is a simple drag-and-drop user interface (UI) to define the flows. The following steps explain the Flow Designer layout, activity library, and terminology used in the Flow Designer.

In this lab, we will configure all of the required elements to deliver a call into a queue. We will then create a new flow and iterate on it adding functionality and exploring opportunities for improvement.

### Objective

- Looking at the configuration of Entry Points (Channels), Entry Point Mapping, Routing Strategy, and Queue
- Verifying the basic flow
- Verify functionality to the flow by looking at various use cases.

---

**Note:** If you have prior experience with creating flows, please navigate to step 2:.
{: .block-warning }

## 2.1: Configuring tenant for Call Delivery

⚠️ You can use this link to download the [Audio Files](https://webexcc.github.io/assets/files/lab_wav.zip){:target="\_blank"}. Those files are already pre-uploaded on the Lab Tenant.

### Create a queue

1. On Webex Control Hub, navigate to **_Queues_** under the **_CUSTOMER Experience_** tab and create a queue: **<w class="attendee_out">attendeeId</w>\_EP**

<img src="/assets/images/fe_33.png">

2. Click New Queue

   > Name your queue:  <w class = "attendee_out">attendeeID</w>\_Q 
   >
   > Description: optional
   >
   > Channel Type: Telephony
   >
   > Queue Routing Type: Longest Available Agent
   >
   > Call Distribution:
   >
   > > Click Add Group
   > >
   > > Select <w class="attendee_out">attendeeId</w>\_Team1
   > >
   > > Save Group
   > >
   > > Create second group
   > >
   > > Select <w class="attendee_out">attendeeId</w>\_Team2
   > >
   > > After: 60 Seconds in queue
   > >
   > > Add Group as: Last
   > >
   > > Save Group
   > >
   > > Click Close
   >
   > ***
   >
   > Service Level Threshold: 60
   >
   > Maximum Time in Queue: 600
   >
   > Default Music in Queue: defaultmusic_on_hold.wav
   >
   > Save

   ***

### Create your first flow

1. Download the [Flow Template](https://webexone.github.io/../../../assets/files/flow_template.json){:target="\_blank"}

   > The file will open in a separate window.
   >
   > If using Firefox, Select the save option.
   >
   > <img src="/assets/images/IVR/saveJson.gif">
   >
   > If using Chrome or Edge, right click and select save.
   >
   > <img src="/assets/images/IVR/saveJsonChrome.gif" width="243">

   ***

2. Click Flows > Manage Flows > Import flows > Select flow_template

   > <img src="/assets/images/fe_2.gif">

3. Click the newly imported flow_template and this will Open the flow

   > <img src="/assets/images/fe_3.gif">
   >
   > Click on the Play Message node
   >
   > > Audio File: 0_English.wav
   >
   > ***
   >
   > Click on the Queue Contact node
   >
   > > Select Static Queue
   > >
   > > Queue: <w class = "attendee_out">attendeeID</w>\_Q 
   >
   > ***
   >
   > Click on the Play Music node
   >
   > > Select Static Audio File
   > >
   > > Music File: defaultmusic_on_hold.wav
   >
   > ***
   >
   > Click the Validation switch to turn on validation
   >
   > Click Publish Flow
   >
   > Add a Publish Note of your choosing
   >
   > Click Publish Flow
   >
   > Click Return to Flow
   >
   > Turn off Validation

   ***

### Verify your Entry Point

1. On Webex Control Hub, navigate to **_Channels_** under the **_CUSTOMER MANAGEMENT_** tab and verify that the **<w class="attendee_out">attendeeId</w>\_EP** is created.

<img src="/assets/images/fe_32.png">

2. Verify the Entry Point configuration
   >
   > Name your Entry Point EP\_<w class="attendee_out">AttendeeID</w>
   >
   > Description: optional
   >
   > Channel Type: telephony
   >
   > Service Level Threshold: 60
   >
   > Flow: Flow_template
   >
   > Music on Hold: defaultmusic_on_hold.wav
   >
   > Click Save
   >
   > ***



### Verify your Entry Point mapping

 On Webex Control Hub, navigate to **_Channels_** under the **_CUSTOMER MANAGEMENT_** tab: 

 <img src="/assets/images/fe_31.png">
   
   >
   > - Go to **_Support Number_** and verify the below: 
   > 
   > - **`Webex calling location`** is set as **`US`**
   >
   > - **`Support Number`** is set to the the EP-DN assigned to you 
   >
   > - **`PSTN Region`** as **`Default`** 
   >
   > - Click **`Save`**
   >
   > ***

### Test your configuration

1. Call your assigned EP-DN from 
   > You should hear the greeting message and then the music in queue
   >
   > Go available in the agent desktop
   >
   > > The call should be delivered to your agent extension
   >
   > End the call, Wrap-up, and Go unavailable
   >
   > ***

## 2.2: Adding Text-To-Speech to the flow

<img src="/assets/images/fe_4.gif">
1. Select the PlayMessage node 
2. Enable **_Text-to-speech_** toggle 
3. Select the Connector  
4. Select Output voice as **_en-US-Standard-A_** 
5. Select Add Text-to-Speech Message 
6. Enter a message 
7. Validate and Publish the flow:   
   > Click the Validation switch to turn on validation
   >
   > Click Publish Flow
   > 
   > Add a Publish Note of your choosing
   >
   > Click Publish Flow
   >
   > Click Return to Flow
   > 
   > Turn off Validation 
   >
   > ---
8. Place a test call to your EP DN


> **Tip:** Please refer the article [Google Text-To-Speech Configuration](https://www.cisco.com/c/en/us/support/docs/contact-center/webex-contact-center/217425-configure-google-text-to-speech-for-webe.html){:target="\_blank"} for complete configuration steps
> {: .block-warning }


## 2.3: Adding Callback functionality to the flows

<img src="/assets/images/fe_5.png">
1. Create new flow variables:
   > Name: CallerANI
   >> Type: String
   >>
   >> No default value
   >
   ---
2. Add a new Menu node
    > Activity Label: Menu_Callback
    >
    > Prompt: Enable Text-to-Speech. Follow the previous lab and enter the message required for this lab 
    >
    > Make Prompt Interruptible: True
    >
    > Digit Number: 1 Link Description: confirm number
    >
    > Digit Number: 2 Link Description: change number
    >
    > Connect No-Input Timeout to the front of the Menu node
    >
    > Connect Unmatched Entry to the front of the Menu node
    >
    > ---
3. Add a Set Variable node
   > Activity Label: callbackANI_set
   >
   > Select Variable: CallerANI
   >
   > Set to Value: \{\{NewPhoneContact.ANI \| slice (NewPhoneContact.ANI.length -10,NewPhoneContact.ANI.length)\}\}
   >
4. Add a Collect Digits node
   > Activity Label: newNumber 
   >
   > Audio File: new_number_English.wav
   >
   > Make Prompt Interruptible: True
   >
   > Minimum Digits: 10
   >
   > Maximum Digits: 10
   >
   > Connect No-Input Timeout to the front of the newNumber node
   >
   > Connect Unmatched Entry to the front of the newNumber node
   >
   > ---
5. Add a Set Variable Node
   > Activity Label: newCB
   >
   > Variable: CallerANI
   >
   > Set Value: \{\{newNumber.DigitsEntered\}\}
   >
   > ---
6. Connect newNumber to newCB
7. Drag and Drop a Callback node 
   > Activity Label: Callback_node
   >
   > Callback Dial Number: CallerANI
   >
   > Static ANI: Any ANI you like but this DN needs to be mapped to an EP or select the default outdial ANI
   >
   > ---
8. Drag and Drop a PlayMusic node  
   > Activity Label: Callback_confirm
   >
   > Static Audio File
   >
   > Music file: callback_confirm_English.wav
   >
   > ---
8. Drag and Drop a Disconnect Contact node
   > Activity Label: Disconnect_contact
   >
   > ---

---

## 2.4: Business Hours Configuration

Business hours(BH) is a feature that lets you define the operational hours of contact center. In addition to that, we can also add holidays, or event driven interventions like extended working hours during festival seasons. This feature is an upgrade over routing strategy.

Business hours aims to remove all such pain points. There are 3 sub entities which comes under business hours:

> 1.  Working hours - Define normal operational hours. Add one or more shifts to have per-day or per-hour timing control
> 2.  Holidays - Define 24 hours break in operations like Christmas Day
> 3.  Overrides - Define an event based intervention in which operational hours are disrupted. Like black Friday sale when CC is operating at additional capacity. Or like emergency downtime, in which we close all operations immediately

The subsequent flow execution from BH activity takes the following priority:

> 1.  Priority-1 Override: checks if any of the override schedules apply at a given moment during execution
> 2.  Priority-2 Holidays: checks if any of the holiday hours schedules apply at a given moment during execution
> 3.  Priority-3 Working hours: checks if any of the working hours shift schedules apply at a given moment during execution
> 4.  Priority-4 Default: If no schedule applies, then route following the "Default" port will be selected

<img src="/assets/images/fe_16.png">

### 1. Create a Business Hours Schedule

- Login with admin credentials to Control Hub by accessing [https://admin.webex.com](https://admin.webex.com){:target="\_blank"}.

- In the left pane navigate to **_Contact Center_** card.

- Scroll down in the left navigation panel to the **_CUSTOMER EXPERIENCE_** section and click on **_Business Hours_**.

<img src="/assets/images/fe_17.png">

- Click on **`Working Hours`** button and select **_Create Working Hours_**

<img src="/assets/images/fe_23.png">

- Add a **`Name`**, **`Timezone`** and **`Shift`** to your schedule

<img src="/assets/images/fe_19.png">

- Select **`Save`** at the bottom

- To add a holiday schedule, click on **_Business Hours_** and select **`Holiday Lists`**

- Select **`Create Holiday List`** and enter the list of holidays.

<img src="/assets/images/fe_20.png">

- Now you can Go back to **`Working Hours`** button and select **_Create Working Hours_** and select the **`Holiday Lists`** created under **`Additional Settings`**

<img src="/assets/images/fe_21.png">

- Similar steps can be followed to create **`Override`** schedule

### 2. Verify the Configuration

Verify the Business Hours configuration by using this on the flow

> **Tip:** Use the **`Reference List`** section within **`Working Hours`** to check the Entity Name the schedule is referenced by
> {: .block-warning }

<img src="/assets/images/fe_25.png">

---

##  2.6: Bringing it all together: Advanced Flow configuration 

### Update your Entry Point

1. On Webex Control Hub, navigate to **_Channels_** under the **_CUSTOMER EXPERIENCE_** tab and update the flow assigned to the **<w class="attendee_out">attendeeId</w>\_EP** to the below.

- Select flow **QtoA_WebexOne_InboundFlow**

2. Place a call to your your assigned EP-DN from 
   > You should hear the greeting message and then the music in queue
   >
   > Go available in the agent desktop
   >
   > > The call should be delivered to your agent extension
   >
   > End the call, Wrap-up, and Go unavailable
   >
   > ***

3. Open the flow **QtoA_WebexOne_InboundFlow** and review the flow configuration  


# Part 3: Introduction to Flow Debugger

From a UI standpoint, the flow builder UI contains a "Debug" button on the bottom pane. Clicking the button brings up the pane displaying a list of previous interactions of the flow in production. By default, there are only 100 latest interactions displayed, but the user can either input in a specific interaction ID or a date range to filter the interactions displayed.

<img src="/assets/images/fe_12.png">

---

Once the user selects an interaction, the Interaction Detail pane displays the list of all the activities involved in the interaction along with their inputs/outputs, start times and end times of execution.

<img src="/assets/images/fe_13.png">

---

## 3.2: Verify the Flow Debugger functionality

Place a call to the flow and trace the call through the Flow Debugger.

> **Tip:** Selct **`Edit: Off`** to open the flow in **`Read-Only`** mode when using using the debug functionality
> {: .block-warning }

# Part 4: Introduction to Flow Versioning

Tagging a version of the flow should come up while publishing. There are 3 predefined tags - Live, Dev, Test, and one default Tag - Latest. The tag selection dropdown is visible after publish button is hit. Multiple tags are allowed to be selected. Once selected and published and those tags are associated to that specific version.

<img src="/assets/images/fe_7.png">

---

During entry point edit, the tags can be selected as well, here only the tags which are currently in use are shown.

<img src="/assets/images/fe_8.png">

---

During debugging, the tags filter allows to filter any of the previous or current interactions that had those tags during execution between the time range selected.

<img src="/assets/images/fe_9.png">

---

While looking at the previous versions history, by clicking on the clock icon located at the top panel the previous versions comes up with their tags. The versions which used to have tags and have been moved to later versions, show the tags with lighter color tone.

<img src="/assets/images/fe_10.png">

---

While using goto activity(which points to another flow), the tag selection drop down appears in the properties pane. This allows flow developer to choose a specific tagged version to goto and their corresponding variables are used for mapping.

<img src="/assets/images/fe_11.png">

---

# Part 5: Flow Error Handling

The error handling feature tries to deal all kinds of errors during the flow execution. Due to the nature of errors, it could be divided into two levels: the activity error and the global error[Global Error Handler].

1. On the activity level, error paths are designed to handle specific problematic situations and it gives the flow designer more freedom on how to properly handle these scenarios
2. For errors that are not captured by the activity error nodes, the global error handler would come into play and process the errors.

<img src="/assets/images/fe_14.png">

## Activity Level Error Handling

> Defined Errors: These are the errors which are already known to flow designers or the activity owner while creating a flow. They are managed by themselves by adding the error node to the activity.

> Undefined Error: Undefined errors are a way to handle unexpected system conditions.

<img src="/assets/images/fe_15.png">

---

# Part 6: Workflow in Outdial Entry Point

The intend of this feature is to get workflow support for Outbound

With this feature, we will get the the option to give the flow, Music on Hold and outbound queue in outdail entry point page on portal. if we don't provide the flow,moh and outdail queue details to the entry point then by default the configurations present will be taken for the call execution which is without flow

## 6.1: Create an Outbound flow

1. Download the [Outbound Flow Template](https://webexone.github.io/../../../assets/files/WebexOne_OutdialFlow.json){:target="\_blank"}

2. Follow the similar steps provided in **`Section 2.1`** to import and publish the flow

3. Within the flow, navigate to Event Flows notice that the Screen pops configured for the AgentOffered event

<img src="/assets/images/fe_27.png">

---

## 6.2: Verify your Outdial Entry Point

1. On Webex Control Hub, navigate to **_Channels_** under the **_CUSTOMER MANAGEMENT_** tab and verify that the **WebexOne_Outdial_EP** is created.

2. Verify the **`Name`**, **`Flow`**, **`Music On Hold`**, **`Outdial Queue`**

<img src="/assets/images/fe_26.png">

### Update the Desktop profile

- Navigate to **_Contact Center Users_** under the **_DESKTOP MANAGEMENT_**.

- Select the Agent profile assigned to the user under **_Desktop Profile_**

- Select **_Dial plans_** and under **_Outdial Entry Point_**, enter the outdial entry point created in the above step

<img src="/assets/images/fe_28.png">

## 6.3: Verify the configuration

Place an outbound call as an agent from Agent Desktop

> **Note:** The **`Outdial queue`** selected as part of the outdail entry point is currently purely for reporing purposes.
> {: .block-warning }

## 6.4: Caveats

### Unsupported Flow Activities

Below activities are not supported for the outdail voice contacts. If we configure these in flow, these activities will fail:

- Queue Contact Activity
- QueueToAgent Activity
- Callback Activity
- Get Queue Info Activity
- Advanced Queue Info Activity
- Blind Transfer Activity

### Supported Flow Activities

Below activities can we used in flow for outdial voice contacts.

- HTTP Request
- Condition
- Parse
- Set Variable
- Business Hours
- EndFlow
- Screen PopUp

---

# Bonus: Experience Management

| Topic                                                                                                                  | Lab Type           | Difficulty Level | Estimated length |
| ---------------------------------------------------------------------------------------------------------------------- | ------------------ | ---------------- | ---------------- |
| [Introduction to Experience Management](#introduction-to-experience-management-post-interaction-and-post-call-surveys) | Watch & Understand | EASY             | 7 min            |
| [Configure Post Call IVR Survey](#configure-post-call-ivr-survey)                                                      | Practical Lab      | EASY             | 10 min           |
| [Configure Post Interaction Digital Survey](#configure-post-interaction-digital-survey)                                | Practical Lab      | EASY             | 10 min           |

### Overview of the lab

In this lab, we will configure all the required elements to collect and view end-customer feedback using the new Experience Management.

### Lab Objective

- Create a basic survey
- Upload audio files to the survey
- Configure the survey in flow designer
- Simulate a customer interaction with survey feedback
- Download and verify survey feedback

  ***

### Pre-requisites

1.  You have **completed Lab 1 - Admin Experience:**
    - You are familiar with Control Hub and navigation within Control Hub
2.  You have **completed Lab 2 - IVR Contact Routing:**
    - You are familiar with creating and modifying flows
3.  You have **completed Lab 3 - Agent Desktop:**
    - You are familiar with logging in as an Agent and accepting inbound interactions
4.  You have **Webex Calling installed** in your mobile phone and supervisor created in Lab 1 from which you can make calls to the contact center

    ***

### Quick Links

> Control Hub: **[https://admin.webex.com](https://admin.webex.com){:target="\_blank"}**\
> Portal: **[https://portal.wxcc-us1.cisco.com/](https://portal.wxcc-us1.cisco.com/){:target="\_blank"}**\
> Agent Desktop: **[https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com){:target="\_blank"}**\

---

## 1. Introduction to Experience Management Post Interaction and Post Call Surveys

> Experience Management is a next-gen tool that facilitates post interaction surveys and outcomes. It allows you to track and measure customer satisfaction using anchor metrics like Net Promoter Score (NPS), Customer Effort Score (CES), and Customer Satisfaction (CSAT). Webex Contact Center brings in an integration of Experience Management for its post call survey interactive voice response (PCS IVR) and digital channels.

### Lab Section

## 2. Configure Post Call IVR Survey

### Create a survey

1. Click on Contact Center under Services from Control Hub
   > <img src="/assets/images/EM/contactCenter.gif" width="200">
2. Under Contact Center, click on Surveys
   > <img src="/assets/images/EM/survey.gif" width="200">
3. Click the "Create new survey" button on the top-right corner of the Survey page
   > Select Survey type as IVR
   >
   > > <img src="/assets/images/EM/surveyType.gif">
   > >
   > > Provide a name for your survey appended with your Attendee ID
   > > <img src="/assets/images/EM/surveyName.gif">
   > >
   > > Choose the additional languages for the survey from the drop-down (optional)
   > > <img src="/assets/images/EM/languageSupport.png">
   > >
   > > Click on Next
4. Add audio files to the Welcome and Thank you notes ([Audio Files](https://webexcc.github.io/assets/files/Survey_wav.zip){:target="\_blank"})
   > Click on the pencil icon to the right
   >
   > >  <img src="/assets/images/EM/welcomeThankyou.gif">
   > >
   > > Select Choose a file when the note expands, pick the audio file (Welcome.wav) and upload
   > > <img src="/assets/images/EM/uploadWelcome.gif">
   > >
   > > Repeat steps for Thank you note (Thankyou.wav)
5. Add a question to your survey
   > Select the NPS question from the drop-down by clicking + Add a question
   >
   > > <img src="/assets/images/EM/addNPS.gif" width="200">
   > >
   > > Choose the corresponding audio file, nps.wav for the NPS question and upload ([Audio Files](https://webexcc.github.io/assets/files/Survey_wav.zip){:target="\_blank"})
   > > <img src="/assets/images/EM/uploadNPS.gif">
   > >
   > > Under Question to show on reporting type the column name as "NPS Score"
   > > <img src="/assets/images/EM/NPSReporting.gif">
6. Update Error handling settings (optional)
   > Upload audio files for Invalid Input and Timeout by clicking on Choose a file under each section
   >
   > Set the maximum number of invalid inputs and timeouts allowed from the drop-down
   >
   > Choose an audio file for exceeding maximum tries
7. Save the survey from the bottom right corner

---

### Add the feedback activity to your flow

> **NOTE:** Refer to the Lab 2 - IVR Contact Routing if you are unfamiliar with working on flow designer
> {: .block-warning }

1. Open your flow created from Lab 2 - IVR Contact Routing
2. Introduce a Menu into your main flow to prompt the caller to opt-in for the survey in between the NewPhoneContact event and the Queue Contact node
   > Activity Label: surveyOptin
   >
   > Prompt: OptinMenu.wav ([Audio Files](https://webexcc.github.io/assets/files/Survey_wav.zip){:target="\_blank"})
   >
   > Make Prompt Interruptible: True
   >
   > Digit Number - 1
   >
   > > Link Description: Opt-In
   >
   > Digit Number - 2
   >
   > > Link Description: Opt-Out
3. Assign true and false values for the Global_FeedbackSurveyOptin variable
   > Drag and drop two Set Variable nodes into your main flow after the Menu
   >
   > Click on the first Set Variable node
   >
   > > Activity Label: OptIn
   > >
   > > Variable: Global_FeedbackSurveyOptin
   > >
   > > Set Value: TRUE
   >
   > Click on the second Set Variable node
   >
   > > Activity Label: OptOut
   > >
   > > Variable: Global_FeedbackSurveyOptin
   > >
   > > Set Value: False
4. Connect the nodes together
   > Connect Custom Menu Links for digit 1 to the Set Variable node with Global_FeedbackSurveyOptin set as true
   >
   > Connect Digit 2 and error handling links to the Set Variable node with Global_FeedbackSurveyOptin set as false
   >
   > Connect the Set Variable blocks back to your flow before Queue Contact
   >
   > Example Flow
   >
   > > <img src="/assets/images/EM/surveyOptin.png">
5. Navigate to the Event Flows tab
6. Add the Feedback V2 node
   > Connect the Feedback V2 node to the AgentDisconnected Activity
   >
   > Click on the Feedback V2 node
   >
   > > Activity Label: PCS_IVR
   > >
   > > Survey Method: Voice Based
   > >
   > > Select survey created earlier from drop-down
   > >
   > > Timeout: 10
7. Complete the flow by adding a Disconnect Contact node after the Feedback V2 node
   > Example Flow
   >
   > > <img src="/assets/images/EM/feedbackV2.png">
8. Validate and Publish the flow

---

## 3. Provide a survey response

> **NOTE:** Refer to the section Basic Features in Lab 3 - Agent Desktop if you are unfamiliar with testing an incoming call
> {: .block-warning }

1. Login to your Agent Desktop and make your state Available
2. Dial your designated DN and accept the incoming voice interaction
3. Provide the DTMF input 1 to opt-in to the survey
4. End the interaction from the Agent Desktop
5. Provide a rating on the scale 0-9

---

## 4. Download and validate the survey response

1. Navigate to the Surveys page on Control Hub
2. Click on the download button on the far right of your survey
   > <img src="/assets/images/EM/downloadResponse.gif">
3. Select the date range for the survey response period as Last 7 days and click Download
   > <img src="/assets/images/EM/downloadDate.gif">
4. Verify your response in the excel sheet to the one you provided on the call
   > <img src="/assets/images/EM/surveyReport.png">

---

# Bonus: Other Flow Enhancments

## 1. Flow Search

The entry point for the Search feature is the newly added <input> located towards top right of flow designer. This list will update to include up to five matching results.

For shortcut to search please select: **`Ctrl`** **`K`**

<img src="/assets/images/fe_29.png">

---

## 2. Flow Aesthetic Improvements

This feature provides support to Curved Links, Configure link color, Activity border color, Link selection color, activity border color, Link thickness and Activity border thickness.

<img src="/assets/images/fe_30.png">

---

<p style="text-align:center"><strong>Congratulations, you have completed this lab! You can continue with the next one.</strong></p>
		
<p style="text-align:center;"><img src="/assets/gitbook/images/webex.png" width="100"></p>
