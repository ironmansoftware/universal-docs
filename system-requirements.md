---
description: System requirements for PowerShell Universal
---

# 📊 System Requirements

## Hardware

Hardware recommendations are based on use and depend on how many scripts are running on the PowerShell Universal server and how many users are accessing the machine. Unix based machines typically require less hardware requirements than Windows based machines. The below recommendations are based on low use of the system.

### Minimum

This is the base line for a Universal server with very minimal server load. It should be used for trial or development purposes only.

* 2 CPU&#x20;
* 4 GB
* 250 GB
* SQLite Database

### Recommended

This is the base line for a Universal server running several jobs an hour, hosting APIs with fewer than 100 requests per hour and a single App. It will support up to 10 concurrent users.

* 4 CPU
* 16 GB
* 500 GB
* MS SQL\PostgreSQL Database

### Performance

This is the base line for a Universal server running dozens of jobs an hour, hosting APIs with greater than 100 requests per hour and up to 5 Apps. It will support up to 50 concurrent users.&#x20;

* 16 CPU
* 32 GB
* 1 TB
* MS SQL\PostgreSQL Database

### Distributed

A distributed system employs multiple instances of PowerShell Universal connected to the same database. It requires either Git or managed deployments to share configuration data. We recommend this for widely used production instances. It provides the best performance, stability and redundancy.

This configuration can support hundreds of jobs per hour, thousands of API requests and many apps. The number of concurrent users will depend on the number of PSU servers in the cluster.

* 32 CPU
* 64 GB
* 1 TB
* MS SQL\PostgreSQL Database

## Software

### Windows

* Optional\*: [Windows PowerShell v5.1](https://www.microsoft.com/en-us/download/details.aspx?id=54616) or later
* Optional\*: PowerShell v7.2 or later
* .NET Framework v4.8.0 or later (only for Windows PowerShell)

### Linux

* Optional\*: PowerShell v7.2 or later
* Validated Distributions: Ubuntu 18.04 and 20.04

### Mac OS

* Optional\*: PowerShell v7.2 or later

{% hint style="info" %}
\*PowerShell Universal packages a version of the PowerShell SDK. If you do not have a version of PowerShell installed, the integrated versions of PowerShell will be used.
{% endhint %}

## Network

PowerShell Universal communicates on the port configured during installation and\or configuration.&#x20;

### Web Server Front End

* Default Port: 5000
* Typical Configured Ports: 443, 80

### TCP Backend

* Dynamically assigned local port on loopback&#x20;

### Database

* MS SQL: 1433
* PostgreSQL: 5432

### Agent&#x20;

* Web Server Front End Port, default 5000

### Git

* Standard HTTP Ports, typically 443

### Online Licensing

Online licensing requires access to www.ironmansoftware.com on port 443. Offline licenses do not require internet access.

### Proxy&#x20;

PowerShell Universal provides proxy configuration settings in the Settings \ General page. These are used for communication with remote git, database or internet services.

