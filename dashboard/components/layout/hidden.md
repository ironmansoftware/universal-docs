# Hidden

Quickly and responsively toggle the visibility value of components and more with the hidden utilities.

## How it works

Hidden works with a range of breakpoints e.g. `xsUp` or `mdDown`, or one or more breakpoints e.g. `-Only 'sm'` or `-Only @('md', 'xl')`. Ranges and individual breakpoints can be used simultaneously to achieve very customized behavior. The ranges are inclusive of the specified breakpoints.

```text
innerWidth  |xs      sm       md       lg       xl
            |--------|--------|--------|--------|-------->
width       |   xs   |   sm   |   md   |   lg   |   xl

smUp        |   show | hide
mdDown      |                     hide | show
```

## Up

 Using any breakpoint `-Up` parameter, the given _children_ will be hidden _at or above_ the breakpoint.

```text
New-UDHidden -Up xl -Content {
    New-UDTypography 'xl'
}
```

## Down

 Using any breakpoint `-Down` parameter, the given _children_ will be hidden _at or below_ the breakpoint.

```text
New-UDHidden -Down xs -Content {
    New-UDTypography 'xs'
}
```

## Only

Using the breakpoint `-Only` parameter, the given _children_ will be hidden _at_ the specified breakpoint\(s\).

The `-Only` parameter can be used in two ways:

* list a single breakpoint
* list an array of breakpoints

```text
New-UDHidden -Only 'sm' -Content {
    New-UDTypography 'sm'
}
New-UDHidden -Only @('sm', 'xl') -Content {
    New-UDTypography 'sm,xl'
}
```

