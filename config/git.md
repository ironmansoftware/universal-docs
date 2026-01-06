---
description: Git integration for PowerShell Universal.
---

# Git

{% hint style="info" %}
Git integration requires a [license](https://ironmansoftware.com/pricing/powershell-universal).
{% endhint %}

PowerShell Universal is capable of synchronizing the configuration scripts with a remote git repository.

## Configuration

### Admin Console

Git sync can be configured in the database by adjusting the settings within the admin console. This is the preferred approach. The benefit is that when you connect new instances of PowerShell Universal to your SQL instance, you will not need to configure git sync again.

To configure git sync, navigate to Settings \ Git within the Admin Console. You will be able to click the Create Git Settings button.

<figure><img src="../.gitbook/assets/image (250).png" alt=""><figcaption><p>Git Settings Dialog</p></figcaption></figure>

{% hint style="info" %}
In PowerShell Universal 5.x and later, Git credentials (Remote URL, Username, and Personal Access Token) are stored in the SQL database rather than in appsettings.json. Editing these settings in the UI will update the database. If you edit Git settings and then click OK, PSU may clear stored credentials even if the fields appear populated. In multi-node environments, you must re-enter credentials on each node individually after making changes.
{% endhint %}

### appsettings.json

You can also use the [Configuration settings](settings.md) to setup git sync. This is useful if you have a single instance of PSU and would like to back up your appsettings.json file. Adjusting settings within the admin console will not update the appsettings.json file. You will need to do so manually and restart PowerShell Universal after changing the settings.

If git sync settings are specified in the database, settings defined in appsettings.json are ignored.

## Git Sync Settings

### Branch

By default, PowerShell Universal will sync with the `master` branch. If you wish to use a different branch, specify the `GitBranch` setting within your `appsettings.json`.

#### Fixing Missing Upstream Tracking

If you encounter the error **"There is no tracking information for the current branch"**, the local branch is not linked to the remote. To fix this:

1. Open PowerShell in `%ProgramData%\UniversalAutomation\Repository` (or the configured repository path)
2. Run:

```powershell
git fetch
git branch --set-upstream-to=origin/main main
git pull
```

### Remote

Remotes are not required. If a remote is not specified, the git repository is stored locally in the Repository directory. If specified, PowerShell Universal will sync with the remote. Proper credentials are required for access to that remote.

#### Azure DevOps URL Format

Azure DevOps repositories should use the modern `dev.azure.com` URL format rather than the legacy `visualstudio.com` domain:

**Correct format:**

```
https://dev.azure.com/<organization>/<project>/_git/<repository>
```

**Examples:**

```
https://dev.azure.com/mycompany/MyProject/_git/PowerShellUniversal
https://dev.azure.com/mycompany/MyProject/_git/PSU%20Scripts
```

If your repository name contains spaces, they should be encoded as `%20` in the URL. Avoid using URLs with the older `visualstudio.com` domain, as they may cause redirect loops or authentication failures with the "too many redirects or authentication replays" error.

For Azure DevOps, your Personal Access Token must have the **Code (Read & Write)** scope. Fine-grained tokens work, but classic PATs are recommended for compatibility across PSU versions.

**Note for GitLab users:** If your GitLab instance requires header-based authentication, you may need to use the External Git Client option and configure Git credential helpers, as PSU's built-in Git client uses HTTP Basic authentication with the PAT as the password. Some GitLab configurations expect a `Private-Token` header instead.

### Authentication

You will need to configure authentication to your remote git repository. We recommend a personal access token.

### External Git Client

You can choose to use an external git client rather than using the library built into PowerShell Universal. This allows you additional configuration options such as using SSH authentication. PowerShell Universal will not use configured username, passwords or PATs when enabling this method. You will need to have a git client installed.

#### Using SSH Keys

You can use PowerShell Universal to generate and manage SSH keys. Within the admin console, click Platform \ SSH Keys. Generate a new SSH key. Next, click the copy button next to the SSH key to get the public key.

Register the public key with the target repository or account. For example, you can follow the [GitHub guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) here.

Within the Git Settings window, select the SSH Key you wish to use with the git sync. When using SSH Keys, ensure that the SSH URL is selected for cloning your repository.&#x20;

```
git@github.com:ironmansoftware/psu-devo
```

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>GitHub SSH URL</p></figcaption></figure>

#### Setting Credentials

When using the external git client, you are responsible for configuring credentials before performing a synchronization.

You can configure credentials via git configuration or the URL passed to PowerShell Universal.

The following command will store the credentials in plaintext on the PowerShell Universal server. You will need to run this command as the service account user so that they have access to the credentials. This will create a `.git-credentials` file that will be used when authenticating against the target URL. You may need to change the URL depending on your git remote.

```batch
git config --global credential.helper store
echo "https://${username}:${password_or_access_token}@github.com" > ~/.git-credentials
```

You can also store credentials directly in the URL provided to PowerShell Universal.

```
https://adam:APP_TOKEN@github.com/myOrg/myRepo.git
```

#### Example: User Name and PAT

To use an external git client and pass a user name and PAT to authenticate with, you can specify them in the git remote URL. For example:

```
https://username:PAT@github.com/ironmansoftware/universal
```

#### Example: SSH and GitHub

First, you will need to configure your local ssh-agent and GitHub account with SSH keys.

You can follow their [guide here](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).

Next, you will provide a SSH URI for the git remote URL in PowerShell Universal. The configured SSH key will be used for the connection.

```
git@github.com:ironmansoftware/universal.git
```

#### SSL Certificate Problem

{% hint style="warning" %}
SSL Certificate problem: unable to get local issuer certificate
{% endhint %}

If you are running on Windows and receive an SSL Certificate problem, you may need to ensure that you have [enabled schannel support](https://stackoverflow.com/questions/23885449/unable-to-resolve-unable-to-get-local-issuer-certificate-using-git-on-windows).

#### Credential Persistence

{% hint style="warning" %}
Unable to persist credentials with the 'wincredman' credential store.
{% endhint %}

If you are on Windows and receive an error about persisting credentials in wincredman, you may need to set the credential persistence to DAPI. You can [learn how to do that here](https://github.com/GitCredentialManager/git-credential-manager/issues/633).

### Manual Mode

Manual mode requires users editing the PowerShell Universal instance to click Edit in order to make changes in the system.

<figure><img src="../.gitbook/assets/image (210).png" alt=""><figcaption></figcaption></figure>

Once the changes are complete, the user can then click Save Changes to begin a commit

<figure><img src="../.gitbook/assets/image (219).png" alt=""><figcaption></figcaption></figure>

On the git commit page, you can view the changed files and enter a commit message.

<figure><img src="../.gitbook/assets/image (466).png" alt=""><figcaption></figcaption></figure>

Once changes have been committed, they will be pushed to the remote and the service will start to synchronize with git again. There is also a chance that a git merge conflict can take place at this time. See [Dealing with Conflicts](git.md#dealing-with-conflicts) for more information.

Manual mode can be set in the git settings within the admin console or within `appsettings.json`.

```json
"Data": {
  "RepositoryPath": "%ProgramData%\\UniversalAutomation\\Repository",
  "ConnectionString": "filename=%ProgramData%\\UniversalAutomation\\database.db;upgrade=true",
  "RunMigrations": true,
  "GitRemote": "",
  "GitUserName": "",
  "GitPassword": "",
  "GitBranch": "",
  "GitSyncBehavior": "TwoWay",
  "GitInitializeBehavior": "",
  "GitSyncInterval": "1",
  "ConfigurationScript": "",
  "ExternalGitClient": false
  "Mode": "Manual" // Or Automatic
},
```

### Method One: Pushing Local Files to Remote

{% hint style="info" %}
The default location for the local repository is `C:\ProgramData\UniversalAutomation\Repository`
{% endhint %}

You must ensure that your local folder is not a pre-existing git repository. Your repository directory should be simply a folder with your PowerShell Universal files. If a `.git` folder exists, and you do not wish to use this repository, you should delete it and PowerShell Universal will create a new repository.

If you are populating a new git repository, you need to ensure that the remote does not have any files in it. It should be a completely bare repository. For example, when creating a repository on GitHub, do not select a license or readme.md file to be created.

![](<../.gitbook/assets/image (275).png>)

Once the repository has been created, you can retrieve the git remote URL and provide that to the PowerShell Universal `appsettings.json` file.

![](<../.gitbook/assets/image (496).png>)

Once you have the branch, git remote URL and credentials, you can provide them to your `appsettings.json` file and the git remote will be populated with your local files.

### Method Two: Pulling from a Git Remote

{% hint style="info" %}
The default location for the local repository is `C:\ProgramData\UniversalAutomation\Repository`
{% endhint %}

You can configure PowerShell Universal to pull from a git remote. In this configuration, you must ensure that your local repository folder is completely empty. Any files within the folder will cause the git sync to fail and prevent it from recovering.

Configure the `appsettings.json` file to include the branch, credentials and git remote URL that you are cloning. Once the fields have been set, you can start the PowerShell Universal service. The first thing the service will do is clone the repository and configure it locally.

### Git Sync Timeout

Git sync will timeout if it cannot contact the remote after 60 minutes. This allows for time to download large repositories or delay with slow networks. You may see the PowerShell Universal service hang on "Synchronizing with git" during start up while the server waits for this to happen. If you wish to reduce this time, you can use the following appsetting.json setting. The value is in minutes.

```json
"Data" : {
    "GitSyncTimeout": 30
}
```

### Sync Interval

**Type:** Integer\
**Default:** 60\
**appsettings.json:** `GitSyncInterval`

The interval, in seconds, between automatic Git synchronization attempts when automatic sync is enabled. The default value is 60 seconds (1 minute).

To adjust the sync frequency, edit `appsettings.json`:

```json
"GitSyncInterval": 300
```

This would change the sync interval to 5 minutes. Lower values increase sync frequency but may impact performance in large repositories or slow networks. Setting this value too low (below 30 seconds) is not recommended for production environments.

### Troubleshooting

#### Azure DevOps: "Too many redirects or authentication replays"

This error typically indicates one of the following issues:

* **Legacy URL format:** Ensure you are using `https://dev.azure.com/<org>/<project>/_git/<repo>` instead of the older `visualstudio.com` domain
* **Invalid PAT scope:** Your Personal Access Token must have **Code (Read & Write)** permissions in Azure DevOps
* **Expired credentials:** Generate a new PAT and re-enter it in PSU's Git settings
* **Encoded spaces:** If your repository name has spaces, ensure they are encoded as `%20` in the URL

**Resolution:**

1. Update the remote URL to use `dev.azure.com`
2. Generate a new PAT with Code (Read & Write) scope
3. Enable **Use External Git Client** and install Git for Windows if the built-in client continues to fail

#### Missing Upstream Tracking

**Error:** "There is no tracking information for the current branch"

**Cause:** The local Git branch is not configured to track a remote branch.

**Resolution:** Open PowerShell in the repository directory and run:

```powershell
git fetch
git branch --set-upstream-to=origin/main main
git pull
```

Replace `main` with your actual branch name. Then click **Synchronize Now** in PSU.

#### Git Sync Stops After Changing Settings in UI

**Symptoms:** After editing Git settings (remote URL, credentials, sync interval, etc.) in the PSU UI and clicking OK, synchronization stops working even though settings appear correct.

**Cause:** In PSU 5.x, Git credentials are stored in the SQL database. Making any change to Git settings through the UI can clear the stored credentials, even if the password field still appears populated in the form.

**Resolution:**

1. Re-enter the Personal Access Token in **Settings → Git**
2. Click **OK** to save
3. In multi-node environments, **repeat this process on every node**—credentials must be entered individually on each server
4. Click **Synchronize Now** to verify sync is working again

The system does not automatically propagate credentials across nodes in a load-balanced or high-availability configuration.

#### Agent and Network Issues

**Symptoms:** Sync works on one node but fails on others, or you see `RpcException` or "service is unavailable" errors in logs.

**Common causes:**

* **Version mismatch:** Ensure all PSU servers and agents are running the same version
* **Firewall rules:** Agents communicate with the PSU server over gRPC on ports **5000** (HTTP) or **5001** (HTTPS)
* **Proxy or WebSocket blocking:** Corporate proxies may block or inspect gRPC traffic; configure git to use the proxy or enable External Git Client

**Resolution:**

1. Verify all nodes are running the same PSU version
2. Check firewall rules allow traffic on ports 5000/5001
3. Test gRPC connectivity between nodes
4. If using a proxy, configure `http_proxy` and `https_proxy` environment variables for the PSU service account

#### Docker and Containerized Deployments

* Ensure the container image includes `git` (run `git --version` to verify)
* Verify outbound network access to the git remote
* Mount persistent volumes for `/data` or `%ProgramData%\UniversalAutomation` to preserve git state across restarts
* If sync silently fails, check container logs for git or network errors

#### Editing .git/config Without Git CLI

If the Git command-line tool is not installed on the server and you encounter upstream tracking errors, you can edit the repository configuration directly through PSU's file browser:

1. Navigate to **Platform → Configuration → Repository → .git → config**
2. Add the following lines (adjust the branch name to match your repository):

```ini
[branch "main"]
    remote = origin
    merge = refs/heads/main
```

3. Click **Save**
4. Return to **Settings → Git** and click **Synchronize Now**

This approach allows you to configure upstream tracking without needing `git` commands, which is particularly useful when Git for Windows is not installed or when running under restricted service accounts.

#### Git Settings Not Persisting

If changes to Git settings are not saved or revert immediately after clicking OK:

**Check file system permissions:**

* Stop the PowerShell Universal service
* Try manually editing `%ProgramData%\PowerShellUniversal\appsettings.json` (or `%ProgramData%\UniversalAutomation\appsettings.json` in older versions)
* Add a comment line, save, and reopen the file to verify your changes persist
* If changes revert, check for antivirus software, Group Policy Objects (GPO), or NTFS permissions blocking writes to the PSU data directory

**Enable debug logging for troubleshooting:**

1. Stop the PowerShell Universal service
2. Edit `appsettings.json` and set:

```json
"SystemLogLevel": "Debug"
```

3. Save and restart the service
4. Attempt to save Git settings again
5. Review `%PROGRAMDATA%\PowerShellUniversal\systemLog.txt` for errors related to configuration writes

**Manually populate Git settings:**

With the service stopped, you can directly populate Git fields in `appsettings.json`:

```json
"GitRemote": "https://dev.azure.com/org/project/_git/repo",
"GitUserName": "any",
"GitPassword": "your-PAT-here",
"GitBranch": "main"
```

Restart the service and verify the settings appear in **Settings → Git**. If they vanish again, the debug logs will indicate whether a permission issue, endpoint protection software, or configuration validation error is causing the reset.

```
```

## Included Files

The files that are included with a git sync are any files within the local repository. This includes PS1 configuration files, pages XML files and any other files you may add manually.

The following are not included:

* appsettings.json
* database.db
* web.config
* PowerShell Universal Application Binaries

## Multiple Git Repositories

PowerShell Universal supports storing multiple git repository configurations within the database. By doing so, you can quickly switch between different configurations of PowerShell Universal. Click the Repositories tab to view the currently configured repositories. From here you can delete and edit repository configurations.

{% hint style="warning" %}
PowerShell Universal does not remove the .git folder when deleting a repository configuration. You will need to manually do this in order to configure a new repository.
{% endhint %}

When you add a new repository configuration, you can click the Apply button to switch to the selected repository. This will delete all files in the repository directory and clone the selected repository. You cannot apply a repository configuration if there are uncommitted changes in your repository. After cloning the repository, PowerShell Universal will completely reload it's configuration.

## Git History and Status Page

The history tab displays all the git commit history for the current repository.

<figure><img src="../.gitbook/assets/image (256).png" alt=""><figcaption></figcaption></figure>

The sync status tab displays the current status of nodes within the PSU cluster.

<figure><img src="../.gitbook/assets/image (214).png" alt=""><figcaption></figcaption></figure>

### Testing Git Sync

The best way to ensure that your git sync is working properly is to click the Synchronize Now button. This will force a sync to run, and you can verify whether the settings entered worked properly.

![](<../.gitbook/assets/image (138).png>)

### Viewing Changes

You can view changes within the table of git syncs. Each sync includes the number of changes found since the last sync, the SHA of the commit and a list of changes between that SHA and the previous one. When files are in a modified state, you will be able to view the diffs using the file diff tool.

![](<../.gitbook/assets/image (372).png>)

### Dealing with Conflicts

{% hint style="info" %}
Conflict resolution is only available in manual git sync mode.
{% endhint %}

When multiple users are editing the PowerShell Universal configuration files, there may be conflicts. PowerShell Universal will display that a particular node is in a conflicted state when attempting to commit changes. You will see a list of changes that are conflicted on the git commit page. Click the Resolve Conflict button to view the conflict in an editor.

<figure><img src="../.gitbook/assets/image (7) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

In this example, the string for this endpoint was edited on both the remote and the local repository.

<figure><img src="../.gitbook/assets/image (226).png" alt=""><figcaption></figcaption></figure>

Edit the text to remove the conflict.

<figure><img src="../.gitbook/assets/image (5) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Save the changes and navigate back to the git commit page. Enter a new commit message for the merge conflict and click Commit Changes.

<figure><img src="../.gitbook/assets/image (469).png" alt=""><figcaption></figcaption></figure>

This will resolve the merge conflict and push to the remote.

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

### Push-Only

Push-only git sync mode will not pull changes from the remote. Any changes made locally will be pushed up to the remote. The console will not be read-only. This configuration is useful for scenarios where you have one machine that is used to for the source-of-truth configuration for a pool of servers that are read-only.

```json
"Data": {
  "RepositoryPath": "%ProgramData%\\UniversalAutomation\\Repository",
  "ConnectionString": "%ProgramData%\\UniversalAutomation\\database.db",
  "DatabaseType": "LiteDB",
  "GitRemote": "https://github.com/myorg/myrepo.git",
  "GitUserName": "any",
  "GitPassword": "MYPAT----------------"
  "GitBranch": "dev",
  "GitSyncBehavior": "PushOnly",
  "ConfigurationScript": ""
},
```

## Personal Access Token

We recommend that you use a personal access token (PAT) over a user name and password. You can configure a personal access token by setting the password property in the `appsettings.json` or other configuration methods.

```javascript
    "Data": {
    "RepositoryPath": "%ProgramData%\\UniversalAutomation\\Repository",
    "ConnectionString": "%ProgramData%\\UniversalAutomation\\database.db",
    "GitRemote": "https://github.com/myorg/myrepo.git",
    "GitUserName": "any",
    "GitPassword": "MYPAT----------------"
  },
```

### GitHub Fine-Grained Tokens

In GitHub, you can retrieve a fine-grained token by click your avatar in the top right, selecting Settings, Developers Settings, Personal Access Tokens and then Fine-Grained Tokens.

When generating the token, ensure that you provide the repository Read-Write to the Content permission. This will automatically add Read to the Metadata permission. You can provide access to just the repository you are looking to clone.

### GitHub Tokens (Classic)

In GitHub, you can retrieve a personal access token by clicking your avatar in the top right, selecting Settings, Developer Settings, Personal Access Tokens and then Tokens (Classic).

When generating your access token, ensure that you select the Repo permissions.

![](<../.gitbook/assets/image (36).png>)

Note, that if you are using BitBucket, you will need to specify the user name in addition to the PAT in `appsettings.json`.

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

## Common Errors

#### Git synchronization failed. unknown certificate lookup failure: 16777280

The lib2gitsharp library was unable to validate the certificate of the remote git repository. You will need to use the [external git client](git.md#external-git-client) and a custom git config in order to address this.

Some common options for git HTTPS support include:

```
http.sslVerify
    Whether to verify the SSL certificate when fetching or pushing over HTTPS.
    Can be overridden by the GIT_SSL_NO_VERIFY environment variable.

http.sslCAInfo
    File containing the certificates to verify the peer with when fetching or pushing
    over HTTPS. Can be overridden by the GIT_SSL_CAINFO environment variable.

http.sslCAPath
    Path containing files with the CA certificates to verify the peer with when
    fetching or pushing over HTTPS.
    Can be overridden by the GIT_SSL_CAPATH environment variable.
```

#### "too many redirects" or authentication replays

The git remote has rejected your credentials to access the repository. Your personal access token may have expired or does not have access to the remote.

#### repository not owned by current user

The local git repository does not have the proper access controls for the user trying to access it. This can happen if PowerShell Universal cloned the repository and then a different service account was set on the service. Because the access controls do not match, the git will not access the folder due. This is a security feature of git.

You can update the owner of the folder to avoid this or configure git to trust the folder. Set the following value into the global git config.

```
[safe]
directory = C:\ProgramData\UniversalAutomation\Repository
```

The global config can be found in: `C:\Program Files\git\etc\gitconfig`

## Benefits of Git Sync vs Manual Git Sync

It is possible to manually git sync a repository. PowerShell Universal uses very basic commands when dealing with git. Any changes made to PowerShell Universal through the admin console or API invoke a `git commit` and the author is set to the identity of the user making the change. During a git sync operation, we first perform a `git pull` to ensure that we have the latest version of files on the remote. Next, we perform a `git push` to push up local commits that have happened since the last sync.

You could achieve this functionality with a scheduled job.

That said, one feature of the git sync is that it analyzes the commit to ensure that only files that were changed during the sync are reloaded. This will stop dashboards from auto-deploying when they haven't changed or APIs services from restarting when environments haven't been updated. So there is a performance gain here.

The other issue is that due to the way that PowerShell Universal watches files (with a `FileSystemWatcher`) and the way that git updates files, the configurations will not reload automatically after a pull. You will have to ensure that you force the configurations to be reevaluated.

## Branching Strategies

Branching strategies in git dictate how changes are moved from one branch to another. Utilizing different types of branching strategies in PowerShell Universal can ensure that teams of different sizes can work effectively together in the platform.

### Single Users and Small Teams

For single users and small teams, it may not be necessary to have more than a single branch. The branch is used for history tracking and provides the ability to roll back changes. Users will access PowerShell Universal directly to make changes or commit changes to the single branch from local clones of the repository directory using a tool like VS Code.

* main - Single branch that accepts all changes directly

### Single Users and Smalls Teams with a Staging Branch

Even single users and small teams may find it advantageous to employ a staging, or dev, branch. This branch will receive changes during development. A standalone instance of PowerShell Universal will be configured to run against this dev branch so that users can validate changes before pushing to production.

When using a staging branch configuration, the PowerShell Universal environments are completely separate. They use a different database and scheduler. Data such as identities, app tokens and job history are not shared across the environments.

{% hint style="info" %}
Each instance of PowerShell Universal requires a [license](../licensing.md). In this configuration, two licenses would be required.
{% endhint %}

A separate PowerShell Universal instance can then be configured to point to a main, or production, branch that will receive updates via merges or Pull Requests in a system like GitHub. In this configuration, it is possible to use one-way git sync to pull changes from main but never push from the platform. This also prevents most merge conflicts as they will be addressed in the dev branch or via the merge tool in the source repository.

* main - Production branch that receives changes from pull requests of the dev branch
* dev - The staging branch used to accept commits and validate changes before pushing to master.

### Medium to Large Size Teams

When considering teams with more than a couple of developers, a more complex branching strategy may be helpful to better evaluate code changes and avoid merge conflicts. PowerShell Universal provides basic merge tools, but better tooling is available for this purpose, such as GitHub pull request, GitLab merge requests and local tools like GitKraken.

In medium size teams, it may be desirable to have additional feature branches that isolate specific changes to a certain branch. For example, a developer may be creating a new set of APIs to manage Azure in PowerShell Universal. In order to avoid breaking changes in the dev branch, developers will create their own feature branch that contains all their changes until it is complete enough to be merged into the development branch.

{% hint style="info" %}
PowerShell Universal provides [developer licenses](../licensing.md) to avoid having to purchase a license for every developer on your team. Licenses would still be required for the production and staging environments.
{% endhint %}

In this type of configuration, local development is ideal because the developers will work on their local PowerShell Universal instance within their feature branch. When the feature is complete, they will create a Pull or Merge request in the source repository to move changes into the dev branch. Testing will be completed on the dev branch before merging to production.

Similar to a main\dev branching strategy, all PowerShell Universal instances will be isolated and will not share a database or scheduler.

Once a set of features is ready for production, a Pull or Merge request will be made from dev to the main branch.

* main - Production branch that will only receive changes from dev
* dev - Staging branch that receives changes from feature branches but is not changed directly
* feature - Feature branch that is committed to directly by developers and merged to dev when ready

Depending on the complexity of your environment, it may be advised to use Deployments rather than git in production. See the Large Teams section below for more information.

### Large Teams

In large teams, we recommend using git for development purposes but use Deployments, or a similar concept, for production.

[Deployments ](deployments.md)provide immutable configuration packages that have been well tested in down-level environments. By using Deployments, you can choose how you develop and manage your code and simply publish the result to your development, staging, QA and production environments. This ensures that all code is well tested before deploying to your critical systems.

You can use automated workflows, like GitHub Actions, to publish your Deployments without having to manually update any system.

## Git Hosting

PowerShell Universal supports any standard git hosting solution. Our customers frequently use the following:

* GitHub
* GitHub Enterprise
* GitLab
* Bitbucket
* Azure DevOps

While these are the most common platforms, we support any platform that talks the git protocol.&#x20;

### Example: Gitea

You can also use simple, self-hosted solutions like [Gitea](https://gitea.com). Here is an example of how to easily configure a Gitea docker container for use with PowerShell Universal.

