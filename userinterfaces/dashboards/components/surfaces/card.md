---
description: Card component for Universal Dashboard
---

# Card

**Cards contain content and actions about a single subject.**

Cards are surfaces that display content and actions on a single topic. They should be easy to scan for relevant and actionable information. Elements, like text and images, should be placed on them in a way that clearly indicates hierarchy.

## Simple Card

Although cards can support multiple actions, UI controls, and an overflow menu, use restraint and remember that cards are entry points to more complex and detailed information.

![](<../../../../.gitbook/assets/image (76).png>)

```powershell
New-UDCard -Title 'Simple Card' -Content {
    "This is some content"
}
```

## Advanced Card

You can use the body, header, footer and expand cmdlets to create advanced cards. The below example creates a card with various features based on a Hyper-V VM.

```powershell
$Header = New-UDCardHeader -Avatar (New-UDAvatar -Content { "R" } -Sx @{ backgroundColor = "#f44336" }) -Action (New-UDIconButton -Icon (New-UDIcon -Icon 'EllipsisVertical')) -Title 'Shrimp and Chorizo Paella' -SubHeader 'September 14, 2016';
$Media = New-UDCardMedia -Image 'https://mui.com/static/images/cards/paella.jpg'
$Body = New-UDCardBody -Content {
    New-UDTypography -Text ' This impressive paella is a perfect party dish and a fun meal to cook together with your guests. Add 1 cup of frozen peas along with the mussels, if you like.' -Sx @{
        color = 'text.secondary'
    } -Variant body2
}
$Footer = New-UDCardFooter -Content {
    New-UDIconButton -Icon (New-UDIcon -Icon 'Heart')
    New-UDIconButton -Icon (New-UDIcon -Icon 'ShareAlt')
}
$Expand = New-UDCardExpand -Content {
    $Description = @"
    Heat oil in a (14- to 16-inch) paella pan or a large, deep skillet over
    medium-high heat. Add chicken, shrimp and chorizo, and cook, stirring
    occasionally until lightly browned, 6 to 8 minutes. Transfer shrimp to a
    large plate and set aside, leaving chicken and chorizo in the pan. Add
    pimentón, bay leaves, garlic, tomatoes, onion, salt and pepper, and cook,
    stirring often until thickened and fragrant, about 10 minutes. Add
    saffron broth and remaining 4 1/2 cups chicken broth; bring to a boil.
    New-UDTypography -Text $Description
}
New-UDCard -Header $Header -Media $Media -Body $Body -Footer $Footer -Expand $Expand -Sx @{
    maxWidth = 345
    border   = '2px solid #f0f2f5'
}
```

<figure><img src="../../../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

## API

* [New-UDCard](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDCard.txt)
* [New-UDCardBody](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDCardBody.txt)
* [New-UDCardExpand](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDCardExpand.txt)
* [New-UDCardFooter](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDCardFooter.txt)
* [New-UDCardHeader](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDCardHeader.txt)
* [New-UDCardMedia](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDCardMedia.txt)
