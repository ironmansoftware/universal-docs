# Running as a Service Account

### Application Service Account

The PowerShell Universal application can be run as a Service Account. This means that the application will run all of its functions as the service account including local application tasks, jobs \(by default\), and dashboards. This is a suggested configuration and is **REQUIRED** in order to execute jobs as other Service Accounts that are NOT the Service Account used for PowerShell Universal.

When this configuration is made, PowerShell Universal is no longer running as the local system account and additional permissions are required for the Service Account. **Windows requires a distinct set of permissions for the Service Account if the account is not in the local Administrators group on the host.**

{% hint style="info" %}
If you are hosting PowerShell Universal in Internet Information Services \(IIS\) - these permissions **ALSO** are required for the Application Pool Identity account.
{% endhint %}

You can manually assign the required permissions in the "Local Security Policy" snap-in located here: Control Panel/ Administrative Tools / Local Security Policy / Local Policies / User Rights Assignment. 

Simply add the User or Group to the following Rights to ensure PowerShell Universal Functionality:

* Log on as a service
* Adjust memory quotas for a process
* replace a process level token

![Local Security Policy User Rights Assignments for Service](../.gitbook/assets/image%20%2820%29.png)

### Script Run As Requirements

By using Secret Variables you can save PSCredentials that can be used to execute scripts as a service account. These service accounts required a specific set of Windows permissions in order to execute jobs properly.

The service account you wish to use must have the "**Log on as batch job**" rights on the Windows host. Administrators on the machine have this by default, so if the service account is NOT an Administrator you must ensure the account has the permission configured.

You can manually assign this permission in the "Local Security Policy" snap-in located here: Control Panel/ Administrative Tools / Local Security Policy / Local Policies / User Rights Assignment. 

Simply add the User or Group to the "Log on as a batch job properties" members to allow the account to properly execute script jobs in PowerShell Universal:

![Local Security Policy User Rights Assignments for Run As](../.gitbook/assets/image%20%287%29.png)

{% hint style="warning" %}
Please consider that some of these settings may already be managed by Group Policy Object \(GPO\) definitions. This may cause these settings to be overwritten or unable to be applied.
{% endhint %}

