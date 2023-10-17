---
title: Agent & Supervisor Experience
author: Niko Theologitis & Arunabh Bhattacharjee
date: 2023-10-04
layout: post
---

Welcome to the Webex Contact Center Agent & Supervisor Experience!

In Part 1, we will look at the Webex Contact Center Agent Experience and associated Administrative toggles with configuring Agents on Webex Contact Center.

In Part 2, we will look at the Webex Contact Center Supervior Experience and associated Administrative toggles associated with Configuring Supervisors on Webex Contact Center.

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

| Topic                                                          | Type          | Dificulty    | Time   |
| -------------------------------------------------------------- | ------------- | ------------ | ------ |
| [Part 1: Agent Desktop Experience](#agent-desktop-overview)    | Exploration   | EASY         | 20 min |
| [Extend the Agent Desktop Experience](#desktop-administration) | Practical Lab | EASY         | 15 min |
| [Desktop Administration](#desktop-administration)              | Exploration   | INTERMEDIATE | 15 min |
| [Part 2: Supervisor Experience](#supervisor-experience)        | Exploration   | EASY         | 20 min |
| [Supervisor Administration](#supervisor-administration)        | Practical Lab | INTERMEDIATE | 15 min |
| [Supervisor Licensing](#supervisor-licensing)                  | Practical Lab | EASY         | 5 min  |
| [BONUS: Customizations & Programmability](#custom-desktop)     | Practical Lab | ADVANCED     | 30 min |

# Part 1: Agent Experience

## Objectives

- Understand the Agent Experience on Webex Contact Center by logging into the Agent Desktop application and exploring out of box capabilities.
- Understand the entire Agent Desktop interface and functions, including Inbound, Outbound and Omnichannel contact workflows.
- Learn about the extensions to the Agent Desktop Experience, exploring widgets available both out of box and customizations - learning the possibilities with Desktop Widgets and custom workflows.
- The Bonus section (OPTIONAL), covers advanced Desktop extensions, diving deep into Desktop layout design and programmatic extensions.

### Pre-Requisites

**You Will Need**

1. **1 extra device** (your personal phone for example) to test inbound calls to Webex Contact Center. You can use your cell phone for this

> Note: For completing the first section of the lab, all the Desktop Administration configurations have already been done for you to experience the fully loaded desktop. To understand what was configured, you may refer to the Desktop Administration Experience in the second half of this lab.

> We will explore each of the Administration elements at a later time in the Desktop Administration section.

- Administrator credentials to Control Hub [admin.webex.com](https://admin.webex.com).
- Agent Login Credentials to the Agent Desktop.
  [desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com)

2. The following items are already pre-configured:

- Agent and Supervisor users are created and configured for logins.
- You have agent's access to the Agent Desktop URL: [https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com)
- Agent is part of 2 Teams. (Your Attendee ID) with team1 and team2.

Example:

> If your attendee ID: 100
>
> 100_team1
>
> 100_team2

3. Agents will use WebRTC endpoints. Webex Calling extensions are also assigned to users (agent and supervisor) to experience alternative login options.

4. An inbound Voice flow is configured for test calls.

### Quick Links

> Control Hub Administration: **[https://admin.webex.com](https://admin.webex.com){:target="\_blank"}**\
> Agent Desktop: **[https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com){:target="\_blank"}**\

## Lab Configuration

> Please submit the form with your Attendee ID. All configuration items in the lab guide will be renamed with that prefix.

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

The following Administration entities have been configured for you:

Please note, that to proceed to the next section, you will need to use the accounts shown in the top 3 rows.

| **Entity**           | **Name**                                                              |
| -------------------- | --------------------------------------------------------------------- |
| Agent 1              | wxcclabs+agent_ID<w class = "attendee-class">attendeeID</w>@gmail.com |
| Supervisor 1         | wxcclabs+supvr_ID<w class = "attendee-class">attendeeID</w>@gmail.com |
| Administrator        | wxcclabs+admin_ID<w class = "attendee-class">attendeeID</w>@gmail.com |
| Desktop Profile      | <w class = "attendee-class">attendeeID</w>\_desktopProfile            |
| Entry Point          | <w class = "attendee-class">attendeeID</w>\_EP                        |
| Queue                | <w class = "attendee-class">attendeeID</w>\_Q                         |
| Team 1               | <w class = "attendee-class">attendeeID</w>\_team1                     |
| Team 2               | <w class = "attendee-class">attendeeID</w>\_team2                     |
| Outdial ANI          | <w class = "attendee-class">attendeeID</w>\_outdialANI                |
| Outdial ANI Entry 1  | <w class = "attendee-class">attendeeID</w>\_outdialANIEntry1          |
| Address Book         | <w class = "attendee-class">attendeeID</w>\_addressBook               |
| Address Book Entry 1 | <w class = "attendee-class">attendeeID</w>\_addressBookEntry1         |
| Multimedia Profile   | <w class = "attendee-class">attendeeID</w>\_MMP                       |

# Agent Desktop Overview

> Desktop multi-language support is based on the language preference settings on the browser. Currently, we support 29 languages:
> Bulgarian, Catalan, Chinese (China), Chinese (Taiwan), Croatian, Czech, Danish, Dutch, English (UK), English (US), Finnish, French, German, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese (Brazil), Portuguese (Portugal), Romanian, Russian, Serbian, Slovak, Slovenian, Spanish, Swedish, and Turkish.

![Image1](/assets/images/Agent/AgentDesktopOverview.png)

When you receive an active interaction, you will notice that the
Agent Desktop is divided into **6 sections**. In the image above you can see a general view of the Agent Desktop and where each section is located.

Here is an overview of the sections:

1. **Task List**: When a request is routed to your queue and you are _Available_, a new request appears in your Task List pane. You must accept the requests to start communication with the customer.

2. **Horizontal Header**: Basic functionalities such as: Title and logo, Agent availability state, Notification Center, Outdial and User Profile. We will explain more in detail some User Profile options in the next section of the lab.

3. **Interaction Control**: When you accept a voice call (inbound or outbound), by default, the Interaction Control pane is expanded. This pane includes: customer information (CAD variables), timers (for example: connected and call on hold time) and call control buttons (Record, Hold, Transfer...).

4. **Auxiliary Information**: The center pane displays details based on your selection of the contact card in the Task List panel. For Voice requests, it will display the customer contacts history. Whereas for any digital channels (email, chat or social messaging), you will see the whole conversation with the customer and you will be able to send new messages.

5. **Agent Interaction History**: You can view your previous contacts of the agent across all the channels (voice, email, chat, and social) in this pane. The pane displays details for the last 24 hours. Moreover, for Voice channel you can callback to the contact phone number.

6. **Navigation pane**: By default you can find the following icons here: Home, Agent Performance Statistics and Help. However, you can customize it and add some additional icons and widgets.

## Login Process

- To Login to the Agent Desktop, launch Google Chrome and to the URL: [https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com)

> **Note: Please Google Chrome as the browser to use the all new WebRTC Voice Option**

> Tip: You can also find this link under Control Hub: [admin.webex.com](https://admin.webex.com) > Contact Center > Settings

- Once you're in the login page, enter the agent credentials (username and password)

> In this example, please use the specific login for your attendee ID

![agent-desktop](/assets/images/agent/01-image.png)

![agent-desktop](/assets/images/agent/02-image.png)

- This is the station Login Screen. Agents may input the number where they need to receive incoming and outdial calls.

> We will use the new feature of Desktop telephony that uses the browser as a device to directly receive calls.

- Notice that the voice option defaults to "Desktop".

- Select Team1 from the list. Agents can belong to multiple teams, but they can only receive calls of 1 specific teams. Your agent is configured for 2 teams.

- Check the **Remember My Credentials** box to save your credentials for future sign-ins.

- Click Sign in to be connected to telephony and complete the login process.

![agent-desktop](/assets/images/agent/03-image.png)

> NOTE: Agents cannot access the Agent Desktop from multiple browsers or multiple tabs of the same browser window. In that case, a warning message will be displayed

![agent-desktop](/assets/images/agent/04-image.png)

> The video below shows a demo about the agent login process and the available options:

![agent-desktop](/assets/images/agent/AgentLogin.gif)

---

**NOTE:**

> The login device and DN can be enforced on the Desktop Profile as follows

- If your administrator configures the default Dial Number (DN), the default DN is prepopulated in the Dial Number and Extension fields.
- If your administrator restricts the DN to the default DN, you cannot edit the prepopulated DN when signing in to the Agent Desktop.

- They can choose between Dial Number or Extension or Desktop

  - Extension: Just in case the agent is using Webex Calling or some other softphone as calling endpoint

    - Dial Number: E.164 format phone number
      - If you check the **International Dialing Format** box, you can choose the country code based on your geographical location from the drop-down list. You can also enter a country code or country name to filter the list. Dial numbers are validated based on the country code

## Explore Agent Desktop Header Actions

The following section explores the Agent Desktop header actions.

### Explore Agent State and Idle codes

The header section of the agent desktop contains the State change toggle where the agent can make themselves available.

This also has the section where you can view the Idle codes.

![agent-desktop-State-Idle](/assets/images/agent/Agent_State_Idle.gif)

> Note: The Idle codes are customizable and configured under **Webex Control Hub > Contact Center Settings > Idle / Wrap up Codes**
> These Idle codes can then be customized per Desktop Profile, on a per user level.

---

### Explore the Agent Personal Statistics

The Agent can access the out of box Agent Personal Statistics Reports on the left navigation screen.

![agent-desktop-Personal-Statistics](/assets/images/agent/Agent_Personal_Statistics.gif)

> Note: These Agent Personal Statistics are canned reports out of the box. However, one can configure custom Analyzer Reports for Agents in the Layout if custom reporting views are needed.

---

### Organizational Messaging using the Webex App

Launch the Webex App from within the Desktop to message other users in the organization. This is a quick way for the Agent to message the Supervisor, or the Supervisor to be able to send messages to the Agent.

Send a message to the supervisor user - search for supervisor or admin user and send a message.

Your Supervisor is configured in the format:
**wxcclabs_supvr_ID<attendeeID>@gmail.com**

![agent-desktop-webex-App](/assets/images/agent/Agent_Webex_App.gif)

---

### Launch the Notification Pane

The notification pane on the desktop shows you the notifications of incoming calls or messages.
The agent can also launch previously delivered screenpops from this pane.

![agent-desktop-Notification-Pane](/assets/images/agent/Agent_Notification_Pane.gif)

---

### Launch the Agent Settings Pane

To review or change the Desktop Settings, click on the persona icon on the top right.

![agent-desktop-Settings-Pane](/assets/images/agent/Agent_Settings_Pane.gif)

---

#### Verify Profile Settings

The Profile settings shows the Agent which Device(s) or Teams are configured for use, allowing the agent to switch the Device OR Teams that they wish to login.

> This is defined in the **Desktop Profile** on the User or Team level.
> Teams are defined on the **User Settings** under Contact Center Settings

![agent-desktop-Profile-Settings](/assets/images/agent/Agent_Profile_Settings.gif)

---

#### Verify Channel Information for Omnichannel

The Channel capacity determines how many contacts the Agent can handle at a maximum, per channel.

> This is defined in the **Multimedia Profile** on the User or Team level.

![agent-desktop-Channel-Information](/assets/images/agent/Agent_Channel_Information.gif)

---

#### Verify Notification Settings

The notification settings under user settings allows you to Enable/Disable the Notifications, Enable Silent Notifications, or Enable/Disable the sound. You can also change the volume of the Chime for the incoming contact.

> Note: These settings persist as long as the browser cache is retained for the user.

![agent-desktop-Notification-Pane](/assets/images/agent/Agent_Notification_Pane.gif)

---

#### Switch to Dark Mode

You can switchover the theme on the Desktop using the Dark mode toggle. This helps with visibility on the eyes in low light conditions and can be a user preference for the theme.

> This is another setting that is preserved with the user's browser cache.

![agent-desktop-Dark-Mode](/assets/images/agent/Agent_Dark_Mode.gif)

---

#### View Desktop Mic & Speaker Options

This is a setting that is enabled for all logged in Agents with the Desktop (WebRTC) option. This can help troubleshoot any audio related settings for the Agent's microphone or speaker volumes.

![agent-desktop-Mic-Speaker](/assets/images/agent/Agent_Mic_Speaker.gif)

---

#### Explore Shortcuts

Try to speed up actions with keyboard shortcuts available out of box on the Agent Desktop.

You can launch the shortcuts using Ctrl+Alt+F for Windows (or Cmd+Option+F for MAC users)

![agent-desktop-Shortcuts](/assets/images/agent/Agent_Shortcuts.gif)

---

#### Change State Shortcuts

Change the state from Idle to Available using the shortcut

**Example for Mac users:**

> Try Ctrl + Option + F to bring up the shortcuts
> Try Ctrl + Option + R to go Ready
> Try Ctrl + Option + N to go Not Ready by typing an Idle code + Enter
> ![agent-desktop-State_Change_Shortscut](/assets/images/agent/Agent_State_Change_Shortscut.gif)

---

#### Download Error Logs

A diagnostic must have for Agents is the ability to download error reports to send to administrators for troubleshooting.

> Use Ctrl + Shift + 2 as a shortcut to download and view the log file!

![agent-desktop-Error-Logs](/assets/images/agent/Agent_Error-Logs.gif)

> What you will notice when you open the file:
> The Desktop uses a combination of secure HTTPS as well as Websocket connectivity to stay connected to the backend.

---

#### Test Your Network

This is specifically for the Desktop Voice option. Agents can also test their local network connectivity for latency and bandwidth requirements on the Agent Desktop - eespecially for diagnostics.

![agent-desktop-Test-Network](/assets/images/agent/Agent_Test_Network.gif)

---

## Explore the new Help Documentation

The help documentation has been enhanced with Webex Help Center. Agents will now be redirected to the new Webex Help Center for online help including search.

![agent-desktop-Help-Documentation](/assets/images/agent/Agent_Help_Documentation.gif)

---

# Make an Incoming Call

> In this section, you will will interact as an agent and test an Incoming call. Review the video of the lab section above to understand the different call handling options.

- In order to test properly an incoming call, first we need to make sure that we have all the call handling options enabled

- Login with your administrator user in the **Control Hub**: [https://admin.webex.com](https://admin.webex.com)
  Navigate to SERVICES > Contact Center > TENANT SETTINGS > Desktop\_
  - Make sure that **`End Call`** and **`End Consult`** are enabled
  - You can also configure _Auto Wrapup and RONA timeouts_

![CH-Settings-Desktop](/assets/images/agent/CH_Settings_Desktop.gif)

---

- Navigate to _DESKTOP EXPERIENCE > Desktop Profiles_ and view _your Desktop Profile_:
  - In the **Collaboration** tab:
    - Make sure the **Buddy Teams** to **`All`**
    - Make sure Enable **`Consult to Queue`** is also set

![CH-Desktop-Profile](/assets/images/agent/CH_Desktop_Profile.gif)

---

- Navigate to CUSTOMER EXPERIENCE > Queue\_ and view your Queue
  - Make sure **`Permit Monitoring, Pause/Resume`** are Enabled
    - Make sure that these settings are also enabled at tenant level
  - You can also set the _Recording Pause Duration_. This is the maxiumum duration that an agent can pause the recording

![CH-Desktop-Queues](/assets/images/agent/CH_Desktop_Queues.gif)

---

- Now place it's time to test the incoming call
  - Login the **Agent Desktop** with _your Agent 1_ user
  - Move to **`Available`** state
  - Place an incoming call to the DN mapped to your EP, in other words, this is the number a customer would call into... (You should have mapped your EP in Lab 2)
  - You will be asked to enter your Attendee Id: i.e. _138#_

![CH-Desktop-Call-In](/assets/images/agent/CH_Desktop_Call_In.gif)

---

- After you have Aaccepted the call in the Agent Desktop of _your Agent 1_
  - Check the **CAD variables** and try to edit any Global Variable
  - Notice the status has changed to **`Engaged`**.

![CH-Desktop-Call-In-Accepted](/assets/images/agent/CH_Desktop_Call_In_Accepted.gif)

---

- Let's play with the call interaction buttons
  - Click on **`Hold`** to pause the conversation with the end-customer and click on **`Resume`** to talk with him again
  - Click on **`Pause Recording`**, say some personal infor and click again on **`Resume`** to continue the recording
  - Click on **`Transfer`**, select **`Queue`** and then in the pull down menu select the `Welcome_EP`
    - End-customer be redirected to a common EP already created
  - **End** the call (this can be done from customer or agent perspective) and select any **Wrap-up code**

> For this part, you will need a third calling device for interacting as aSupervisor
> {: .block-warning }
> <br/>

- Now, lets create a new Chrome profile so we can login the Supervisor on the same browser

  - Select `Profiles` on Chrome
  - Select `Add Profile`
  - Select `continue without an account`
  - Give it a name .i.e `supervisor`
  - Click `done`

![CH-Desktop-Call-In-Accepted](/assets/images/agent/Chrome-Create-Profile.gif)

---

- After you create a new Chrome Profile, login in the **Agent Desktop** with _your Supervisor_ user and move to **`Available`** status

  - In a separate device (you mobile phone for example), login in Webex App with your _Supervisor_ user
  - Place the call from the third calling endpoint (your personal phone for example)
  - Try **`Consult, Conference and Transfer`** functions between End Customer, Agent and Supervisor.

### Agent States:

- **Available**: Indicates that you are ready to accept and respond to contact requests that are routed to you. After you sign in, you must select Available from the drop-down list to accept voice call, chat, email, and social messaging conversation requests.

- **Idle**: Indicates that you are signed in but not ready to accept any routed requests. When you sign in to the desktop, your state is set to the default idle reason configured by your administrator.

- **RONA (Redirection on No Answer)**: Indicates that you have not accepted a voice call, chat, email, or social messaging conversation request within the specified time. Your administrator configures the time available to accept an incoming request from any channel. If you cannot accept the request within the specified time displayed in the timer, the action button on the popover flashes for a few seconds and your state automatically changes to RONA. The request is returned to the queue. When your state changes to RONA, a popover appears and you can select the state that you want to be moved: to Idle or to Available

- **Engaged**: indicates that you are busy and connected with a customer. When you have accepted the contact request, the Available state changes to the Engaged - Available label. When you're in this state, you can continue to receive active requests on other channels, depending on the channel capacity. If you don't want to receive more requests, you can select any Idle state, so you will be moved to Engaged - Idle label.

#### Manage Voice Calls

- **Call Associated Data (CAD) variables**: These variables allow the administrator to collect call data such as a case number or any action code of the customer. In Flow Designer, your administrator configures the variables, labels of the variables, and the order in which they must appear on the Interaction Control panel. While you are on a call, you can edit the CAD variables if your administrator configures the CAD variables as editable.

- **Hold/Resume**: You can put the customer on hold so that you can consult with another agent or lookup additional information without having the customer listening to you. Click on Resume to take a call off hold.

- **Pause/Resume Recording**: Your administrator can choose for each Queue either to record all the calls or not. In case the recording is enabled, the agent can Pause and Resume the recording.

- **End**: After you have helped your customer with queries, it is a good practice to ask the customer to end the voice call. If necessary, you can also end the call. When the customer ends the call, agent will need to select some Wrap Up Reasons from the dialog box appears.

- **Consult**: You can initiate a consult call with another agent while you are on an active call with a customer.

- **Transfer**: If you cannot resolve a customer query and want to escalate the active voice call (inbound or outbound), you can transfer the call to another agent or supervisor.

- Either for **Consult and Transfer** you have the following options:

  - _Agent_: You can either select an agent from the drop-down list, or use the search field to filter the list. The drop-down list displays the names of available agents.

  - _Queue_: You can select a Queue or Entry Point from the drop-down list, or use the search field to filter the list. The drop-down list displays the queues that are available to transfer the call.

  - _DN_: You can enter a name or number; select a name or number from the drop-down list; or use the search field to filter the list. The drop-down list shows the grouped list of contacts in your address book. Names are listed along with the numbers for the contacts in the address book.

- **Conference**: To start a three-way conference call between you, the customer and another agent. For this option, you (primary agent) must have initiated a consult call. Click Transfer to transfer the call to the consulting agent. The consulted agent can exit the call by clicking Exit Conference, and the call continues between the primary agent and the customer. Only the primary agent can end the Conference.

## Outdial

> In this section, we will test Outdial calls using different Outdial ANIs and Address Books.

(screenshot - GIF)

- Navigate to _Management Portal > Provisioning > Outdial ANI_
  - Click on **`New Outdial ANI`**
  - Name: <w class = "attendee-class">attendeeID</w>\_outdialANI
  - Add Outdial ANI entry
    - Name: <w class = "attendee-class">attendeeID</w>\_outdialANIEntry1
    - Number: Select your mapped DN

<br/>

(screenshot - GIF)

- Navigate to _Management Portal > Provisioning > Address Book_
  - Click on **`New Address Book`**
  - Name: <w class = "attendee-class">attendeeID</w>\_addressBook
  - Parent Type: **`Site`**
  - Add Address Book entries
    - Name: <w class = "attendee-class">attendeeID</w>\_addressBookEntry1
    - International calls are disabled, **so only US numbers are supported**. For example: +18662293239 (Cisco Helpdesk)

<br/>

(screenshot - GIF)

- Navigate to _Management Portal > Provisioning > Desktop Profiles_
  - Search for _your Desktop Profile_ and make sure that **Outdial is enabled and `Outdial Entry Point-1` (created by the system) selected**
  - Select _your Outdial ANI_

<br/>

(screenshot - GIF)

- Navigate to _Management Portal > Tenant > Settings_
  - See the number of the **Default Outdial ANI**

> **This is a required setting at tenant level, so PLEASE DON'T EDIT IT**
> {: .block-danger }

<br/>

(screenshot - GIF)

- Now, login in the **Agent Desktop** with _your Agent1_ with the Webex Extension of the Agent
  - Open the Outdial on the Horizontal Header
  - Input your personal phone number
  - **Don't select any Outdial ANI**
  - Click on the telephone button to place the call
  - The call will be delivered to your phone number from the **Default Outdial ANI** defined at Tenant level
  - Now repeat the same but **choosing _your Outdial ANI_** configured before. You will see that the call is coming with a different ANI

<br/>

- Finally, let's see how **Adress Book** works
  - Open the Outdial window and swith to the Address Book tab
  - You will see the the list of entries of <w class = "attendee-class">attendeeID</w>\_addressBook configured before
  - You can search by entry name or DN
  - Try to call any of the numbers in the list

## Exploring User Profile

> In this section, we will explore what are the available options and settings under the User Profile.

<div style="padding-bottom:60.25%; position:relative; display:block; width: 100%">
	<iframe src="https://app.vidcast.io/share/embed/149fe8d1-c27e-4c7e-a0b9-af072487c543" width="100%" height="100%" title="User Profile" frameborder="0" loading="lazy" allowfullscreen style="position:absolute; top:0; left: 0"></iframe>
</div>
<br/>

- First, we will see how to change from one team to another one
  - In order to notice some difference when we make the Team change, we need to modify some setting from _your Team 2_ (created in Lab 1) . For that, we will assign a different **Multimedia Profile** to that team.

<br/>

- Navigate to the _Management Portal > Provisioning > Teams_
  - Find _your Team 2_ and click on `Edit`
  - Check _your User settings_ and make sure that there is not **Multimedia Profile** assigned. **User settings have preference over Team setting**, so the Multimedia Profile at User level will be applied.
  - Change the **Multimedia Profile** of the team from <w class = "attendee-class">attendeeID</w>\_MMP`to`Default_Telephony_Profile

<br/>

- Now, login in the **Agent Desktop** selecting <w class = "attendee-class">attendeeID</w>\_team1
  - Open _your User Profile_ and check that the **Channel Capacity**
  - Now, click on _your Team_, you will see a dropdown list with other available Teams
  - Click on <w class = "attendee-class">attendeeID</w>\_team2
  - **`Save Team Selection`** to confirm that you want to change a team

<br/>

- You will see notification appeared in the **Notification Center**
  - You can change the **Notification settings** to disable the incoming notifications or the sound
  - Mark the notification as `Read`
  - Go to the **User Profile** and check the **Channel Capacity** again, it's different

<br/>

- Test some additional options:
  - **Switch to Dark Mode**
  - **Keyboard shortcuts**
  - **Download error log**

# Verify Desktop Administration

The following section and describes Desktop Administration that brought together all the features you experienced on the Agent Desktop.

Here is a schematic showing how the Agent Desktop configuraton aligns to all the entities on Webex Control Hub.

(screenshot)

## Administration Entities

The following Administration entities have been configured for you.

To verify, navigate to WebexOne

| **Entity**           | **Name**                                                               |
| -------------------- | ---------------------------------------------------------------------- |
| Agent 1              | <w class = "attendee-class">attendeeID</w>_agent1@mailinator.com       |
| Supervisor 1         | <w class = "attendee-class">attendeeID</w>\_supervisor1@mailinator.com |
| Desktop Profile      | <w class = "attendee-class">attendeeID</w>\_desktopProfile             |
| Entry Point          | <w class = "attendee-class">attendeeID</w>\_EP                         |
| Queue                | <w class = "attendee-class">attendeeID</w>\_Q                          |
| Team 1               | <w class = "attendee-class">attendeeID</w>\_team1                      |
| Team 2               | <w class = "attendee-class">attendeeID</w>\_team2                      |
| Outdial ANI          | <w class = "attendee-class">attendeeID</w>\_outdialANI                 |
| Outdial ANI Entry 1  | <w class = "attendee-class">attendeeID</w>\_outdialANIEntry1           |
| Address Book         | <w class = "attendee-class">attendeeID</w>\_addressBook                |
| Address Book Entry 1 | <w class = "attendee-class">attendeeID</w>\_addressBookEntry1          |
| Multimedia Profile   | <w class = "attendee-class">attendeeID</w>\_MMP                        |

> **NOTE:** Please create all the tenant entities following the naming convention mentioned specified in the table above. Your attendeeID is provided in the email in the **"Attendee ID"** line.
> {: .block-warning }

> Be aware that all entities that don't match with attendee IDs will be deleted
> {: .block-warning }

## Send Product Feedback

Before you move onto the bonus sections, we would love to hear from you!
Explore the product feedback option from right within the Agent Desktop.
Please fill in the survey and help us improve the product!

(content + screenshot)

---

  <script>
    document.addEventListener('DOMContentLoaded', () => {
      console.log('DOMContentLoaded OKOK')
    })

    window.addEventListener('load', () => {
      console.log('window load OK')
    })
  </script>

<p style="text-align:center"><strong>Congratulations, you have completed the Agent Experience lab! Please proceed to the <a href="https://webexone.github.io/pages/SupervisorExperience/">Supervisor Experience Lab.</a></strong></p>
		
<p style="text-align:center;">![agent-desktop](/assets/gitbook/images/webex.png)</p>
