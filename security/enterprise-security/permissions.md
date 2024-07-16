---
description: Permissions for resources within PowerShell Universal
---

# Permissions

PowerShell Universal leverages permissions throughout the platform to provide fine-grained authorization against different scopes and resources. Built-in roles have a read-only set of permissions that are automatically applied to users with those roles. Custom roles can have custom permissions set. Additionally, individual users can have their own set of permissions.&#x20;

Permissions are stored in the database and not as part of the `.universal` configuration files.&#x20;

## Permission Identifiers

Each permission uses an identifier to authorize a user to access a resource. They are strings that utilize the scope and resource type, followed by an access type.&#x20;

For example, the following would provide read access to all API features.&#x20;

```
apis/read
```

Wildcards can be used in permission identifiers to include sub-scopes over multiple access types. The following provides access to all script features.&#x20;

```
automation.scripts/*
```

## Managing Permissions

{% hint style="warning" %}
PowerShell Universal v5 is still in beta and this is subject to change.
{% endhint %}

Permissions can be managed for an identity by click Security \ Permissions. You can select the identity and define a permission identifier to grant to the identity. This will blend with the permissions granted by any role assignments they may have.&#x20;

Roles currently cannot be assigned permissions.

## Default Role Permissions

Below are the default role permissions.&#x20;

### Administrator



| Identifier | Description                         |
| ---------- | ----------------------------------- |
| \*         | Full access to PowerShell Universal |

### Operator



| Identifier    | Description                         |
| ------------- | ----------------------------------- |
| apis/\*       | Full access to APIs.                |
| automation/\* | Full access to automation features. |
| apps/\*       | Full access to Apps.                |
| platform/\*   | Full access to platform features    |
| settings/\*   | Full access to platform features    |

### Execute



| Identifier         | Description                             |
| ------------------ | --------------------------------------- |
| apis/read          | Read access to APIs                     |
| apis/execute       | Execute access to APIs                  |
| automation/read    | Read access to automation features.     |
| automation/execute | Execute access to automation features.  |
| apps/read          | Read access to Apps.                    |
| apps/execute       | Execute access to Apps.                 |
| platform/read      | Read access to platform features.       |
| settings/read      | Read access to settings.                |

### Reader



| Identifier      | Description                         |
| --------------- | ----------------------------------- |
| apis/read       | Read access to APIs.                |
| apps/read       | Read access to Apps.                |
| automation/read | Read access to automation features. |

### API Editor&#x20;



| Identifier | Description         |
| ---------- | ------------------- |
| apis/\*    | All access to APIs. |

### API Reader

| Identifier | Description          |
| ---------- | -------------------- |
| apis/read  | Read access to APIs. |

### App Editor



| Identifier | Description         |
| ---------- | ------------------- |
| apps/\*    | All access to apps. |

### App Reader



|           |                      |
| --------- | -------------------- |
| apps/read | Read access to apps. |
