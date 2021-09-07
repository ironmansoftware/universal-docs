---
description: A button that can be used to invoke a script or API.
---

# Button

## Invoke a Script with a Button

You can invoke a script with a button. This will allow you to specify arguments, environment and run as credentials for the script. 

Set the target of the button to script and select the script you would like to use. You can then select the environment and run as credentials. Finally, specify parameters to pass to the script. 

![](../../.gitbook/assets/image%20%28242%29.png)

Clicking the button will run the script and show a toast notification after the click. 

![](../../.gitbook/assets/image%20%28250%29.png)

## Invoke an API with a Button

Set the target to API and select the endpoint that you want to invoke. The endpoint must be a POST endpoint. Parameters can be specified. Parameters will be passed as part of a JSON object. 

![](../../.gitbook/assets/image%20%28241%29.png)

## Customize the Button 

Buttons support customizing the text and icon shown within the button.

![](../../.gitbook/assets/image%20%28249%29.png)

## Properties

| Property | Description | Available Since |
| :--- | :--- | :--- |
| Id | The ID of this component | 2.2.0 |
| Target Type | The type of target. Supports Script and API.  | 2.2.0 |
| Target | The script or API to invoke. | 2.2.0 |
| Run As | The run as credential to use when invoking a script. Not used for APIs. | 2.2.0 |
| Environment | The environment to run the script within. Not used for APIs. | 2.2.0 |
| Parameters | Name value pairs of parameters. For scripts, they are passed as parameters. For APIs, they are passed as a single JSON object. | 2.2.0 |
| Text | The text to display within the button | 2.2.0 |
| Icon | The icon to display within the button | 2.2.0 |
| Toast on Success | Shows a success toast message when the button successfully calls the target. | 2.2.0 |
| Toast on Error | Shows a failure toast message when the button fails to call the target. | 2.2.0 |
|  |  |  |

