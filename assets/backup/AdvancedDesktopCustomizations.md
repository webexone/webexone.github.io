---
title: Advanced Desktop Customizations
author: Niko Theologitis & Arunabh Bhattacharjee
date: 2023-10-12
layout: post
---

## Table of Contents

| Topic                                                          | Type               | Dificulty | Time   |
| -------------------------------------------------------------- | ------------------ | --------- | ------ |
| [Agent Desktop Experience](#agent-desktop-overview)            | Demo & Walkthrough | EASY      | 20 min |
| [Extend the Agent Desktop Experience](#desktop-administration) | Practical Lab      | EASY      | 15 min |
| [Desktop Administration](#desktop-administration)              | Exploration        | EASY      | 15 min |

## Bonus: Advanced Desktop Customizations

The next section covers advanced customizations elements on the Agent Desktop and showcases the HOW in terms of customizing the desktop.
Refer to the sections to understand how the desktop layout was configured.

To get a copy of the Desktop Layout used in Webex One, go to:

You can open this file in any file editor.

## Basic JSON elements

The following are the top-level and most important properties to know for JSON layout:

- **`appTitle`**: To specify a title on the horizontal header of the Desktop. The default title is `Webex Contact Center`.

- **`logo`**: To specify a URL for the company logo. If you do not provide a URL, then the Webex Contact Center logo appears by default.

- **`taskPageIllustration`**: To specify a custom illustration for the task page based on organization preferences and brand alignment. When an agent signs in, the task page displays the configured illustration as a background. By default, the task page appears without illustration.
- **`stopNavigateOnAcceptTask`**: To determine whether to shift the focus to a newly accepted task, when the agent accepts the new task while working on a previous task. The default value is `false`.

- **`dragDropEnabled`**: To enable the drag-and-drop and resizing of the widgets on the custom pages, set the value to `true`. The default value is `false`.

- **`notificationTimer`**: To set the duration (in seconds) after which the desktop notifications on the Desktop are automatically dismissed. The notification appears at the top-right corner of the Desktop. The default timeout value is 8 seconds. The valid range for timeout values is 1-10 seconds. For the timeout changes to take effect, the browser must be refreshed after the changes are made.

- **`maximumNotificationCount`**: To set the number of desktop notifications to be displayed at a time on the Desktop. The default value is 3. The range for desktop notifications is 1-10. The desktop notifications are stacked. If there are many notifications, they appear with a slight delay depending on the `notificationTimer` settings.

- **`browserNotificationTimer`**: To set the duration (in seconds) after which the browser toaster notifications on the Desktop are automatically dismissed. Toaster is a native browser notification that appears only if the Desktop is not the active browser window or tab. The Desktop browser window or tab is inactive when

- **`wxmConfigured`**: (Optional) To configure Webex Experience Management, set the value to `true`. The default value is `false`.
- **`desktopChatApp`**: To configure multiple Cisco-offered chat applications such as Webex App.

- **`webexConfigured`**: Webex App along with its messaging, calling, and meeting functionalities, can be configured within the Desktop. This configuration allows agents to collaborate with other agents, supervisors, and subject matter experts (SMEs) in their organization without navigating away from the Desktop.

- **`headerActions`**: To change the order of the icons on the horizontal header of the Desktop. The default order is as follows:  **`["webex", "outdial", "notification"]`**.

- **`area`**: The `area` property is the core section of the Desktop Layout. You can define the layout as per the area.

<br/>

## Personalize the title and logo

> In this video, you will learn the desktop layout customization process. After watching this, you will be able to customize the Agent Desktop with a custom logo, custom title. You will also learn how to enable/disbale standard widgets:
> {: .block-tip }

<div style="padding-bottom:60.25%; position:relative; display:block; width: 100%">
	<iframe src="https://app.vidcast.io/share/embed/de0e97f2-d0bc-447a-b326-93ccbf190203" width="100%" height="100%" title="Create a Custom Desktop Layout" frameborder="0" loading="lazy" allowfullscreen style="position:absolute; top:0; left: 0"></iframe>
</div>

<br/>

- Login to **[https://portal.wxcc-us1.cisco.com](https://portal.wxcc-us1.cisco.com){:target="\_blank"}** with admin credentials.

- Navigate to **_Provisioning_** –> **_Desktop Layout_**.

- Click on **_New Layout_** button.

- Click on **_Download_** button to download the **Default Desktop Layout.json** file.

- Open the **Default Desktop Layout.json** file with any text editor (e.g. Notepad, Sublime text).

- Modify the **_appTitle_** key value with your company name in order to change Agent Desktop title.

- Modify the **_logo_** key value with your company logo URL or use this **https://raw.githubusercontent.com/wxcctechsummit/holcct2100/main/labslive/CiscoLiveLogo.jpg**.

- Modify the wxmConfigured and webexConfigured key values to **_true_** to enable the standard (out of box) widgets.

- **_Save As_** JSON file with a distinguishable name.
  <br/>

- Login as admin to **_Desktop Layout_** module in the **[Webex Contact Center Management Portal](https://portal.wxcc-us1.cisco.com){:target="\_blank"}**.

- Click on **_New Layout_**.

- Provide the following **name**: <w class = "attendee-class">attendeeID</w>\_desktopLayout

- Select <w class = "attendee-class">attendeeID</w>\_team2 as Team.

- Click **_Upload_** button to upload the modified JSON file.

- Click **_Save_** button to apply the layout.
  <br/>

- Login to the **[Agent Desktop](https://desktop.wxcc-us1.cisco.com/){:target="\_blank"}**.

- Open the **_User Profile_** and click on the arrow `>` under **_Team_**.

- Change the team of the agent to <w class = "attendee-class">attendeeID</w>\_team2

- Click on **_Save Team Selection_**.

- Confirm the changes by clicking on **_Change Team_**.

- Wait for few seconds to see the results.

- Now you should be able to see the new logo, new title and will be able to access the out of box widgets i.e Webex & Custom Experience Analytics.
  <br/>

## Reorder components of Horizontal Header

> In this section, you will learn how to reorder components of Horizontal Header.
> {: .block-tip }

<div style="padding-bottom:60.25%; position:relative; display:block; width: 100%">
	<iframe src="https://app.vidcast.io/share/embed/41edcf4e-25c5-45b6-8315-4a922ee615e3" width="100%" height="100%" title="Reorder components of Horizontal Header" frameborder="0" loading="lazy" allowfullscreen style="position:absolute; top:0; left: 0"></iframe>
</div>

- Take the same desktop layout file that you used in the last section.

- Open the desktop layout file with any text editor (e.g. Notepad, Sublime text).

- Make sure the layout version is 0.0.7 or higher.

- Under **_advancedHeader_**, change the order of components.

- **_Save As_** JSON file and upload it on **[Webex Contact Center Management Portal](https://portal.wxcc-us1.cisco.com){:target="\_blank"}** against your team.

- Now login to the **[Agent Desktop](https://desktop.wxcc-us1.cisco.com/){:target="\_blank"}** or refresh the browser if you are already logged in.

- You should be able to see the order of components in the Horizontal header as per your configuration.
  <br/>

## Create iFrame Widget & change default landing page

> The iFrame widget is a special widget that can be used to embed a different application. The iFrame widget creates an HTML iFrame and renders your application.
> {: .block-warning}

> In this section, you will learn how to create a iFrame widget and how to change the default landing page in the Agent Desktop. For this example, we are using Webex Contact Center Analyzer Report as a iFrame widget.
> {: .block-tip }

<div style="padding-bottom:60.25%; position:relative; display:block; width: 100%">
	<iframe src="https://app.vidcast.io/share/embed/d6e4883a-282e-4376-8b3e-b5bf67fc6b43" width="100%" height="100%" title="Create custom widget & change default landing page" frameborder="0" loading="lazy" allowfullscreen style="position:absolute; top:0; left: 0"></iframe>
</div>

- Take the default desktop layout file.

- Open the desktop layout file with any text editor (e.g. Notepad, Sublime text).

- Create another section under **_navigation_** similar to that of existing Customer Experience Analytics.

  > Check out this sample [Analyzer_iFrame_Widget.json](https://github.com/CiscoDevNet/webex-contact-center-api-samples/blob/main/widget-samples/iframe-widget-sample/Analyzer_iFrame_Widget_Layout.json)

- In the new section, add the **_label_** key value with your choice.

- Add the **_icon_** key value with your choice.

- Add a new key **_isDefaultLandingPage_** and its value should be set as **_true_**.

- **_src_** key value should be same as URL of your analyzer report.

- **_Save As_** JSON file and upload it on **[Webex Contact Center Management Portal](https://portal.wxcc-us1.cisco.com){:target="\_blank"}** against your team.

- Now login to the **[Agent Desktop](https://desktop.wxcc-us1.cisco.com/){:target="\_blank"}** or refresh the browser if you are already logged in.

- You should be able to see the new widget you added when you login to the agent desktop as it is set as the default landing page.

<br/>

## Populate Custom Widget with desktop parameters

> A Custom Widget is a component with some specific encapsulated functionality, exported as a custom HTML element that is placed within the desktop.
> {: .block-warning}

> Watch the demo below to understand the ability to pass default Desktop parameters into your Custom widget. This will help developers understand how data is handled in the Desktop STORE and injected into widgets inside of Webex Contact Center desktop.
> {: .block-tip }

<div style="padding-bottom:60.25%; position:relative; display:block; width: 100%">
	<iframe src="https://app.vidcast.io/share/embed/7ca5247d-462b-4b49-859c-62bee86477a3" width="100%" height="100%" title="Part 1 of 2: Sample Widget 101 & passing parameters" frameborder="0" loading="lazy" allowfullscreen style="position:absolute; top:0; left: 0"></iframe>
</div>

<div style="padding-bottom:60.25%; position:relative; display:block; width: 100%">
	<iframe src="https://app.vidcast.io/share/embed/6e211cd5-e0c6-4c38-a1dc-df647b60a0b3" width="100%" height="100%" title="Part 2 of 2: Sample Widget 101 & passing parameters" frameborder="0" loading="lazy" allowfullscreen style="position:absolute; top:0; left: 0"></iframe>
</div>

<br/>

Below, you will find a breakdown of all possible data and type definitions that is available through the STORE key:

- **STORE.agent**: Desktop profile info and settings.
- **STORE.agentContact**: Agent tasks and interactions
- **STORE.app**: Company logo, title and dark mode
- **STORE.auth**: Authentication token used for Single Sign On
- **STORE.generalNotifications**: Application notifications
- **STORE.dynamic**: Connector (smaller) or Desktop (larger) view area

<br/>

> Check the **[Developer guide](https://developer.webex-cx.com/documentation/guides/desktop/#custom-widgets)** for more details about Custom Widgets.
> {: .block-warning}

> If you want to explore and play around with the possible types of custom widgets you can create, check the below **Git repository with some samples:
> [https://github.com/CiscoDevNet/webex-contact-center-widget-starter/tree/master/Examples](https://github.com/CiscoDevNet/webex-contact-center-widget-starter/tree/master/Examples)**
> {: .block-warning}

<br/>

## JavaScript SDK and Modules

> Desktop JavaScript SDK is an npm package that allows you to request up-to-date information from the Desktop. Using the SDK, you can request information such as agent details, assigned tasks, details of specific tasks, current browser locale, and the authentication token for Single Sign-On (SSO) integration.
> {: .block-warning}

- To start using the JavaScript SDK, run the following command in your project folder: `npm install @wxcc-desktop/sdk --save` or `yarn add @wxcc-desktop/sdk`.

- Once you have installed the package in your project, include it in the appropriate component file following the ES6 import pattern: `import {Desktop} from "@wxcc-desktop/sdk";`.

- `Desktop` is the root module of the JavaScript SDK. The root module provides a reference to the following sub-modules:

  - Configuration Module
  - Localization Module
  - Actions Module
  - Logger Module
  - Agent State Information Module
  - Agent Contact Module
  - Dialer Module
  - Screen Pop Module
  - Shortcut Key Module
  - Call Monitoring Module

- Check the [Developer Guide](https://developer.webex-cx.com/documentation/guides/desktop#javascript-sdk-and-modules) for more details about each module.

<br/>

<br/>

---

  <script>
    document.addEventListener('DOMContentLoaded', () => {
      console.log('DOMContentLoaded OKOK')
    })

    window.addEventListener('load', () => {
      console.log('window load OK')
    })
  </script>

<p style="text-align:center"><strong>Congratulations, you have completed the Advanced Desktop Customizations Lab!</strong></p>
		
<p style="text-align:center;">![agent-desktop](/assets/gitbook/images/webex.png)</p>
