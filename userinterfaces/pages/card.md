---
description: Card component for Pages.
---

# Card

Cards contain a title and content text.&#x20;

![A simple card on a page.](<../../.gitbook/assets/image (347).png>)

## Data Source

You can load data from an API endpoint or job. The data properties will be available as variables within your text.&#x20;

For example, if you may have an endpoint that returns data like the following.&#x20;

```powershell
@{
    FirstName = "Adam"
    LastName = "Driscoll"
}
```

You could then use the following variables within the title and content text.&#x20;

```
Hello, $FirstName $LastName! 
```
