---
slug: google-sheet-database
title: google_sheet_database
date: 2025-10-28 12:23:53
updated: 
tags:
- google 
categories:
  - Note
---
slug: google-sheet-database

# How to Use Google Sheets / Excel as a Database?

1. Create a Google Spreadsheet
2. Set up dummy data fields (field names must be in English):
* id: serial number
* name: full name
* image: image
* email: email address
* phone: phone number

**Note: the form referred to below means (Sheet 1), not DB**
![](https://i.imgur.com/N1vHWEx.png)


3. Publish the Google Spreadsheet to the web
* For this demo, since there is only one sheet, we use "Entire document" directly. If there are multiple sheets and you only want some of them to be publicly accessible, just select the specific sheets you want to make public.

(Click "Publish to the web") then click Publish.


4. Next, remember to set the sheet's **View** permission to "Anyone with the link", to prevent permission errors in the following steps. The link here (this is the format you'll need later — click Copy link).

![](https://i.imgur.com/oyv4FR3.png)

Obtain a Google API Key
==

1. Create a new GCP project
This step is only needed if you don't have a project yet. Go to the Google Cloud Platform page and click New Project, give it a name, and create it.

2. Enable the Google Sheets API
Once you have a GCP project, go to the API Library: https://console.cloud.google.com/apis/library?hl=zh-TW

Search for "sheet" in the search bar and you will see "Google Sheets API":
![](https://i.imgur.com/nSgWAp0.png)
Click on it and then click "Enable" to activate the Google Sheets API for your project:
![](https://i.imgur.com/6Ps757J.png)
After enabling it, the page will return to GCP and you will see a banner reminding you that credentials are required to use the API.

Click "Create credentials" directly, or open: https://console.cloud.google.com/apis/credentials/wizard?hl=zh-TW

3. Create credentials
The first step in creating credentials involves a few selections:
![](https://i.imgur.com/GgjLWkQ.png)
"Select an API": choose "Google Sheets API".
"What data will you be accessing?" — After reading the documentation this is still a bit unclear in terms of use case, but selecting "Application data" works fine.

"Are you planning to use this API with Compute Engine, Kubernetes Engine, App Engine, or Cloud Functions?" — Since this guide is only for reading data from Google Sheets and does not involve any of those services, select "No, I'm not using them".

Then click "Next".

The next step is to fill in information about the service account so you can identify its purpose when you come back to it later:
![](https://i.imgur.com/9kpTubt.png)
After filling in the details, click "Create and Continue".

The remaining two items are optional and can be skipped — click "Done".

4. Create an API Key
After the previous step, the page will return to the Credentials page. Click "Create credentials" at the top and select "API key":
![](https://i.imgur.com/ce31aaN.png)
After a few seconds, a small window will appear showing "Your API key". This key is what you will append to your Google Sheets requests:

![](https://i.imgur.com/mj5sTgE.png)

The window also warns that you should restrict the key to prevent it from being used by others. Click "Restrict key" to go to the settings page.

It is strongly recommended to set restrictions. In this demo, the key is restricted to only work on the demo page and only with the Google Sheets API.

Now that we have an API key, we can use the new URL to make a GET request.

Google Sheets API v4 URL format:
==

```
https://sheets.googleapis.com/v4/spreadsheets/{spreadsheet-id}/values/{sheet-name}?alt=json&key={API-key}
```
* {spreadsheet-id}: visible in the spreadsheet's URL.
> The ID in the share link is NOT the same as the published link ID.
* {sheet-name}: the name of each individual sheet. The default is "Sheet1". Chinese names are also supported (tested and confirmed).
* {API-key}: the key we obtained from GCP in the previous section.

Here is a simple fetch example:
```
 fetch('https://sheets.googleapis.com/v4/spreadsheets/1JD19NEjYZNXuML_AX4G9Tg3SmQ8r9O7rayQNEkt_uq0/values/%E5%B7%A5%E4%BD%9C%E8%A1%A81?alt=json&key={api key}')
        .then(res => res.json())
        .then(res => {
          console.log(res)

```
Actual test result:
![](https://i.imgur.com/2msBaqR.png)

Related links for this article:
> Google Sheet 
https://docs.google.com/spreadsheets/d/1JD19NEjYZNXuML_AX4G9Tg3SmQ8r9O7rayQNEkt_uq0/edit?usp=sharing


