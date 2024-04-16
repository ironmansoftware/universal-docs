---
description: Migrate from PowerShell Universal v4 to v5.
---

# 🔁 Migration

## v5.0.0

### LiteDB Support

LiteDB is no longer supported in v5.0.0. You will need to transfer the following into a SQL, SQLite, or PostgreSQL database.&#x20;

* App Tokens
* Event Hub Sessions
* Job History
  * Jobs
  * Job Output
  * Job Feedback
* Identities
* Terminal History

#### Extracting LiteDB Data

#### Importing into SQLite

#### Importing into SQL

#### Importing into PostreSQL
