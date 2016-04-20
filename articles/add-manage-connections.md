<properties
    pageTitle="Manage connections in PowerApps | Microsoft PowerApps"
    description="Add or manage connections to SharePoint, SQL, OneDrive for Business, Salesforce, Office 365, OneDrive, DropBox, Twitter, Google Drive and more in PowerApps"
    services=""
    suite="powerapps"
    documentationCenter="na"
    authors="archnair"
    manager="darshand"
    editor=""
    tags=""/>

<tags
   ms.service="powerapps"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="na"
   ms.date="04/13/2016"
   ms.author="archanan"/>

# Manage connections in PowerApps

[AZURE.VIDEO nb:cid:UUID:0156313a-0d00-80c4-fa80-f1e592051e49]

Connections in PowerApps allow you to easily access your data while building apps. PowerApps includes commonly-used connections, including: SharePoint, SQL, Office 365, OneDrive for Business, Salesforce, Excel, Dropbox, Twitter and more.

For example, you can use connections to:

- Update a list on a SharePoint site.
- Get Excel data from your OneDrive for Business or Dropbox account.
- Connect to Office 365 and send email.
- Create a Twitter connection to send a tweet.

You can create new connections in PowerApps in multiple scenarios, such as:

1. While creating a new [app from data](get-started-create-from-data.md)

1. While create a new [app from blank](get-started-create-from-blank.md) or editing an existing app by [adding a new data source](add-data-connection.md)

1. While opening an app that was shared with you and creating connections required by the app

1. Creating new connections in [powerapps.com](https://web.powerapps.com).

However, to manage connections such as deleting connections or updating connections, you can only do it in [powerapps.com](https://web.powerapps.com).

This tutorial will cover how to manage connections in [powerapps.com](https://web.powerapps.com).

### Prerequisites
- [Sign up](signup-for-powerapps.md) for PowerApps, [install](http://aka.ms/powerappsinstall) it, open it, and then sign in by providing the same credentials that you used to sign up.

## Add a new connection to PowerApps

1. Go to [powerapps.com](https://web.powerapps.com) and sign in with your work on organization account.

1. Select **Connections** in the left pane

  ![Connections Manage](./media/add-manage-connections/manage-connections.png)

1. Select **Add a connection** on the top right

  ![Add a connection](./media/add-manage-connections/add-new-connections.png)

1. From the list of **Available connections**, select the connection you want to setup, such as SharePoint Online and provide your credentials to setup the connection

  ![SharePoint Connector](./media/add-manage-connections/sharepointapi.png)

1. Once the connection is setup, it will appear in the **Connections**

 ![SharePoint Connection](./media/add-manage-connections/sharepointconnection.png)

## Delete a connection

1. To delete a connection, go to the **Connections** page and select a connection

  ![Connections Manage](./media/add-manage-connections/connection-list.png)

1. In the details view of the connection, select **Delete** icon on the top right

  ![Connections Manage](./media/add-manage-connections/deleteicon.png)

## Update a connection

1. To update an existing connection, to go the **Connections** page and  select the edit icon. This will prompt you to update your connection with new credentials.

  ![Connections Manage](./media/add-manage-connections/editicon.png)


## Summary and next steps
In this topic, you learnt how to create, update and delete connections and authorized PowerApps to use this connection within any apps you create. As next steps, you can try to create apps using the connections you have just created.

- [Create an app from a set of data](get-started-create-from-data.md)
- [Create an app from a template](get-started-test-drive.md)
- [Add a new data source to an existing app](add-data-connection.md)