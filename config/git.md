---
description: Git integration for PowerShell Universal.
---

# Git

PowerShell Universal is capable of synchronizing the configuration scripts with a remote git repository. You can use the [Configuration settings](settings.md) to setup git sync. 

## Git Synchronization Behavior

Git sync will automatically push and pull changes between the default remote branch. Universal currently does not support multiple branches. 

If you setup git sync with a preexisting git remote, the changes will be pulled and synchronized locally. You cannot have any changes locally.

If you setup git sync with a bare repository, the local changes will be sync'd and the repository will be initialized. 

## Personal Access Token

We recommend that you use a personal access token \(PAT\) over a user name and password. You can configure a personal access token by setting the password property in the `appsettings.json` or other configuration methods. 

```text
  "Data": {
    "RepositoryPath": "%ProgramData%\\UniversalAutomation\\Repository",
    "ConnectionString": "%ProgramData%\\UniversalAutomation\\database.db",
    "GitRemote": "https://github.com/myorg/myrepo.git",
    "GitUserName": "any",
    "GitPassword": "MYPAT----------------"
  },
```

## User name and password

You can also configure a git remote to authenticate with a user name and password. Set the user name and password either with the `appsettings.json` file or another configuration method. 

```text
  "Data": {
    "RepositoryPath": "%ProgramData%\\UniversalAutomation\\Repository",
    "ConnectionString": "%ProgramData%\\UniversalAutomation\\database.db",
    "GitRemote": "https://github.com/myorg/myrepo.git",
    "GitUserName": "myusername",
    "GitPassword": "mypassword"
  },
```

