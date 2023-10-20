---
title: Admin and Flow Experience
author: Bhushan Suresh
date: 2023-10-15
layout: post
---
```
Last modified: Wed, 20 Sep 2023
```

<script>
    function update(){them = Array.from(document.querySelectorAll("input")).reduce((acc, input) => ({...acc, [input.id + "_out"] : input.value}),{});
	Object.entries(them).forEach((entry) => {
    Array.from(document.getElementsByClassName(entry[0])).forEach((element,index) => 
    {
      console.log(document.getElementsByClassName(entry[0])[index].innerHTML); 
      document.getElementsByClassName(entry[0])[index].innerHTML = entry[1];
    })})

  event.preventDefault()
  if(document.forms["IVRdeets"][1].value != "Your Attendee ID"){
    localStorage.setItem("attendeeID",document.forms["IVRdeets"][1].value)
  }  
  }
</script>

# Table of Contents

| Topic                                                                                 | Lab Type           | Difficulty Level | Estimated length |
| ------------------------------------------------------------------------------------- | ------------------ | ---------------- | ---------------- |
| [Part 1: Introduction to the new Admin Experience](#introduction-to-the-new-admin-experience) | Watch & Understand | EASY             | 10 min           |
| [    1:1 Control Hub User Management Tasks](#control-hub-user-management-tasks)               | Practical Lab      | EASY             | 10 min           |
| [    1:2 Contact Center User Configuration](#contact-center-user-configuration)               | Practical Lab      | EASY             | 10 min            |
| [    1:3 Bulk Operations](#bulk-operations)                                                   | Practical Lab      | EASY             | 5 min            |
| [    1:4: Access to the Agent Desktop](#access-to-the-agent-desktop)                           | Practical Lab      | EASY             | 10 min           |
| [Part 2: Introduction to Flow Designer](#introduction-to-flow-designer) | Watch & Understand | EASY    | 10 min|  
| [    2:1 Configuring tenant for Call Delivery](#configuring-tenant-for-call-delivery)        | Practical Lab | EASY            | 10 min           |
| [    2:2 Adding a comfort message while a call is in queue](#adding-a-comfort-message-while-a-call-is-in-queue) | Practical Lab | EASY            | 8 min            |
| [    2:3 Creating alternating comfort messages while a call is in queue](#creating-alternating-comfort-messages-while-a-call-is-in-queue)                                           | Practical Lab | EASY            | 15 min            |
| [    2:4 Creating an opt-out option with ANI readout](#creating-an-opt-out-option-with-ani-readout)                   | Practical Lab | EASY            | 15 min           |
| [    2:5 Adding the ability to receive a callback at a different number](#adding-the-ability-to-receive-a-callback-at-a-different-number)                   | Practical Lab | EASY            | 15 min           |
| [    2:6 Adding the ability to collect an extension and present it to an agent during a callback](#adding-the-ability-to-collect-an-extension-and-present-it-to-an-agent-during-a-callback)                   | Practical Lab | EASY            | 15 min | 
| [    2:7 Introduction to Flow Debugger](#introduction-to-flow-debugger)                   | Practical Lab | EASY            | 15 min | 
| [    2:8 Introduction to Flow Versioning](#introduction-to-flow-versioning)                   | Practical Lab | EASY            | 15 min | 
| [Part 3: Bonus - Experience Management](#bonus---experience-management)                   | Practical Lab | EASY            | 15 min | 


# Overview of the Admin Experience 

In this Lab, we will go through Admin UI by completing the tasks that are required for the general pre-configuration of a tenant. These tasks are to be undertaken by a customer administrator. By following each of the steps, you would have prepared your tenant to begin configuring different services offered by the platform. At the end of the lab, you should be able to log in to an agent interface with the configured user extension.
You can do the tasks from the lab guide either on the **Lab Tenant** (you need to request access from the lab support team) or you can do it directly on your **Gold Tenant** / personal tenant.

### Introduction

### Lab Objective

- This lab is designed to help you do the initial setup and configuration of the tenant.
- The lab contains multiple exercises on Control Hub (Admin Portal) to make you comfortable with the Webex Contact Center application.

### Pre-requisites

- You have Admin access to Control Hub 
- You have the PSTN number (dialed number) registered on the Control Hub

### Quick Links

> Control Hub: **[https://admin.webex.com](https://admin.webex.com){:target="\_blank"}**\
> Agent Desktop: **[https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com){:target="\_blank"}**\

### Lab Section

## Introduction to the new Admin Experience

> The overall aim of admin consolidation is to provide a single pane of glass (SPOG) experience for administrators so that admins need not have frequent context switch by having to traverse different applications. The following video outlines the new features of a new admin experience. This introduces, the new left navigation panel for Webex Contact Center in Control Hub as well as other configuration settings which were migrated from the Management Portal.

![Admin_Experience](/assets/images/AE_image1.png)

## Control Hub User Management Tasks

> The following video outlines the process to manage different types of users to the Customer tenant. Following the steps, you will add new users and set the Calling extension. While adding the user, we will see how to select user roles.

### 1. Define your Attendee ID and Other parameters

>Please **SKIP task #1** if you are doing the labs on the **Gold Tenant**. The task below is only for the **Lab Tenant** option where you have received an email with the Lab tenant credentials. In a such case, please copy and paste the Attendee ID number from the email into the corresponding field (Example: IDXXX).
{: .block-tip }

<form id="IVRdeets">

  <label for="attendee">Attendee ID:</label>
  <input type="text" id="attendee" name="attendee" onChange="update()"><br>

<br>

  <button onclick="update()">Save</button>
</form>

<script>
document.forms["IVRdeets"][1].value = localStorage.getItem("attendeeID") || "Your Attendee ID"


update()
</script>


### 2. Add agent and supervisor users and set the calling extensions

> We don't recommend using the @maildrop.cc or @mailinator.com accounts on your **Gold Tenant** due to security reasons. An attacker can easily gain access to your tenant and execute the outbound calls. 
{: .block-warning }

> - As a result of the task below you should add two new users (agent and supervisor) to the Control Hub and assign Webex CC Agent and Supervisor licenses. 
> - Please **SKIP task #2** if you are working with the **Lab Tenant**. This tenant is integrated with SSO where the agents and supervisors have been pre-created according to the table below. 
{: .block-tip }




| **User Role** | **User email**                                                                | **Endpoint** |
| ------------- | ----------------------------------------------------------------------------- | ------------- | 
| Agent         | wxcclabs+agent_<w class="attendee_out">AttendeeID</w>@gmail.com | WebRTC |
| Supervisor    | wxcclabs+supvr_<w class="attendee_out">AttendeeID</w>@gmail.com | Webex App |


- Login to the [Control Hub](https://admin.webex.com){:target="\_blank"} with the admin account.

- In the left navigation pane go to **_Users_** under **Management**.

- Click on **_Manage Users_** button.

- Select **_Manually add users_**.

- Set the agent's **First name**, **Last name** and input the **Email addresses** of the agent.

- Click on `+` sign and add the supervisor in the same way.

- For consistency, verify that the **Email addresses** are same as in the table above and click **_Next_**.

- In **Step 2: Assign license for users** select **_Webex Calling (Professional)_** & **_Contact Center (Premium Agent)_**.

- On the next page, make sure that the **_Location_** is selected under **_Assign Numbers_**. The correct value should be already selected by default.

- The **_Phone Number_** left as **None**.

- On the same page, Enter the correct `Extension` under **_Assign Numbers_**. The correct Extensions should be provided to you with the admin credentials.

- In step **Step 4: Review** verify the data and Click **_Add users_**.

- On the next page, you should get confirmation **"2 users added"**. Confirm the same by pressing **_Close_**.

- Now select the supervisor user and modify his role to **_Premium Agent - Supervisor Role_** by clicking the **_Edit Licenses_** button in the **_Licenses_** section.

- Click **_Save_** and **_Close_** to confirm the changes.

- Validate the users by going to the email account. Open the Control Hub validation email and follow the **Cisco Webex** instructions to activate the both accounts. 
 
- Refresh the **_Users_** page in the Control Hub, make sure that both users are in **Active** status.

## Contact Center User Configuration

> The following video outlines how to create a Site, Team, and Multimedia Profile that will be assigned to the Contact Center users. We will also learn how to navigate to the Webex Contact Center admin section and how to associate customer-created Site, Team, and Multi-Media Profile with new users.

![Admin_Experience](/assets/images/admin_exp_1.gif)

| **Entity**          | **Name**                                                |
| ------------------- | ------------------------------------------------------- |
| Multimedia Profiles | <w class="attendee_out">Your_Attendee_ID</w>_MMP   |
| Site                | <w class="attendee_out">Your_Attendee_ID</w>_Site  |
| Team1               | <w class="attendee_out">Your_Attendee_ID</w>_Team1 |



> **NOTE:** If you are using the **Lab Tenant** the **Attendee ID** should be used as a name prefix for all your configurations.
> {: .block-tip }

### 1. Create new Multimedia Profile

- Login with admin credentials to Control Hub by accessing [https://admin.webex.com](https://admin.webex.com){:target="\_blank"}.

- In the left pane navigate to **_Contact Center_** card.

- Click **_Settings_** in the upper menu.

- Scroll down in the left navigation panel to the **_DESKTOP EXPERIENCE_** section and click on **_Multimedia Profiles_**.

- Click on `Create Multimedia Profile` button.

- Input Name as **<w class="attendee_out">Your_Attendee_ID</w>_MMP**.

- In the Media Details section, leave the **Blended** mode and input `1` for **_Voice_**, `3` for **_Chat_**, `3` for **_Email_**, `3` for **_Social_**, and click **_Create_** button in the lower right corner.

### 2. Create new Site

- Navigate to **_USER MANAGEMENT_** in the left navigation panel and select **_Sites_**.

- Click on `Create Site` button and provide the Name as **<w class="attendee_out">Your_Attendee_ID</w>_Site**.

- Select your MMP in the **_Multimedia profile_** drop down list and hit **_Create_**.

### 3. Create new Team

- Navigate to **_Teams_** under the **_USER MANAGEMENT_**.

- Click on `Create Team`.

- Input _Name_ as **<w class="attendee_out">Your_Attendee_ID</w>_Team1**.

- Select your site from the **_Parent Site_** drop-down.

- Select the **_team type_** `Agent Based`.

- Select your **_Multimedia profile_**.

- Left as a default value **_Global Layout_** in the **_Desktop layout_** drop-down and click on **_Create_** button.

### 4. Activate the Contact Center Settings for the users 

- Navigate to **_Contact Center Users_** under the **_USER MANAGEMENT_**.

- Find your and select the agent, to launch the **_Edit_** view for a particular User configuration.

- Click on **_Contact Center Enabled_** toggle to move it to **_On_**.

- In the **_Agent Settings_** section, select your site in the **_Site_** drop-down.

- Click the **_Teams_** area and select your team

- Select the default **_Agent-Profile_** in the **_Desktop Profile_** drop-down list.

- Choose the **_Multimedia Profile_** and hit **_Save_**.

- In the User's table make sure that the agent is now shown with the **_Contact Center Enabled_** flag as `Yes` and **_Status_** as `Active`.

- Repeat the steps above for the supervisor.


## Bulk Operations

> In this section you will learn how to use the Bulk Configuration in Control Hub by creating a second team. As an administrator, you can use Bulk Operations to create, modify, import, or export configuration objects in Webex Contact Center. This feature provides greater speed and efficiency to deploy and configure Webex Contact Center systems.

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




### Create the second Team

- Go to the Control Hub by accessing [https://admin.webex.com](https://admin.webex.com){:target="\_blank"}.

- In the left pane navigate to **_Contact Center_** card.

- Select **_Bulk Operations_** in the Webex CC navigation pane from the left.

- Click **_Create Bulk Operations_** button in the right upper corner.

![Bulk Menue](/assets/images/Bulk-1.gif)

- In Step 1 select the configuration object **_Team_** in the drop-down list.

- In the Export section enter the **MyTeam** as the file name and click **Next** button.

- Once the task is **Completed** click on **_Download export file_** button under the **Action** and open the csv file in the notepad.

- The first line is the headers, it is mandatory to have it during the import process. Remove all lines from the CSV file except the first line with headers and the line with **<w class="attendee_out">Your_Attendee_ID</w>_Team1**.

```csv
NAME,SITE,TYPE,MULTIMEDIA PROFILE,SKILL PROFILE,DN,CAPACITY,DESKTOP LAYOUT
xxxx_team1,pod110_Site,AGENT,pod110_MMP,,,,Global Layout
```

- Rename the Team1 to **<w class="attendee_out">Your_Attendee_ID</w>_Team2** and save the file. You should have only 2 rows in the file.
  Example:

```csv
NAME,SITE,TYPE,MULTIMEDIA PROFILE,SKILL PROFILE,DN,CAPACITY,DESKTOP LAYOUT
xxxx_team2,pod110_Site,AGENT,pod110_MMP,,,,Global Layout
```

- Go back to the **Bulk Operations** menu and click **_Create Bulk Operations_** button again.

- In step 1, select the **_Team_** configuration object from the drop-down list and **import** the CSV file by dragging it into the Import section.

- Click **Next** button and wait the results. The status should be shown as **Completed**.

- Go to the Management Portal, click on **_Provisioning_** -> **_Team_** and verify that the **<w class="attendee_out">Your_Attendee_ID</w>_Team2** is created.

- In the Management Portal directly associate the **<w class="attendee_out">Your_Attendee_ID</w>_Team2** with your agent and supervisor by adding your users to that team (__Advanced Settings -> Agents__).


## Access to the Agent Desktop

> By following the steps below, you will log in to the Agent Desktop with your credentials and indicate the number (DN) where you want to receive the calls.

> The Lab Tenant is located in the US datacenter. It does not allow outbound international calls. If you have the U.S. numbers you can use that for sign in as an agent or supervisor. Otherwise, please WebRTC for agent and download the Webex App for supervisor according to the steps below.
{: .block-warning }

### 1. Download and Login in the Webex app for PC or Mac

>Please **SKIP task #1** if you are doing the labs on the **Gold Tenant**.

> For the **Lab Tenant** you would need Webex app for placing calls to Entry Point and sign in as supervisor. Alternatively, if you have the US number, you can use it as an supervisor's extension. This tenant does not allow numbers outside of the United States. In this lab, we will use the Webex app for your PC or Mac for the **supervisor** account.
{: .block-warning }

- Download the Webex app from **[https://www.webex.com/downloads.html](https://www.webex.com/downloads.html){:target="\_blank"}**.

![Webex App](/assets/images/Lab1-AD-1.png)

- Install the application on your PC/Mac.

- Open Webex app and сlick **Sign In**. Specify the supervisor credentials.


### 2. Agent Desktop Login

> **Note**: To log in to the agent desktop, use either a different web browser or a new incognito web page. This will prevent the browser caching issues with admin and agent credentials.
> Depending on your tenant's location the agent ULR link can be different. The example below is for the tenant in the US datacenter.
{: .block-tip }

- Navigate to **[https://desktop.wxcc-us1.cisco.com/](https://desktop.wxcc-us1.cisco.com/){:target="\_blank"}** in the chrome browser with the incognito mode.

- Enter the agent’s **email ID** which you created in the previous task.

- Enter the **Password** for the appropriate username.

- In the **_Station Credentials_** pane, select **"Desktop"**.

- Select the team **<w class="attendee_out">Your_Attendee_ID</w>_Team1**.

- Click **_Submit_** button. The browser may ask you to confirm use the microphone from the browser. 

- Make sure that you are successfully logged in to the Agent Desktop.

![Agent Sign In](/assets/images/AG-2.gif)

---

<p style="text-align:center"><strong>Congratulations, you have completed this lab! You can continue with the next one.</strong></p>
		
<p style="text-align:center;"><img src="/assets/gitbook/images/webex.png" width="100"></p>

# Introduction to Flow Designer

In this lab, we will configure all of the required elements to deliver a call into a queue.  We will then create a new flow and iterate on it adding functionality and exploring opportunities for improvement.

## Introduction

### Lab Objective

- Configure Entry Point, Entry Point Mapping, Routing Strategy, and Queue
- Create a basic flow
- Add functionality to the flow by making small changes

  ---

### Pre-requisites

- Complete Lab 1 "Admin Experience"
  - You have the administrator's access to the Tenant Management Portal.
  - Agent and Supervisor users created and configured
  - You have agent's access to the Agent Desktop
  - You have the supervisor's access to the Tenant Management Portal.
  - Agent is part of 2 Teams.
  - Webex Calling extensions are assigned to a WxCC users (agent and supervisor).
  
    ---

### Quick Links

> Control Hub: **[https://admin.webex.com](https://admin.webex.com){:target="\_blank"}**\
> Portal: **[https://portal.wxcc-us1.cisco.com/](https://portal.wxcc-us1.cisco.com/){:target="\_blank"}**\
> Agent Desktop: **[https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com){:target="\_blank"}**\

  ---



### Fill in the form with the details provided and agent email address you created in the previous lab, then click "Update Directions" 
>Please skip the task if you are doing the labs on the Gold Tenant. The task below is only for the Lab Tenant option where you have received an email with the Lab tenant credentials. In a such case, please copy and paste the data from the email into the corresponding fields.
{: .block-tip }
<form id="IVRdeets">
  
  <label for="DN">EP DN you were assigned:</label><br>
  <input type="tel" id="DN" name="DN" onChange="update()"><br>
  
  <label for="attendee">Attendee ID:</label><br>
  <input type="text" id="attendee" name="attendee" onChange="update()"><br>
  
  <label for="agent">Agent Email Address:</label><br>
  <input type="email" id="agent" name="agent" onChange="update()"><br>

  <label for="supervisorEXT">Supervisor Extension:</label><br>
  <input type="number" id="agent" name="supervisorEXT" onChange="update()"><br>
<br>

  <button onclick="update()">Update Directions</button>
</form>

<script>
document.forms["IVRdeets"][0].value = localStorage.getItem("EPDN") || "Your EP DN"
document.forms["IVRdeets"][1].value = localStorage.getItem("attendeeID") || "Your Attendee ID" 
document.forms["IVRdeets"][2].value = localStorage.getItem("agentEmail") || "Agent Email"
document.forms["IVRdeets"][3].value = localStorage.getItem("supervisorEXT") || "Supervisor Extension"
update()
</script>


---

## Lab Section - Flow Designer
> Flow designer is a simple drag-and-drop user interface (UI) to define the flows. The following video explains the Flow Designer layout, activity library, and terminology used in the Flow Designer.

![Flow Experience](/assets/images/fe_1.gif)

## Configuring tenant for Call Delivery

⚠️ You can use this link to download the [Audio Files](https://webexcc.github.io/assets/files/lab_wav.zip){:target="\_blank"}. Those files are already pre-uploaded on the Lab Tenant.

### Create a queue
1. Click on Provisioning > Entry Points/Queues > Queue
    > <img src="/assets/images/IVR/openQueue.gif">
    ---
2. Click New Queue
    > Name your queue Q_<w class="attendee_out">AttendeeID</w>
    >
    > Description: optional
    >
    > Channel Type: Telephony
    >
    > Queue Routing Type: Longest Available Agent
    > 
    > Call Distribution:
    >> Click Add Group
    >>
    >> Select <w class="attendee_out">Your_Attendee_ID</w>_Team1
    >>
    >> Save Group
    >>
    >> Create second group
    >>
    >> Select <w class="attendee_out">Your_Attendee_ID</w>_Team2
    >>
    >> After: 60 Seconds in queue
    >>
    >> Add Group as: Last
    >>
    >> Save Group
    >>
    >> Click Close
    >
    > ---
    >
    > Service Level Threshold: 60
    >
    > Maximum Time in Queue: 600
    >
    > Default Music in Queue: defaultmusic_on_hold.wav
    >
    > Save

    ---

### Create your first flow
1. Download the [Flow Template](https://webexcc.github.io/../../../assets/files/flow_template.json){:target="\_blank"}
   > The file will open in a separate window.  
   >
   > If using Firefox, Select the save option.
   >
   > <img src="/assets/images/IVR/saveJson.gif">
   >
   > If using Chrome or Edge, right click and select save.
   >
   ><img src="/assets/images/IVR/saveJsonChrome.gif" width="243">
   
      ---
2. Click Flows > Manage Flows > Import flows > Select flow_template
   > <img src="/assets/images/fe_2.gif">

3. Click the ellipsis next to the newly imported flow_template and select Open 
   > <img src="/assets/images/IVR/openFlow.JPG" height="40">
   > 
   > Rename the flow to <w class="attendee_out">AttendeeID</w>_TechSummit by clicking on the pencil icon at the top of the screen, next to the flow name
   >
   > Click on the Play Message node
   >> Audio File: welcome.wav 
   >
   > ---
   > Click on the Queue Contact node
   >> Select Static Queue
   >>
   >> Queue: Q_<w class="attendee_out">AttendeeID</w>
   >>
   > ---
   >
   > Click on the Play Music node
   >> Select Static Audio File
   >>
   >> Music File: defaultmusic_on_hold.wav
   >>
   >  ---
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

    ---



### Create your Entry Point

1. Click on Provisioning > Entry Points/Queues > Entry point
2. Click Create new Entry point [Show Me](https://webexcc.github.io/../../../assets/images/IVR/openEP.gif){:target="\_blank"}
    > Name your Entry Point EP_<w class="attendee_out">AttendeeID</w>
    >
    > Description: optional
    >
    > Channel Type: telephony
    >
    > Service Level Threshold: 60
    >
    > Flow: <w class="attendee_out">AttendeeID</w>_TechSummit
    >
    > Music on Hold: defaultmusic_on_hold.wav
    >
    > Click Save
    >
    > ---

### Create your Entry Point mapping

1. Click on Provisioning > Entry Point Mapping [Show Me](https://webexcc.github.io/../../../assets/images/IVR/openEPmap.gif){:target="\_blank"}
2. Click new mapping
    > In location, select "Office"
    >
    > In Available Numbers select <w class= "DN_out" >Your EP DN</w>
    >
    > In Entry point select EP_<w class="attendee_out">AttendeeID
    >
    > Click Save
    >
    > ---


### Test your configuration
1. Call <w class= "DN_out" >Your EP DN</w> from your supervisor extension
    > You should hear the greeting message and then the music in queue
    >
    > Go available in the agent desktop
    >> The call should be delivered to your agent extension
    >
    > End the call, Wrap-up, and Go unavailable
    >
    > ---

## Adding Functionality to Your Flow

## Adding a comfort message while a call is in queue
1. Delete the connection which loops from the end of the Play Music node back to the beginning of the Play Music node.
2. Drag a new Play Message node under the Play Music node. 
3. Click on the Play message node
   > 
   > Activity Label: comfortMessage
   >
   > Audio File: comfort_1_English
   >
   > ---
4. Click on the Play Music node
   > Set the music duration to 15 seconds 
   >
   > --- 
5. Connect the end of the Play Music node to the beginning of the play message node.
6. Connect the end of the Play Message node to the beginning of the Play Music node.
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
   > [Compare](https://webexcc.github.io/../../../assets/images/IVR/comfortMessage.JPG){:target="\_blank"}
   >
   > ---
8. Place a test call to <w class= "DN_out" >Your EP DN</w>
   > Did you hear the comfort message every 15 seconds?
   >
   > ---

### Creating alternating comfort messages while a call is in queue
1. Create a new flow variable: 
    > Click on the cog in the lower left corner of the canvas <img src="/assets/images/IVR/flowCog.JPG" height="40"> (or on the background of the flow) 
    >
    > Click Add Flow Variables
    >> Name: Loop_Count
    >> 
    >> Variable Type: Integer
    >>
    >> Default value: 0
    >
    > Click Save
    >
    > ---

2. Delete the connection from the Play Music node to the comfortMessage node.
3. Drag a Set Variable node onto the canvas and place it below the Play Music node
4. Click on the Set Variable node
    > Activity Label: lCount
    >
    > Variable: Loop_Count
    >
    > Set Value: \{\{ Loop_Count + 1 \}\}
    >
    > ---
5. Connect the Play Music node to lCount
6. Drag a Condition node on the canvas
7. Connect the end of the Set Variable node to the Condition node
8. Click on the condition node
    > Activity Label: evenOdd
    >
    > Expression: \{\{ Loop_Count is odd\}\}
    >
    > ---
9. Drag another Play Message node onto the canvas 
    > Activity Label: websiteMessage
    >
    > Audio File: website_English.wav
    >
    > ---
10. Connect the True node edge from evenOdd to comfortMessage
11. Connect the False node edge from evenOdd to websiteMessage
12. Connect the end of websiteMessage node to the Play Music node
13. Publish your flow [Compare](https://webexcc.github.io/../../../assets/images/IVR/altMessages.JPG){:target="\_blank"}
14. Place a test call to <w class= "DN_out" >Your EP DN</w>
    > Did you hear the comfort message and website message alternate every 15 seconds?
    >
    > ---

### Creating an opt-out option with ANI readout
1. Create new flow variables:
   > Name: callbackANI
   >> Type: String
   >>
   >> No default value
   >
   > ---
   >
   > Name: rDigit
   >> Type: string
   >>
   >> No default value
   >
   > ---
   >
   > Name: sPosition
   >> Type: Integer
   >>
   >> Default Value: 0
   >>
   ---
2. Delete the connection from the websiteMessage node to Play Music
3. Drag a Menu node onto the canvas
   > Activity Label: callback_opt
   >
   > Audio File: opt_out_English.wav
   >
   > Make Prompt Interruptible: True
   >
   > Digit Number: 1 Link Description: optOut 
   >
   > Connect the No-Input Timeout node edge to Play Music
   >
   > Connect the Unmatched Entry node edge to Play Music
   >
   > ---
4. Connect the websiteMessage to the callback_opt node
5. Add a Set Variable node
   > Activity Label: callbackANI_set
   >
   > Select Variable: callbackANI
   >
   > Set to Value: \{\{NewPhoneContact.ANI \| slice (NewPhoneContact.ANI.length -10,NewPhoneContact.ANI.length)\}\}
   >
   ---
6. Connect the callback_opt optOut node edge to callbackANI_set 
7. Add a Play Message Node
   > Activity Label: cfrom
   >
   > Audio File: calling_from_English.wav
   >
   > ---
8. Connect callbackANI_set to cfrom
9. Add a Set Variable node
   > Activity Label: rDigit_set
   >
   > Select Variable: rDigit
   >
   > Set to Value: \{\{callbackANI \| slice (sPosition,sPosition+1)\}\}
   >
   ---
10. Connect cfrom to rDigit_set
11. Add a Play Message node
   > Activity Label: playDigit 
   >
   > Click Add Audio Prompt Variable
   >> Audio Prompt Variable: \{\{rDigit\}\}_English.wav
   >>
   >> Delete the Audio File Drop Down
   >> 
   >> ---
12. Connect rDigit_set to playDigit
13. Add a Set Variable node
    > Activity Label: advance
    >
    > Select Variable: sPosition
    >
    > Set to Value: \{\{sPosition+1\}\}
    >
   ---
14. Connect playDigit to advance
15. Add a Condition node
    > Activity Label: positionCheck
    > 
    > Condition: \{\{sPosition <= (callbackANI.length -1) \}\}
    >
    > True: Connect to rDigit_set 
    >
    > False: Add a new Disconnect Contact node and connect it here
    >
   ---
16. Connect advance to positionCheck  
17. Publish your flow [Compare](https://webexcc.github.io/../../../assets/images/IVR/aniRead.JPG){:target="\_blank"}
18. Place a test call to <w class= "DN_out" >Your EP DN</w>
    > When you are given the option for a callback, press 1.
    >> Did you hear your 10 digit callback number being read back?

    ---



### Adding the ability to receive a callback at a different number
1. Add a new Menu node
    > Activity Label: confirmNumber
    >
    > Prompt: number_confirm_English.wav
    >
    > Make Prompt Interruptible: True
    >
    > Digit Number: 1 Link Description: confirm number
    >
    > Digit Number: 2 Link Description: change number
    >
    > Connect No-Input Timeout to the front of the confirmNumber node
    >
    > Connect Unmatched Entry to the front of the confirmNumber node
    >
    > ---
2. Delete the False node edge from positionCheck to Disconnect Contact
3. Connect the False node edge from positionCheck to confirmNumber
4. Connect the confirm number node edge to Disconnect Contact
5. Add a Collect Digits node
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
6. Connect the change number node edge to newNumber
7. Add a Set Variable Node
   > Activity Label: newCB
   >
   > Variable: callbackANI
   >
   > Set Value: \{\{newNumber.DigitsEntered\}\}
   >
   > ---
8. Connect newNumber to newCB
9.  Add a Set Variable Node
    > Activity Label:resetPosition
    >
    > Variable: sPosition
    >
    > Set Value: 0
    >
    > ---
10. Connect newCB to resetPosition
11. Add a Play message node
    > Activity Label: rcontext
    > 
    > Audio File: entered_English.wav
    >
    > ---
12. Connect resetPosition to rcontext
13. Connect rcontext to rDigit_set
14. Publish your flow [Compare](https://webexcc.github.io/../../../assets/images/IVR/changeNumber.JPG){:target="\_blank"}
15. Place a test call to <w class= "DN_out" >Your EP DN</w>
    > When you are given the option for a callback, press 1.
    >
    > Press 2 to enter a different number.
    >> Did you hear your 10 digit callback number being read back?
    >>
    >> Did you hear the number you entered read back?

    ---



### Adding the ability to collect an extension and present it to an agent during a callback
1. Create new flow variable:
   > Name: Extension
   >
   >> Type: String
   >>
   >> No default value
   >>
   >> Set as agent Viewable: True
   >>
   >> Desktop Label: Extension
   >
    ---
2. Add a Menu node
   > Activity Label: needExt
   > 
   > Audio File: ext_English.wav 
   >
   > Make Prompt Interruptible: True
   >
   > Digit Number: 1 Link Description: collect ext
   >
   > ---  
3. Delete to connection from the confirm number node edge of confirmNumber to Disconnect Contact
4. Connect the confirm number node edge of confirmNumber to needExt
5. Add a Collect Digits node
   > Activity Label: getEXT
   >
   > Audio File: enter_ext_English
   >
   > Make Prompt Interruptible: True
   >
   > Connect the No-Input Timeout node edge to the front of the getEXT node
   >
   > Connect the Unmatched Entry node edge to the front of the getEXT node
   > 
   > ---
6. Connect the collect ext node edge of needExt to getEXT
7. Add a Set Variable node
    > Activity Label: setExt
    >
    > Variable: Extension
    >
    > Set Value: \{\{getEXT.DigitsEntered\}\}
8. Connect getEXT to setEXT
9. Add a Set variable node
    > Activity Label: clrsPos
    >
    > Variable: sPosition 
    >
    > Set Value: 0
    >
    > ---
10. Connect setEXT to clrsPos
11. Add a Play Message node
    > Activity Label: entEXT
    >
    > Audio File: entered_English.wav
    >
    > ---

12. Connect clrsPos to entEXT
13. Use Shift + left click to select nodes:
   - rDigit_set
   - playDigit
   - advance
   - positionCheck
14. Click the copy button in the lower left corner of the canvas
15. Drag the copied versions of the nodes under the clrsPos node
16. Rename the copied nodes the original names = _EXT (example: rDigit_set_EXT)
17. Connect entEXT > rDigit_set_EXT > playDigit_EXT > advance_EXT > positionCheck_EXT
18. Edit rDigit_set_EXT 
    > Set value: \{\{Extension \| slice (sPosition,sPosition+1)\}\}
    >
    > ---
19. Edit positionCheck_EXT
    > Expression: \{\{sPosition <= (Extension.length -1) \}\}
    >
    > Connect True node edge to rDigit_set_EXT
    >
    >  ---
20. Add a Menu node   
    > Activity Label: confirmEXT
    >
    > Audio File: ext_confirm_English.wav
    >
    > Make Prompt Interruptible: True
    >
    > Digit Number: 1 Link Description: confirmed
    >
    > Digit Number: 2 Link Description: again
    >
    > Connect No-Input Timeout to the front of the confirmEXT node
    >
    > Connect Unmatched Entry to the front of the confirmEXT node
    >
    > Connect the Again node edge to getEXT
    >
    > ---
21. Connect the False node edge of positionCheck_EXT to confirmEXT
22. Add a Callback node
    > Activity Label: callback
    >
    > Callback Dial Number: callbackANI
    >
    > Callback Queue: Q_<w class="attendee_out">AttendeeID</w>
    >
    > ---
23. Connect the confirmed node edge of confirmedEXT to callback
24. Add a Play Message node
    > Activity Label: callbackConfirm
    >
    > Audio File: callback_confirm_English.wav
    >
    > ---
25. Connect callback to callbackConfirm
26. Connect callbackConfirm to Disconnect Contact
27. Connect the No-Input Timeout and Unmatched Entry node edges from needExt to Disconnect Contact
28. Publish your flow [Compare](https://webexcc.github.io/../../../assets/images/IVR/collectExt.JPG){:target="\_blank"}
29. Place a test call to <w class= "DN_out" >Your EP DN</w>
    > Press one to receive a callback 
    >
    > Press one to keep the number which was read back
    >
    > Press one to receive a callback at an extension
    >
    > Enter <w class= "supervisorEXT_out">Your Supervisor Extension</w> and press #.
    >
    > In the agent desktop, go available.
    >
    > When your agent phone rings, answer the call.
    > 
    > Listen to the prompts and enter the Extension shown on the agent desktop.
    >
    > Your Supervisor extension should ring, answer it.
    >
    > ---  

---

# Introduction to Flow Debugger
> Flow designer is a simple drag-and-drop user interface (UI) to define the flows. The following video explains the Flow Designer layout, activity library, and terminology used in the Flow Designer.

---

# Introduction to Flow Versioning
> Flow designer is a simple drag-and-drop user interface (UI) to define the flows. The following video explains the Flow Designer layout, activity library, and terminology used in the Flow Designer.

---


# Bonus - Experience Management

| Topic                                                                                    | Lab Type      | Difficulty Level | Estimated length |
| ---------------------------------------------------------------------------------------- | ------------- | --------------- | ---------------- |
| [Introduction to Experience Management](#introduction-to-experience-management-post-interaction-and-post-call-surveys) | Watch & Understand | EASY            | 7 min            |
| [Configure Post Call IVR Survey](#configure-post-call-ivr-survey) | Practical Lab | EASY | 10 min |
| [Configure Post Interaction Digital Survey](#configure-post-interaction-digital-survey) | Practical Lab | EASY | 10 min |


## Overview of the lab
In this lab, we will configure all the required elements to collect and view end-customer feedback using the new Experience Management.


### Lab Objective

- Create a basic survey
- Upload audio files to the survey
- Configure the survey in flow designer
- Simulate a customer interaction with survey feedback
- Download and verify survey feedback

  ---

### Pre-requisites

1.  You have **completed Lab 1 - Admin Experience:**
    -   You are familiar with Control Hub and navigation within Control Hub
2.  You have **completed Lab 2 - IVR Contact Routing:**
    -   You are familiar with creating and modifying flows
3.  You have **completed Lab 3 - Agent Desktop:**
    -   You are familiar with logging in as an Agent and accepting inbound interactions
4.  You have **Webex Calling installed** in your mobile phone and supervisor created in Lab 1 from which you can make calls to the contact center
  
    ---

### Quick Links

> Control Hub: **[https://admin.webex.com](https://admin.webex.com){:target="\_blank"}**\
> Portal: **[https://portal.wxcc-us1.cisco.com/](https://portal.wxcc-us1.cisco.com/){:target="\_blank"}**\
> Agent Desktop: **[https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com){:target="\_blank"}**\

  ---

## Introduction to Experience Management Post Interaction and Post Call Surveys
> Experience Management is a next-gen tool that facilitates post interaction surveys and outcomes. It allows you to track and measure customer satisfaction using anchor metrics like Net Promoter Score (NPS), Customer Effort Score (CES), and Customer Satisfaction (CSAT). Webex Contact Center brings in an integration of Experience Management for its post call survey interactive voice response (PCS IVR) and digital channels.

<div style="padding-bottom:60.25%; position:relative; display:block; width: 100%">
	<iframe src="https://app.vidcast.io/share/embed/0049a028-85b6-4b56-90f7-1fc696201ea3" width="100%" height="100%" title="Introduction to Experience Management" frameborder="0" loading="lazy" allowfullscreen style="position:absolute; top:0; left: 0"></iframe>
</div>


### Lab Section
## Configure Post Call IVR Survey

### Create a survey
1. Click on Contact Center under Services from Control Hub 
    > <img src="/assets/images/EM/contactCenter.gif" width="200">
    > 
2. Under Contact Center, click on Surveys
    > <img src="/assets/images/EM/survey.gif" width="200">
    > 
3.  Click the "Create new survey" button on the top-right corner of the Survey page
    >Select Survey type as IVR
    >> <img src="/assets/images/EM/surveyType.gif">
    >>
    >Provide a name for your survey appended with your Attendee ID
    >> <img src="/assets/images/EM/surveyName.gif">
    >>
    >Choose the additional languages for the survey from the drop-down (optional)
    >> <img src="/assets/images/EM/languageSupport.png">
    >>
    >Click on Next
    >
4. Add audio files to the Welcome and Thank you notes ([Audio Files](https://webexcc.github.io/assets/files/Survey_wav.zip){:target="\_blank"})
    >Click on the pencil icon to the right
    >>  <img src="/assets/images/EM/welcomeThankyou.gif">
    >>
    >Select Choose a file when the note expands, pick the audio file (Welcome.wav) and upload
    >> <img src="/assets/images/EM/uploadWelcome.gif">
    >>
    >Repeat steps for Thank you note (Thankyou.wav)
    >>
5. Add a question to your survey
    >Select the NPS question from the drop-down by clicking + Add a question
    >><img src="/assets/images/EM/addNPS.gif" width="200">
    >>
    >Choose the corresponding audio file, nps.wav for the NPS question and upload  ([Audio Files](https://webexcc.github.io/assets/files/Survey_wav.zip){:target="\_blank"})
    >><img src="/assets/images/EM/uploadNPS.gif">
    >>
    >Under Question to show on reporting type the column name as "NPS Score"
    >><img src="/assets/images/EM/NPSReporting.gif">
    >>
6. Update Error handling settings (optional)
    >Upload audio files for Invalid Input and Timeout by clicking on Choose a file under each section
    >
    >Set the maximum number of invalid inputs and timeouts allowed from the drop-down
    >
    >Choose an audio file for exceeding maximum tries
    >
7. Save the survey from the bottom right corner

---

### Add the feedback activity to your flow

> **NOTE:** Refer to the Lab 2 - IVR Contact Routing if you are unfamiliar with working on flow designer
{: .block-warning }

1. Open your flow created from Lab 2 - IVR Contact Routing
2. Introduce a Menu into your main flow to prompt the caller to opt-in for the survey in between the NewPhoneContact event and the Queue Contact node
    > Activity Label: surveyOptin
    >
    > Prompt: OptinMenu.wav  ([Audio Files](https://webexcc.github.io/assets/files/Survey_wav.zip){:target="\_blank"})
    >
    > Make Prompt Interruptible: True
    >
    > Digit Number - 1 
    >>Link Description: Opt-In
    >
    > Digit Number - 2 
    >>Link Description: Opt-Out
    >
3.  Assign true and false values for the Global_FeedbackSurveyOptin variable
    >Drag and drop two Set Variable nodes into your main flow after the Menu
    >
    >Click on the first Set Variable node
    >>Activity Label: OptIn
    >>
    >>Variable: Global_FeedbackSurveyOptin
    >>
    >>Set Value: TRUE
    >>
    >
    >Click on the second Set Variable node
    >>Activity Label: OptOut
    >>
    >>Variable: Global_FeedbackSurveyOptin
    >>
    >>Set Value: False
    >>
    >
4. Connect the nodes together
    >Connect Custom Menu Links for digit 1 to the Set Variable node with Global_FeedbackSurveyOptin set as true
    >
    >Connect Digit 2 and error handling links to the Set Variable node with Global_FeedbackSurveyOptin set as false
    >
    >Connect the Set Variable blocks back to your flow before Queue Contact
    >
    >Example Flow
    >><img src="/assets/images/EM/surveyOptin.png">
    >>
5. Navigate to the Event Flows tab
6. Add the Feedback V2 node
    >Connect the Feedback V2 node to the AgentDisconnected Activity
    >
    >Click on the Feedback V2 node
    >>Activity Label: PCS_IVR
    >>
    >>Survey Method: Voice Based
    >>
    >>Select survey created earlier from drop-down
    >>
    >>Timeout: 10
    >>
    >
7. Complete the flow by adding a Disconnect Contact node after the Feedback V2 node
    >Example Flow
    >><img src="/assets/images/EM/feedbackV2.png">
    >>
8. Validate and Publish the flow
   
   
---

## Provide a survey response

> **NOTE:** Refer to the section Basic Features in Lab 3 - Agent Desktop if you are unfamiliar with testing an incoming call
{: .block-warning }

1. Login to your Agent Desktop and make your state Available
2. Dial your designated DN and accept the incoming voice interaction
3. Provide the DTMF input 1 to opt-in to the survey
4. End the interaction from the Agent Desktop 
5. Provide a rating on the scale 0-9


---
## Download and validate the survey response

1. Navigate to the Surveys page on Control Hub
2. Click on the download button on the far right of your survey
    > <img src="/assets/images/EM/downloadResponse.gif">
    >
3. Select the date range for the survey response period as Last 7 days and click Download
    > <img src="/assets/images/EM/downloadDate.gif">
    >
4. Verify your response in the excel sheet to the one you provided on the call
    > <img src="/assets/images/EM/surveyReport.png">
    >

---







<p style="text-align:center"><strong>Congratulations, you have completed this lab! You can continue with the next one.</strong></p>
		
<p style="text-align:center;"><img src="/assets/gitbook/images/webex.png" width="100"></p>	