---
title: Agent & Supervisor Experience
author: Niko Theologitis & Arunabh Bhattacharjee
date: 2023-10-04
layout: post
---

In Part 1, we will explore the Webex Contact Center Agent Experience and the associated administrative toggles for configuring agents in the Webex Contact Center.

In Part 2, we will examine the Webex Contact Center Supervisor Experience and the associated administrative toggles for configuring supervisors in the Webex Contact Center.

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

# Part 1: Agent Experience

### Objectives

- Explore the Agent Experience on the Webex Contact Center by logging into the Agent Desktop application and navigating its out-of-the-box capabilities.
- Familiarize yourself with the complete Agent Desktop interface and its functions, covering Inbound, Outbound, and Omnichannel contact workflows.
- Dive into extensions of the Agent Desktop Experience, understanding the available widgets—both out-of-the-box and custom—and recognizing the potential of Desktop Widgets and customized workflows.
- The Bonus section (OPTIONAL) delves into advanced Desktop extensions, focusing on Desktop layout design and programmatic extensions.

### Pre-Requisites

> Note: To complete the initial section of the lab, all Desktop Administration configurations are already set up. This ensures you can experience a fully equipped desktop. For insights on what was configured, please refer to the Desktop Administration Experience later in this lab.

> We'll delve into each Administrative element in the following **Desktop Administration** sections that covers `configuration and administrative tasks`.

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

### Quick Links

For this lab, you'll only require access to two web portals:

