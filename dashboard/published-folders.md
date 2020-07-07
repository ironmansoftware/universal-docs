---
description: Serve files from PowerShell Universal
---

# Published Folders

{% hint style="info" %}
This section covers a pre-release version of Universal. You can download nightly builds from our [Downloads page](https://ironmansoftware.com/downloads).
{% endhint %}

Published folders allow you to share a local folder through your Universal website. Any file within the published folder will be accessible via a web request. This can be helpful for storing images or other files that you may want to provide via your Universal Dashboard.

## Publishing a Folder

From the `Dashboard / Published Folders` page, you can click Add Published Folder. You will need to enter the local path as well as the request path. The local path is the folder that you wish to publish. The request path is the path that the end user will request to download the files from the folder. 

You can choose to turn on authentication and authorization for the folder. 

![](../.gitbook/assets/image%20%28101%29.png)

Once the folder has been published, it will be listed in the published folders table. 

![](../.gitbook/assets/image%20%28100%29.png)

## Download Files

You can now download files that are found in the published folder by visit the request path. In the example above, I could visit the following URL to download the test.txt file. 

```text
http://localhost:5000/src/test.txt
```

You'll notice that unauthenticated requests will not be able to access the file. 

```text
PS C:\src\universal\src> invoke-webrequest http://localhost:5000/src/test.txt
Invoke-WebRequest: Response status code does not indicate success: 401 (Unauthorized).
```

