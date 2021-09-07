---
description: Git integration for PowerShell Universal.
---

# Git

PowerShell Universal is capable of synchronizing the configuration scripts with a remote git repository. You can use the [Configuration settings](settings.md) to setup git sync.

## Git Status Page

{% hint style="warning" %}
This feature will be available in PowerShell Universal 2.3. 
{% endhint %}

The git status page lists the synchronized repository, branch and the list of commits that have occurred. 

![](../.gitbook/assets/image%20%28274%29.png)

## Git Synchronization Behavior

### Two-Way

By default, git synchronization will work both ways. If you make changes within the PSU admin console, those changes will be committed and sync'd to the configured remote.

Any changes that are made in the remote will be pulled locally.

If you setup git sync with a preexisting git remote, the changes will be pulled and synchronized locally. You cannot have any changes locally.

If you setup git sync with a bare repository, the local changes will be sync'd and the repository will be initialized.

### One-Way

You can adjust the git synchronization behavior by changing the `GitSyncBehavior` setting in `appsettings.json`. When set to `OneWay`, the admin console and management API will become read-only. The PowerShell Universal system will pull from the remote but will never push or commit locally.

```javascript
    "Data": {
    "RepositoryPath": "%ProgramData%\\UniversalAutomation\\Repository",
    "ConnectionString": "%ProgramData%\\UniversalAutomation\\database.db",
    "DatabaseType": "LiteDB",
    "GitRemote": "https://github.com/myorg/myrepo.git",
    "GitUserName": "any",
    "GitPassword": "MYPAT----------------"
    "GitBranch": "dev",
    "GitSyncBehavior": "OneWay",
    "ConfigurationScript": ""
  },
```

## Personal Access Token

We recommend that you use a personal access token \(PAT\) over a user name and password. You can configure a personal access token by setting the password property in the `appsettings.json` or other configuration methods.

```javascript
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

```javascript
    "Data": {
    "RepositoryPath": "%ProgramData%\\UniversalAutomation\\Repository",
    "ConnectionString": "%ProgramData%\\UniversalAutomation\\database.db",
    "GitRemote": "https://github.com/myorg/myrepo.git",
    "GitUserName": "myusername",
    "GitPassword": "mypassword"
  },
```

