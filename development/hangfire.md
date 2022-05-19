---
description: Job execution engine information.
---

# Hangfire

[Hangfire](https://www.hangfire.io/) is the scheduling library that PowerShell Universal uses to execute and schedule jobs. It may be useful to view the status of the Hangfire job execution queues. This is typically useful if you have jobs that aren't running or schedules not starting at the proper times.&#x20;

You can access the Job Details dashboard by clicking the Job Details button in Settings \ General \ Diagnostics.&#x20;

![Job Details](<../.gitbook/assets/image (305).png>)

## Scheduled Jobs

Scheduled jobs will display jobs that you have scheduled yourself. You will see other jobs scheduled for internal tasks within PowerShell Universal.&#x20;

![Scheduled Jobs](<../.gitbook/assets/image (315) (1).png>)

## Jobs

You can use the Jobs tab to view jobs that are running, have executed or have failed. Jobs should typically not be marked as failed within Hangfire. This is a sign of an internal error within PowerShell Universal.&#x20;

![Jobs Tab](<../.gitbook/assets/image (313).png>)
