---
description: Time line control for PowerShell Universal Dashboard
---

# Timeline

The timeline control can be used to display a sequence of events over time.&#x20;

## Basic Timeline&#x20;

Create a basic timeline with information on both sides of the timeline.&#x20;

![](<../../../../.gitbook/assets/image (348) (1) (2) (1).png>)

```powershell
New-UDTimeline -Children {
    New-UDTimelineItem -Content {
        'Breakfast'
    } -OppositeContent {
        '7:45 AM'
    } 
    New-UDTimelineItem -Content {
        'Welcome Message'
    } -OppositeContent {
        '9:00 AM'
    }
    New-UDTimelineItem -Content {
        'State of the Shell'
    } -OppositeContent {
        '9:30 AM'
    }
    New-UDTimelineItem -Content {
        'General Session'
    } -OppositeContent {
        '11:00 AM'
    }
}
```

## Alternating Timeline

![](<../../../../.gitbook/assets/image (301).png>)

```powershell
New-UDTimeline -Children {
    New-UDTimelineItem -Content {
        'Breakfast'
    } -OppositeContent {
        '7:45 AM'
    } 
    New-UDTimelineItem -Content {
        'Welcome Message'
    } -OppositeContent {
        '9:00 AM'
    }
    New-UDTimelineItem -Content {
        'State of the Shell'
    } -OppositeContent {
        '9:30 AM'
    }
    New-UDTimelineItem -Content {
        'General Session'
    } -OppositeContent {
        '11:00 AM'
    }
} -Position alternate
```

## Colors

![](<../../../../.gitbook/assets/image (317) (1).png>)

```powershell
New-UDDashboard -Title 'PowerShell Universal' -Content {
        New-UDTimeline -Children {
            New-UDTimelineItem -Content {
                'Breakfast'
            } -OppositeContent {
                '7:45 AM'
            }  -Color 'error'
            New-UDTimelineItem -Content {
                'Welcome Message'
            } -OppositeContent {
                '9:00 AM'
            } -Color 'info'
            New-UDTimelineItem -Content {
                'State of the Shell'
            } -OppositeContent {
                '9:30 AM'
            } -Color 'success'
            New-UDTimelineItem -Content {
                'General Session'
            } -OppositeContent {
                '11:00 AM'
            } -Color 'grey'
        } -Position alternate
}
```

## Icons

![](<../../../../.gitbook/assets/image (310) (1).png>)

```powershell
New-UDTimeline -Children {
    New-UDTimelineItem -Content {
        'Breakfast'
    } -OppositeContent {
        '7:45 AM'
    }  -Icon (New-UDIcon -Icon Microsoft)
    New-UDTimelineItem -Content {
        'Welcome Message'
    } -OppositeContent {
        '9:00 AM'
    } -Icon (New-UDIcon -Icon Apple)
    New-UDTimelineItem -Content {
        'State of the Shell'
    } -OppositeContent {
        '9:30 AM'
    } -Icon (New-UDIcon -Icon NetworkWired)
    New-UDTimelineItem -Content {
        'General Session'
    } -OppositeContent {
        '11:00 AM'
    } -Icon (New-UDIcon -Icon User)
} -Position alternate
```

## API

* New-UDTimeline
* New-UDTimelineItem
