---
title: 'Lab 5: SMS Configuration'
---


# Table of Contents
- [Table of Contents](#table-of-contents)
- [Introduction](#introduction)
    - [Lab Objective](#lab-objective)
    - [Pre-requisite](#pre-requisite)
- [Lab Section](#lab-section)
  - [Step 1. Verify SMS Number Assignment](#step-1-verify-sms-number-assignment)
  - [Step 2. SMS Asset registration to Webex Engage](#step-2-sms-asset-registration-to-webexcc)
    - [1. Register SMS asset to Webex Engage](#1-register-sms-asset-to-webexcc)
  - [Step 3. SMS Entry Point and Queue creation](#step-3-sms-entry-point-and-queue-creation)
    - [1. Create Entry Point in Managment Portal](#1-create-entry-point-in-managment-portal)
  - [Step 4. Create/Upload SMS flow](#step-4-createupload-sms-flow)
  - [Verification - send SMS and accept the request](#verification---send-sms-and-accept-the-request)
  - [Back to top](#back-to-top)
    - [Congratulations, you have completed this section!](#congratulations-you-have-completed-this-section)


# Introduction

### Lab Objective

In this Lab, we will go through the tasks that are required to complete the basic SMS integration. You will be able to initiate a SMS contact to the Contact Center and be able to accept/respond to the contact by logging in as an agent.  

In this lab you will be configuring **SMS** number settings, SMS Assets, Entry Point and corresponding workflows. All these steps are required for integrating SMS with our application.  


### Pre-requisite

1. You recived an admin credentials to configure in Managment Portal and Webex Connect.
2. You recived the SMS number associated with your tenat.
3. You have successfully completed the previous Lab **Preconfiguration**

# Lab Section

## Step 1. Verify SMS Number Assignment

- Login to your respective Webex Connect UI using the provided URL https://cl1pod**X**.imiconnect.io/ (where **X** is your POD number).

- Navigate to Assets > Numbers and verify that the tenant you are using has a SMS number assigned 

<img align="middle" src="new_images\Lab5_SMS\Lab_5_1_check_number_png" width="1000" />
<br/>
<br/>

>**Note**: SMS Numbers cannot be procured directly from the Webex CC integrated IMI Connect tenant. For production use, please note that customers will have to work with Partners to go through a procurement process to enable SMS and get numbers assigned to the tenant.


## Step 2. SMS Asset registration to Webex Engage

### 1. Register SMS asset to Webex Engage

- In the SMS number assigned, under actions select the 'Manage' option 

<img align="middle" src="new_images\Lab5_SMS\Lab_5_2_manage_number_png" width="1000" />
<br/>
<br/>

- Click 'Register to Webex Engage option' 

<img align="middle" src="new_images\Lab5_SMS\Lab_5_3_register_number_png" width="1000" />
<br/>
<br/>

- In the resulting window, select a service under which this asset would be managed

<img align="middle" src="new_images\Lab5_SMS\Lab_5_4_register_number_svc_png" width="1000" />
<br/>
<br/>

- Verify that the 'Register to Webex Engage' option is now disabled and there is a message indicating the time when the asset was registered along with the service to which it is assigned. 

<img align="middle" src="new_images\Lab5_SMS\Lab_5_5_registered_png" width="1000" />
<br/>
<br/>

## Step 3. SMS Entry Point and Queue creation

### 1. Create Entry Point in Managment Portal 

- Login to Webex Contact Centre administration portal 

- Click on **_Provisioning_** and select **_Entry Points/Queues_** > **_Entry Point_**.

- Click on `New Entry Point`.

<img align="middle" src="images/Lab5_6.jpg" width="1000" />
<br/>
<br/>

- Input **_Name_** as `SMS_EP`.

- Select `Social Channel` in the **_Channel Type_** section.

- Select `SMS` in the **_Social Channel Type_** section.

- Leave the **_Asset Name_** as appered value `SMS Number assigned in your Connect tenant`.

- The **_Time Zone_** can stay as default value.

- Click on **Save** after comparing your values with the screenshot below.

<img align="middle" src="images/Lab5_7.jpg" width="1000" />
<br/>
<br/>

- Click on **_Provisioning_** and select **_Entry Points/Queues_** > **_Queue_**.

- Click on `New Queue`.

<img align="middle" src="images/Lab5_8.jpg" width="1000" />
<br/>
<br/>

- Input **_Name_** as `SMS_Queue`.

- Select `Social Channel` in the **_Channel Type_** section.

- Click `Add Group` in the **_Conversation distribution_** section.

<img align="middle" src="images/Lab5_9.jpg" width="1000" />
<br/>
<br/>

- Select the Agent based teams created in the previous lab and click `Save` . Once saved, click `Close` to exit this window. 

<img align="middle" src="images/Lab5_10.jpg" width="1000" />
<br/>
<br/>

- Input **_Maximum Time in Queue_** as `300`.

- The **_Time Zone_** can stay as default value.

- Click on **Save** after comparing your values with the screenshot below.

<img align="middle" src="images/Lab5_11.jpg" width="1000" />
<br/>
<br/>


## Step 4. Create/Upload SMS flow

- Download the SMS flow from the [GitHub page](https://github.com/CiscoDevNet/webexcc-digital-channels/tree/imi_flow_simplification/Webex%20Connect%20Flows){:target="_blank"}.

- Navigate to **webex connect flows -> 3.0-> template-> media specific workflows -> smsinbound flow.workflow.zip**, select the zip file and click download.

<img align="middle" src="new_images\Lab5_SMS\Lab_5_6_SMS_github_flow_png" width="1000" />
<br/>
<br/>

- Unzip the downloaded file.

- Go to Webex Connect, click on **Services** and select the service in which the Asset is created in step 2. It should be **My First Service**

- In the service click on **FLOWS** -> **CREATE FLOW** 

- Enter the **FLOW NAME** as **SMS Inbound Flow**, select the **TYPE** as **Work Flow** and under **METHOD** select **Upload a flow**.

- Drag and drop the **SMS inbound flow.workflow** flow that is downloaded in zip file, click **CREATE** and then click **SAVE**.

<img align="middle" src="new_images\Lab5_SMS\Lab_5_6_SMS_upload_flow_png" width="1000" />
<br/>
<br/>

- Once the flow is saved, the 'Configure SMS Event' node will open. Select the SMS number assigned to your tenant in the **_INCOMING NUMBER_** section 

- Input **_*_** as `Keyword` and click on **Verify**

<img align="middle" src="new_images\Lab5_SMS\Lab_5_7_SMS_node_1_png" width="1000" />
<br/>
<br/>
  
- Once the **Success** message is displayed, click on **Save**

- In the created workflow find the **Queue Task**, click twice, select the **QUEUE NAME** as **SMS_Queue** and click on **SAVE**.

<img align="middle" src="images/Lab5_15.jpg" width="1000" />
<br/>
<br/>

- Find and open all the **SMS** nodes and select the SMS number assigned to your tenant in the **_FROM NUMBER_** section 

<img align="middle" src="new_images\Lab5_SMS\Lab_5_8_SMS_all_sms_nodes_png" width="1000" />
<br/>
<br/>

<img align="middle" src="new_images\Lab5_SMS\Lab_5_9_SMS_from_number_png" width="1000" />
<br/>
<br/>

- Finally click on Make Live on top right corner and click Make Live.

<img align="middle" src="new_images\Lab5_SMS\Lab_5_91_flow_live_png" width="1000" />
<br/>
<br/>

- Wait for 2 minutes and verify that the flow is **published** successfully. 


[To top of this lab](#table-of-contents)

## Verification - send SMS and accept the request

- Login to the Agent Desktop and make the agent Available. 

<img align="middle" src="images/Lab2_Agent1.png" width="1000" />
<br/>
<br/>

- From your mobile number send a SMS to the number that is assigned to your Webex Connect tenant and the one used in the flow configuration earlier.

- The SMS will be offered to the agent. Click "Accept" to handle the SMS.

<img align="middle" src="images/Lab5_20.jpg" width="1000" />
<br/>
<br/>

- Type a response and hit send button.

<img align="middle" src="images/Lab5_21.jpg" width="1000" />
<br/>
<br/>

- End the contact

<img align="middle" src="images/Lab5_22.jpg" width="1000" />
<br/>
<br/>

- Add wrap up and close the task. 

<img align="middle" src="images/Lab5_23.jpg" width="1000" />
<br/>
<br/>


[Back to top](#table-of-contents)
---

### Congratulations, you have completed this section! 

<script>
function mainPage() {window.location.href = "Home";}
function nextLab() 
 {
 window.location.href = "Lab6_Whatsapp";
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

