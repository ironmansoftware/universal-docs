---
description: psu is a command line utility for working with PowerShell Universal.
---

# psu Command Line Tool

`psu` is included with the PowerShell Universal installation media.

## admin

Admin account operations

### reset

Reset the local admin account password in the event of a lockout. The account will be `admin` with a password of `admin` .

{% code overflow="wrap" %}
```powershell
psu admin reset --connection-string 'Data Source=C:\ProgramData\UniversalAutomation\database.db'
```
{% endcode %}

| Argument            | Description                                            | Required |
| ------------------- | ------------------------------------------------------ | -------- |
| --connection-string | The database connection string                         | ✅        |
| --database-type     | PostgreSQL, SQL or SQLite (default)                    | ❌        |
| --encryption-key    | Database vault encryption key, if changed.             | ❌        |
| --password          | Database vault password, if changed.                   | ❌        |
| --key-size          | Database vault password key size, if changed from 128. | ❌        |

## db

Commands for working with the PowerShell Universal database.

### convert

Convert a v4 LiteDB Database to SQLite

```
psu db convert --path C:\ProgramData\UniversalAutomation\databased.db
```

| Argument | Description                         | Required |
| -------- | ----------------------------------- | -------- |
| --path   | The path of the database to convert | ✅        |

### schema

Migrate from one schema version to another. Migrating to lower versions can cause data loss. This can also be used to create a new database from scratch at the target schema.

```
psu db schema --connection-string 'Server=SQL;Data Source=PSU;Integrated Security=True' --schema-version 5.1.0 --database-type 'SQL'
```

| Argument            | Description                                       | Required |
| ------------------- | ------------------------------------------------- | -------- |
| --connection-string | Connection string to the database                 | ✅        |
| --target-version    | The database schema version. Defaults to "Latest" | ❌        |
| --database-type     | PostgreSQL, SQL or SQLite (default)               | ❌        |

### migrate

{% hint style="warning" %}
Converting one database type to another can be a problematic process and you may experience issues. It is better to choose the final database type at the type of the first installation. Be aware that SQLite does not scale; if you expect your instance to grow at a later time, you should choose another database type.
{% endhint %}

Migrates from one database to another. This command can migrate between database types.

```
psu db migrate --source-connection-string 'Server=SQL;Data Source=PSU;Integrated Security=True' -source-database-type 'SQL' --target-connection-string 'Server=PostgreSQL;Data Source=PSU;Integrated Security=True' --target-database-type 'PostgreSQL'
```

| Argument                   | Description                         | Required |
| -------------------------- | ----------------------------------- | -------- |
| --target-connection-string | Target database connection string   | ✅        |
| --source-connection-string | Source database connection string   | ✅        |
| --target-database-type     | PostgreSQL, SQL or SQLite (default) | ❌        |
| --source-database-type     | PostgreSQL, SQL or SQLite (default) | ❌        |

#### Migrating between versions

We recommend you update the schema of your database to the version you wish to migrate to before running the migration command to avoid differences in the schema.

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```powershell
# Update source schema version
psu db schema --connection-string 'Data Source=C:\ProgramData\UniversalAutomation\database.db' --database-type 'SQLite'
# Migrate to new data source
psu db migrate --source-connection-string 'Data Source=C:\ProgramData\UniversalAutomation\database.db' --target-connection-string 'Server=PostgreSQL;Data Source=PSU;Integrated Security=True' --target-database-type 'PostgreSQL'
```
{% endcode %}

## git

Commands for working with PSU git repositories. This command uses the internal git services to work with the local repository.

### clone

Clones a git repository using the git sync service.

```
psu git clone --url http://github.com/ironmansoftware/psu.git --path C:\ProgramData\UniversalAutomation\Repository --username 'adamdriscoll' --password 'gh__1234123' --branch main
```

| Argument   | Description                            | Required |
| ---------- | -------------------------------------- | -------- |
| --url      | The URL of the git remote.             | ✅        |
| --path     | The local path to clone to             | ✅        |
| --username | The user name for the remote.          | ❌        |
| --password | The password for the remote            | ❌        |
| --branch   | The branch to clone (default is main). | ❌        |

### pull

Pulls from a git remote. A clone will be called if the local repository does not exist.

```
psu git pull --url http://github.com/ironmansoftware/psu.git --path C:\ProgramData\UniversalAutomation\Repository --username 'adamdriscoll' --password 'gh__1234123' --branch main
```

| Argument   | Description                            | Required |
| ---------- | -------------------------------------- | -------- |
| --url      | The URL of the git remote.             | ✅        |
| --path     | The local path to clone to             | ✅        |
| --username | The user name for the remote.          | ❌        |
| --password | The password for the remote            | ❌        |
| --branch   | The branch to clone (default is main). | ❌        |

### push

Pushes to a git remote. The repository needs to be cloned first. Changes will not be staged during the push.

```
psu git push --url http://github.com/ironmansoftware/psu.git --path C:\ProgramData\UniversalAutomation\Repository --username 'adamdriscoll' --password 'gh__1234123' --branch main
```

| Argument   | Description                            | Required |
| ---------- | -------------------------------------- | -------- |
| --url      | The URL of the git remote.             | ✅        |
| --path     | The local path to clone to             | ✅        |
| --username | The user name for the remote.          | ❌        |
| --password | The password for the remote            | ❌        |
| --branch   | The branch to clone (default is main). | ❌        |
