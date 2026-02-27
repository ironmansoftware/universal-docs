---
description: Immutable configuration packages for PowerShell Universal.
---

# Deployments

Deployments provide the ability to package and version PowerShell Universal configuration repositories. They can be deployed to a cluster of PowerShell Universal nodes to ensure tall nodes have the same configuration without the need to configure [git sync](git.md). Deployments are packaged as PowerShell Modules and can be deployed directly from PowerShell repositories.

{% hint style="warning" %}
Deployments cannot be used with git sync. When using deployments, it is recommended to manage git and source control outside of PowerShell Universal.
{% endhint %}

Deployments can also be used as a way to quickly snapshot PSU configurations and roll back or forward without having to manually change files.

## Creating a Deployment

You will need the `Settings.Deployments\Create` permission to create new deployments.

### API

The PowerShell Universal Management API and module can be used to create PowerShell Universal deployments. The `New-PSUDeployment` cmdlet can be used to generate a new deployment. This deployment will be stored in the database. It will contain the current state of the PowerShell Universal repository for the computer it is connected to.

The `-Path` is optional and will contain the module `NuPkg` file.

```powershell
New-PSUDeployment -Name 'Production' -Version '1.0.1' -Path .\production.1.0.1.nupkg
```

You can also call the API of HTTP.

```powershell
Invoke-RestMethod http://localhost:5000/api/v1/deployments -Method POST -Body (@{
   Name = 'Production'
   Version = '1.0.1'
} | ConvertTo-Json)
```

#### Applying a Deployment as Module

If you want your deployment module to appear on the PSModulePath, you can append the `asModule` query string parameter to the path. This ensures that functions in the deployment module are available in the environment.

{% code overflow="wrap" %}
```powershell
Invoke-RestMethod http://localhost:5000/api/v1/deployments?asModule=true -Method POST -InFile mymodule.nupkg
```
{% endcode %}

### Admin Console

We do not recommend manually creating deployments as automation should be preferred, but it is possible through the admin console.

Click Settings \ Deployments to access the deployments page. You will need the `Setings.Deployments\Read` permission to view this page. Click Create Deployment to configure a new deployment. This deployment will be shown in the deployments table.

## Applying a Deployment

Applying a deployment reconfigures all nodes in a PowerShell Universal cluster with the selected deployment's contents. Only a single API call is required to reconfigure the entire cluster.

You will need the `Settings.Deployments\Execute` permission to apply a deployment.

### Pinning

Pinning applies a deployment and ensures that the admin console and Management API are read-only. This prevents users from editing resources in the cluster.

{% hint style="info" %}
Pinning is recommended for production PowerShell Universal clusters.
{% endhint %}

### API

You can use the `Select-PSUDeployment` cmdlet or Management API to apply a deployment. This can be done using a PowerShell repository or by selecting a deployment that is within the database.

<pre class="language-powershell"><code class="lang-powershell"><strong>Get-PSUDeployment -Name 'Production' -Version '1.0.1' -Pin | Select-PSUDeployment 
</strong></code></pre>

### Admin Console

We do not recommend managing deployments through the admin console, but it is possible. Always prefer automation over manual deployment processes. In the admin console, click Settings \ Deployments.

From there, you can see all the deployments listed that have been created in the PSU environment. Click the Apply button to apply the deployment to the cluster. You will have the option to Pin the deployment.

### PowerShell Repository

You can use the management API and Universal module to apply a deployment directly from a PowerShell repository, like the PowerShell Gallery or file share. The repository needs to be registered on all nodes in the cluster in order to apply the deployment successfully. You can use `Register-PSResourceRepository` to register a repository.

To apply the deployment, call `Select-PSUDeployment` with the `Module` parameter set.

```powershell
Select-PSUDeployment -ModuleName 'Production' -ModuleVersion '1.0.1'
```

### GitHub Actions

You can use the `ironmansoftware/deploy-universal` action to deploy your depository directly from GitHub. It checks out the current repository and pushes the changes up to PowerShell Universal.

Below is an example of the YAML to do so. To learn more about the deploy action, [click here](https://github.com/ironmansoftware/deploy-universal).

```yaml
name: Deploy
on: [workflow_dispatch]

jobs:
    build:
      name: Deploy
      runs-on: ubuntu-latest
      steps:
        - uses: actions/checkout@v1
        - uses: ironmansoftware/deploy-universal@1.0
          with:
            url: 'https://431d-2600-6c44-1a7f-f1f9-30aa-ed10-8683-5259.ngrok-free.app'
            apptoken: '${{ secrets.UNIVERSAL_APP_TOKEN }}'
            name: 'Production'
            version: '1.4.1'
            description: 'Production Configuration'
```

## Git vs Deployments

Git sync and deployments offer similar functionality. Both git sync and deployments ensures that all nodes within a cluster share a configuration but each has different pro and cons.

### Git

Git allows users to make commits directly in PowerShell Universal. They will be able to view history and compare changes without having to leave the admin console. Git can also be complicated and problematic to configure. PowerShell Universal offers limited git features. Git sync has the benefit of knowing the difference between the current configuration and the incoming configuration and can reload only the resources that change. That said, this is often complicated and error prone.

#### Pros

* Shared configuration across cluster
* Git interaction directly in the admin console
* View commit history directly in admin console
* Incremental resource updates limit downtime

#### Cons

* Requires external git repository for clusters
* Can be complicated configure
* Changes to external git systems can prevent PSU from syncing
* Incremental resource updates are complicated and error prone
* Editing directly in shared PSU instances can be problematic for large teams

### Deployments

Deployments provide a way to apply immutable deployment packages to PowerShell Universal clusters. External systems are not required, and deployment packages are merely PowerShell modules that can be stored in the database or, optionally, external PowerShell resource repositories. Deployments do not contain any file history, nor do they integrate with source control. Deployments can be created in PowerShell Universal or outside with standard PowerShell cmdlets.

#### Pros

* Simple to create and deploy with standard PowerShell cmdlets
* No external systems required
* Immutable configurations that are simple for PowerShell Universal to deploy
* Can be integrated with PowerShell Resource Repositories for versioning

#### Cons

* Source control needs to be accomplished outside PSU
* External systems required to automate deployments
* Reconfiguration may take time as the entire server configuration is reset
