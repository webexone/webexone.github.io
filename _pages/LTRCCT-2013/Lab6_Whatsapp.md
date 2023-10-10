---
title: 'Lab 6: Whatsapp Configuration'
author: Dave Easton, Karthik Sundaram
date: 2023-10-04
layout: post
---

# Table of Contents

- [Table of Contents](#table-of-contents)
- [Introduction](#introduction)
  - [Lab Objective](#lab-objective)
  - [Pre-requisite](#pre-requisite)
- [Lab Section](#lab-section)
  - [Step 1. Verify Whatsapp Number Assignment](#step-1-verify-whatsapp-number-assignment)
  - [Step 2. Whatsapp Asset registration to Webex Engage](#step-2-whatsapp-asset-registration-to-webexcc)
  - [Step 3. Whatsapp Entry Point and Queue creation](#step-3-whatsapp-entry-point-and-queue-creation)
  - [Step 4. Create/Upload Whatsapp flow](#step-4-createupload-whatsapp-flow)
  - [Verification - send Whatsapp message and accept the request](#verification---send-whatsapp-message-and-accept-the-request)
  - [Back to top](#back-to-top)
    - [Congratulations, you have completed this section!](#congratulations-you-have-completed-this-section)

# Introduction

### Lab Objective

In this Lab, we will go through the tasks that are required to complete the basic whatsapp integration. You will be able to initiate a Whatsapp contact to the Contact Center and be able to accept/respond to the contact by logging in as an agent.

In this lab you will be configuring **WhatsApp** number settings, Assets, Entry Point and corresponding workflows. All these steps are required for integrating Whatsapp with our application.

### Pre-requisite

1. You received the admin credentials to configure in the Management Portal and Webex Connect.
2. You received the WhatsApp number associated with your individual lab.
3. You have successfully completed the previous Lab **Preconfiguration**

# Lab Section

## Step 1. Verify Whatsapp Number Assignment

- Login to your respective Webex Connect UI using the provided URL https://labtenant.us.webexconnect.io

- Navigate to Assets > Numbers and verify that the tenant you are using has a WhatsApp number assigned

<img align="middle" src="/images/Lab6_1.png" width="1000" />
<br/>
<br/>

> **Note**: Whatsapp Numbers cannot be procured directly from the Webex CC integrated Webex Connect tenant. For production use, please note that customers will have to work with Partners to go through a procurement process to enable Whatsapp and get numbers assigned to the tenant.

- Identify and make note of the APP ID (We will need this later in the flow configuration)

<img align="middle" src="/images/Lab6_1_a.png" width="1000" />
<br/>
<br/>

- Select actions and click **Manage**

<img align="middle" src="/images/Lab6_1_b.png" width="1000" />
<br/>
<br/>

- Identify and make a note of the **Number** and **WABA ID** (We will need this later in the flow configuration)

<img align="middle" src="/images/Lab6_1_c.png" width="1000" />
<br/>
<br/>

## Step 2. Whatsapp Asset registration to Webex Engage

- In the Whatsapp number assigned, under actions select the 'Manage' option

<img align="middle" src="/images/Lab6_2.png" width="1000" />
<br/>
<br/>

- Click 'Register to Webex Engage option'

<img align="middle" src="new_images\Lab6_whatsapp\Lab_6.1_register_to_engage.png" width="1000" />
<br/>
<br/>

- In the resulting window, select a service under which this asset would be managed

<img align="middle" src="new_images\Lab6_whatsapp\Lab_6.2_register_to_svc.png" width="1000" />
<br/>
<br/>

- Verify that the 'Register to Webex Engage' option is now disabled and there is a message indicating the time when the asset was registered along with the service to which it is assigned.

<img align="middle" src="new_images\Lab6_whatsapp\Lab_6.3_register_success.png" width="1000" />
<br/>
<br/>

## Step 3. Whatsapp Entry Point and Queue creation

- Login to Webex Contact Centre administration portal

- Click on **_Provisioning_** and select **_Entry Points/Queues_** > **_Entry Point_**.

- Click on `New Entry Point`.

<img align="middle" src="/images/Lab5_6.jpg" width="1000" />
<br/>
<br/>

- Input **_Name_** as `Whatsapp_EP_0XX` where <0XX> is your 3-digit lab ID.

- Select `Social Channel` in the **_Channel Type_** section.

- Select `Whatsapp` in the **_Social Channel Type_** section.

- Leave the **_Asset Name_** as appered value `Whatsapp Asset assigned in your Connect tenant`.

- The **_Time Zone_** can stay as default value.

- Click on **Save** after comparing your values with the screenshot below.

<img align="middle" src="/images/Lab6_7.png" width="1000" />
<br/>
<br/>

- Click on **_Provisioning_** and select **_Entry Points/Queues_** > **_Queue_**.

- Click on `New Queue`.

<img align="middle" src="/images/Lab5_8.jpg" width="1000" />
<br/>
<br/>

- Input **_Name_** as `Whatsapp_Queue_0XX` where <0XX> is your 3-digit lab ID.

- Select `Social Channel` in the **_Channel Type_** section.

- Click `Add Group` in the **_Conversation distribution_** section.

<img align="middle" src="/images/Lab6_9.png" width="1000" />
<br/>
<br/>

- Select the Agent based teams created in the previous lab and click `Save` . Once saved, click `Close` to exit this window.

<img align="middle" src="/images/Lab6_10.png" width="1000" />
<br/>
<br/>

- Input **_Maximum Time in Queue_** as `300`.

- The **_Time Zone_** can stay as default value.

- Click on **Save** after comparing your values with the screenshot below.

<img align="middle" src="/images/Lab6_11.png" width="1000" />
<br/>
<br/>

## Step 4. Create/Upload Whatsapp flow

- Download the Whatsapp flow from the [GitHub page](https://github.com/CiscoDevNet/webexcc-digital-channels/tree/main/Webex%20Connect%20Flows/v3.0/Template/Event%20Handling%20Workflows){:target="\_blank"}.

- Navigate to **webex connect flows -> 3.0->template -> media specific workflows -> whatsapp inbound flow.workflow.zip**, select the zip file and click download.

<img align="middle" src="new_images\Lab6_whatsapp\Lab_6.4_dl_wa_flow_github.png" width="1000" />
<br/>
<br/>

- Unzip the downloaded file.

- Go to Webex Connect, click on **Services** and select the service in which the Asset is created in step 2. It should be **My First Service 0XX**

- In the service click on **FLOWS** -> **CREATE FLOW**

- Enter the **FLOW NAME** as **Whatsapp Inbound Flow**, select the **TYPE** as **Work Flow** and under **METHOD** select **Upload a flow**.

- Drag and drop the **whatsapp inbound flow.workflow** flow that is downloaded in zip file, click **CREATE**

<img align="middle" src="new_images\Lab6_whatsapp\Lab_6.5_import_wa_flow.png" width="1000" />
<br/>
<br/>

- Once the flow is saved, the 'Configure Whatsapp Event' node will open. Select incoming message as trigger and click **Save**

<img align="middle" src="/images/Lab6_14.png" width="1000" />
<br/>
<br/>

- Open Custom variables and update the value for **WANNumber** , **WANumber_Countrycode** and **appid** (These are the values that were identified in Step-1)

<img align="middle" src="/images/Lab6_15.png" width="1000" />
<br/>
<br/>

- In the created workflow find the **Queue Task**, click twice, select the **QUEUE NAME** as **Whatsapp_Queue_0XX** and click on **SAVE**.

<img align="middle" src="/images/Lab6_16.png" width="1000" />
<br/>
<br/>

- Finally click on Make Live on top right corner and click Make Live. In the application drop down box, select the app that corresponds to your LAB ID.

<img align="middle" src="/images/Lab6_17.png" width="1000" />
<br/>
<br/>

- Wait for 2 minutes and verify that the flow is published successfully.

<img align="middle" src="new_images\Lab6_whatsapp\Lab_6.6_flow_live.png" width="1000" />
<br/>
<br/>

[To top of this lab](#table-of-contents)

## Verification - send Whatsapp message and accept the request

- Login to the Agent Desktop and make the agent Available.

<img align="middle" src="/images/Lab2_Agent1.png" width="1000" />
<br/>
<br/>

- In your personal mobile phone, add the Whatsapp number configured in the previous step as a new contact. (The screenshot is for reference. Please use the number assigned to your pod)

<img align="middle" src="/images/Lab6_23.png" width="1000" />
<br/>
<br/>

- Open Whatsapp and look up the contact created in the previous step

<img align="middle" src="/images/Lab6_24.png" width="500" />
<br/>
<br/>

- Send a message to the contact identified in the previous step to initiate the conversation.

<img align="middle" src="/images/Lab6_25.png" width="500" />
<br/>
<br/>

- The Whatsapp contact will be offered to the agent. Click "Accept" to handle the contact.

<img align="middle" src="/images/Lab6_19.png" width="1000" />
<br/>
<br/>

- Type a response and hit send button.

<img align="middle" src="/images/Lab6_20.png" width="1000" />
<br/>
<br/>

- End the contact

<img align="middle" src="/images/Lab6_21.png" width="1000" />
<br/>
<br/>

- Add wrap up and close the task.

<img align="middle" src="/images/Lab6_22.png" width="1000" />
<br/>
<br/>

## [Back to top](#table-of-contents)

### Congratulations, you have completed this section!

<script>
function mainPage() {window.location.href = "Home";}
function nextLab() 
 {
 window.location.href = "Lab7_Email_Advanced";
 }
</script>

<div id="button-row">
<button onclick="mainPage()" style="
  border-radius: 5px;
  background-color: rgb(116,191,75);
  padding: 10px;">Home Page</button>

<button onclick="nextLab()" style="
  position: absolute;
  right: 200px;
  border-radius: 5px;
  background-color: rgb(116,191,75);
  padding: 10px;">Go to the Next Lab</button>

</div>
