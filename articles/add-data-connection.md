<properties	pageTitle="Add a new data connection | Microsoft PowerApps"
	description="Add a new data connection to an existing app or when building a new blank app"
	services=""
	suite="powerapps"
	documentationCenter="na"
	authors="archnair"
	manager="erikre"
	editor=""
	tags=""/>

<tags
   ms.service="powerapps"
   ms.devlang="na"
   ms.topic="get-started-article"
   ms.tgt_pltfrm="na"
   ms.workload="na"
   ms.date="04/19/2016"
   ms.author="archanan"/>


# Add a new data connection #

You can add a connection to a data source, including SharePoint Online, Salesforce, Dropbox, Twitter, and more. In your app, you "connect" to the data source, and then display the data within your app. For example, you can connect to OneDrive to display Excel data in your app, you can connect to Twilio to send an SMS message from your app, you can connect to SQL Azure and update a table from your app, and so on.

This topic shows you how to create a data connection within PowerApps. [Connections list](connections-list.md) lists all the available connections you can add.

## What you need to get started ##

- [Build an app](get-started-create-from-blank.md)
- Account and sign-in details for the service you are connecting to


## Add a data source to your app  ##
1. In PowerApps, select the **Content** tab:  

	![Content tab in the ribbon](./media/add-data-connection/content-tab.png)

1. Select **Data sources**:  

	![Data sources](./media/add-data-connection/data-sources.png)

1. The Data sources pane slides out on the right. Select **Add data source**:

	![Data sources pane](./media/add-data-connection/add-data-source.png)

1. Select an existing connection OR choose to add a new connection:

	![List of connections](./media/add-data-connection/list-of-connections.png)

1. From the list of available connections, choose the data source you want to connect to, such as **SharePoint Online** and select it.

	![List of APIs](./media/add-data-connection/list-of-api.png)

1. Click **Connect** and provide your credentials for SharePoint Online.

   ![SharePoint Online connect screen](./media/add-data-connection/sharepoint-connect.png)

1. Once the connection is established, select a site from the list of **Recent Sites** OR enter a **New Site**.

	![Select a SharePoint site](./media/add-data-connection/select-sp-site.png)

1. Select the table you want to use in your app using the checkbox. You can also select multiple tables. Select **Connect**:  

	![Select the tables in SharePoint](./media/add-data-connection/select-sp-tables.png)

1. The data sources are now added to your app and ready to be consumed:  

	![List of datasources addded to the app](./media/add-data-connection/data-sources-list.png)

## Consume the data source in your app ##

1. For tabular datasources such as SharePoint, SQL, Dynamics CRM or Excel, you will be able to consume the data in the app by binding the imported table to the controls in the app. See how to [show list of items in your app](add-gallery.md) or how to [show, add or edit a record from a table](add-form.md) for more details.

1. For non-tabular data sources such as Twitter or Microsoft Translator, you can consume the data source in your app by calling functions supported by that service.

	 For example, once you import Microsoft Translator as a datasource in your app (by following steps called out in the previous section), it will show up in the data source pane.

	 ![Twitter datasource](./media/add-data-connection/translator.png)

	 You can add a Text box to your app and bind the "Text" property of the Text box to MicrosoftTranslator.Translate("Hello","fr"). This function will translate the text "Hello" to French and you will see it in the text box.

  ![Function bar for Translator](./media/add-data-connection/translator-func.png)

	![Text box for Translator](./media/add-data-connection/translation-textbox.png)

## More good stuff
For some examples of adding connections, take a look at these:  
Create an app from Salesforce  **--> NEED LINK**  
Create an app from Dynamics  **--> NEED LINK**  
[Create an app using Excel data](get-started-create-from-data.md)