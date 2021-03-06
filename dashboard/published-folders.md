---
description: Serve files from PowerShell Universal
---

# Published Folders

Published folders allow you to share a local folder through your Universal website. Any file within the published folder will be accessible via a web request. This can be helpful for storing images or other files that you may want to provide via your Universal Dashboard.

## Publishing a Folder

From the `Dashboard / Published Folders` page, you can click Add Published Folder. You will need to enter the local path as well as the request path. The local path is the folder that you wish to publish. The request path is the path that the end user will request to download the files from the folder.

You can choose to turn on authentication and authorization for the folder.

![](https://github.com/ironmansoftware/universal-docs/tree/f9bbd5b16eec8502456cad78419a36af3172a317/.gitbook/assets/image%20%2899%29%20%281%29.png)

Once the folder has been published, it will be listed in the published folders table.

![](../.gitbook/assets/image%20%28100%29.png)

## Download Files

You can now download files that are found in the published folder by visit the request path. In the example above, I could visit the following URL to download the test.txt file.

```http
http://localhost:5000/src/test.txt
```

You'll notice that unauthenticated requests will not be able to access the file.

```text
PS C:\src\universal\src> invoke-webrequest http://localhost:5000/src/test.txt
Invoke-WebRequest: Response status code does not indicate success: 401 (Unauthorized).
```

## Default Documents

Default documents allow you to load files when a user specifies the folder and not the document within a folder. This can be handy when a user visits `/docs` but does not specify `/docs/index.html`. Instead of returning a 404, you can return the `index.html` when the user specifies `/docs`.

To configure default documents, set the `-DefaultDocument` parameter on `New-PSUPublishedFolder`.

```text
New-PSUPublishedFolder -Path C:\website -RequestPath /docs -DefaultDocument @("index.hml")
```

## API 

### New-PSUPublishedFolder

Create a published folder. Can be used in the `publishedFolders.ps1` file or via the management REST API.

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| RequestPath | string | The relative path to server documents from. | true |
| Path | string | The absolute file system path to server files from. | true |
| Authentication | Switch | Whether authentication is required to access this folder. | false |
| Role | string\[\] | Roles that can access this folder. Leave blank for any role. | false |
| DefaultDocument | string\[\] | Default documents to server with out specifying the file name. | false |
| ComputerName | string | The URL to the PSU management API.  | false |
| AppToken | string | The AppToken used to access the PSU management API | false |
| UseDefaultCredentials | Switch | Whether to use the current user's credentials to access the PSU management API | false |

