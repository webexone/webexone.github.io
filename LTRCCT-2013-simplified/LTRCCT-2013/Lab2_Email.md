---
title: 'Lab 2: Email Configuration'
---

# Table of Contents
- [Step 1. Gmail account configuration](#step-1-gmail-account-configuration)
- [Step 2. Create Email Asset and Register to WebeXCC](#step-2-create-email-asset-and-register-to-webexcc)
- [Step 3. Email Entry Point and Queue creation](#step-3-email-entry-point-and-queue-creation)
- [Step 4. Create/Upload Email flow](#step-4-createupload-email-flow)
- [Verification: Send an Email and accept the task](#verification-send-an-email-and-accept-the-task)


# Introduction

### Lab Objective

In this Lab, we will go through the tasks that are required to complete the basic email configuration. You will be able to initiate an email to the Contact Center and be able to accept/respond to the email by logging in as an agent.  

In this lab you will be configuring **Gmail** Account settings, Email Assets, Entry Point and corresponding workflows. All those steps are required for connecting the Email account with our application.  

### Pre-requisite

1. You received an admin credentials to configure in Management Portal and Webex Connect.
2. You received Email account credentials.
3. Lab1 Preconfiguration has been completed

**Preconfiguration**.

### Quick Links

> Control Hub: **[https://admin.webex.com](https://admin.webex.com){:target="_blank"}**\
> Portal: **[https://portal.wxcc-us1.cisco.com/portal](https://portal.wxcc-us1.cisco.com/portal){:target="_blank"}**\
> Agent Desktop: **[https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com){:target="_blank"}**\
> Gmail: **[https://mail.google.com](https://mail.google.com){:target="_blank"}**\
> Workflows: **[GitHub page](https://github.com/CiscoDevNet/webexcc-digital-channels){:target="_blank"}**\
> Webex Connect: **[https://labtenant.us.webexconnect.io](https://labtenant.us.webexconnect.io){:target="_blank"}**\

# Lab Section

### Configuration Order
<img align="middle" src="images/Lab2_ConfigOrder.png" width="1000" />
<br/>
<br/>

## Step 1. Gmail account configuration
Starting May 30, 2022 the **Less Secure Apps** feature was disabled on all Google accounts. As long as this setting was enabled, it was possible to send emails via Gmail SMTP. In this lab, we will be using new OAuth 2.0 authentication for outbound email functionality.

>**Note**: For this lab, we have created a Gmail account. Optionally, use your own account for polling and handling the emails. It can be a Gmail account or Office 365 account or any account which has email forwarding. The instructions below are applicable only for the Gmail accounts.


### 1. Gmail forwarding activation (for incoming emails)

| **User email**                       |
| ------------------------------------ | 
| Use your own existing gmail account or create a new one for this lab   | 


- Login to the Gmail account. If this is your firtst login, select **Turn off smart features** 

- Enable POP3/IMAP setting by clicking on settings icon on top right corner and selecting **See all settings**.

<img align="middle" src="images/Lab2_Gmail1.png" width="1000" />
<br/>
<br/>

- Now Click on **Forwarding and POP/IMAP**, enable the `POP Download` and `IMAP access` then click **Save Changes**.

<img align="middle" src="images/Lab2_Gmail2.png" width="1000" />
<br/>
<br/>


### 2. Create a project at Google API Console 
We need to activate the API if we want to use a Gmail accont for outbound email. 

- Login to [Google Developers Console](https://console.developers.google.com/){:target="_blank"} with your Gmail credentials.

- You will have to agree with the Terms of Service and pick their Country of residence. Then click **Select a project** and create a **NEW PROJECT**.

<img align="middle" src="new_images\LAB2_email\Lab2_2_google_console_new_project_png" width="1000" />
<br/>
<br/>

- Keep the default project's name and press **Create** at the bottom. Make sure that now you have selected this project. 

<img align="middle" src="new_images\LAB2_email\Lab2_3_google_console_proj_name_png" width="1000" />
<br/>
<br/>

### 3. Enable Gmail API (for outgoing emails)

- Enter `Gmail API` in the search bar and click on it once found.

<img align="middle" src="new_images\LAB2_email\Lab2_4_google_console_gmail_API_png" width="1000" />
<br/>
<br/>

- You need to enable the API for your project by clickin **ENABLE** button.

<img align="middle" src="new_images\LAB2_email\Lab2_5_google_console_gmail_API_enable_png" width="1000" />
<br/>
<br/>

### 4. Configure OAuth Consent Screen and Scopes

- Once the API is enabled, you’ll be taken to a nice dashboard that says, `"To use this API, you may need credentials"`.

<img align="middle" src="new_images\LAB2_email\Lab2_6_google_console_gmail_API_may_need_creds_png" width="1000" />
<br/>
<br/>

- To create an OAuth client ID, you must first configure your consent screen. Under the APIs and Services section, click on **OAuth Consent Screen**, set the user type as `External` and click **CREATE** button.

<img align="middle" src="new_images\LAB2_email\Lab2_7_google_console_oauth_external_png" width="1000" />
<br/>
<br/>

-  It will bring you to a page with many fields. Just enter the **App name** as `WebexApp`, choose your **User support email** and enter the same email in the **Developer contact information**. In the end press **SAVE AND CONTINUE**.

<img align="middle" src="new_images\LAB2_email\Lab2_8_google_console_app_info_png" width="1000" />
<br/>
<br/>

- On the next screen, you need to provide Auth 2.0 Scopes for Google APIs. Click the **Add Or Remove Scopes** button and add https://www.googleapis.com/auth/gmail.send to the list of scopes since we only want to send emails from Gmail and not read any user data. Click **SAVE AND CONTINUE**.

<img align="middle" src="new_images\LAB2_email\Lab2_9_google_console_scopes_png" width="1000" />
<br/>
<br/>

- On the test user page, click **ADD USERS** and enter your gmail address. Click **Save and Continue**.

<img align="middle" src="new_images\LAB2_email\Lab2_91_google_console_test_user_png" width="1000" />
<br/>
<br/>


### 5. Credentials and authentication with OAuth 2.0

Now create a new client ID that will be used to identify your application to Google’s OAuth servers.

- In the APIs & Services section, click on **Credentials** and then pick **OAuth client ID** from the drop-down list of the **CREATE CREDENTIALS** button. 

<img align="middle" src="new_images\LAB2_email\Lab2_92_google_console_oauth_client_ID_png" width="1000" />
<br/>
<br/>

- Select `Web application` in the **Application type**

- You can leave the default name. The name of your OAuth 2.0 client is only used to identify the client in the Google Cloud console and will not be shown to application users. 

- In the **Authorized redirect URIs** section click **ADD URI** button and set `https://labtenant.us.webexconnect.io/callback`. Click **CREATE** button in the end.

<img align="middle" src="new_images\LAB2_email\Lab2_93_email_CreateoAuthClientID.jpg" width="1000" />
<br/>
<br/>

- Download a JSON file with your credentials – you’ll need it later.

<img align="middle" src="new_images\LAB2_email\Lab2_931_google_console_json_png" width="1000" />
<br/>
<br/>


## Step 2. Create an Email Asset and Register to WebexCC

### 1. Create Email Asset

- As an admin, login to Webex Connect UI using the provided URL https://labtenant.us.webexconnect.io/

- Select **Assets** -> **Apps** -> **CONFIGURE NEW APP** -> **Email**.

<img align="middle" src="new_images\LAB2_email\lab2_94_create_email_app_gif" width="1000" />
<br/>
<br/>

- Set the settings according to the table below:

| **Entity**          | **Name** |
| ------------------- | -------- |
| Asset Name | EmailAsset_0XX  where <0XX> is your 3-digit attendee ID  |
| Email ID   | Your gmail address here  |
| Authentication Type | OAuth 2.0   |
| SMTP Server  | smtp.gmail.com |
| Username     | Your gmail address here |
| Port     | 465 |
| Security     | SSL |
| Client ID | \<client_id from JSON file\>   |
| client Secret | \<client_secret from JSON file\>    |
| Authorization URL | https://accounts.google.com/o/oauth2/auth |
| Scope | https://mail.google.com/ https://www.googleapis.com/auth/gmail.send |
| Access Token URL | https://oauth2.googleapis.com/token |
| Refresh Token URL | https://oauth2.googleapis.com/token |

> where \<ID\> is your POD ID



- Click **GENERATE TOKEN** and follow the step on the screenshot:

<img align="middle" src="new_images\LAB2_email\lab2_95_generate_token_gif" width="1000" />
<br/>
<br/>

- Verify that the **ACCESS TOKEN** and **REFRESH TOKEN** are generated and click **SAVE**.

<img align="middle" src="new_images\LAB2_email\Lab2_96_email_app_save_tokens_png" width="1000" />
<br/>
<br/>

- Click on **REGISTER TO Engage** and Select the service **My First Service_0XX**. In the end click **REGISTER**.

<img align="middle" src="new_images\LAB2_email\lab2_97_register_to_engage_gif" width="1000" />
<br/>
<br/>

### 2. Add forwarding Address

- Copy the forwarding address from the created asset in the previous step then go back to your gmail account. 
 
<img align="middle" src="images/Lab2_Assest4.png" width="1000" />
<br/>
<br/>

- Go back to the Gmail account and click on settings icon on top right corner -> Select **See all settings**.

<img align="middle" src="images/Lab2_Gmail1.png" width="1000" />
<br/>
<br/>

- Click on **Forwarding and POP/IMAP** -> click on **Add a forwarding address** -> Paste the copied forwarding address from the created asset. Then click on **Next**. In a new pop up tab click **Proceed** and then click **OK** when it prompts.

<img align="middle" src="images/Lab2_Gmail6.gif" width="1000" />
<br/>
<br/>

- Go back to Webex Connect and click on **Tools** -> **Export Logs**. 

- Under Inbound logs, Select the App that was created -> Select Channel Event as `Incoming Email` -> Select the period as `Today`. Wait until status is changed to **Ready for download** and click **Download** icon. 

<img align="middle" src="images/Lab2_ExportLog1.gif" width="1000" />
<br/>
<br/>

- Once a log file is downloaded, open the log file, under the **Subject** column, copy the confirmation code. 

<img align="middle" src="images/Lab2_ExportLog2.png" width="1000" />
<br/>
<br/>

- Go back to the Gmail account, paste the code in the email account verification section and click verify.

<img align="middle" src="images/Lab2_Gmail8.png" width="1000" />
<br/>
<br/>

- Select **Forward a copy of incoming mail to** the verified address and click **Save Changes**.

<img align="middle" src="images/Lab2_Gmail9.png" width="1000" />
<br/>
<br/>

## Step 3. Email Entry Point and Queue creation

### 1. Create Entry Point in Management Portal 

- Click on **_Provisioning_** and select **_Entry Points/Queues_** > **_Entry Point_**.

- Click on `New Entry Point`.

- Input **_Name_** as `Email_EP_0XX where 0XX is your 3 digit lab ID`.

- Select `Email` in the **_Channel Type_** section.

- Leave the **_Asset Name_** as appered value `EmailASSET_0XX`.

- Set **_Service Level Threshold_** as `2` hours.

- The **_Time Zone_** can stay as default value.

- Click on **Save** after comparing your values with the screenshot below.

<img align="middle" src="new_images/LAB2_email/Lab2_Email_0XX.png" width="1000" />

<br/>
<br/>

### 2. Create 2 Queues in Management Portal 

- Click on **_Provisioning_** and select **_Entry Points/Queues_** > **_Queue_**.

- Click on `New Queue`.

- Input **_Name_** as `Email_Q_0XX` where 0XX is your 3 digit Lab ID.

- Select `Email` in the **_Channel Type_** section.

- Leave the **_Queue Routing Type_** as default value `Longest Available Agent`.

- In the the **_Email Distribution_** click on **Add Group** and select `Team1_0XX` where 0XX is your 3 digit Lab ID.

- Set **_Service Level Threshold_** as `2` hours.

- Set **_Maximum Time in Queue_** as `3` hours.

- The **_Time Zone_** can stay as default value.

- Click on **Save** after comparing your values with the screenshot below.

<img align="middle" src="images/Lab2_Email_Q.png" width="1000" />
<br/>
<br/>

- Create a second queue by repeating the same steps as above.

- Input **_Name_** as `Email_Q2_0XX`.

- Select `Email` in the **_Channel Type_** section.

- In the the **_Email Distribution_** click on **Add Group** and select `Team2_0XX`.

<img align="middle" src="images/Lab2_Email_Q2.png" width="1000" />
<br/>
<br/>

## Step 4. Create/Upload Email flow

- Download the email flow from the [GitHub page](https://github.com/CiscoDevNet/webexcc-digital-channels/tree/imi_flow_simplification/Webex%20Connect%20Flows) 

- Navigate to **webex connect flows -> 3.0 -> template -> media specific workflows -> email inbound flow.workflow.zip**, select the zip file and click download.

- Unzip the downloaded file.

- Go to Webex Connect, click on **Services** and select the service in which the Asset is created in step 2. It should be **My First Service_0XX**

- In the service click on **FLOWS** -> **CREATE FLOW** .

- Enter the **FLOW NAME** as **Email Inbound Flow**, select the **TYPE** as **Work Flow** and under **METHOD** select **Upload a flow**.

- Drag and drop the **Email Inbound Flow.workflow** flow that is downloaded in zip file, click **CREATE** and then click **SAVE**.

<img align="middle" src="new_images\LAB2_email\Lab2_98_create_email_flow_png" width="1000" />
<br/>
<br/>

- Click **Save** and in the created workflow find the **Queue Task**, click twice, select the **QUEUE NAME** as **Email_Q_0XX** and click on **SAVE**.

<img align="middle" src="new_images\LAB2_email\Lab2_99_email_Qtask_node_png" width="1000" />
<br/>
<br/>

- Click **Settings** on top right corner and switch to **Custom variables** tab. Here in the **bizemailid** row, update the default value with your email address of the Gmail account. Click **SAVE**.

<img align="middle" src="images/Lab2_WF3.png" width="1000" />
<br/>
<br/>

- Finally click on Make Live on top right corner -> Select the Application/Asset that we have created and click Make Live.

<img align="middle" src="images/Lab2_WF4.png" width="1000" />
<br/>
<br/>

[To top of this lab](#table-of-contents)

## Verification: Send an Email and accept the task

- Go to personal email account and send an email to the support email address that was initially configured in the Email Asset.

- Go to the Agent Desktop and make the agent Available. 

<img align="middle" src="images/Lab2_Agent1.png" width="1000" />
<br/>
<br/>

- The Email will be offered to the agent. Click **Accept** to handle the email. Click "Reply" or Reply All" to the email and hit send button.

<img align="middle" src="new_images\LAB2_email\Lab2__991_email_reply_in_agent_desktop_png" width="1000" />
<br/>
<br/>

- Add wrap up and close the task.


[Back to top](#table-of-contents)
---

### Congratulations, you have completed this section! 

<script>
function mainPage() {window.location.href = "Home";}
function nextLab() 
 {
 window.location.href = "Lab3_Chat";
 }
</script>

<div id="button-row">
<button onclick="mainPage()" style="
  border-radius: 5px;
  background-color: rgb(116,191,75);
  padding: 10px;">Main Page</button>

<button onclick="nextLab()" style="
  position: absolute;
  right: 200px;
  border-radius: 5px;
  background-color: rgb(116,191,75);
  padding: 10px;">Next Lab</button>

</div>
