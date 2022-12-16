# Setup Guide for connecting EBM (Enterprise Bot Manager) to human agent handover  

> This Genesys Cloud Developer Blueprint provides instructions on how to connect EBM (Enterprise Bot Manager) Chat Bots with Genesys Cloud, facilitating handover from chatbot to a human agent at appropriate points within a conversation.  In addition to checking agent availability, the connector passes chatbot transcripts to the agent at transfer. 

![High-level Architecture for EBM and Genesys Cloud chat integration](https://storage.googleapis.com/genesys_images/blueprint.png)

### Information required within your Genesys environment (example setup)

The following information from your Genesys Cloud Admin login is required for setup within EBM:

1. Get your Cloud Environment URL

Go to your existing URL instance and get your domain and top-level domain e.g. 

**ht<span>tps://</span>apps.euw2.pure.cloud** is our environment, therefore the Cloud Environment URL within EBM should be set to **euw2.pure.cloud**

2. Get your Organization ID

Get your Organization ID (from *Genesys Admin -> Account Settings -> Organization Settings*) 

![Organization ID](https://storage.googleapis.com/genesys_images/menu-organization.png)

Please note the **Advanced** option may need to be clicked to show the Organization ID

![Organization ID](https://storage.googleapis.com/genesys_images/organization-advanced-id.png)

3. Get your Chat Widget Deployment Key

Create a Chat Widget (from *Genesys Admin -> Contact Center -> Widgets*):

![Chat Widget](https://storage.googleapis.com/genesys_images/menu-chat-widget.png)

Select "Create Widget:

![Add Chat Widget](https://storage.googleapis.com/genesys_images/chatwidget.png)

- Give the chat widget a name
- Select the "Third Party" Widget Type
- Select "Save"

This will create the Chat Widget and generate your Deployment Key.

![Add Chat Widget](https://storage.googleapis.com/genesys_images/chatwidget2.png)

4. Get your Client ID and Client Secret

Create an app (from *Genesys Admin -> Integrations -> OAuth*)

![Chat Widget](https://storage.googleapis.com/genesys_images/menu-oauth-app.png)

Select "Add Client":

![Chat Widget](https://storage.googleapis.com/genesys_images/app-create1.png)

- Give your app a name
- **Grant Types** should be set to "Client Credentials"
- Select the tab "Roles"
- Assign the "**Trusted External User**" Role to the app
- Select "Save"

![Chat Widget](https://storage.googleapis.com/genesys_images/app-roles.png)

This will return you to the App screen where you should see your Client ID and Client Secret:

![Chat Widget](https://storage.googleapis.com/genesys_images/app-tokens.png)

5. Get your Handover Skill Name

Create a Queue (from *Genesys Admin -> Contact Center -> Queues*)

![Chat Widget](https://storage.googleapis.com/genesys_images/menu-queue.png)

Select "Create Queue":

![Chat Widget](https://storage.googleapis.com/genesys_images/queue-create.png)

- Enter a Queue Name
- Select "Save"

Select "Routing" Tab

![Chat Widget](https://storage.googleapis.com/genesys_images/queue-routing.png)

- "Routing Method" is "Standard Routing (Default)"
- "Evaluation Method" is set to "Disregard skills, next agent"
- Select "Save & Continue"

Select "Members Tab"

![Chat Widget](https://storage.googleapis.com/genesys_images/queue-members.png)

- Add appropriate users/groups to the Queue

### EBM Sample Setup (example setup)

Access the EBM Broker for your environment: 

- Select "Add Agent Service"
- Add "Genesys Chat Fallback"
- Select "Create"

Enter the following information:

![Chat Widget](https://storage.googleapis.com/genesys_images/ebm-broker.png)

- Cloud Environment - enter "Cloud Environment URL" from Genesys Setup Step 1
- Organization ID - enter "Organization ID" from Genesys Setup Step 2
- Deployment ID - enter the "Deployment Key" from Genesys Setup Step 3
- Client ID - enter the "Client ID" from Genesys Setup Step 4
- Client Access Token Secret - enter the "Client Secret" from Genesys Setup Step 4
- Handover Skill - enter the "Queue Name" from Genesys Setup Step 5
- Handover Error - text to send back to EBM to trigger an appropriate error handling intent

EBM conversational flows and an appropriate points be handed over to a Genesys Queue using the Intent "Human Handover" capabilities.