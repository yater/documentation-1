---
title: "Configuring a Windows SMB share"
description: "How to set up a general purpose Server Message Block share."
tags: ["networking","samba"]
---

If sharing a lot of data securely with many users is the goal, then setting up an SMB share can help. SMB shares allow the management and administration of large or small pools of data. SMB shares can be connected to any major operating systems including Windows, MacOS, and Linux.

To get started, make sure a <a href="/hub/initial-setup/storage/datasets/">dataset has been created</a>. This dataset stores the data that is going to be shared. Next, activate the SMB service, create the share, and configure permissions for the share.

## SMB Service

Connecting to an SMB share does not work when the related system service is not activated. To turn the SMB service on, go to **Services** and click the slider for *SMB*. If you want the service to activate whenever TrueNAS boots, set *Start Automatically*. 

The SMB service settings can be configured by clicking <i class="fas fa-pen" aria-hidden="true" title="Pen"></i>. Don't forget to click *SAVE* when changing the settings. Unless a specific setting is needed, it is recommended to use the default settings for the SMB service.

## SMB Share

Now create the Windows SMB share. Go to **Sharing > Windows Shares (SMB)** and click **ADD**. The only required field to continue is the *Path*. Set the path to the pool or dataset you want to share by entering a path in the field or clicking a directory in the file browser.

A descriptive *Name* helps identify the share. Otherwise, TrueNAS automatically assigns the name of the pool or dataset shared to the name of the SMB share.

A *Purpose* can be defined for the share. The *Purpose* is a preset for settings of the share. Depending on the purpose chosen, TrueNAS adjusts the settings of the share based off the purpose chosen. For example, if you chose *Private SMB Datasets and Shares*, TrueNAS automatically tunes some settings so the share can be used as a private share.

An optional *Description* can be specified to help explain the purpose of the share. For a more granular configuration, click **ADVANCED MODE**.

After changing the desired settings, click **SAVE**.

## Define Share Access

Users connecting to the SMB share must have [user accounts](/hub/tasks/administrative/users/) on the TrueNAS system before they can connect. You can also [create groups of users](/hub/tasks/administrative/groups/) to simplify assigning permissions to large numbers of users.

When LDAP has been configured and you want users from the LDAP server to have access the SMB share, set **Samba Schema** in **Directory Services > LDAP > ADVANCED MODE**.

{{% alert color="warning" %}}
If the LDAP setting **Samba Schema** is enabled, then the local TrueNAS user accounts cannot be used to connect to the share. Only user accounts configured on the LDAP server can connect to the share.
{{% /alert %}}

### Edit ACLs

The final step for setting up a general purpose SMB share is to control the permissions of the users accessing the share. After an SMB share has been created, it appears in the **Sharing > Windows Shares (SMB)** list. Go to the list and click <i class="fas fa-ellipsis-v" aria-hidden="true" title="Options"></i>&nbsp; **> Edit ACL** for the desired share.

Here you can change permissions for *owner@*, *group@*, and *everyone@*. New permissions for specific users or groups can also be defined by clicking *ADD ACL ITEM*. For more information on configuring ACLs, see <a href="/hub/tasks/advanced/editingacls/">Managing Access Control Lists</a>.
