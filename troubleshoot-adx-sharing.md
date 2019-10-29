# Troubleshoot common issues in sharing and receiving data from Azure Data Explorer

This article explains how to troubleshoot common issues in sharing and receiving data from Azure Data Explorer.

## Azure Data Share invitation not showing up
In some cases, when a new user clicks Accept Invitation from the e-mail invitation that was sent, they may be presented with an empty list of invitations. This could be due to the following reasons:

1. Azure Data Share service is not registered as a resource provider of any Azure subscription in the Azure tenant. You will experience this issue if there is no Data Share resource in your Azure tenant. When you create an Azure Data Share resource, it automatically regisers the resource provider in your Azure subscription. You can also manually regiser the Data Share service following these steps. You'll need to have the Azure Contributor role to complete these steps.

* In the Azure portal, navigate to Subscriptions
* Select the subscription that you're using for Azure Data Share
* Click on Resource Providers
* Search for Microsoft.DataShare
* Click Register

1. Invitation is sent to your email alias instead of your Azure login email. If you have regiserted the Azure Data Share service or have already created a Data Share resource in the Azure tenant, but still cannot see the invitation, it maybe because the provider has entered your email alias as recipient instead of your Azure login email address. Contact your data provider and ensure that they have sent the invitation to your Azure login e-mail address and not your e-mail alias.

1. Invitation is no longer available after being accepted. The link in the email takes you to the Data Share Invitation page in Azure Portal, which only lists pending invitations. If you have already accepted the invitation, it will no longer show upw in the Data Share Invitation page. Proceed to your Data Share resource which you used to accept the invitation into to view received shares and configure your target Azure Data Explorer cluster setting.

## Received database not showing up

* Azure Subscription: If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.
* An Azure Data Explorer cluster to receive data into.
* A Data Share Invitation from your Data Provider.
* Permission to add role assignment to your Azure Data Explorer resource. This permission exists in Owner role.
