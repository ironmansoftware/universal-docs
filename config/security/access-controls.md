---
description: Access controls for PowerShell Universal.
---

# Access Controls

{% hint style="info" %}
Access controls requires a [license](https://ironmansoftware.com/pricing/powershell-universal).
{% endhint %}

## About

Access controls allow you to define who has access to particular resources inside PowerShell Universal. Currently, access controls only apply to scripts.&#x20;

There are three types of access controls.&#x20;

* Global
* Resource
* Tag

PowerShell Universal uses a least-privileged model and users have no access without an access control that applies to their role.&#x20;

Access controls are defined within the `accessControls.ps1` file within your PowerShell Universal configuration repository.&#x20;

## Admin Console

You can define access controls in the admin console under Security \ Access Controls.&#x20;

![](<../../.gitbook/assets/image (174).png>)

## Access Control Types

There are five different privileges that can be granted to users. These values are available on the `[PowerShellUniversal.AccessControlType]` enumeration.&#x20;

* View (1)
* Edit (2)
* Create (4)
* Delete (8)
* Execute (16)

You can define multiple access control types on a single access control by using a binary or operator.

For example, this creates a privilege for both Create and View.&#x20;

```powershell
$Type = ([PowerShellUniversal.AccessControlType]::Create -bor [PowerShellUniversal.AccessControlType]::View)
```

You can also use the integer values for a more terse syntax. This creates the same Create and View privileges.

```powershell
$Type = 1 -bor 4
```

## Global Access Controls

Global access controls allow you to define an access for a role for all resources of the chosen type.&#x20;

For example, to allow any user with the `ScriptBuilder` role to create a script, you can define an access control using the following command. You'll also want to grant the View privilege so that the user can also view scripts.&#x20;

```powershell
$Type = ([PowerShellUniversal.AccessControlType]::Create -bor [PowerShellUniversal.AccessControlType]::View)
New-PSUAccessControl -Role 'ScriptBuilder' -ObjectType 'Script' -Type $Type
```

## Resource Access Controls

Resource access controls allow you to specify access controls directly on a resource.&#x20;

This example defines the execute privilege on the `OnBoarding.ps1` script to the `ScriptRunner` role.&#x20;

```powershell
$Type = ([PowerShellUniversal.AccessControlType]::Execute -bor [PowerShellUniversal.AccessControlType]::View)
New-PSUAccessControl -Role 'ScriptRunner' -ObjectId 'OnBoarding.ps1' -ObjectType 'Script' -Type $Type
```

## Tag Access Controls

Tag access controls allow you to specify an access control based on a tag. All tagged resources will have this access control defined. This allows you to group resources and apply access controls to the group.&#x20;

The following example provides the edit privilege to the `ScriptEditor` role and the `HR` tag.

```powershell
$Type = ([PowerShellUniversal.AccessControlType]::Edit -bor [PowerShellUniversal.AccessControlType]::View)
New-PSUAccessControl -Role 'ScriptEditor' -Tag 'HR' -Type $Type
```

## API&#x20;

* [New-PSUAccessControl](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSUAccessControl.txt)
