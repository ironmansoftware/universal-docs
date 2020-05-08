# Scripts

Scripts are the basic entity within Universal Automation. Scripts are just PowerShell scripts. They are stored on disk and also persisted to a local or remote Git repository. 

## Add a New Script

To add a new script, you can click the New Script button within the Automation / Scripts page. There are various settings you can provide for the script. 

![](../.gitbook/assets/image%20%2818%29.png)

**Name**

Name of the script as shown in Universal Automation. This will also be the name used to persist the script to disk. This setting needs to be unique within the current folder. 

**Description**

A description of the script. This is shown in various places within the UA UI and also returned by the Universal cmdlets. 

**Disable Manual Invocation**

Prevents a script from being run manually. This is enforced in the UI as well as the web server and cmdlets. 

**Manual Time**

This setting is used to track the amount of time saved. 

**Max Job History**

Defaults to 100. It defines the amount of jobs that are stored when running this script. Jobs are also cleaned up based on the server-wide job retention duration setting from within the Settings / General page. 

**Error Action**

Changes how the script reacts when there is an error within the script. By default, terminating and non-terminating errors are ignored and the script will always be successful. You can change this setting to stop to cause scripts to fail immediately when an error is encountered. 

**PowerShell Version**

Allows you to define the required PowerShell version for the script. By default, it uses the server-wide default PowerShell version. PowerShell versions are automatically located the first the Universal Server starts up. You can also add PowerShell Versions on the Settings / General page. 

## Running a Script

You can run a script in the UI by click the Run button the Automation / Scripts page or by clicking View and then Run. In each case, you will be presented with the Run Dialog that allows you to select various settings for the job. 

![](../.gitbook/assets/image%20%2820%29.png)

### Running a Script With Parameters

Universal Automation automatically determines the parameters as defined within your scripts. It takes advantage of static code analysis to determine the type, default values and some validation that is then presented within the UI. 

For example, you may have a script with the following parameters. 

```text
param(
    $Test,
    [DateTime]$Time, 
    [int]$Number,
    [PSCredential]$Credential,
    [System.ConsoleColor]$Color
)
```

The result is a set of input options that are based on the types of parameters. 

![](../.gitbook/assets/image%20%286%29.png)

### Running a Script as Another User

You can run scripts as another user by configuring secret variables. PowerShell Universal uses the Microsoft Secret Management module to integrate with secret providers. See variables for more information on secrets. 

To run as another user, simply add or import a PSCredential variable. From there, you can select the credential from within the run dialog. 

![](../.gitbook/assets/image%20%2823%29.png)



