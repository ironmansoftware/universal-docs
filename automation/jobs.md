# Jobs

Jobs are the result of running a script. Jobs are retained based on the script and server level settings.  

## Viewing Jobs 

Jobs can be viewed by clicking the Automation / Jobs page. Click the View button to navigate to the job. Jobs in progress can also bee cancelled. 

![](../.gitbook/assets/image%20%289%29.png)

### View Job Output

Standard job output is shown on the Output Tab of the job page. This should contain text from various PowerShell streams. 

![](../.gitbook/assets/image%20%285%29.png)

### View Job Pipeline Output

Pipeline output for jobs are also stored within UA. Any object that is written to the pipeline is stored as CliXml and available for view within the Pipeline Output tab. 

You can expand the tree view to see the objects and properties from the pipeline. 

![](../.gitbook/assets/image%20%2811%29.png)

### Viewing Errors

Any errors written to the error stream will be available on the Error tab within the job page. 

![](../.gitbook/assets/image%20%2813%29.png)

## Feedback 

Some jobs will require feedback. Any script that contains a Read-Host call will wait until there is user interaction with that job. The job will be in a Waiting for Feedback state and you can respond to that feedback by click the Response to Feedback button on the job page. 

![](../.gitbook/assets/image%20%287%29.png)

