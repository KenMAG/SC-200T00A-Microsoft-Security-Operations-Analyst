---
lab:
    title: 'Exercise 1 - Configure your Microsoft Sentinel environment'
    module: 'Learning Path 7 - Configure your Microsoft Sentinel environment'
---

# Learning Path 7 - Lab 1 - Exercise 1 - Configure your Microsoft Sentinel environment

## Lab scenario

You're a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You need to understand the configuration of the Microsoft Sentinel environment to ensure it meets the company requirements to minimize cost, meet compliance regulations, and provide the most manageable environment for your security team to perform their daily job responsibilities.

>**Important:** The lab exercises for Learning Path #7 are in a *standalone* environment. If you exit the lab before completing it, you will be required to re-run the configurations again.

### Estimated time to complete this lab: 30 minutes

### Task 1 - Explore Microsoft Sentinel settings in Defender XDR

1. Log in to **WIN1** virtual machine as Admin with the password: **Pa55w.rd**.

1. In the Microsoft Edge browser, navigate to the Defender XDR at <https://security.microsoft.com>.
  
1. In the **Sign in** dialog box, copy, and paste in the tenant Email account for the admin username provided by your lab hosting provider and then select **Next**.

1. In the **Enter password** dialog box, copy, and paste in the admin's tenant password provided by your lab hosting provider and then select **Sign in**.

    >**Note:** You may be prompted to enter the *Temporary Access Pass* (TAP) instead of a password.

<!--- 1. In the Search bar of the Azure portal, type "Microsoft Sentinel," then select

1. Select **+ Create**.

1. Select **Create a new workspace**.

1. Select **Create new** for the Resource group.

1. Enter *Defender-RG* and select **Ok**.

1. For the Name, enter *defenderWorkspace*.

1. You can leave the default region for the workspace.

1. Select **Review + create** to validate the new workspace.

1. Select **Create** to deploy the workspace.

### Task 2 - Deploy Microsoft Sentinel to a workspace

Deploy Microsoft Sentinel to the workspace.

1. When the workspace deployment completes, select **Home** from the Microsoft Azure "breadcrumb" menu.

1. You should see a **Microsoft Sentinel** tile in the *Azure services* section of the portal. Select it.

1. Select **+ Create** from the menu items.

1. Select the *defenderWorkspace* you created in Task 1.

1. Select **Add**. --->

1. In the Microsoft Defender navigation menu, scroll down and expand the **System** section.

1. Select **Settings**, and then select **Microsoft Sentinel**.

1. In the *SIEM workspaces*, *Workspaces* pane, the **SentinelWorkspace-01** workspace is listed as Primary and shows a *Connected* Status.

1. Select the **SentinelWorkspace-01** to open the workspace settings options.

1. Expand each of the different sections to explore the available configuration options.

### Task 2 - Configure data retention

1. While still on the  workspace settings options page, expand **Log Analytics settings**, and select the **Configure Log Analytics workspace** link.

1. This opens a new browser tab to the Azure portal's Log Analytics workspace settings for the **SentinelWorkspace-01**.

1. Scroll down the navigation menu and expand the *Settings* section, then select **Usage and estimated costs**.

1. Select **Data retention** from the menu items.

1. Change data retention period to **180 days**.

1. Select **OK**.

1. Return to the Microsoft Defender XDR browser tab, and close the workspace settings options page.

### Task 3: Create a Watchlist

In this task, you create a watchlist in Microsoft Sentinel.

1. In the search box at the bottom of the Windows 11 screen, enter *Notepad*. Select **Notepad** from the results.

1. Type *Hostname* then enter for a new line.

1. From row 2 of the notepad, copy the following hostnames, each one in a different line:

    ```Notepad
    Host1
    Host2
    Host3
    Host4
    Host5
    ```

1. From the menu select, **File - Save As**, Name the file *HighValue.csv*, change the file type to **All files(*.*)** and select **Save**. **Hint:** The file can be saved in the *Documents* folder.

1. Close Notepad.

1. Select **Home** from the Microsoft Azure "breadcrumb" menu.

1. You should see **Microsoft Sentinel** tile in the *Azure services* section of the portal. Select it.

1. Select the **defenderWorkspace** Microsoft Sentinel workspace.

1. In Microsoft Sentinel, select the **Watchlist** option under the Configuration area.

1. Select **+ New** from the command bar.

1. In the Watchlist wizard, enter the following:

    |General setting|Value|
    |---|---|
    |Name|**HighValueHosts**|
    |Description|**High Value Hosts**|
    |Watchlist alias|**HighValueHosts**|

1. Select, **Next: Source >**.

1. Select **Browse for files** under *Upload file* and browse for the *HighValue.csv* file you created.

1. In the *SearchKey field,* select **Hostname**.

1. Select **Next: Review and Create >**.

1. Review the settings you entered and select **Create**.

1. The screen returns to the Watchlist page.

1. Select **Refresh** from the menu to see the new watchlist.

1. Select the *HighValueHosts* watchlist and on the right pane, select **View in logs**.

    >**Important:** It could take up to ten minutes for the watchlist to appear. **Please continue to with the following task and run this command on the next lab**.

    >**Note:** You can now use the _GetWatchlist('HighValueHosts') in your own KQL statements to access the list. The column to reference would be *Hostname*.

1. Close the *Logs* window by selecting the 'x' in the top-right and select **OK** to discard the unsaved edits.

### Task 5: Create a Threat Indicator

In this task, you create an indicator in Microsoft Sentinel.

1. In Microsoft Sentinel, select the **Threat intelligence** option in the Threat management area.

1. Select **+ Add New** from the command bar.

1. Select the **TI Object**.

1. From the *Object type* dropdown, select **Indicator**.

1. Select the **+ New observable** dropdown and select **Domain name**.

1. For Domain, enter a domain name, for example type *contoso.com*.

1. In the **Name** field, enter the same value used for the Domain.

1. In the *Indicator types*, select **malicious-activity**.

1. Set the **Valid from** field to today's date.

1. Scroll down to the **Description** and enter *This domain is known to be malicious*.

1. Select **Add**.

1. Select the **Logs** option under the *General* area of the *Sentinel* navigation menu. You might want to disable the "Always show queries" option and close the *Queries* window to run the KQL statements.

    >**Note:** In the default *New Query 1* tab, the **_GetWatchList('HighValueHosts')** query should still be there, and will now produce results if run.

1. Select the *+* sign to create a new query tab.

1. Run the following KQL statement.

    ```KQL
    ThreatIntelligenceIndicator
    ```

    >**Note:** It could take up to five minutes for the indicator to appear.

1. Scroll the results to the right to see the DomainName column. You can also run the following KQL statement to just see the DomainName column.

    ```KQL
    ThreatIntelligenceIndicator 
    | project DomainName
    ```

### Task 6: Configure log retention

In this task, you'll change the retention period for the SecurityEvent table.

1. In Microsoft Sentinel, select the **Settings** option under the *Configuration* area.

1. Select **Workspace settings**.

1. In Log Analytics workspace, select the **Tables** option under the *Settings* area.

1. Search and select the table **SecurityEvent**, and then select the ellipsis link (...).

    >**Note:** You may need to scroll to the right to see the ellipsis link.

1. Select **Manage Table**.

1. Change the *Interactive retention period* to **90 days**.

1. Reset the *Total retention period* to **180 days** (if needed). Notice that *Archive period* is set to *90 days*, because *Azure Monitor* automatically treats the remaining 90 days of total retention as low-cost, long-term retention.

1. Select **Save** to apply the changes.

## You have completed the lab
