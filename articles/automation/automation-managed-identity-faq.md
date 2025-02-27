---
title: Azure Automation migration to managed identity FAQ
description: This article gives answers to frequently asked questions when you're migrating from a Run As account to a managed identity.
services: automation
ms.subservice: process-automation
ms.topic: conceptual
ms.date: 07/25/2021
ms.custom: devx-track-azurepowershell
#Customer intent: As an implementer, I want answers to various questions.
---

#  FAQ for migrating from a Run As account to a managed identity 

The following FAQ can help you migrate from a Run As account to a managed identity in Azure Automation. If you have any other questions about the capabilities, post them on the [discussion forum](https://aka.ms/retirement-announcement-automation-runbook-start-using-managed-identities). When a question is frequently asked, we add it to this article so that it benefits everyone.

## How long will you support a Run As account?
 
Automation Run As accounts will be supported until *September 30, 2023*. Although we continue to support existing users, we recommend that all new users use managed identities for runbook authentication. 

Existing users can still create a Run As account. You can go to the account properties and renew a certificate upon expiration until *January 30, 2023*. After that date, you won't be able to create a Run As account from the Azure portal. 

You'll still be able to create a Run As account through a [PowerShell script](/azure/automation/create-run-as-account#create-account-using-powershell) until support ends. You can [use this script](https://github.com/azureautomation/runbooks/blob/master/Utility/AzRunAs/RunAsAccountAssessAndRenew.ps1) to renew the certificate after *January 30, 2023*, until *September 30, 2023*. This script will assess the Automation account that has configured Run As accounts and renew the certificate if you choose to do so. On confirmation, the script will renew the key credentials of the Azure Active Directory (Azure AD) app and upload new a self-signed certificate to the Azure AD app.

## Will existing runbooks that use the Run As account be able to authenticate?
Yes, they'll be able to authenticate. There will be no impact to existing runbooks that use a Run As account.

## How can I renew an existing Run As account after January 30, 2023, when portal support to renew the account is removed?
You can [use this script](https://github.com/azureautomation/runbooks/blob/master/Utility/AzRunAs/RunAsAccountAssessAndRenew.ps1) to renew the Run As account certificate after January 30, 2023, until September 30, 2023.

## Can Run As accounts still be created after September 30, 2023, when Run As accounts will retire?
Yes, you can still create Run As accounts by using the [PowerShell script](../automation/create-run-as-account.md#create-account-using-powershell). However, this will be an unsupported scenario.

## Can Run As accounts still be renewed after September 30, 2023, when Run As account will retire?
You can use [this script](https://github.com/azureautomation/runbooks/blob/master/Utility/AzRunAs/RunAsAccountAssessAndRenew.ps1) to renew the Run As account certificate after September 30, 2023, when Run As accounts will retire. However, it will be an unsupported scenario.

## Will runbooks that still use the Run As account be able to authenticate after September 30, 2023?
Yes, the runbooks will be able to authenticate until the Run As account certificate expires.

## What is a managed identity?
Applications use managed identities in Azure AD when they're connecting to resources that support Azure AD authentication. Applications can use managed identities to obtain Azure AD tokens without managing credentials, secrets, certificates, or keys. 

For more information about managed identities in Azure AD, see [Managed identities for Azure resources](/azure/active-directory/managed-identities-azure-resources/overview). 

## What can I do with a managed identity in Automation accounts? 
An Azure Automation managed identity from Azure AD allows your runbook to access other Azure AD-protected resources easily. This identity is managed by the Azure platform and doesn't require you to provision or rotate any secrets. 

Key benefits are:
- You can use managed identities to authenticate to any Azure service that supports Azure AD authentication.
- Managed identities eliminate the overhead associated with managing Run As accounts in your runbook code. You can access resources via a managed identity of an Automation account from a runbook without worrying about creating the service principal, Run As certificate, Run As connection, and so on.
- You don't have to renew the certificate that the Automation Run As account uses.
 
## Are managed identities more secure than a Run As account?
A Run As account creates an Azure AD app that's used to manage the resources within the subscription through a certificate that has contributor access at the subscription level by default. A malicious user could use this certificate to perform a privileged operation against resources in the subscription, leading to potential vulnerabilities. 

Run As accounts also have a management overhead that involves creating a service principal, Run As certificate, Run As connection, certificate renewal, and so on. Managed identities eliminate this overhead by providing a secure method for users to authenticate and access resources that support Azure AD authentication without worrying about any certificate or credential management.

## Can a managed identity be used for both cloud and hybrid jobs?
Azure Automation supports [system-assigned managed identities](/azure/automation/automation-security-overview#managed-identities) for both cloud and hybrid jobs. Currently, Azure Automation [user-assigned managed identities](/azure/automation/automation-security-overview#managed-identities-preview) can be used for cloud jobs only and can't be used for jobs that run on a hybrid worker.

## Can I use a Run As account for new Automation account?
Yes, but only in a scenario where managed identities aren't supported for specific on-premises resources. We'll allow the creation of a Run As account through a [PowerShell script](/azure/automation/create-run-as-account#create-account-using-powershell).

## How can I migrate from an existing Run As account to a managed identity?
Follow the steps in [Migrate an existing Run As account to a managed identity](/azure/automation/migrate-run-as-accounts-managed-identity).

## How do I see the runbooks that are using a Run As account and know what permissions are assigned to that account?
Use [this script](https://github.com/azureautomation/runbooks/blob/master/Utility/AzRunAs/Check-AutomationRunAsAccountRoleAssignments.ps1) to find out which Automation accounts are using a Run As account. If your Azure Automation accounts contain a Run As account, it will have the built-in contributor role assigned to it by default. You can use the script to check the Azure Automation Run As accounts and determine if their role assignment is the default one or if it has been changed to a different role definition.

## Next steps

If your question isn't answered here, you can refer to the following sources for more questions and answers:

- [Azure Automation](https://docs.microsoft.com/answers/topics/azure-automation.html)
- [Feedback forum](https://feedback.azure.com/d365community/forum/721a322e-bd25-ec11-b6e6-000d3a4f0f1c)
