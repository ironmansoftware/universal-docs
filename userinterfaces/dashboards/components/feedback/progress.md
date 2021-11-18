---
description: Progress component for Universal Dashboard
---

# Progress

## Circular Progress

![](../../../../.gitbook/assets/image%20%2880%29.png)

```text
New-UDProgress -Circular -Color Blue
```

## Linear Indeterminate

![](../../../../.gitbook/assets/image%20%2862%29.png)

```text
New-UDProgress
```

## Linear Determinate

![](../../../../.gitbook/assets/image%20%2869%29.png)

```text
New-UDProgress -PercentComplete 75
```

**New-UDProgress**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| PercentComplete | Object | The percent complete for the progress. | false |
| BackgroundColor | DashboardColor | The background color. | false |
| ProgressColor | DashboardColor | The progress bar color. | false |
| Circular | SwitchParameter | Whether the progress is circular. | false |
| Color | String | The color of the progress. | false |
| Size | String | The size of the progress. | false |

