# Variables

Variables allow for the global definition of variables that are available within scripts. You can also import secrets that are also available within scripts or as run as credentials. 

## Creating a Variable 

To create a variable, navigate to the Automation / Variables page. Click Add Variable to define a new variable. 

Standard variables are just name \ value pairs of strings. They will be added to your scripts before they are run. 

![&apos;](../.gitbook/assets/image%20%2812%29.png)

## Creating a Secret Variable

Secret variables are stored within the selected vault. The value of those variables are never stored within Universal. To define a new secret variable, click Add Variable on the variables page and select the Secret tab. 

From this dialog, you'll be able to define string and PSCredentials in the specified vault. 

![](../.gitbook/assets/image%20%289%29.png)

## Importing Secret Variables

You can also import pre-existing secrets as variables into Universal. The variable values are not imported but will be looked up during execution. Click the Import Secret button to import secrets. 





