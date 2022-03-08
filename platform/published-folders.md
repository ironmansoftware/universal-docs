---
description: Serve files from PowerShell Universal
---

# Published Folders

Published folders allow you to share a local folder through your Universal website. Any file within the published folder will be accessible via a web request. This can be helpful for storing images or other files that you may want to provide via your Universal Dashboard.

## Publishing a Folder

From the `Dashboard / Published Folders` page, you can click Add Published Folder. You will need to enter the local path as well as the request path. The local path is the folder that you wish to publish. The request path is the path that the end user will request to download the files from the folder.

You can choose to turn on authentication and authorization for the folder.

![](<../.gitbook/assets/image (388).png>)

Once the folder has been published, it will be listed in the published folders table.

![](<../.gitbook/assets/image (96).png>)

## Download Files

You can now download files that are found in the published folder by visit the request path. In the example above, I could visit the following URL to download the test.txt file.

```http
http://localhost:5000/src/test.txt
```

You'll notice that unauthenticated requests will not be able to access the file.

```powershell
PS C:\src\universal\src> invoke-webrequest http://localhost:5000/src/test.txt
Invoke-WebRequest: Response status code does not indicate success: 401 (Unauthorized).
```

## Default Documents

Default documents allow you to load files when a user specifies the folder and not the document within a folder. This can be handy when a user visits `/docs` but does not specify `/docs/index.html`. Instead of returning a 404, you can return the `index.html` when the user specifies `/docs`.

To configure default documents, set the `-DefaultDocument` parameter on `New-PSUPublishedFolder`.

```powershell
New-PSUPublishedFolder -Path C:\website -RequestPath /docs -DefaultDocument @("index.hml")
```

## Impersonation

{% hint style="warning" %}
Impersonation only works when using [Windows authentication](../api/security.md#authenticating-with-windows-authentication).
{% endhint %}

By default, when PSU accesses files when serving them to users, it will do so as the service account the process is running as. If you wish to access files as the user that is downloading the file, you can turn on impersonation.&#x20;

```powershell
New-PSUPublishedFolder -Path C:\website -RequestPath /docs -DefaultDocument @("index.hml") -Impersonation
```

## API&#x20;

* [New-PSUPublishedFolder](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSUPublishedFolder.txt)

