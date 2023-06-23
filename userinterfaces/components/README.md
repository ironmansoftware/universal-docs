# Components

A Universal app website is composed of components. In addition to the core component, you can also extend Universal with a large set of community created components.

Additional components can be downloaded from the [UD Marketplace](https://marketplace.universaldashboard.io/).

External components are distributed as PowerShell modules and can be used in an app by using `Import-Module`.

When building an app, you can simply call the PowerShell cmdlets within your app script to create a new component.

```powershell
New-UDApp -Title 'Dashboard' -Content {
    New-UDTypography -Text 'Hello, world!'
}
```

## Adding Components to Apps

You can add component modules by clicking the Components button on the App page and then adding the components. This list will also include components downloaded from the Marketplace.

![Add Components to a Dashboard](<../../.gitbook/assets/image (105).png>)

### Manual Component Installation

You can manually install components into the assets folder by including the appropriate folder structure and files. All components need to be valid PowerShell modules.

Each component should be in a folder with the module name and an additional folder with the version.

![](<../../.gitbook/assets/image (254).png>)

### Including Components in the Repository

You can also include components within the code Repository. By including them in the repository, they will be downloaded when using [git sync](../../config/git.md). This functionality is only enabled when git sync is enabled.

After a git pull is performed on the remote repository, Components will be automatically loaded and available within the Components page within PowerShell Universal. The structure and layout of the components folder is the same as the main assets folder.

![](<../../.gitbook/assets/image (481).png>)
