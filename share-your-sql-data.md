---
title: 'Tutorial: Share data from Azure SQL Database or Azure SQL Data Warehouse'
description: Tutorial - Share data from Azure SQL Database or Azure SQL Data Warehouse
author: joannapea
ms.author: joanpo
ms.service: data-share
ms.topic: tutorial
ms.date: 07/10/2019
---
# Tutorial: Share data from Azure SQL-based sources

In this tutorial you will learn how to set up a new Azure Data Share and start sharing SQL-based data with customers and partners outside of your Azure organization.

In this tutorial, you'll learn how to:

> [!div class="checklist"]
> * Create a Data Share.
> * Add tables and views to your Data Share.
> * Add recipients to your Data Share. 

## Prerequisites

* Azure Subscription: If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.
* An Azure SQL Database or Azure SQL Data Warehouse with tables and views that you want to share.
* Your data consumer's Azure login e-mail address (using their e-mail alias will not work).
* Permission for the data share to access the data warehouse. This can be done through the following steps: 
    1. Set yourself as the Azure Active Directory Admin for the server.
    1. Connect to the Azure SQL Database/Data Warehouse using Azure Active Directory.
    1. Use Query Editor (preview) to execute the following script to add the Data Share MSI as a db_owner. You must connect using Active Directory and not SQL Server authentication. 
    
            create user <share_acct_name> from external provider;
        
            exec sp_addrolemember db_owner, <share_acct_name>;
    
Note that the *<share_acc_name>* is the name of your Data Share Account. If you have not created a Data Share account as yet, you can come back to this pre-requisite later.         

* Client IP SQL Server Firewall access: This can be done through the following steps: 
        1. Navigate to *Firewalls and Virtual Networks*
        1. Click the **on** toggle to allow access to Azure Services. 

Once these pre-requisites are complete, you are ready for sharing data from SQL-based sources. 

## Sign in to the Azure portal

Sign in to the [Azure portal](https://portal.azure.com/).

## Create a Data Share Account

Create an Azure Data Share resource in an Azure resource group.

1. Select the **Create a resource** button (+) in the upper-left corner of the  portal.

1. Search for *Data Share*.

1. Select Data Share (preview) and Select **Create**.

1. Fill out the basic details of your Azure Data Share resource with the following information. 

     **Setting** | **Suggested value** | **Field description**
    |---|---|---|
    | Name | *datashareacount* | Specify a name for your data share account. |
    | Subscription | Your subscription | Select the Azure subscription that you want to use for your data share account.|
    | Resource group | *test-resource-group* | Use an existing resource group or create a new resource group. |
    | Location | *East US 2* | Select a region for your data share account.
    | | |

1. Select **Create** to provision your data share account. Provisioning a new data share account typically takes about 2 minutes or less. 

1. When the deployment is complete, select **Go to resource**.

## Create a Data Share

1. Navigate to your Data Share Overview page.

    ![Share your data](./media/share-receive-data.png "Share your data") 

1. Select **Start sharing your data**.

1. Select **Create**.   

1. Fill out the details for your Data Share. Specify a name, description of share contents, and terms of use (optional). 

    ![EnterShareDetails](./media/enter-share-details.png "Enter Share details") 

1. Select **Continue**

1. To add Datasets to your Data Share, select **Add Datasets**. 

    ![Datasets](./media/datasets.png "Datasets")

1. Select the dataset type that you would like to add. For the case of SQL-based sharing, select Azure SQL Database or Azure SQL Data Warehouse depending on where your data is stored. 

1. Navigate to the object you would like to share and select 'Add Datasets'. 

    ![SelectDatasets](./media/select-datasets.png "Select Datasets")    

1. In the Recipients tab, enter in the email addresses of your Data Consumer by selecting '+ Add Recipient'. 

    ![AddRecipients](./media/add-recipient.png "Add recipients") 

1. Select **Continue**

1. If you'd like your data consumer to be able to receive regular snapshots of your data, enable the snapshot schedule. 

    ![EnableSnapshots](./media/enable-snapshots.png "Enable snapshots") 

1. Select a start time and recurrence interval. 

1. Select **Continue**

1. In the Review + Create tab, review your Package Contents, Settings, Recipients, and Synchronization Settings. Select **Create**

Your Azure Data Share has now been created and the recipient of your Data Share is now ready to accept your invitation. 

## Next steps

In this tutorial, you learnt how to create an Azure Data Share and invite recipients. To learn about how a Data Consumer can accept and receive a data share, continue to the [accept and receive SQL data](receive-sql-data.md) tutorial. 
