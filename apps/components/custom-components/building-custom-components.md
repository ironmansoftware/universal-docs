---
description: This document outlines how to build custom Universal app components.
---

# Building Custom JavaScript Components

Universal is extensible and you can build custom JavaScript components and frameworks. This document will cover how to build custom components that integrate with the Universal app platform.

{% hint style="warning" %}
This is an advanced topic and not required if you simply want to use Universal Apps.
{% endhint %}

{% hint style="info" %}
For a complete working example, see the [ud-mermaid](https://github.com/ironmansoftware/ud-mermaid) project on GitHub. This is a production-ready custom component that integrates the Mermaid diagramming library with PowerShell Universal.
{% endhint %}

## Overview

Building a custom React component for PowerShell Universal involves several key pieces:

1. **Project Structure**: A Node.js project with Webpack for bundling React components
2. **React Component (JSX)**: The React component that renders your UI
3. **PowerShell Module (PSM1)**: PowerShell functions that create component definitions
4. **Module Manifest (PSD1)**: Standard PowerShell module metadata
5. **Build Process**: Webpack configuration to bundle JavaScript assets
6. **Component Registration**: Registering your component with Universal Dashboard

### How It Works

The integration between PowerShell and React works like this:

1. **PowerShell Side**: Your PowerShell function returns a hashtable with component properties
2. **Asset Registration**: The bundled JavaScript is registered with PowerShell Universal's AssetService
3. **Component Type**: The `type` property links the PowerShell hashtable to the React component
4. **Prop Passing**: Hashtable properties automatically become React props
5. **Rendering**: Universal Dashboard loads the JavaScript bundle and renders the React component

```
PowerShell Function → Hashtable → Asset Service → React Component → DOM
```

### The ud-mermaid Example

Throughout this guide, we'll reference the [ud-mermaid](https://github.com/ironmansoftware/ud-mermaid) project as a real-world example. This component wraps the Mermaid.js diagramming library for use in PowerShell Universal, demonstrating:

- Third-party JavaScript library integration
- React hooks usage (useEffect, useRef)
- Configuration object passing
- Professional project structure
- Build automation

## Step-By-Step

This following section will take you step-by-step through the different aspects of building a Universal App component.

### 1. Installing Dependencies

You will need to install the following dependencies before creating your component.

* [NodeJS](https://nodejs.org/en/) - Required for npm and running build tools

### 2. Create a New Project

Create a new directory for your component project:

```powershell
New-Item -Path .\MyComponent -ItemType Directory
Set-Location .\MyComponent
```

Initialize a new npm project:

```powershell
npm init -y
```

This creates a basic project structure including:
- `package.json` - Node.js dependencies and build scripts

### 3. Install JavaScript Dependencies

Install the required build tools and React dependencies:

```powershell
npm install --save-dev @babel/core @babel/preset-env @babel/preset-react babel-loader webpack webpack-cli css-loader style-loader @babel/plugin-proposal-class-properties @babel/plugin-syntax-dynamic-import --legacy-peer-deps
```

Install the Universal Dashboard package:

```powershell
npm install universal-dashboard --legacy-peer-deps
```

For example, the [ud-mermaid](https://github.com/ironmansoftware/ud-mermaid) project includes the `mermaid` package as an additional dependency:

```json
"dependencies": {
    "mermaid": "^9.4.3",
    "universal-dashboard": "^1.0.1"
}
```

Install any additional libraries your component needs:

```powershell
npm install mermaid --legacy-peer-deps
```

### 4. Create Project Structure

Create the necessary directories for your component:

```powershell
New-Item -Path .\Components -ItemType Directory
```

### 5. Create Your React Component

Create a React component in the `Components/` directory. Your component should:

1. Import from `universal-dashboard` 
2. Use the `withComponentFeatures` HOC (Higher-Order Component)
3. Accept props that match your PowerShell function parameters

**Example from ud-mermaid** (`Components/mermaid.jsx`):

```jsx
import React, { useEffect, useRef } from 'react';
import { withComponentFeatures } from 'universal-dashboard';
import mermaid from 'mermaid';

const UDMermaid = (props) => {
  const mermaidRef = useRef(null);
  const { id, diagram, config } = props;

  useEffect(() => {
    mermaid.initialize(config || {});
    
    if (mermaidRef.current) {
      mermaidRef.current.removeAttribute('data-processed');
      mermaid.contentLoaded();
    }
  }, [diagram, config]);

  return (
    <div className="mermaid" id={id} ref={mermaidRef}>
      {diagram}
    </div>
  );
};

export default withComponentFeatures(UDMermaid);
```

### 6. Register Your Component

Create an `index.js` file in the `Components/` directory that registers your component with Universal Dashboard:

```javascript
import UDMermaid from './mermaid';
UniversalDashboard.register("ud-mermaid", UDMermaid);
```

The string you pass to `register()` becomes the `type` property you'll use in your PowerShell function.

### 7. Create PowerShell Functions

Now you will need to author the PowerShell module code. You will need to update the PSM1 file to load assets and define functions that create component definitions.

The PSM1 file should:

1. Register the bundled JavaScript file with the AssetService
2. Define functions that return hashtables with component properties

**Example from ud-mermaid** (`UniversalDashboard.Mermaid.psm1`):

```powershell
# Register JavaScript assets with PowerShell Universal
Get-ChildItem "$PSScriptRoot\*.js" | ForEach-Object {
    $Item = [UniversalDashboard.Services.AssetService]::Instance.RegisterAsset($_.FullName)
    if ($_.Name.StartsWith("index.") -and $_.Name.EndsWith(".bundle.js")) {
        $AssetId = $Item
    }
}

function New-UDMermaid {
    param(
        [Parameter()]
        [string]$Id = (New-Guid).ToString(),
        [Parameter(Mandatory)]
        [string]$Diagram,
        [Parameter()]
        [hashtable]$Config
    )

    @{
        assetId = $AssetId 
        isPlugin = $true 
        type = "ud-mermaid"  # This matches the name used in UniversalDashboard.register()
        id = $Id
        diagram = $Diagram
        config = $Config
    }
}
```

**Key hashtable properties:**
- `assetId` - The ID returned from RegisterAsset
- `isPlugin` - Always set to `$true` for custom components
- `type` - Must match the name you used in `UniversalDashboard.register()`
- `id` - A unique identifier for the component instance
- Additional properties are passed as props to your React component

### 8. Configure Webpack

Your `webpack.config.js` should bundle your components and externalize React and Universal Dashboard dependencies. Here's the essential configuration from ud-mermaid:

```javascript
module.exports = (env) => {
  return {
    entry: {
      'index': __dirname + '/components/index.js'
    },
    output: {
      path: BUILD_DIR,
      filename: '[name].[hash].bundle.js',
      library: 'udcomponent',
      libraryTarget: 'var'
    },
    module: {
      rules: [
        { test: /\.(js|jsx)$/, exclude: [/public/], loader: 'babel-loader' },
        { test: /\.css$/, loader: "style-loader!css-loader" }
      ]
    },
    externals: {
      'react': 'react',
      'react-dom': 'reactdom',
      UniversalDashboard: 'UniversalDashboard'
    },
    resolve: {
      extensions: ['.js', '.jsx']
    }
  };
}
```

**Important externals:**
- `react` and `react-dom` - Provided by PowerShell Universal
- `UniversalDashboard` - The Universal Dashboard global object

### 8.1. Configure Babel

Create a `.babelrc` file to configure JSX and modern JavaScript transformation:

```json
{
  "presets": [
    ["@babel/preset-env", {
      "targets": {
        "browsers": [">0.5%", "not dead"]
      }
    }],
    "@babel/preset-react"
  ],
  "plugins": [
    "@babel/plugin-proposal-class-properties",
    "@babel/plugin-syntax-dynamic-import",
    "@babel/plugin-proposal-optional-chaining",
    "@babel/plugin-proposal-nullish-coalescing-operator"
  ]
}
```

This configuration:
- Transforms JSX to JavaScript
- Transpiles modern JavaScript for browser compatibility
- Enables useful JavaScript language features

### 9. Create Module Manifest

Create a standard PowerShell module manifest (`.psd1`) with your component metadata:

```powershell
@{
    RootModule = 'UniversalDashboard.Mermaid.psm1'
    ModuleVersion = '1.0.0'
    Author = 'Your Name'
    Description = 'Custom component description'
    FunctionsToExport = @('New-UDMermaid')
}
```

### 10. Build The Project

You can now build your project. It will output a module you can load into PowerShell Universal.&#x20;

First, add build scripts to your `package.json`:

```json
"scripts": {
    "build": "webpack -p --env production",
    "dev": "webpack-dev-server --config webpack.config.js -p --env development"
}
```

Then run the build:

```powershell
npm run build
```

**Optional: Create a build script** (like ud-mermaid's `component.build.ps1`):

```powershell
# component.build.ps1
$OutputPath = "$PSScriptRoot\output"

Remove-Item -Path $OutputPath -Force -ErrorAction SilentlyContinue -Recurse
Remove-Item -Path "$PSScriptRoot\public" -Force -ErrorAction SilentlyContinue -Recurse

npm install --legacy-peer-deps
npm run build

New-Item -Path $OutputPath -ItemType Directory

Copy-Item $PSScriptRoot\public\*.* $OutputPath
Copy-Item $PSScriptRoot\UniversalDashboard.MyComponent.psd1 $OutputPath
Copy-Item $PSScriptRoot\UniversalDashboard.MyComponent.psm1 $OutputPath
```

Then run it:

```powershell
.\component.build.ps1
```

The build process:
1. Bundles all JavaScript/React code using Webpack
2. Outputs bundled files with hash names (e.g., `index.78a6d857.bundle.js`)
3. Copies module files (`.psm1`, `.psd1`) to the output directory

### 11. Use in PowerShell Universal

Within your app, load your module and execute the function.&#x20;

```powershell
Import-Module .\output\UniversalDashboard.Mermaid.psd1

New-UDApp -Content {
   New-UDMermaid -Diagram @"
graph TD
    A[Start] --> B[Process]
    B --> C[End]
"@
}
```

## Project Structure Example

Here's the typical structure of a custom component project (from [ud-mermaid](https://github.com/ironmansoftware/ud-mermaid)):

```
project/
├── Components/
│   ├── index.js              # Component registration
│   └── mermaid.jsx           # React component
├── output/                   # Build output (git ignored)
│   ├── index.[hash].bundle.js
│   ├── UniversalDashboard.Mermaid.psm1
│   └── UniversalDashboard.Mermaid.psd1
├── package.json              # Node.js dependencies
├── webpack.config.js         # Webpack configuration
├── component.build.ps1       # Optional build script
├── UniversalDashboard.Mermaid.psm1   # PowerShell module
└── UniversalDashboard.Mermaid.psd1   # Module manifest
```

## Props

Props are values that are either passed from the PowerShell hashtable provided by the user or by the Universal App `withComponentsFeature` high-order function.

### Standard

The properties that you set in your hashtable in PowerShell will automatically be sent in as props to React component.

For example, if you set the `diagram` and `config` properties in the hashtable:

```powershell
function New-UDMermaid {
    param(
        [Parameter()]
        [string]$Id = (New-Guid).ToString(),
        [Parameter(Mandatory)]
        [string]$Diagram,
        [Parameter()]
        [hashtable]$Config
    )

    @{
        type = "ud-mermaid"
        isPlugin = $true
        assetId = $AssetId 
        id = $Id
        diagram = $Diagram
        config = $Config
    }
}
```

Then you will have access to those props in React:

```javascript
import React, { useEffect, useRef } from 'react';
import { withComponentFeatures } from 'universal-dashboard';
import mermaid from 'mermaid';

const UDMermaid = (props) => {
  const { id, diagram, config } = props;

  useEffect(() => {
    mermaid.initialize(config || {});
  }, [diagram, config]);

  return <div className="mermaid" id={id}>{diagram}</div>;
};

export default withComponentFeatures(UDMermaid);
```

**Best Practices for Props:**
- Use descriptive prop names that match PowerShell parameter names
- Handle optional props with default values or conditional logic
- Hashtables in PowerShell become JavaScript objects automatically

### React Hooks and Component Lifecycle

When building custom components, you can use all standard React hooks. The ud-mermaid component demonstrates using `useEffect` and `useRef` for managing component lifecycle and DOM references:

```javascript
import React, { useEffect, useRef } from 'react';

const UDMermaid = (props) => {
  const mermaidRef = useRef(null);
  const { diagram, config } = props;

  // Run when diagram or config changes
  useEffect(() => {
    mermaid.initialize(config || {});
    
    if (mermaidRef.current) {
      mermaidRef.current.removeAttribute('data-processed');
      mermaid.contentLoaded();
    }
  }, [diagram, config]); // Dependency array

  return <div ref={mermaidRef}>{diagram}</div>;
};
```

**Common patterns:**
- `useEffect` - For initialization, cleanup, and responding to prop changes
- `useRef` - For accessing DOM elements directly
- `useState` - For managing internal component state
- `useMemo` / `useCallback` - For performance optimization

### Endpoints

Endpoints are special in the way they are registered and the way that they are passed as props to your component. You will need to call `Register` on the endpoint in PowerShell and pass in the Id and PSCmdlet variables.

```powershell
function New-UD95Button {
    param(
        [Parameter()]
        [string]$Id = [Guid]::NewGuid(),
        [Parameter()]
        [string]$Text,
        [Parameter()]
        [Endpoint]$OnClick
    )

    if ($OnClick)
    {
        $OnClick.Register($Id, $PSCmdlet)
    }

    @{
        type = "ud95-button"
        isPlugin = $true 
        assetId = $AssetId

        id = $Id 
        text = $Text 
        onClick = $OnClick
    }
}
```

Endpoints are created from ScriptBlocks and are executed when that event happens.

```powershell
New-UD95Button -Text 'Hello' -OnClick {
    Show-UDToast -Message 'Test' 
}
```

Universal will automatically wire up the endpoint to a function within JavaScript. This means that you can use the props to call that endpoint.

Notice the `props.onClick` function call. This will automatically call the PowerShell script block on the server.

```javascript
import React from 'react';
import { withComponentFeatures } from 'universal-dashboard';
import { Button } from 'react95';

const UD95Button = props => {

    const p = {
        onClick: () => props.onClick()
    }

    return <Button {...p}>{props.text}</Button>
}

export default withComponentFeatures(UD95Button);
```

### setState

The `setState` prop is used to set the state of the component. This ensures that the state is tracked and your component will work with `Get-UDElement`.

For example, with a text field, you'll want to call `props.setState` and pass in the new text value for the state.

```javascript
const UDTextField = (props) => {
    const onChange = (e) => {
        props.setState({value: e.target.value})
    }

    return <TextField  {...props} onChange={onChange} />
}

export default withComponentFeatures(UDTextField);
```

### children

The `children` prop is a standard React prop. If your component supports child items, such as a list or select box, you should use the standard `props.children` prop to ensure that the cmdlets `Add-UDElement` , `Remove-UDElement` and `Clear-UDElement` function correctly.

## Troubleshooting and Debugging

### Common Issues

**Component not rendering:**
1. Verify the `type` in your PowerShell function matches `UniversalDashboard.register()` name
2. Check that the asset is properly registered with AssetService
3. Ensure `isPlugin` is set to `$true`
4. Confirm the bundled JavaScript file exists in the module directory

**Props not passing correctly:**
1. Verify property names match between PowerShell hashtable and React component
2. Check browser console for JavaScript errors
3. Use React DevTools to inspect component props

**Build failures:**
1. Run `npm install --legacy-peer-deps` to ensure dependencies are installed
2. Check for syntax errors in JSX files
3. Verify webpack.config.js externals are correctly configured
4. Ensure babel is configured properly for JSX transformation

### Debugging Tips

**Browser Console:**
Open browser developer tools (F12) to see JavaScript errors and warnings.

**React DevTools:**
Install React DevTools browser extension to inspect component hierarchy and props.

**PowerShell Debugging:**
Use `Write-Host` or `Write-Debug` in your PowerShell functions to trace execution.

**Webpack Dev Server:**
During development, use webpack-dev-server for hot reloading:

```powershell
npm run dev
```

Then configure PowerShell Universal to load from the dev server URL.

## Example: Complete Component Workflow

Here's a complete example based on the [ud-mermaid](https://github.com/ironmansoftware/ud-mermaid) project:

**1. Create React component** (`Components/mermaid.jsx`):
```jsx
import React, { useEffect, useRef } from 'react';
import { withComponentFeatures } from 'universal-dashboard';
import mermaid from 'mermaid';

const UDMermaid = (props) => {
  const mermaidRef = useRef(null);
  const { id, diagram, config } = props;

  useEffect(() => {
    mermaid.initialize(config || {});
    if (mermaidRef.current) {
      mermaidRef.current.removeAttribute('data-processed');
      mermaid.contentLoaded();
    }
  }, [diagram, config]);

  return <div className="mermaid" id={id} ref={mermaidRef}>{diagram}</div>;
};

export default withComponentFeatures(UDMermaid);
```

**2. Register component** (`Components/index.js`):
```javascript
import UDMermaid from './mermaid';
UniversalDashboard.register("ud-mermaid", UDMermaid);
```

**3. Create PowerShell function** (`UniversalDashboard.Mermaid.psm1`):
```powershell
Get-ChildItem "$PSScriptRoot\*.js" | ForEach-Object {
    $Item = [UniversalDashboard.Services.AssetService]::Instance.RegisterAsset($_.FullName)
    if ($_.Name.StartsWith("index.") -and $_.Name.EndsWith(".bundle.js")) {
        $AssetId = $Item
    }
}

function New-UDMermaid {
    param(
        [Parameter()]
        [string]$Id = (New-Guid).ToString(),
        [Parameter(Mandatory)]
        [string]$Diagram,
        [Parameter()]
        [hashtable]$Config
    )

    @{
        assetId = $AssetId 
        isPlugin = $true 
        type = "ud-mermaid"
        id = $Id
        diagram = $Diagram
        config = $Config
    }
}
```

**4. Build and test**:
```powershell
# Build
npm run build

# Test in PowerShell Universal
Import-Module .\output\UniversalDashboard.Mermaid.psd1

New-UDApp -Content {
    New-UDMermaid -Diagram @"
graph TD
    A[Christmas] -->|Get money| B(Go shopping)
    B --> C{Let me think}
    C -->|One| D[Laptop]
    C -->|Two| E[iPhone]
    C -->|Three| F[Car]
"@
}
```

## Additional Resources

- **ud-mermaid GitHub Repository**: [https://github.com/ironmansoftware/ud-mermaid](https://github.com/ironmansoftware/ud-mermaid) - Complete working example
- **React Documentation**: [https://react.dev](https://react.dev)
- **Webpack Documentation**: [https://webpack.js.org](https://webpack.js.org)