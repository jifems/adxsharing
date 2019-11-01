# Troubleshoot common issues in sharing and receiving data from Azure Data Explorer

This article explains how to troubleshoot common issues in sharing and receiving data from Azure Data Explorer.

## Permission error when sharing data (add dataset failure)
In order to share data from your Azure Data Explorer cluster, you need to be Owner of the Azure Data Explorer cluster. Note that creator of the Azure Data Explorer cluster is not necessarily the owner. To check your permission, go to Azure Data Explorer cluster, select **Access control (IAM)**, then **Role assignments**. Note if this is the first time you are sharing data from this particular Azure Data Explorer cluster, it may take a few minutes for the role assignment to take effect. Please try again after a few minutes.

## Permission error to map target ADX cluster
In order to specify a target Azure Data Explorer cluster to access shared data, you need to be Owner of the target Azure Data Explorer cluster. Note that creator of the Azure Data Explorer clluster is not necessarily the owner. To check your permission, go to Azure Data Explorer cluster, select **Access control (IAM)**, then **Role assignments**. Note if this is the first time you are receiving data into this particular Azure Data Explorer cluster, it may take a few minutes for the role assignment to take effect. Please try again after a few minutes.

## Azure Data Share invitation not showing up
In some cases, when a new user clicks Accept Invitation from the e-mail invitation that was sent, they may be presented with an empty list of invitations. This could be due to the following reasons:

**1. Azure Data Share service is not registered as a resource provider of any Azure subscription in the Azure tenant.** You will experience this issue if there is no Data Share resource in your Azure tenant. When you create an Azure Data Share resource, it automatically regisers the resource provider in your Azure subscription. You can also manually regiser the Data Share service following these steps. You'll need to have the Azure Contributor role to complete these steps.

* In the Azure portal, navigate to **Subscriptions**
* Select the subscription you want to use to create Azure Data Share resource
* Click on **Resource Providers**
* Search for **Microsoft.DataShare**
* Click **Register**

**2. Invitation is sent to your email alias instead of your Azure login email.** If you have regiserted the Azure Data Share service or have already created a Data Share resource in the Azure tenant, but still cannot see the invitation, it maybe because the provider has entered your email alias as recipient instead of your Azure login email address. Contact your data provider and ensure that they have sent the invitation to your Azure login e-mail address and not your e-mail alias.

**3. Invitation has already been accepted.** The link in the email takes you to the Data Share Invitation page in Azure Portal, which only lists pending invitations. If you have already accepted the invitation, it will no longer show up in the Data Share Invitation page. Proceed to your Data Share resource which you used to accept the invitation into to view received shares and configure your target Azure Data Explorer cluster setting.

## Map to target UI does not show my Azure Data Explorer cluster
The target Azure Data Explorer cluster must be in the same Azure Data Center as the source Azure Data Explorer cluster. Only the Azure Data Explorer cluster in the same Azure Data Center will show up in the selection list. If you don't have an Azure Data Explorer cluster in the same region as the source, please create one and then continue with Map to target.

## Shared database is not showing up
If you already have a database of the same name in your consumer's ADX cluster, the shared database will not show up in the consumer's ADX cluster.

## Your question is still not answered?
Please contact azdatasharesupport@microsoft.com for support.
