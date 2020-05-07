# Execution Engine

## Job Scheduling

The job execution engine is driven by [Hangfire](https://www.hangfire.io/). It's a job library for .NET that provides the ability to schedule jobs, retry jobs and scale horizontally with multiple agents. Eventually, UA will take more advantage of the features of [Hangfire](https://www.hangfire.io/).

## Execution

Jobs in UA are run in an out-of-process PowerShell host. Depending on the version of PowerShell that is run, either PowerShell.exe or Pwsh.exe will be run. A custom PowerShell host is loaded into the PowerShell process to listen for output, input requests and to provide the ability to interact with the host from the job engine.

Using [gRPC](https://grpc.io/), the job engine can communicate between the job scheduling process and the independent PowerShell hosts. By keeping the processes isolated, they will not conflict with each other.

