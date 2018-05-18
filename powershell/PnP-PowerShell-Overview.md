# PnP PowerShell overview

SharePoint Patterns and Practices (PnP) contains a library of PowerShell commands (PnP PowerShell) that allows you to perform complex provisioning and artifact management actions towards SharePoint. The commands use CSOM and can work against both SharePoint Online as SharePoint On-Premises. 

![SharePoint Patterns and Practices](https://devofficecdn.azureedge.net/media/Default/PnP/sppnp.png)

_**Applies to:** SharePoint Online | SharePoint 2016 | SharePoint 2013_

## Installation #

There are 3 ways to install the cmdlets. We recommend, where possible, to install them from the [PowerShell Gallery](https://www.powershellgallery.com). Alternatively you can download the setup files or run a PowerShell script to download the PowerShellGet module and install the cmdlets subsequently.

### PowerShell Gallery ###
If you main OS is Windows 10, of if you have [PowerShellGet](https://github.com/powershell/powershellget) installed, you can run the following commands to install the PowerShell cmdlets:

|**SharePoint Version**|**Command to install**|
|------------------|------------------|
|SharePoint Online|```Install-Module SharePointPnPPowerShellOnline ```|
|SharePoint 2016|```Install-Module SharePointPnPPowerShell2016```|
|SharePoint 2013|```Install-Module SharePointPnPPowerShell2013```|

*Notice*: if you install the latest PowerShellGet from Github, you might receive an error message stating 
>PackageManagement\Install-Package : The version 'x.x.x.x' of the module 'SharePointPnPPowerShellOnline' being installed is not catalog signed.

In order to install the cmdlets when you get this error specify the -SkipPublisherCheck switch with the Install-Module cmdlet, e.g. ```Install-Module SharePointPnPPowerShellOnline -SkipPublisherCheck -AllowClobber```

### Setup files ##
You can download setup files from the [releases](https://github.com/SharePoint/pnp-powershell/releases) section of the PnP PowerShell repository. These files will up be updated on a monthly basis. Run the install and restart any open instances of PowerShell to use the cmdlets.

### Installation script ##
This is an alternative for installation on machines that have at least PowerShell v3 installed. You can find the version of PowerShell  by opening PowerShell and running ```$PSVersionTable.PSVersion```. The value for ```Major``` should be above 3.

To install the cmdlets you can run the below command which will install PowerShell Package Management and then install the PowerShell Modules from the PowerShell Gallery.

```powershell
Invoke-Expression (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/OfficeDev/PnP-PowerShell/master/Samples/Modules.Install/Install-SharePointPnPPowerShell.ps1')
```

## Updating ##
Every month a new release will be made available of the PnP PowerShell Cmdlets. If you earlier installed the cmdlets using the setup file, simply download the [latest version](https://github.com/SharePoint/PnP-PowerShell/releases/latest) and run the setup. This will update your existing installation.

If you have installed the cmdlets using PowerShellGet with ```Install-Module``` from the PowerShell Gallery then you will be able to use the following command to install the latest updated version:

```powershell
Update-Module SharePointPnPPowerShell*
``` 

This will automatically load the module after starting PowerShell 3.0.

You can check the installed PnP-PowerShell versions with the following command:

```powershell
Get-Module SharePointPnPPowerShell* -ListAvailable | Select-Object Name,Version | Sort-Object Version -Descending
```

## Getting Started #

To use the library you first need to connect to your tenant:

```powershell
Connect-PnPOnline –Url https://yoursite.sharepoint.com –Credentials (Get-Credential)
```

To view all cmdlets, enter

```powershell
Get-Command -Module *PnP*
```

At the following links you will find a few videos on how to get started with the cmdlets:

* https://channel9.msdn.com/blogs/OfficeDevPnP/PnP-Web-Cast-Introduction-to-Office-365-PnP-PowerShell
* https://channel9.msdn.com/blogs/OfficeDevPnP/Introduction-to-PnP-PowerShell-Cmdlets
* https://channel9.msdn.com/blogs/OfficeDevPnP/PnP-Webcast-PnP-PowerShell-Getting-started-with-latest-updates

### Setting up credentials ##
See this [wiki page](https://github.com/SharePoint/PnP-PowerShell/wiki/How-to-use-the-Windows-Credential-Manager-to-ease-authentication-with-PnP-PowerShell) for more information on how to use the Windows Credential Manager to setup credentials that you can use in unattended scripts

## Cmdlet overview


### Apps 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Get&#8209;PnPAppInstance](../../module/sharepoint-pnp/GetPnPAppInstance.md)** |Returns a SharePoint AddIn Instance in the site|All
**[Uninstall&#8209;PnPAppInstance](../../module/sharepoint-pnp/UninstallPnPAppInstance.md)** |Removes an app from a site|All
**[Import&#8209;PnPAppPackage](../../module/sharepoint-pnp/ImportPnPAppPackage.md)** |Adds a SharePoint Addin to a site|All


### Base Cmdlets 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Get&#8209;PnPAppAuthAccessToken](../../module/sharepoint-pnp/GetPnPAppAuthAccessToken.md)** |Returns the access token from the current client context (In App authentication mode only)|All
**[Get&#8209;PnPAuthenticationRealm](../../module/sharepoint-pnp/GetPnPAuthenticationRealm.md)** |Gets the authentication realm for the current web|All
**[Get&#8209;PnPAzureADManifestKeyCredentials](../../module/sharepoint-pnp/GetPnPAzureADManifestKeyCredentials.md)** |Creates the JSON snippet that is required for the manifest JSON file for Azure WebApplication / WebAPI apps|All
**[Get&#8209;PnPContext](../../module/sharepoint-pnp/GetPnPContext.md)** |Returns a Client Side Object Model context|All
**[Set&#8209;PnPContext](../../module/sharepoint-pnp/SetPnPContext.md)** |Sets the Client Context to use by the cmdlets|All
**[Get&#8209;PnPHealthScore](../../module/sharepoint-pnp/GetPnPHealthScore.md)** |Retrieves the current health score value of the server|All
**[Connect&#8209;PnPOnline](../../module/sharepoint-pnp/ConnectPnPOnline.md)** |Connects to a SharePoint site and creates a context that is required for the other PnP Cmdlets|All
**[Disconnect&#8209;PnPOnline](../../module/sharepoint-pnp/DisconnectPnPOnline.md)** |Disconnects the context|All
**[Get&#8209;PnPProperty](../../module/sharepoint-pnp/GetPnPProperty.md)** |Will populate properties of an object and optionally, if needed, load the value from the server. If one property is specified its value will be returned to the output.|All
**[Execute&#8209;PnPQuery](../../module/sharepoint-pnp/ExecutePnPQuery.md)** |Executes any queued actions / changes on the SharePoint Client Side Object Model Context|All
**[Get&#8209;PnPStoredCredential](../../module/sharepoint-pnp/GetPnPStoredCredential.md)** |Returns a stored credential from the Windows Credential Manager|All
**[Set&#8209;PnPTraceLog](../../module/sharepoint-pnp/SetPnPTraceLog.md)** |Defines if tracing should be turned on. PnP Core, which is the foundation of these cmdlets uses the standard Trace functionality of .NET. With this cmdlet you can turn capturing of this trace to a log file on or off.|All


### Branding 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Add&#8209;PnPCustomAction](../../module/sharepoint-pnp/AddPnPCustomAction.md)** |Adds a custom action to a web|All
**[Get&#8209;PnPCustomAction](../../module/sharepoint-pnp/GetPnPCustomAction.md)** |Returns all or a specific custom action(s)|All
**[Remove&#8209;PnPCustomAction](../../module/sharepoint-pnp/RemovePnPCustomAction.md)** |Removes a custom action|All
**[Get&#8209;PnPHomePage](../../module/sharepoint-pnp/GetPnPHomePage.md)** |Returns the URL to the home page|All
**[Set&#8209;PnPHomePage](../../module/sharepoint-pnp/SetPnPHomePage.md)** |Sets the home page of the current web.|All
**[Add&#8209;PnPJavaScriptBlock](../../module/sharepoint-pnp/AddPnPJavaScriptBlock.md)** |Adds a link to a JavaScript snippet/block to a web or site collection|All
**[Add&#8209;PnPJavaScriptLink](../../module/sharepoint-pnp/AddPnPJavaScriptLink.md)** |Adds a link to a JavaScript file to a web or sitecollection|All
**[Get&#8209;PnPJavaScriptLink](../../module/sharepoint-pnp/GetPnPJavaScriptLink.md)** |Returns all or a specific custom action(s) with location type ScriptLink|All
**[Remove&#8209;PnPJavaScriptLink](../../module/sharepoint-pnp/RemovePnPJavaScriptLink.md)** |Removes a JavaScript link or block from a web or sitecollection|All
**[Get&#8209;PnPMasterPage](../../module/sharepoint-pnp/GetPnPMasterPage.md)** |Returns the URLs of the default Master Page and the custom Master Page.|All
**[Set&#8209;PnPMasterPage](../../module/sharepoint-pnp/SetPnPMasterPage.md)** |Sets the default master page of the current web.|All
**[Set&#8209;PnPMinimalDownloadStrategy](../../module/sharepoint-pnp/SetPnPMinimalDownloadStrategy.md)** |Activates or deactivates the minimal downloading strategy.|All
**[Add&#8209;PnPNavigationNode](../../module/sharepoint-pnp/AddPnPNavigationNode.md)** |Adds a menu item to either the quicklaunch or top navigation|All
**[Remove&#8209;PnPNavigationNode](../../module/sharepoint-pnp/RemovePnPNavigationNode.md)** |Removes a menu item from either the quicklaunch or top navigation|All
**[Disable&#8209;PnPResponsiveUI](../../module/sharepoint-pnp/DisablePnPResponsiveUI.md)** |Disables the PnP Responsive UI implementation on a classic SharePoint Site|All
**[Enable&#8209;PnPResponsiveUI](../../module/sharepoint-pnp/EnablePnPResponsiveUI.md)** |Enables the PnP Responsive UI implementation on a classic SharePoint Site|All
**[Get&#8209;PnPTheme](../../module/sharepoint-pnp/GetPnPTheme.md)** |Returns the current theme/composed look of the current web.|All
**[Set&#8209;PnPTheme](../../module/sharepoint-pnp/SetPnPTheme.md)** |Sets the theme of the current web.|All


### Client-Side Pages 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Get&#8209;PnPAvailableClientSideComponents](../../module/sharepoint-pnp/GetPnPAvailableClientSideComponents.md)** |Gets the available client side components on a particular page|SharePoint Online
**[Add&#8209;PnPClientSidePage](../../module/sharepoint-pnp/AddPnPClientSidePage.md)** |Adds a Client-Side Page|SharePoint Online
**[Get&#8209;PnPClientSidePage](../../module/sharepoint-pnp/GetPnPClientSidePage.md)** |Gets a Client-Side Page|SharePoint Online
**[Remove&#8209;PnPClientSidePage](../../module/sharepoint-pnp/RemovePnPClientSidePage.md)** |Removes a Client-Side Page|SharePoint Online
**[Set&#8209;PnPClientSidePage](../../module/sharepoint-pnp/SetPnPClientSidePage.md)** |Sets parameters of a Client-Side Page|SharePoint Online
**[Add&#8209;PnPClientSidePageSection](../../module/sharepoint-pnp/AddPnPClientSidePageSection.md)** |Adds a new section to a Client-Side page|SharePoint Online
**[Add&#8209;PnPClientSideText](../../module/sharepoint-pnp/AddPnPClientSideText.md)** |Adds a Client-Side Page|SharePoint Online
**[Add&#8209;PnPClientSideWebPart](../../module/sharepoint-pnp/AddPnPClientSideWebPart.md)** |Adds a Client-Side Component to a page|SharePoint Online


### Content Types 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Add&#8209;PnPContentType](../../module/sharepoint-pnp/AddPnPContentType.md)** |Adds a new content type|All
**[Get&#8209;PnPContentType](../../module/sharepoint-pnp/GetPnPContentType.md)** |Retrieves a content type|All
**[Remove&#8209;PnPContentType](../../module/sharepoint-pnp/RemovePnPContentType.md)** |Removes a content type from a web|All
**[Remove&#8209;PnPContentTypeFromList](../../module/sharepoint-pnp/RemovePnPContentTypeFromList.md)** |Removes a content type from a list|All
**[Get&#8209;PnPContentTypePublishingHubUrl](../../module/sharepoint-pnp/GetPnPContentTypePublishingHubUrl.md)** |Returns the url to Content Type Publishing Hub|All
**[Add&#8209;PnPContentTypeToList](../../module/sharepoint-pnp/AddPnPContentTypeToList.md)** |Adds a new content type to a list|All
**[Set&#8209;PnPDefaultContentTypeToList](../../module/sharepoint-pnp/SetPnPDefaultContentTypeToList.md)** |Sets the default content type for a list|All
**[Remove&#8209;PnPFieldFromContentType](../../module/sharepoint-pnp/RemovePnPFieldFromContentType.md)** |Removes a site column from a content type|All
**[Add&#8209;PnPFieldToContentType](../../module/sharepoint-pnp/AddPnPFieldToContentType.md)** |Adds an existing site column to a content type|All


### Document Sets 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Remove&#8209;PnPContentTypeFromDocumentSet](../../module/sharepoint-pnp/RemovePnPContentTypeFromDocumentSet.md)** |Removes a content type from a document set|All
**[Add&#8209;PnPContentTypeToDocumentSet](../../module/sharepoint-pnp/AddPnPContentTypeToDocumentSet.md)** |Adds a content type to a document set|All
**[Add&#8209;PnPDocumentSet](../../module/sharepoint-pnp/AddPnPDocumentSet.md)** |Creates a new document set in a library.|All
**[Set&#8209;PnPDocumentSetField](../../module/sharepoint-pnp/SetPnPDocumentSetField.md)** |Sets a site column from the available content types to a document set|All
**[Get&#8209;PnPDocumentSetTemplate](../../module/sharepoint-pnp/GetPnPDocumentSetTemplate.md)** |Retrieves a document set template|All


### Event Receivers 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Add&#8209;PnPEventReceiver](../../module/sharepoint-pnp/AddPnPEventReceiver.md)** |Adds a new event receiver|All
**[Get&#8209;PnPEventReceiver](../../module/sharepoint-pnp/GetPnPEventReceiver.md)** |Returns all or a specific event receiver|All
**[Remove&#8209;PnPEventReceiver](../../module/sharepoint-pnp/RemovePnPEventReceiver.md)** |Removes/unregisters a specific event receiver|All


### Features 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[New&#8209;PnPExtensbilityHandlerObject](../../module/sharepoint-pnp/NewPnPExtensbilityHandlerObject.md)** |Creates an ExtensibilityHandler Object, to be used by the Get-SPOProvisioningTemplate cmdlet|All
**[Disable&#8209;PnPFeature](../../module/sharepoint-pnp/DisablePnPFeature.md)** |Disables a feature|All
**[Enable&#8209;PnPFeature](../../module/sharepoint-pnp/EnablePnPFeature.md)** |Enables a feature|All
**[Get&#8209;PnPFeature](../../module/sharepoint-pnp/GetPnPFeature.md)** |Returns all activated or a specific activated feature|All


### Fields 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Add&#8209;PnPField](../../module/sharepoint-pnp/AddPnPField.md)** |Adds a field to a list or as a site column|All
**[Get&#8209;PnPField](../../module/sharepoint-pnp/GetPnPField.md)** |Returns a field from a list or site|All
**[Remove&#8209;PnPField](../../module/sharepoint-pnp/RemovePnPField.md)** |Removes a field from a list or a site|All
**[Set&#8209;PnPField](../../module/sharepoint-pnp/SetPnPField.md)** |Changes one or more properties of a field in a specific list or for the whole web|All
**[Add&#8209;PnPFieldFromXml](../../module/sharepoint-pnp/AddPnPFieldFromXml.md)** |Adds a field to a list or as a site column based upon a CAML/XML field definition|All
**[Add&#8209;PnPTaxonomyField](../../module/sharepoint-pnp/AddPnPTaxonomyField.md)** |Adds a taxonomy field to a list or as a site column.|All
**[Set&#8209;PnPView](../../module/sharepoint-pnp/SetPnPView.md)** |Changes one or more properties of a specific view|All


### Files and Folders 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Add&#8209;PnPFile](../../module/sharepoint-pnp/AddPnPFile.md)** |Uploads a file to Web|All
**[Copy&#8209;PnPFile](../../module/sharepoint-pnp/CopyPnPFile.md)** |Copies a file or folder to a different location|All
**[Find&#8209;PnPFile](../../module/sharepoint-pnp/FindPnPFile.md)** |Finds a file in the virtual file system of the web.|All
**[Get&#8209;PnPFile](../../module/sharepoint-pnp/GetPnPFile.md)** |Downloads a file.|All
**[Move&#8209;PnPFile](../../module/sharepoint-pnp/MovePnPFile.md)** |Moves a file to a different location|All
**[Remove&#8209;PnPFile](../../module/sharepoint-pnp/RemovePnPFile.md)** |Removes a file.|All
**[Rename&#8209;PnPFile](../../module/sharepoint-pnp/RenamePnPFile.md)** |Renames a file in its current location|All
**[Set&#8209;PnPFileCheckedIn](../../module/sharepoint-pnp/SetPnPFileCheckedIn.md)** |Checks in a file|All
**[Set&#8209;PnPFileCheckedOut](../../module/sharepoint-pnp/SetPnPFileCheckedOut.md)** |Checks out a file|All
**[Add&#8209;PnPFolder](../../module/sharepoint-pnp/AddPnPFolder.md)** |Creates a folder within a parent folder|All
**[Ensure&#8209;PnPFolder](../../module/sharepoint-pnp/EnsurePnPFolder.md)** |Returns a folder from a given site relative path, and will create it if it does not exist.|All
**[Get&#8209;PnPFolder](../../module/sharepoint-pnp/GetPnPFolder.md)** |Return a folder object|All
**[Move&#8209;PnPFolder](../../module/sharepoint-pnp/MovePnPFolder.md)** |Move a folder to another location in the current web|All
**[Remove&#8209;PnPFolder](../../module/sharepoint-pnp/RemovePnPFolder.md)** |Deletes a folder within a parent folder|All
**[Rename&#8209;PnPFolder](../../module/sharepoint-pnp/RenamePnPFolder.md)** |Renames a folder|All
**[Get&#8209;PnPFolderItem](../../module/sharepoint-pnp/GetPnPFolderItem.md)** |List content in folder|All
**[Copy&#8209;PnPItemProxy](../../module/sharepoint-pnp/CopyPnPItemProxy.md)** |Proxy cmdlet for using Copy-Item between SharePoint provider and FileSystem provider|All
**[Move&#8209;PnPItemProxy](../../module/sharepoint-pnp/MovePnPItemProxy.md)** |Proxy cmdlet for using Move-Item between SharePoint provider and FileSystem provider|All


### Information Management 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Get&#8209;PnPSiteClosure](../../module/sharepoint-pnp/GetPnPSiteClosure.md)** |Get the site closure status of the site which has a site policy applied|All
**[Set&#8209;PnPSiteClosure](../../module/sharepoint-pnp/SetPnPSiteClosure.md)** |Opens or closes a site which has a site policy applied|All
**[Set&#8209;PnPSitePolicy](../../module/sharepoint-pnp/SetPnPSitePolicy.md)** |Sets a site policy|All
**[Get&#8209;PnPSitePolicy](../../module/sharepoint-pnp/GetPnPSitePolicy.md)** |Retrieves all or a specific site policy|All


### Lists 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Get&#8209;PnPDefaultColumnValues](../../module/sharepoint-pnp/GetPnPDefaultColumnValues.md)** |Gets the default column values for all folders in document library|All
**[Set&#8209;PnPDefaultColumnValues](../../module/sharepoint-pnp/SetPnPDefaultColumnValues.md)** |Sets default column values for a document library|All
**[Get&#8209;PnPList](../../module/sharepoint-pnp/GetPnPList.md)** |Returns a List object|All
**[New&#8209;PnPList](../../module/sharepoint-pnp/NewPnPList.md)** |Creates a new list|All
**[Remove&#8209;PnPList](../../module/sharepoint-pnp/RemovePnPList.md)** |Deletes a list|All
**[Set&#8209;PnPList](../../module/sharepoint-pnp/SetPnPList.md)** |Updates list settings|All
**[Add&#8209;PnPListItem](../../module/sharepoint-pnp/AddPnPListItem.md)** |Adds an item to a list|All
**[Get&#8209;PnPListItem](../../module/sharepoint-pnp/GetPnPListItem.md)** |Retrieves list items|All
**[Remove&#8209;PnPListItem](../../module/sharepoint-pnp/RemovePnPListItem.md)** |Deletes an item from a list|All
**[Set&#8209;PnPListItem](../../module/sharepoint-pnp/SetPnPListItem.md)** |Updates a list item|All
**[Set&#8209;PnPListItemPermission](../../module/sharepoint-pnp/SetPnPListItemPermission.md)** |Sets list item permissions|All
**[Move&#8209;PnPListItemToRecycleBin](../../module/sharepoint-pnp/MovePnPListItemToRecycleBin.md)** |Moves an item from a list to the Recycle Bin|All
**[Set&#8209;PnPListPermission](../../module/sharepoint-pnp/SetPnPListPermission.md)** |Sets list permissions|All
**[Get&#8209;PnPProvisioningTemplateFromGallery](../../module/sharepoint-pnp/GetPnPProvisioningTemplateFromGallery.md)** |Retrieves or searches provisioning templates from the PnP Template Gallery|All
**[Request&#8209;PnPReIndexList](../../module/sharepoint-pnp/RequestPnPReIndexList.md)** |Marks the list for full indexing during the next incremental crawl|All
**[Add&#8209;PnPView](../../module/sharepoint-pnp/AddPnPView.md)** |Adds a view to a list|All
**[Get&#8209;PnPView](../../module/sharepoint-pnp/GetPnPView.md)** |Returns one or all views from a list|All
**[Remove&#8209;PnPView](../../module/sharepoint-pnp/RemovePnPView.md)** |Deletes a view from a list|All


### Microsoft Graph 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Connect&#8209;PnPMicrosoftGraph](../../module/sharepoint-pnp/ConnectPnPMicrosoftGraph.md)** |Uses the Microsoft Authentication Library (Preview) to connect to Azure AD and to get an OAuth 2.0 Access Token to consume the Microsoft Graph API|All
**[Get&#8209;PnPUnifiedGroup](../../module/sharepoint-pnp/GetPnPUnifiedGroup.md)** |Gets one Office 365 Group (aka Unified Group) or a list of Office 365 Groups|All
**[New&#8209;PnPUnifiedGroup](../../module/sharepoint-pnp/NewPnPUnifiedGroup.md)** |Creates a new Office 365 Group (aka Unified Group)|All
**[Remove&#8209;PnPUnifiedGroup](../../module/sharepoint-pnp/RemovePnPUnifiedGroup.md)** |Removes one Office 365 Group (aka Unified Group) or a list of Office 365 Groups|All
**[Set&#8209;PnPUnifiedGroup](../../module/sharepoint-pnp/SetPnPUnifiedGroup.md)** |Sets Office 365 Group (aka Unified Group) properties|All


### Provisioning 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Add&#8209;PnPDataRowsToProvisioningTemplate](../../module/sharepoint-pnp/AddPnPDataRowsToProvisioningTemplate.md)** |Adds datarows to a list inside a PnP Provisioning Template|All
**[Remove&#8209;PnPFileFromProvisioningTemplate](../../module/sharepoint-pnp/RemovePnPFileFromProvisioningTemplate.md)** |Removes a file from a PnP Provisioning Template|All
**[Add&#8209;PnPFileToProvisioningTemplate](../../module/sharepoint-pnp/AddPnPFileToProvisioningTemplate.md)** |Adds a file to a PnP Provisioning Template|All
**[Convert&#8209;PnPFolderToProvisioningTemplate](ConvertPnPFolderToProvisioningTemplate.md)** |Creates a pnp package file of an existing template xml, and includes all files in the current folder|All
**[Add&#8209;PnPListFoldersToProvisioningTemplate](../../module/sharepoint-pnp/AddPnPListFoldersToProvisioningTemplate.md)** |Adds folders to a list in a PnP Provisioning Template|All
**[Apply&#8209;PnPProvisioningTemplate](ApplyPnPProvisioningTemplate.md)** |Applies a provisioning template to a web|All
**[Convert&#8209;PnPProvisioningTemplate](ConvertPnPProvisioningTemplate.md)** |Converts a provisioning template to an other schema version|All
**[Get&#8209;PnPProvisioningTemplate](../../module/sharepoint-pnp/GetPnPProvisioningTemplate.md)** |Generates a provisioning template from a web|All
**[Load&#8209;PnPProvisioningTemplate](LoadPnPProvisioningTemplate.md)** |Loads a PnP file from the file systems|All
**[New&#8209;PnPProvisioningTemplate](../../module/sharepoint-pnp/NewPnPProvisioningTemplate.md)** |Creates a new provisioning template object|All
**[Save&#8209;PnPProvisioningTemplate](SavePnPProvisioningTemplate.md)** |Saves a PnP file to the file systems|All
**[New&#8209;PnPProvisioningTemplateFromFolder](../../module/sharepoint-pnp/NewPnPProvisioningTemplateFromFolder.md)** |Generates a provisioning template from a given folder, including only files that are present in that folder|All
**[Set&#8209;PnPProvisioningTemplateMetadata](../../module/sharepoint-pnp/SetPnPProvisioningTemplateMetadata.md)** |Sets metadata of a provisioning template|All


### Publishing 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Set&#8209;PnPAvailablePageLayouts](../../module/sharepoint-pnp/SetPnPAvailablePageLayouts.md)** |Sets the available page layouts for the current site|All
**[Set&#8209;PnPDefaultPageLayout](../../module/sharepoint-pnp/SetPnPDefaultPageLayout.md)** |Sets a specific page layout to be the default page layout for a publishing site|All
**[Add&#8209;PnPHtmlPublishingPageLayout](../../module/sharepoint-pnp/AddPnPHtmlPublishingPageLayout.md)** |Adds a HTML based publishing page layout|All
**[Add&#8209;PnPMasterPage](../../module/sharepoint-pnp/AddPnPMasterPage.md)** |Adds a Masterpage|All
**[Add&#8209;PnPPublishingImageRendition](../../module/sharepoint-pnp/AddPnPPublishingImageRendition.md)** |Adds an Image Rendition if the Name of the Image Rendition does not already exist. This prevents creating two Image Renditions that share the same name.|All
**[Get&#8209;PnPPublishingImageRendition](../../module/sharepoint-pnp/GetPnPPublishingImageRendition.md)** |Returns all image renditions or if Identity is specified a specific one|All
**[Remove&#8209;PnPPublishingImageRendition](../../module/sharepoint-pnp/RemovePnPPublishingImageRendition.md)** |Removes an existing image rendition|All
**[Add&#8209;PnPPublishingPage](../../module/sharepoint-pnp/AddPnPPublishingPage.md)** |Adds a publishing page|All
**[Add&#8209;PnPPublishingPageLayout](../../module/sharepoint-pnp/AddPnPPublishingPageLayout.md)** |Adds a publishing page layout|All
**[Add&#8209;PnPWikiPage](../../module/sharepoint-pnp/AddPnPWikiPage.md)** |Adds a wiki page|All
**[Remove&#8209;PnPWikiPage](../../module/sharepoint-pnp/RemovePnPWikiPage.md)** |Removes a wiki page|All
**[Get&#8209;PnPWikiPageContent](../../module/sharepoint-pnp/GetPnPWikiPageContent.md)** |Gets the contents/source of a wiki page|All
**[Set&#8209;PnPWikiPageContent](../../module/sharepoint-pnp/SetPnPWikiPageContent.md)** |Sets the contents of a wikipage|All


### Records Management 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Set&#8209;PnPInPlaceRecordsManagement](../../module/sharepoint-pnp/SetPnPInPlaceRecordsManagement.md)** |Activates or deactivates in place records management|SharePoint Online
**[Clear&#8209;PnPListItemAsRecord](../../module/sharepoint-pnp/ClearPnPListItemAsRecord.md)** |Undeclares a list item as a record|SharePoint Online
**[Set&#8209;PnPListItemAsRecord](../../module/sharepoint-pnp/SetPnPListItemAsRecord.md)** |Declares a list item as a record|SharePoint Online
**[Test&#8209;PnPListItemIsRecord](../../module/sharepoint-pnp/TestPnPListItemIsRecord.md)** |Checks if a list item is a record|SharePoint Online


### Search 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Get&#8209;PnPSearchConfiguration](../../module/sharepoint-pnp/GetPnPSearchConfiguration.md)** |Returns the search configuration|All
**[Set&#8209;PnPSearchConfiguration](../../module/sharepoint-pnp/SetPnPSearchConfiguration.md)** |Sets the search configuration|All
**[Submit&#8209;PnPSearchQuery](../../module/sharepoint-pnp/SubmitPnPSearchQuery.md)** |Executes an arbitrary search query against the SharePoint search index|All
**[Get&#8209;PnPSiteSearchQueryResults](../../module/sharepoint-pnp/GetPnPSiteSearchQueryResults.md)** |Executes a search query to retrieve indexed site collections|All


### SharePoint Recycle Bin 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Clear&#8209;PnpRecycleBinItem](../../module/sharepoint-pnp/ClearPnpRecycleBinItem.md)** |Permanently deletes all or a specific recycle bin item|All
**[Move&#8209;PnpRecycleBinItem](../../module/sharepoint-pnp/MovePnpRecycleBinItem.md)** |Moves all items or a specific item in the first stage recycle bin of the current site collection to the second stage recycle bin|SharePoint Online
**[Restore&#8209;PnpRecycleBinItem](../../module/sharepoint-pnp/RestorePnpRecycleBinItem.md)** |Restores the provided recycle bin item to its original location|All
**[Get&#8209;PnPRecycleBinItem](../../module/sharepoint-pnp/GetPnPRecycleBinItem.md)** |Returns the items in the recycle bin from the context|All
**[Get&#8209;PnPTenantRecycleBinItem](../../module/sharepoint-pnp/GetPnPTenantRecycleBinItem.md)** |Returns the items in the tenant scoped recycle bin|SharePoint Online


### SharePoint WebHooks 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Add&#8209;PnPWebhookSubscription](../../module/sharepoint-pnp/AddPnPWebhookSubscription.md)** |Adds a new Webhook subscription|SharePoint Online
**[Remove&#8209;PnPWebhookSubscription](../../module/sharepoint-pnp/RemovePnPWebhookSubscription.md)** |Removes a Webhook subscription from the resource|SharePoint Online
**[Set&#8209;PnPWebhookSubscription](../../module/sharepoint-pnp/SetPnPWebhookSubscription.md)** |Removes a Webhook subscription from the resource|SharePoint Online
**[Get&#8209;PnPWebhookSubscriptions](../../module/sharepoint-pnp/GetPnPWebhookSubscriptions.md)** |Gets all the Webhook subscriptions of the resource|SharePoint Online


### Sites 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Set&#8209;PnPAppSideLoading](../../module/sharepoint-pnp/SetPnPAppSideLoading.md)** |Enables the App SideLoading Feature on a site|All
**[Get&#8209;PnPAuditing](../../module/sharepoint-pnp/GetPnPAuditing.md)** |Get the Auditing setting of a site|All
**[Set&#8209;PnPAuditing](../../module/sharepoint-pnp/SetPnPAuditing.md)** |Set Auditing setting for a site|All
**[Get&#8209;PnPSite](../../module/sharepoint-pnp/GetPnPSite.md)** |Returns the current site collection from the context.|All
**[Add&#8209;PnPSiteCollectionAdmin](../../module/sharepoint-pnp/AddPnPSiteCollectionAdmin.md)** |Adds one or more users as site collection administrators to the site collection in the current context|All
**[Get&#8209;PnPSiteCollectionAdmin](../../module/sharepoint-pnp/GetPnPSiteCollectionAdmin.md)** |Returns the current site collection administrators of the site colleciton in the current context|All
**[Remove&#8209;PnPSiteCollectionAdmin](../../module/sharepoint-pnp/RemovePnPSiteCollectionAdmin.md)** |Removes one or more users as site collection administrators from the site collection in the current context|All
**[Install&#8209;PnPSolution](../../module/sharepoint-pnp/InstallPnPSolution.md)** |Installs a sandboxed solution to a site collection. WARNING! This method can delete your composed look gallery due to the method used to activate the solution. We recommend you to only to use this cmdlet if you are okay with that.|All
**[Uninstall&#8209;PnPSolution](../../module/sharepoint-pnp/UninstallPnPSolution.md)** |Uninstalls a sandboxed solution from a site collection|All


### Taxonomy 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Get&#8209;PnPSiteCollectionTermStore](../../module/sharepoint-pnp/GetPnPSiteCollectionTermStore.md)** |Returns the site collection term store|All
**[Export&#8209;PnPTaxonomy](../../module/sharepoint-pnp/ExportPnPTaxonomy.md)** |Exports a taxonomy to either the output or to a file.|All
**[Import&#8209;PnPTaxonomy](../../module/sharepoint-pnp/ImportPnPTaxonomy.md)** |Imports a taxonomy from either a string array or a file|All
**[Set&#8209;PnPTaxonomyFieldValue](../../module/sharepoint-pnp/SetPnPTaxonomyFieldValue.md)** |Sets a taxonomy term value in a listitem field|All
**[Get&#8209;PnPTaxonomyItem](../../module/sharepoint-pnp/GetPnPTaxonomyItem.md)** |Returns a taxonomy item|All
**[Remove&#8209;PnPTaxonomyItem](../../module/sharepoint-pnp/RemovePnPTaxonomyItem.md)** |Removes a taxonomy item|All
**[Get&#8209;PnPTaxonomySession](../../module/sharepoint-pnp/GetPnPTaxonomySession.md)** |Returns a taxonomy session|All
**[Get&#8209;PnPTerm](../../module/sharepoint-pnp/GetPnPTerm.md)** |Returns a taxonomy term|All
**[New&#8209;PnPTerm](../../module/sharepoint-pnp/NewPnPTerm.md)** |Creates a taxonomy term|All
**[Get&#8209;PnPTermGroup](../../module/sharepoint-pnp/GetPnPTermGroup.md)** |Returns a taxonomy term group|All
**[New&#8209;PnPTermGroup](../../module/sharepoint-pnp/NewPnPTermGroup.md)** |Creates a taxonomy term group|All
**[Remove&#8209;PnPTermGroup](../../module/sharepoint-pnp/RemovePnPTermGroup.md)** |Removes a taxonomy term group and all its containing termsets|All
**[Import&#8209;PnPTermGroupFromXml](../../module/sharepoint-pnp/ImportPnPTermGroupFromXml.md)** |Imports a taxonomy TermGroup from either the input or from an XML file.|All
**[Export&#8209;PnPTermGroupToXml](../../module/sharepoint-pnp/ExportPnPTermGroupToXml.md)** |Exports a taxonomy TermGroup to either the output or to an XML file.|All
**[Get&#8209;PnPTermSet](../../module/sharepoint-pnp/GetPnPTermSet.md)** |Returns a taxonomy term set|All
**[Import&#8209;PnPTermSet](../../module/sharepoint-pnp/ImportPnPTermSet.md)** |Imports a taxonomy term set from a file in the standard format.|All
**[New&#8209;PnPTermSet](../../module/sharepoint-pnp/NewPnPTermSet.md)** |Creates a taxonomy term set|All


### Tenant Administration 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Get&#8209;PnPAccessToken](../../module/sharepoint-pnp/GetPnPAccessToken.md)** |Gets the OAuth 2.0 Access Token to consume the Microsoft Graph API|All
**[Clear&#8209;PnPTenantRecycleBinItem](../../module/sharepoint-pnp/ClearPnPTenantRecycleBinItem.md)** |Permanently deletes a site collection from the tenant scoped recycle bin|All
**[Restore&#8209;PnPTenantRecycleBinItem](../../module/sharepoint-pnp/RestorePnPTenantRecycleBinItem.md)** |Restores a site collection from the tenant scoped recycle bin|SharePoint Online
**[Get&#8209;PnPTenantSite](../../module/sharepoint-pnp/GetPnPTenantSite.md)** |Uses the tenant API to retrieve site information.|SharePoint Online
**[New&#8209;PnPTenantSite](../../module/sharepoint-pnp/NewPnPTenantSite.md)** |Creates a new site collection for the current tenant|All
**[Remove&#8209;PnPTenantSite](../../module/sharepoint-pnp/RemovePnPTenantSite.md)** |Removes a site collection from the current tenant|SharePoint Online
**[Set&#8209;PnPTenantSite](../../module/sharepoint-pnp/SetPnPTenantSite.md)** |Uses the tenant API to set site information.|SharePoint Online
**[Get&#8209;PnPTimeZoneId](../../module/sharepoint-pnp/GetPnPTimeZoneId.md)** |Returns a time zone ID|All
**[Get&#8209;PnPWebTemplates](../../module/sharepoint-pnp/GetPnPWebTemplates.md)** |Returns the available web templates.|SharePoint Online


### User and group management 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Get&#8209;PnPGroup](../../module/sharepoint-pnp/GetPnPGroup.md)** |Returns a specific group or all groups.|All
**[New&#8209;PnPGroup](../../module/sharepoint-pnp/NewPnPGroup.md)** |Adds group to the Site Groups List and returns a group object|All
**[Remove&#8209;PnPGroup](../../module/sharepoint-pnp/RemovePnPGroup.md)** |Removes a group from a web.|All
**[Set&#8209;PnPGroup](../../module/sharepoint-pnp/SetPnPGroup.md)** |Updates a group|All
**[Get&#8209;PnPGroupPermissions](../../module/sharepoint-pnp/GetPnPGroupPermissions.md)** |Returns the permissions for a specific SharePoint group|All
**[Set&#8209;PnPGroupPermissions](../../module/sharepoint-pnp/SetPnPGroupPermissions.md)** |Adds and/or removes permissions of a specific SharePoint group|All
**[Get&#8209;PnPUser](../../module/sharepoint-pnp/GetPnPUser.md)** |Returns site users of current web|All
**[New&#8209;PnPUser](../../module/sharepoint-pnp/NewPnPUser.md)** |Adds a user to the built-in Site User Info List and returns a user object|All
**[Remove&#8209;PnPUser](../../module/sharepoint-pnp/RemovePnPUser.md)** |Removes a specific user from the site collection User Information List|All
**[Remove&#8209;PnPUserFromGroup](../../module/sharepoint-pnp/RemovePnPUserFromGroup.md)** |Removes a user from a group|All
**[Add&#8209;PnPUserToGroup](../../module/sharepoint-pnp/AddPnPUserToGroup.md)** |Adds a user to a group|All


### User Profiles 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[New&#8209;PnPPersonalSite](../../module/sharepoint-pnp/NewPnPPersonalSite.md)** |Office365 only: Creates a personal / OneDrive For Business site|SharePoint Online
**[Get&#8209;PnPUserProfileProperty](../../module/sharepoint-pnp/GetPnPUserProfileProperty.md)** |You must connect to the tenant admin website (https://:<tenant>-admin.sharepoint.com) with Connect-PnPOnline in order to use this cmdlet.  |All
**[Set&#8209;PnPUserProfileProperty](../../module/sharepoint-pnp/SetPnPUserProfileProperty.md)** |Office365 only: Uses the tenant API to retrieve site information.  You must connect to the tenant admin website (https://:<tenant>-admin.sharepoint.com) with Connect-PnPOnline in order to use this command.  |SharePoint Online


### Utilities 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Send&#8209;PnPMail](../../module/sharepoint-pnp/SendPnPMail.md)** |Sends an email using the Office 365 SMTP Service or SharePoint, depending on the parameters specified. See detailed help for more information.|All


### Web Parts 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Get&#8209;PnPWebPart](../../module/sharepoint-pnp/GetPnPWebPart.md)** |Returns a webpart definition object|All
**[Remove&#8209;PnPWebPart](../../module/sharepoint-pnp/RemovePnPWebPart.md)** |Removes a webpart from a page|All
**[Get&#8209;PnPWebPartProperty](../../module/sharepoint-pnp/GetPnPWebPartProperty.md)** |Returns a web part property|All
**[Set&#8209;PnPWebPartProperty](../../module/sharepoint-pnp/SetPnPWebPartProperty.md)** |Sets a web part property|All
**[Add&#8209;PnPWebPartToWebPartPage](../../module/sharepoint-pnp/AddPnPWebPartToWebPartPage.md)** |Adds a webpart to a web part page in a specified zone|All
**[Add&#8209;PnPWebPartToWikiPage](../../module/sharepoint-pnp/AddPnPWebPartToWikiPage.md)** |Adds a webpart to a wiki page in a specified table row and column|All
**[Get&#8209;PnPWebPartXml](../../module/sharepoint-pnp/GetPnPWebPartXml.md)** |Returns the webpart XML of a webpart registered on a site|All


### Webs 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Set&#8209;PnPIndexedProperties](../../module/sharepoint-pnp/SetPnPIndexedProperties.md)** |Marks values of the propertybag to be indexed by search. Notice that this will overwrite the existing flags, i.e. only the properties you define with the cmdlet will be indexed.|All
**[Add&#8209;PnPIndexedProperty](../../module/sharepoint-pnp/AddPnPIndexedProperty.md)** |Marks the value of the propertybag key specified to be indexed by search.|All
**[Remove&#8209;PnPIndexedProperty](../../module/sharepoint-pnp/RemovePnPIndexedProperty.md)** |Removes a key from propertybag to be indexed by search. The key and it's value remain in the propertybag, however it will not be indexed anymore.|All
**[Get&#8209;PnPIndexedPropertyKeys](../../module/sharepoint-pnp/GetPnPIndexedPropertyKeys.md)** |Returns the keys of the property bag values that have been marked for indexing by search|All
**[Get&#8209;PnPPropertyBag](../../module/sharepoint-pnp/GetPnPPropertyBag.md)** |Returns the property bag values.|All
**[Remove&#8209;PnPPropertyBagValue](../../module/sharepoint-pnp/RemovePnPPropertyBagValue.md)** |Removes a value from the property bag|All
**[Set&#8209;PnPPropertyBagValue](../../module/sharepoint-pnp/SetPnPPropertyBagValue.md)** |Sets a property bag value|All
**[Request&#8209;PnPReIndexWeb](../../module/sharepoint-pnp/RequestPnPReIndexWeb.md)** |Marks the web for full indexing during the next incremental crawl|All
**[Get&#8209;PnPRequestAccessEmails](../../module/sharepoint-pnp/GetPnPRequestAccessEmails.md)** |Returns the request access e-mail addresses|SharePoint Online
**[Set&#8209;PnPRequestAccessEmails](../../module/sharepoint-pnp/SetPnPRequestAccessEmails.md)** |Sets Request Access Emails on a web|SharePoint Online
**[Get&#8209;PnPSubWebs](../../module/sharepoint-pnp/GetPnPSubWebs.md)** |Returns the subwebs of the current web|All
**[Get&#8209;PnPWeb](../../module/sharepoint-pnp/GetPnPWeb.md)** |Returns the current web object|All
**[New&#8209;PnPWeb](../../module/sharepoint-pnp/NewPnPWeb.md)** |Creates a new subweb under the current web|All
**[Remove&#8209;PnPWeb](../../module/sharepoint-pnp/RemovePnPWeb.md)** |Removes a subweb in the current web|All
**[Set&#8209;PnPWeb](../../module/sharepoint-pnp/SetPnPWeb.md)** |Sets properties on a web|All
**[Invoke&#8209;PnPWebAction](../../module/sharepoint-pnp/InvokePnPWebAction.md)** |Executes operations on web, lists and list items.|All
**[Set&#8209;PnPWebPermission](../../module/sharepoint-pnp/SetPnPWebPermission.md)** |Sets web permissions|All


### Workflows 
Cmdlet|Description|Platform
:-----|:----------|:-------
**[Add&#8209;PnPWorkflowDefinition](../../module/sharepoint-pnp/AddPnPWorkflowDefinition.md)** |Adds a workflow definition|All
**[Get&#8209;PnPWorkflowDefinition](../../module/sharepoint-pnp/GetPnPWorkflowDefinition.md)** |Returns a workflow definition|All
**[Remove&#8209;PnPWorkflowDefinition](../../module/sharepoint-pnp/RemovePnPWorkflowDefinition.md)** |Removes a workflow definition|All
**[Resume&#8209;PnPWorkflowInstance](../../module/sharepoint-pnp/ResumePnPWorkflowInstance.md)** |Resumes a previously stopped workflow instance|All
**[Stop&#8209;PnPWorkflowInstance](../../module/sharepoint-pnp/StopPnPWorkflowInstance.md)** |Stops a workflow instance|All
**[Add&#8209;PnPWorkflowSubscription](../../module/sharepoint-pnp/AddPnPWorkflowSubscription.md)** |Adds a workflow subscription to a list|All
**[Get&#8209;PnPWorkflowSubscription](../../module/sharepoint-pnp/GetPnPWorkflowSubscription.md)** |Returns a workflow subscriptions from a list|All
**[Remove&#8209;PnPWorkflowSubscription](../../module/sharepoint-pnp/RemovePnPWorkflowSubscription.md)** |Removes a workflow subscription|All


## Additional resources
<a name="bk_addresources"> </a>

-  [SharePoint PnP PowerShell on GitHub](https://github.com/SharePoint/PnP-PowerShell)
