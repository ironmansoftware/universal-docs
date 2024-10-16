---
description: Installation instructions for PowerShell Universal.
---

# ⬇️ Installation

## MSI Install (Windows)

The MSI install will create a PowerShell Universal service. By default, PowerShell Universal will be listening on port 5000. You will be able to navigate to `http://localhost:5000`

MSI downloads are available on our [download page](https://ironmansoftware.com/downloads).

System installs will run as a Windows service. User installs will run when the user logins into the machine and runs in the user's context.

### MSI Parameters

The following table contains the parameters you can specify if running `msiexec` against our MSI install for automation purposes.

| Parameter              | Description                                                                                                                  | Default Value                                             |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| INSTALLFOLDER          | The installation folder for PowerShell Universal                                                                             | %ProgramFiles(x86)%\Universal                             |
| TCPPORT                | The TCP port the HTTP server will be listening on.                                                                           | 5000                                                      |
| REPOFOLDER             | The repository folder to save the configuration files to.                                                                    | %ProgramData%\UniversalAutomation\Repository              |
| CONNECTIONSTRING       | The SQL, SQLite, or PostgreSQL connection string.                                                                            | Data Source=%ProgramData%\UniversalAutomation\database.db |
| DATABASETYPE           | SQL, SQLite, or PostgreSQL                                                                                                   | SQLite                                                    |
| STARTSERVICE           | Whether to start the service after install (0 or 1)                                                                          | 1                                                         |
| SERVICEACCOUNT         | The service account to set for the Windows service. Use the format of domain\username.                                       | None                                                      |
| SERVICEACCOUNTPASSWORD | The service account password to set for the Windows Service. The password will be masked with \*\*\*'s in the installer log. | None                                                      |
| TELEMETRY              | Anonymous telemetry collection                                                                                               | 0                                                         |
| ADDPSMODULEPATH        | Adds the PowerShell Universal module directory to the PSModulePath environment variable.                                     | 1                                                         |
| STARTSERVICE           | Whether to start the service after install.                                                                                  | 1                                                         |
| INSTALLTYPE            | Whether to perform a server or user install.                                                                                 | Server                                                    |

### Example

Below is an example of how to run `msiexec.exe` to install PowerShell Universal and provide parameters to the installer.

{% code overflow="wrap" %}
```powershell
 Start-Process msiexec.exe -ArgumentList "/I C:\Users\adamr\Downloads\PowerShellUniversal.4.2.7.msi /q /norestart /L*V `"C:\users\adamr\desktop\msi.log.txt`" STARTSERVICE=0 SERVICEACCOUNT=contoso\service_account SERVICEACCOUNTPASSWORD=ThisPasswordWillBeReplacedWithAsterisksInTheMSILogs" -Wait -NoNewWindow
```
{% endcode %}

## ZIP Install

You can also download the ZIP from our [Downloads page](https://ironmansoftware.com/downloads/) if you would like to xcopy deploy the files on Windows or Linux.

### Windows

You can start Universal by unzipping the contents, unblocking the files and then executing `Universal.Server.exe`.

```
Expand-Archive -Path .\Universal.zip -DestinationPath .\Universal
Get-ChildItem .\Universal -Recurse | Unblock-File
Start-Process .\Universal\Universal.Server.exe
```

### Linux

You can use the following command line on Linux to install and start PowerShell Universal.

```
 wget https://imsreleases.blob.core.windows.net/universal/production/4.2.7/Universal.linux-x64.4.2.7.zip
 sudo apt install unzip 
 unzip Universal.linux-x64.4.2.7.zip -d PSU
 chmod +x ./PSU/Universal.Server
 ./PSU/Universal.Server
```

## Linux Service

You can use `systemd` to start PowerShell Universal as a service. The below script is an example of downloading a version of PowerShell Universal and installing it as a service.&#x20;

```bash
# ----
# This script will install PowerShell Universal on Linux as a service
# This has been tested on Ubuntu 20.04 (ARM64) on a Raspberry Pi 4
# ----
# Dependencies:
# wget
# unzip
#
# Make sure they are installed
# ----

# These are used to derive the download URL
PSU_VERSION="5.0.0" # Change this to the current version
PSU_ARCH="arm64" # Change this to your desired architecture
PSU_FILE="Universal.linux-${PSU_ARCH}.${PSU_VERSION}.zip"
PSU_URL="https://imsreleases.blob.core.windows.net/universal/production/${PSU_VERSION}/${PSU_FILE}"

# These are used for installing PowerShell Universal
# If you'd like to use a different path, change this
PSU_PATH="/opt/psuniversal"
PSU_EXEC="${PSU_PATH}/Universal.Server"

# These are for installing it as a service
PSU_SERVICE="psuniversal"
PSU_USER="psuniversal"

# ----
# BEGIN
# ----

echo "Creating $PSU_PATH and granting access to $USER"
sudo mkdir $PSU_PATH
sudo setfacl -m "u:${USER}:rwx" $PSU_PATH

echo "Creating user $PSU_USER and making it the owner of $PSU_PATH"
sudo useradd $PSU_USER -m
sudo chown $PSU_USER -R $PSU_PATH

echo "Downloading PowerShell Universal $PSU_VERSION ($PSU_ARCH)"
wget -q $PSU_URL -O $PSU_FILE

echo "Extracting $PSU_FILE to $PSU_PATH"
unzip -o -qq $PSU_FILE -d $PSU_PATH

echo "Make $PSU_EXEC executable"
sudo chmod +x $PSU_EXEC

echo "Creating service configuration"
cat <<EOF > ~/$PSU_SERVICE.service
[Unit]
Description=PowerShell Universal
[Service]
ExecStart=$PSU_EXEC
SyslogIdentifier=psuniversal
User=$PSU_USER
Restart=always
RestartSec=5
[Install]
WantedBy=multi-user.target
EOF

echo "Creating and starting service"
sudo cp -f ~/$PSU_SERVICE.service /etc/systemd/system
sudo systemctl daemon-reload
sudo systemctl enable $PSU_SERVICE
sudo systemctl start $PSU_SERVICE
sudo systemctl status $PSU_SERVICE --no-pager

# If you don't use UFW, you can comment this out
echo "Allow port 5000/tcp"
sudo ufw allow 5000/tcp

# ----
# END
# ----
```

## PowerShell Module

You can use the PowerShell Universal PowerShell module to install the Universal server. To install the module, use `Install-Module`.

```
Install-Module Universal
```

To install the Universal server, you can use `Install-PSUServer`.

```
Install-PSUServer -LatestVersion
```

If you run this command on Windows, a Windows service will be created and started on your machine. If you run this command on Linux, a systemd service will be created and started. If you run this command on Mac OS, the PowerShell Universal server will be downloaded and extracted.

## Chocolatey Package (Windows)

{% hint style="warning" %}
Chocolatey packages for PowerShell Universal are usually available within a week of release but will not be available the day of a release.
{% endhint %}

You can install PowerShell Universal using the [Chocolatey package](https://chocolatey.org/packages/powershelluniversal). The package runs the MSI install. It will install Universal as a service and open a web browser after the install.

You can login with the "admin" user and any password.

```
choco install powershelluniversal
```

### Docker

See the [Docker page](docker.md#installation).

## IIS Install

Please visit the [IIS hosting documentation](../config/hosting/hosting-iis.md) for information on how to configure PowerShell Universal as an IIS website.

## Antivirus Configuration

PowerShell Universal takes full advantage of PowerShell and the PowerShell SDK. It includes PowerShell scripts directly in the product. You will want to consider configuring antivirus to allow for execution of PowerShell scripts in PowerShell Universal.

### Directories

The following directories will contain scripts and executable files that may need to be excluded from antivirus checks.

The following are examples from a standard Windows system. Changing paths within appsettings.json or within the installer will require changing which directories are execluded.

| Path                              | Description                                                                                                  |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| %ProgramData%\PowerShellUniversal | Contains log files and appsettings.json                                                                      |
| %ProgramData%\UniversalAutomation | Contains PowerShell scripts and artifacts. Contains the single file database when not using SQL integration. |
| %ProgramFiles(x86)\Universal      | Contains PowerShell Universal application executables, libraries and modules.                                |

### Executables

It may be necessary to exclude certain executables that will run PowerShell scripts. The below is a list of executables that will run PowerShell from PowerShell Universal.

| Name                 | Description                                            |
| -------------------- | ------------------------------------------------------ |
| Universal.Server.exe | The PowerShell Universal core service.                 |
| Universal.Agent.exe  | The PowerShell Universal agent environment executable. |
| pwsh.exe             | PowerShell 7.x                                         |
| PowerShell.exe       | PowerShell 5.x                                         |

## Default Admin Name and Password

&#x20;You can use the `$ENV:PSUDefaultAdminName` and `$ENV:PSUDefaultAdminPassword` environment variables to change this behavior. These values are only used if no administrator account already exists. This is useful for cloud-based installations.&#x20;

## Agent

The PowerShell Universal Agent is used for executing Event Hub actions. Depending on your environment, you will install it in different ways.&#x20;

### Windows (MSI)

The PowerShell Universal Agent MSI is available on our download page. After installing the MSI, you will have a PowerShell Universal Agent service running on your machine. You will need to [configure it](../api/event-hubs.md) to connect to PowerShell Universal.&#x20;

### ZIP

There are ZIP files for each platform we support on our downloads page. Each ZIP will contain a `PowerShellUniversal.Agent.exe` or `PowerShellUniversal.Agent` file that can be used to start an agent. You will need to run the process as a service for it to start whenever the machine is rebooted.&#x20;

## Next Steps

At this point, Universal is up and running. You can navigate to the admin console by visiting `http://localhost:5000` by default. Login with the default admin name and password or create a default admin account.&#x20;
