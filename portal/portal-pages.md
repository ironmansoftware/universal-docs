---
description: Pages in the portal.
---

# Portal Pages

Portal pages contain one or more portal widgets. Each widget on a portal page can be resized and may accept properties to configure the widget's behavior. Widget's are self contained UI elements that provide features without the need to write code.&#x20;

{% hint style="info" %}
Portal Pages are currently in preview.
{% endhint %}

## Creating a Page

You can create a portal page by navigating to Portal \ Pages in the Admin Console's menu. Next, click Create New Portal Page.&#x20;

## Editing a Page

Click the view button for the page in order to begin editing the content of the page. Once viewing the page, you can click Edit to enter edit mode.&#x20;

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>Edit Page Button</p></figcaption></figure>

### Adding Widgets

To add an UI element to the page, click Add Widget to select from a list of Widgets to add to the page.&#x20;

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption><p>Adding a Portal Widget. </p></figcaption></figure>

If you do not have widgets shown in the modal, you can add pre-made ones to your environment using the [library](../platform/library.md). Once you find the Portal Widget to add, click the Add button under the description.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption><p>Portal Widget Modal</p></figcaption></figure>

Doing so will add the Portal Widget to the page.&#x20;

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption><p>Portal Widget on Portal Page</p></figcaption></figure>

### Configuration Portal Widgets

Portal Widgets can contain properties that change the behavior of the UI element. In most cases, a default value will be defined so a UI element is shown. Click the Properties button to view the properties for the widget.

All widgets have a height and width property that can be set. By default, the widget will span 100% of the page and take up as much height as is necessary to show the content of the widget.&#x20;

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption><p>Widget Properties</p></figcaption></figure>

### Positioning Portal Widgets

Portal Pages use a grid system to lay out Portal Widgets. Each row has 24 possible columns. You can use the widget's width property to define how many of the columns the widget will span. For example, you can place 2 widgets side by side by setting both of their widths to 12.&#x20;

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>Side by side Portal Widgets</p></figcaption></figure>

You can use the positional buttons on the button of the Portal Widget card to move the widget between rows and change the order of the columns.&#x20;

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p>Portal Widget Movement Controls</p></figcaption></figure>

The blue border around the widgets indicates their size and position. The outer blue border is representative of the row the widgets are currently positioned in. The inner blue border is the size and position of the widget itself.&#x20;

### Saving a Page

Once you have completed your changes to the contents of the page. Click the Save button to persist any changes to the Repository.&#x20;

## Role-Based Access

Pages can be assigned to users based on their role. Use the Page's properties to assign these roles. Users with the Pages assigned will see the pages on their Portal.&#x20;

## Permissions

Permission related to pages. See [Permissions ](../config/security/permissions.md)for information on how these values are used.&#x20;



| Identifier     | Description                                                  |
| -------------- | ------------------------------------------------------------ |
| portal         | Configuration access to the Portal, Portal Pages and Widgets |
| portal.pages   | Configuration access to Portal Pages                         |
| portal.widgets | Configuration access to Portal Widgets                       |