> Control Hub Administration: **[https://admin.webex.com](https://admin.webex.com){:target="\_blank"}**\
> Contact Center Desktop: **[https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com){:target="\_blank"}**\

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

## Agent Desktop Overview

> Desktop multi-language support is based on the language settings on the browser. Currently, we support 29 languages, including:
> Bulgarian, Catalan, Chinese (China), Chinese (Taiwan), Croatian, Czech, Danish, Dutch, English (UK), English (US), Finnish, French, German, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese (Brazil), Portuguese (Portugal), Romanian, Russian, Serbian, Slovak, Slovenian, Spanish, Swedish, and Turkish.

![Image1](/assets/images/Agent/AgentDesktopOverview.png)

The Agent Desktop is divided into **6 sections**.
The image above shows the general view after receiving an interaction.

Here is an overview of the sections:

1. **Task List**: When a request is routed to your queue and you are _Available_, a new request appears in your Task List pane. You must accept the requests to start communication with the customer.

2. **Horizontal Header**: Basic functionalities such as: Title and logo, Agent availability state, Notification Center, Outdial and User Profile. We will explain more in detail some User Profile options in the next section of the lab.

3. **Interaction Control**: When you accept a voice call (inbound or outbound), by default, the Interaction Control pane is expanded. This pane includes: customer information (CAD variables), timers (for example: connected and call on hold time) and call control buttons (Record, Hold, Transfer...).

4. **Auxiliary Information**: The center pane displays details based on your selection of the contact card in the Task List panel. For Voice requests, it will display the customer contacts history. Whereas for any digital channels (email, chat or social messaging), you will see the whole conversation with the customer and you will be able to send new messages.

5. **Agent Interaction History**: You can view your previous contacts of the agent across all the channels (voice, email, chat, and social) in this pane. The pane displays details for the last 24 hours. Moreover, for Voice channel you can callback to the contact phone number.

6. **Navigation pane**: By default you can find the following icons here: Home, Agent Performance Statistics and Help. However, you can customize it and add some additional icons and widgets.

## Desktop Login Process

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

### Explore Agent Desktop Header Actions

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
**wxcclabs_supvr_ID\<attendeeID\>@gmail.com**

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

### Verify Profile Settings

The Profile settings shows the Agent which Device(s) or Teams are configured for use, allowing the agent to switch the Device OR Teams that they wish to login.

> This is defined in the **Desktop Profile** on the User or Team level.
> Teams are defined on the **User Settings** under Contact Center Settings

![agent-desktop-Profile-Settings](/assets/images/agent/Agent_Profile_Settings.gif)

---

### Verify Channel Information for Omnichannel

The Channel capacity determines how many contacts the Agent can handle at a maximum, per channel.

> This is defined in the **Multimedia Profile** on the User or Team level.

![agent-desktop-Channel-Information](/assets/images/agent/Agent_Channel_Information.gif)

---

### Verify Notification Settings

The notification settings under user settings allows you to Enable/Disable the Notifications, Enable Silent Notifications, or Enable/Disable the sound. You can also change the volume of the Chime for the incoming contact.

> Note: These settings persist as long as the browser cache is retained for the user.

![agent-desktop-Notification-Pane](/assets/images/agent/Agent_Notification_Pane.gif)

---

### Switch to Dark Mode

You can switchover the theme on the Desktop using the Dark mode toggle. This helps with visibility on the eyes in low light conditions and can be a user preference for the theme.

> This is another setting that is preserved with the user's browser cache.

![agent-desktop-Dark-Mode](/assets/images/agent/Agent_Dark_Mode.gif)

---

### View Desktop Mic & Speaker Options

This is a setting that is enabled for all logged in Agents with the Desktop (WebRTC) option. This can help troubleshoot any audio related settings for the Agent's microphone or speaker volumes.

![agent-desktop-Mic-Speaker](/assets/images/agent/Agent_Mic_Speaker.gif)

---

### Explore Shortcuts

Try to speed up actions with keyboard shortcuts available out of box on the Agent Desktop.

You can launch the shortcuts using Ctrl+Alt+F for Windows (or Cmd+Option+F for MAC users)

![agent-desktop-Shortcuts](/assets/images/agent/Agent_Shortcuts.gif)

---

### Change State Shortcuts

Change the state from Idle to Available using the shortcut

**Example for Mac users:**

> Try Ctrl + Option + F to bring up the shortcuts
> Try Ctrl + Option + R to go Ready
> Try Ctrl + Option + N to go Not Ready by typing an Idle code + Enter
> ![agent-desktop-State_Change_Shortscut](/assets/images/agent/Agent_State_Change_Shortscut.gif)

---

### Download Error Logs

A diagnostic must have for Agents is the ability to download error reports to send to administrators for troubleshooting.

> Use Ctrl + Shift + 2 as a shortcut to download and view the log file!

![agent-desktop-Error-Logs](/assets/images/agent/Agent_Error-Logs.gif)

> What you will notice when you open the file:
> The Desktop uses a combination of secure HTTPS as well as Websocket connectivity to stay connected to the backend.

---

### Test Your Network

This is specifically for the Desktop Voice option. Agents can also test their local network connectivity for latency and bandwidth requirements on the Agent Desktop - eespecially for diagnostics.

![agent-desktop-Test-Network](/assets/images/agent/Agent_Test_Network.gif)

---

### Explore the new Help Documentation

The help documentation has been enhanced with Webex Help Center. Agents will now be redirected to the new Webex Help Center for online help including search.

> Note: This will now open a new tab for the

![agent-desktop-Help-Documentation](/assets/images/agent/Agent_Help_Documentation.gif)

---

## Make an Incoming Call

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

- When the call arrives - you will be able to see an incoming popover when the Agent is offered the contact. It will have an Accept and Decline button since it is a Browser powered softphone.

![Agent Popover](/assets/images/agent/Agent_Popover.png)

> **Click on the Accept Button to take the call**

![CH-Desktop-Call-In](/assets/images/agent/CH_Desktop_Call_In.gif)

> Note: The variables displayed in the incoming popover and on the Desktop can be ordered in a custom manner.
> This is done on the flow designer on the flow level.

![Variable-Order](/assets/images/agent/Agent_VariableOrder.png)

---

- After you have Accepted the call in the Agent Desktop of _your Agent 1_
  - Check the **CAD variables** and try to edit any of the Editable Variables. This is customizable via Flow Designer.
  - Notice the status of the Desktop has changed to **`Engaged`**.

![CH-Desktop-Call-In-Accepted](/assets/images/agent/CH_Desktop_Call_In_Accepted.gif)

> **Note**: While you are engaged for a voice call, you are still marked available on other channels based on your channel capacity. This is the configuration on the Multimedia Profile settings on the Agent Desktop.

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

### Agent States

- **Available**: Indicates that you are ready to accept and respond to contact requests that are routed to you. After you sign in, you must select Available from the drop-down list to accept voice call, chat, email, and social messaging conversation requests.

- **Idle**: Indicates that you are signed in but not ready to accept any routed requests. When you sign in to the desktop, your state is set to the default idle reason configured by your administrator.

- **RONA (Redirection on No Answer)**: Indicates that you have not accepted a voice call, chat, email, or social messaging conversation request within the specified time. Your administrator configures the time available to accept an incoming request from any channel. If you cannot accept the request within the specified time displayed in the timer, the action button on the popover flashes for a few seconds and your state automatically changes to RONA. The request is returned to the queue. When your state changes to RONA, a popover appears and you can select the state that you want to be moved: to Idle or to Available

- **Engaged**: indicates that you are busy and connected with a customer. When you have accepted the contact request, the Available state changes to the Engaged - Available label. When you're in this state, you can continue to receive active requests on other channels, depending on the channel capacity. If you don't want to receive more requests, you can select any Idle state, so you will be moved to Engaged - Idle label.

### Manage Voice Calls

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

## Outdial Calls

> In this section, we will test Outdial calls using different Outdial ANIs and Address Books.

### Make an Outdial Call

- While Logged into the Agent Desktop, look for the Address book.
- You will see two contacts that are preloaded for you. You can directly make a call to any of those numbers.

> Not choosing an option on the dropdown selects the Default Outdial ANI (Calling Number Mask) of the tenant. This is configured on Control Hub, under the Desktop Settings. admin.webex.com > Contact Center > Desktop Settings > Outdial ANI

![Agent-AddressBook](/assets/images/agent/Agent_AddressBook.gif)

---

> **Note: These are live numbers published on cisco.com!**

- Alternatively, you can select a customized Calling Number mask by selecting the Outdial ANI dropdown. This Outdial ANI dropdown can be configured on the `Outdial ANI` settings in Control Hub.

![Agent-OutdialANI_Mask](/assets/images/agent/Agent_OutdialANI_Mask.gif)

---

> _You will notice that upon clicking the dial button, the Agent is presented with a floating pop-over that displays call varibales and is then connected to the call, and then the remote party is connected - following which the call legs are bridged._

![Agent-Outdial_Call](/assets/images/agent/Agent_Outdial_Call.gif)

---

> **Note: Outdial also supports pre-dial activities that can be configured on the WebexCC Flow Designer. The Flow Designer has been configured for you with the Custom Caller Associated Data Variables that are visibile upon Outdial**

![CH-Outdial_Flow](/assets/images/agent/CH_Outdial_Flow.gif)

---

### Verify the Outdial Configuration

- On Control Hub, Navigate to _DESKTOP EXPERIENCE > Outdial ANI_
  - In the Search bar type your attendee number to find your Outdial ANI**`NNN_OutdialANI`**
  - Click on it, and look at all the settings:

<br/>

![CH_Outdial_Verify](/assets/images/agent/CH_Outdial_Verify.gif)

---

- In Control Hub, Navigate to DESKTOP EXPERIENCE > _Address Books_
  - Click on **`WebexOneAddressBook`**
  - Look at settings: `Please do change these settings as they are global and will affect all users on Tenant`

<br/>

![CH_AddressBook_Verify](/assets/images/agent/CH_AddressBook_Verify.gif)

---

- In Control Hub, Navigate to _DESKTOP EXPERIENCE > Desktop Profiles_
  - Search for _your Desktop Profile_
  - Select `Dial Plans`
  - Make sure that **Outdial is enabled and your Outdial ANI `NNN_OutdialANI` is selected**
  - This is where you also assign the Address Book

<br/>

![CH_Desktop_Profiles_Verify](/assets/images/agent/CH_Desktop_Profiles_Verify.gif)

---

- In Control Hub, Navigate to _TENANT SETTINGS > Voice_
  - See the number of the **Default Outdial ANI**

> **This is a required setting at tenant level, so PLEASE DON'T EDIT IT**
> {: .block-danger }

<br/>

![CH_OutdialANI_Number](/assets/images/agent/CH_OutdialANI_Number.gif)

---

<br/>

## Exploring Profile Settings & Switching Teams

> In this section, we will explore what are the available options and settings under the Profile Settings.

<br/>

- First, we will see how to change from one team to another one

![Agent_Switch_Teams](/assets/images/agent/Agent_Switch_Teams.gif)

---

- We are applying a different Layout.json per Team, to showcase how two teams might look differently.

- To see where that is applied
  - Navigate to the _USER MANAGEMENT > Teams_
  - Search _your Team 2_ and click on `Edit`
  - At quick glance you can see that your Team1 is using the `Gloabl Layout` and Team2 is using the `WebexOne_DesktopLayout`
  - You can click each team to explore further

![Agent_Switch_Teams_Show](/assets/images/agent/Agent_Switch_Teams_Show.gif)

---

<br/>

- **CLARIFY** You will see a new notification appears in the **Notification Center**
  - You can change the **Notification settings** to disable the incoming notifications or the sound.
  - Mark the notification as `Read`.
  - Go to the **User Profile** and check the **Channel Capacity** again, it's different.

(screenshot - GIF)

## Custom Widget Landscape

> The next section covers the experience you just saw with switching to the new team : Team2

**Team2 has a dedicated desktop layout that shows you the power of custom widgets and extensibility of the Desktop**

### Header Widgets and Advanced Header order

- You will notice that the Agent desktop now has a custom widget in the Header area that is displaying the shift timer.

- You will also notice that the order of the widgets has been changed, with the state timer now in the center.

- This is the "Advanced Header" feature and allows you to embed widgets in the header area along with the help of the `advancedHeader`` component in the Desktop Layout.

![Agent_Header](/assets/images/agent/Agent_Header.gif)

---

### Exploring Navigation Area Widgets

The left pane of the Agent Desktop now has a large number of custom widgets, showing you the power of extensibility in the Agent Desktop.

#### Analyzer Report Custom Widget

- Custom Analyzer Reports can be embedded in the Contact Center Desktop directly by pointing to the permalink inside the layout.
- This loads up an iFrame version of the widget on the desktop.
- For more information on this widget, speak to your lab proctor.

![Agent_Widget_Analyzer](/assets/images/agent/Agent_Widget_Analyzer.gif)

---

#### Smartsheet Custom Widget

- External Sites can be embedded into the Agent Desktop for Agent and Supervisor Workflows.
- In this example, a shareable and embeddable link from Smarsheet.com is embedded into the Desktop workflow.

![Agent_Widget_Smartsheet](/assets/images/agent/Agent_Widget_Smartsheet.gif)

---

#### State Change Custom Widget

- Webcomponent widgets like the Example Widget allows developers to pass data from the Desktop into the widget.
- Here, in this example you can see that Agent Desktop data is passed into another widget that is hosted externally.
- The widget can be configured to obtain access to the Agent's Access Token to perform workflow automations.
- Expanding the Drawer, this custom widget also allows you to change the Agent State.
- Once the State is changed, you can see the Team and other information show up.
- This shows you the power of the extensible Webex Contact Center Desktop JS SDK (JavaScript Software Development Kit) and event driven architectures of custom widgets.
- For more information on this widget, speak to your lab proctor.

![Agent_Widget_Example](/assets/images/agent/Agent_Widget_Example.gif)

---

- Part of the Desktop SDK is a method that can be applied to pause recording if an agent was to enter for example, a customers Credit card information, example below.
- **FYI**, you must be on an `active` call.

![Agent_Widget_Pause_Resume](/assets/images/agent/Agent_Widget_Pause_Resume.gif)

---

#### Custom Address Book Widget

- Another sample widget in the form of a custom Address book widget shows you the power of creating Attendant Console like widgets in the Agent Desktop.
- Clicking the Call button actually makes a call externally, showcasing the power of the "Click to Call" functionality built into this custom widget.
- For more information on this widget, speak to your lab proctor.

![Agent_Widget_AddressBook](/assets/images/agent/Agent_Widget_AddressBook.gif)

---

#### Custom Call Control Widget

- Another example widget shows you how you can perform various actions programmatically using the Webex Contact Center Desktop JavaScript Software Development Kit (JS SDK) that has been used to extend functionality beyond what is possible out of box.
- A simple example task would be: Make a call, and then either Hold or Unhold the call, or experiment with Pause and Resume of the Recording while entering credit card information.
- For more information on this widget, speak to your lab proctor.

![Agent_Widget_CallControls](/assets/images/agent/Agent_Widget_CallControls.gif)

---

#### Send SMS Widget

- Another example widget shows you how the Agent Desktop can be configured to send outbound SMSes in call by configuring Webex Connect flows.
- **FYI**, To use these `call controls` you must be on an `active` call.
- This custom widget allows you to enter your cell number, and any text - to send yourself a message.
- In the background, the Widget is configured to use Webex Connect webhooks to send a custom payload and trigger a custom workflow.
- For more information on this widget, speak to your lab proctor.

![Agent_Widget_SMS](/assets/images/agent/Agent_Widget_SMS.gif)

---

<br/>

# Verify Desktop Administration

The following section and describes Desktop Administration that brought together all the features you experienced on the Agent Desktop.

> **This is more of a walkthrough, to understand how these toggles are configured**

Here is a schematic showing how the Agent Desktop configuraton aligns to all the entities on Webex Control Hub.

(schematic - overview)

## Administration Entities

The following Administration entities have been configured for you.

To verify, navigate to Control Hub Portal > Contact Center Settings

(screenshot - GIF)

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

> **NOTE:** All of the above the tenant entities follow the naming convention mentioned specified in the table above. Your attendeeID is provided in the email in the **"Attendee ID"** line.
> All of this configuration has been done for you.

---

# Part 2: Supervisor Experience

### Objective

This lab is designed to introduce the audience to the Extensible Supervisor Desktop (ESD), its configuration and capabilities.

At the end of the lab, you should have a good understanding of the Supervisor role on Webex Contact Center, the Supervisor Desktop and common Supervisor workflows available.

#### You are provided two users on Control Hub to simulate the lab activities

| **User Role** | **User email**                                                          | **User Extension**                                          |
| ------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------- |
| Agent         | wxcclabs+agent_ID<w class="attendee_out">Your_Attendee_ID</w>@gmail.com | WebRTC (Browser)                                            |
| Supervisor    | wxcclabs+supvr_ID<w class="attendee_out">Your_Attendee_ID</w>@gmail.com | <w class= "supervisorEXT_out">Your Supervisor Extension</w> |

#### Quick Links

> Control Hub: **[https://admin.webex.com](https://admin.webex.com/)**  
> Supervisor Desktop: **[https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com/)**
> Webex App (Download): \*\*\*\*

## Supervisor Desktop Modes

> **The following section explains the types of login modes into the Supervisor Desktop**
>
> The Supervisor Role is assigned as a part of the Control Hub License.
> When you assign a Control Hub Supervisor License, you are automatically assigned the Default Supervisor User Profile.

We will review this on Control Hub Settings.

> Control Hub > Contact Center Users > Supervisor User > User Profile: Supervisor Profile

- Look up your Supervisor User bu going to admin.webex.com > Contact Center > User Management (Category) > Contact Center Users
- Ensure that the Supervisor user wxcclabs+supvr_ID_your_attendee_ID\_@gmail.com has the `Supervisor Profile` in the `User Profile` field

![Supervisor_UserProfile](/assets/images/supervisor/Supervisor_UserProfile.gif)

---

**Supervisor Only Mode:**

- You can choose not to be an Agent but still login to the Supervisor Desktop. This is called the **Supervisor Only Role**.
- This is enabled by setting up a User with the Supervisor License and a Primary Team.
- Contact Center need not be enabled for the User.
- In this role, you will still need a Primary Team assigment which will be used to display the statistics.
- The Supervisor Only Role is used for Team Statistics and Reporting.

**Supervisor and Agent Mode**

- You can to take calls from the Queue as a supervisor. This is called the **Supervisor and Agent Role**
- This is enabled by setting up a User with the Supervisor License, a Primary Team AND marking the user Contact Center enabled.

![Supervisor_And_Agent_Role](/assets/images/supervisor/Supervisor_And_Agent_Role.gif)

### Pre-requisites:

1.  A supervisor user configured as described below.
2.  A agent logged in and in conversation with a customer so you can monitor the call.
3.  Webex App Installed - Please install and download the Webex App from: https://www.webex.com/downloads.html

> **We will use the [Webex App](https://www.webex.com/downloads.html) as the Supervisor endpoint Device.**

---

<br>

## Supervisor Login

- Sign in to the **Supervisor Desktop**: https://desktop.wxcc-us1.cisco.com with your supervisor credentials.

- In the next window, set your role as **Supervisor** and your **own extension**. Please note that you can set your role either as **supervisor** or **agent and supervisor**. We will select this second option at the end of this lab.

> **This mode will help you perform midcall monitoring and reporting**

![Supervisor_Login](/assets/images/supervisor/Supervisor_Login.gif)

---

- When you sign in to the **Supervisor Desktop**, the appearance depends on how the Webex Contact Center administrator has configured the desktop layout. The **Supervisor Desktop** display size must be greater than 500 x 500 pixels (width x height). You must set your web browser zoom to 100% for the best experience with the Supervisor Desktop. With this lab layout you get :

1. **Home Page**: Displays a user friendly interface that provides a consolidated view of key contact center metrics and filters. This is the default landing page in the Supervisor Desktop. The administrator can customize the Home Page in the layout JSON file.

![Supervisor_Home](/assets/images/supervisor/Supervisor_Home.png)

---

2. **Task**: Displays all the tasks when you sign in to the Desktop in dual role (supervisor and agent) or as a supervisor, interactions such as voice, chat, email, and social messaging conversations, along with monitoring. The icon displays a badge indicating the number of requests that you have not accepted across various channels.

![Supervisor_Task](/assets/images/supervisor/Supervisor_Task.gif)

---

3. **Team Performance**: Displays real-time information about an agent and a consolidated view of an agent’s performance as part of the team. You can also monitor and send 1:1 messages to an agent.

![Supervisor_TeamPerformance](/assets/images/supervisor/Supervisor_TeamPerformace.gif)

---

> Note: **Supervisor Desktop** supports localization in 30 languages. The following are the supported languages:
> Bulgarian, Catalan, Chinese (China), Chinese (Taiwan), Croatian, Czech, Danish, Dutch, English (UK), English (US),Finnish,French, German, Hungarian, Italian,Japanese, Korean, Norwegian,Polish,Portuguese (Brazil), Portuguese (Portugal), Romanian, Russian, Serbian, Slovak, Slovenian, Spanish, Swedish, Turkish, and Ukrainian.
>
> The Supervisor Desktop language is based on the language preference settings on your browser.
>
> For example, let us consider that you have selected the preferred language as French on the Google Chrome browser.
>
> When you launch the Supervisor Desktop in the Google Chrome browser, the Supervisor Desktop UI appears in Français (French).

- Click on the third menu option, you now see the **Team Performance Details** page where your agents activities are displayed : status, call duration, team, ... In the last column, you are presented two options : **chat** or **monitor**. The monitoring option is obvisously only enabled when an agent is in conversation with a customer otherwise the icon will be greyed.

- The columns displayed are the following

| **Column**             | **Description**                                                                                                                                                                                                                                                                                                                                |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Agent Name             | Displays name and avatar (Webex image) of the agent.                                                                                                                                                                                                                                                                                           |
| Agent State            | The work status while using the Supervisor Desktop. The agent availability state includes Available, Idle codes, or RONA.                                                                                                                                                                                                                      |
| Agent State Duration   | The time that the agent has been in the current state. The state timer format is hh:mm:ss (for example, 01:10:25).                                                                                                                                                                                                                             |
| Phone Number           | Dial number or extension of the agent signed in.                                                                                                                                                                                                                                                                                               |
| Site                   | Name of the site with which the agent is associated.                                                                                                                                                                                                                                                                                           |
| Team                   | Name of the team with which the agent is associated.                                                                                                                                                                                                                                                                                           |
| Channels               | The mode of communication through which an agent can communicate.For example, voice call.                                                                                                                                                                                                                                                      |
| Contact Queue          | Name of the queue from where the agent receives the incoming call.                                                                                                                                                                                                                                                                             |
| Contact Status         | The status of the agent in an active call. Example: Connected, Consulting, Conference, or Wrap up                                                                                                                                                                                                                                              |
| Time in Contact Status | The time spent by an agent in an active call. For example, the time an agent is in conference call.                                                                                                                                                                                                                                            |
| Total Contact Duration | Total duration of the contact from when it was first connected (including any other state like consult or conference in the same contact). The time elapsed since the agent accepted the request. The connected timer format is hh:mm:ss (for example, 01:10:25).                                                                              |
| Sign In Time           | The time an agent has signed in to theSupervisor Desktop. The date and time format is dynamic and displays according to location.                                                                                                                                                                                                              |
| Action                 | You can perform the following actions:• Review and Monitor - Based on the privilege provided by Administrator as part of user profile, you can review and monitor an ongoing agent call silently. • Send1:1 message to Agent – Based on the privilege provided by Administrator as part of user profile, you can send 1:1 message to an agent. |

- you can customize this view to show / hide columns or group information at your convenience.

![Supervisor_Modify_Columns](/assets/images/Supervisor/Supervisor_Modify_Columns.gif)

## Chat with your agents

Collaboration between agents and supervisors can help your Contact Center to be more effective and efficient for your customers and this is why we have enabled Webex messaging features in both Agent and Supervisor desktops.

- Click on the **Send Message** button

![Supervisor_Message](/assets/images/Supervisor/Supervisor_Message.gif)

- Fill the chat window with a message to send to your agent

![Supervisor_Message_Sent](/assets/images/Supervisor/Supervisor_Message_Sent.gif)

- On the agent side, observe the message notification received

![Supervisor_Message_Sent_Agent](/assets/images/Supervisor/Supervisor_Message_Sent_Agent.gif)

- If, as an agent, you want to answer to the supervisor, your will need to click on the **Webex logo** to open the Webex app embedded in the **Agent Desktop**. You can then reply to the supervisor directly.

![Supervisor_Message_Sent_To_Sup](/assets/images/Supervisor/Supervisor_Message_Sent_To_Sup.gif)

- On the supervisor side, observe the message notification received

![Supervisor_Message_Received_from_Agent](/assets/images/Supervisor/Supervisor_Message_Received_from_Agent.gif)

## Monitor calls

- As a supervisor, the **Team Performance Details** page allows you to see all connected agents and decide to monitor calls by clicking on the **Review and Monitor** icon.

![Supervisor_Monitor](/assets/images/Supervisor/Supervisor_Monitor.gif)

---

- The following popup will be displayed. Click on **Start Monitoring**. Please note a supervisor can monitor other call types such as callbacks, outdial calls, outbound preview campaign calls.

![Supervisor_Monitor_Accept](/assets/images/supervisor/Supervisor_Monitor_Accept.gif)

---

- In your **Supervisor Desktop**, an incoming popover window will be displayed and your softphone will ring as Webex Contact Center is now trying to reach you. You recognize the agent you want to monitor and other call variables are displayed. The Flow configuration defines variables to display on this popover (max 6). Accept the call on your supervisor softphone.

![Supervisor_Monitor_Floating](/assets/images/Supervisor/Supervisor_Monitor_Floating.gif)

---

- As a supervisor, the call you are now monitoring is displayed in your desktop with agent and customer details of which the call variables so you are aware of the context of the call. You can view previous communications with a customer across all channels (voice, email, chat, and social) in the **Contact History** pane. The pane displays details for the last 24 hours.

![Supervisor_Monitor_History](/assets/images/Supervisor/Supervisor_Monitor_History.gif)

---

- You can pause the monitoring and start is again if you will

![Supervisor_Monitor_Pause](/assets/images/Supervisor/Supervisor_Monitor_Pause.gif)

---

## Supervisor and Agent flow

- When you sign in to the Supervisor Desktop, you can - depending or your team assignement - choose either the supervisor role or supervisor AND agent role.

![Lab_4_ESD](/assets/images/Supervisor/Lab4_ESD_14_monitor.png)

- In the case, the supervisor experience is a bit different as your agent status appears in the header section of the Desktop.

![Lab_4_ESD](/assets/images/Supervisor/Supervisor_No_Message.gif)

- If, as a supervisor, you chose to monitor a call, your status is set to **Engaged** and you cannot take other calls as an agent.

![Supervisor_Engaged](/assets/images/Supervisor/Supervisor_Engaged.gif)

---

# Verify Supervisor Desktop Administration

> **The following section outlines where you can find the main configuration settings for Supervisors, and their Teams, Queues and other segmentation settings**

## Desktop Layout Regions for Supervisor

- The Supervisor Layout is enabled for a user via the [Desktop Layout JSON](https://webexone.github.io/assets/files/ESD_default_layout.json.zip) file for supervisor from GitHub.
- Open the file in any JSON editor, check and make sure it contains **_supervisor_** and **_supervisorAgent_** sections.
  - **_supervisor_** section is used when the user signs in to supervisor desktop with **_Supervisor_** role.
  - **_supervisorAdmin_** section is used when the user signs in to supervisor desktop with **_Supervisor and Agent_** role.

![Lab_4_WebexCC_Config_1](/assets/images/Supervisor/DC_Lab_4_Supervisor_WebexCC_1.png)

- Lets see where this is uploaded.
- On Webex Control Hub (admin.webex.com) - Go to _DESKTOP EXPERIENCE_ -> _Desktop Layout_

![CH_DesktopLayout](/assets/images/Supervisor/CH_DesktopLayout.gif)

---

- This is where we can upload a new Desktop layout for the Supervisor and also validate the layout.

![Lab_4_WebexCC_Config_3](/assets/images/Supervisor/DC_Lab_4_Supervisor_WebexCC_3.png)

---

- To verify layout Assignments, go to Control Hub > **_Teams_** and search for your Team (Team1 or Team2). You will find the WebexOne_desktopLayout in there.

![Lab_4_WebexCC_Config_4](/assets/images/Supervisor/DC_Lab_4_Supervisor_WebexCC_4.png)

## User Profile

- Under **_Provisioning_** -> **_User Profiles_**, find default **_Supervisor Profile_**, and let us take a look at it.

![Lab_4_WebexCC_Config_6](/assets/images/Supervisor/DC_Lab_4_Supervisor_WebexCC_6.png)

- We are able to view the Module Settings and Team settings and Access Rights.
- This is where we are able to check on the Supervisor settings.

![Lab_4_WebexCC_Config_7](/assets/images/Supervisor/DC_Lab_4_Supervisor_WebexCC_7.png)

- Go ahead and create a New User Profile: Name it <attendeeID>\_SupervisorProfile. Make this of type Supervisor.

- Try to select a subset of module settings, and teams. Here is where you can decide which teams you want to be able to monitor.

![Lab_4_WebexCC_Config_8](/assets/images/Supervisor/DC_Lab_4_Supervisor_WebexCC_8.png)

- Scroll to the bottom of the page and save the supervisor profile.

![Lab_4_WebexCC_Config_9](/assets/images/Supervisor/DC_Lab_4_Supervisor_WebexCC_9.png)

- Go to **Provisioning\*** -> **_Users_**, find your supervisor user, and Edit the User Profile to point to the new User Profile you just created: attendeeID_supervisorProfile

![Lab_4_WebexCC_Config_10](/assets/images/Supervisor/DC_Lab_4_Supervisor_WebexCC_10.png)

- Set the following parameters and save changes:

![Lab_4_WebexCC_Config_11](/assets/images/Supervisor/DC_Lab_4_Supervisor_WebexCC_11.png)

# Supervisor Licensing

> In This section, we will review the Supervisor Licensing that creates the supervisor.

- Login to Control Hub using your administrator account.
- Go to **_Users_**, click on supervisor's account, scroll dow to **_Licenses_** section and press **_Edit Licenses_** button.

![Lab_4_Supervisor_Config_1](/assets/images/Supervisor/DC_Lab_4_Supervisor_Config_1.png)

- Press **_Edit Licenses_** button on **_Edit services_** page.

![Lab_4_Supervisor_Config_2](/assets/images/Supervisor/DC_Lab_4_Supervisor_Config_2.png)

- Go to **_Contact Center_** tab, tick **_Licenses Agent_** checkbox and assign **_Premium Agent - Supervisor Role_** license. Then save changes.

![Lab_4_Supervisor_Config_3](/assets/images/Supervisor/DC_Lab_4_Supervisor_Config_3.png)

- Check and make sure supervisor license has been assigned. Then click on **_Close_** button to return to the user settings.

![Lab_4_Supervisor_Config_4](/assets/images/Supervisor/DC_Lab_4_Supervisor_Config_4.png)

- Check and make sure supervisor license is displayed in **_Licenses_** section of user seetings on Control Hub.

![Lab_4_Supervisor_Config_5](/assets/images/Supervisor/DC_Lab_4_Supervisor_Config_5.png)

- Go to **_Contact Center_** -> **_Settings_** and press **_Synchronize Users_** button to sync all changes from Control Hub to Webex CC Management Portal.

![Lab_4_Supervisor_Config_6](/assets/images/Supervisor/DC_Lab_4_Supervisor_Config_6.png)

## Send Product Feedback

Thank you for completing the Agent and Supervisor labs, we would love to hear direct product feedback from you!

Explore the product feedback option from right within the Contact Center Desktop.

Click the icon to launch the Experience Management Survey.

![ExperienceManagementSurvey](/assets/images/Supervisor/ExperienceManagementSurvey.gif)

---

Please fill in the survey and help us improve the product!

![ExperienceManagementSurvey_Form](/assets/images/Supervisor/ExperienceManagementSurvey_Form.gif)

---

<p style="text-align:center"><strong>Congratulations, you have officially completed the Agent and Supervisor Experience labs!</strong></p>
		
<p style="text-align:center;"><img src="/assets/gitbook/images/webex.png" width="100"></p>
