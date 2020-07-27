---
description: This document outlines how to build custom Universal Dashboard components.
---

# Building Custom Components

Universal Dashboard is extensible and you can build custom JavaScript components and frameworks. This document will cover how to build custom components that integrate with the Universal Dashboard platform. 

## Technology Overview

Below is a list of some of the technologies used when building Universal Dashboard components. You will not need to be an expert to produce a component but should be aware of what to search when you encounter a problem. 

### React

Universal Dashboard's client-side application is built using the [React framework](https://reactjs.org/). React makes it easy to build components that update the DOM only when necessary and has a pretty robust ecosystem of users. It's one of the most popular JavaScript frameworks at the time of this writing. 

### Babel 

[Babel ](https://babeljs.io/)is a transcompiler for JavaScript. It works well with React and allows you to use modern constructs while compiling for backwards compatibility of browsers. Universal Dashboard uses Babel for it's core component frameworks. 

### Webpack

[Webpack](https://webpack.js.org/) is an asset bundler. It's extremely customizable and is responsible for turning your JSX files into a bundle that can then be distributed with Universal Dashboard components. 

## Structure

There are some basic parts to a Universal Dashboard component. You will need to understand the structure in order to successfully build your own. 

### PowerShell Module

Universal Dashboard custom components are PowerShell modules. They export functions that can be used to create the component when run within a dashboard. The PowerShell module is also responsible for registering the JavaScript assets with Universal Dashboard. 

### JavaScript Bundle

The JavaScript bundle is produced by the Webpack bundling process. It consists of one or more JS files that you will need to register with UD. 

### Example Component Module Structure

The most basic structure for a UD component module will include a single JavaScript file, a PSM1 file to export a function and register the JavaScript and a PSD1 module manifest.

```text
- UniversalDashboard.95
    - index.23adfdasf.js
    - UniversalDashboard.95.psd1
    - UniversalDashboard.95.psm1
```

## Step-By-Step

This following section will take you step-by-step through the different aspects of building a UD component. This assumes you are running PowerShell Universal 1.2 or later and using the PowerShell Universal Dashboard v3 framework. 

For a full example of a component, [click here](https://github.com/ironmansoftware/ud-95). 

### 1. Installing Dependencies

You will need to install the following dependencies before creating your component. 

* [NodeJS](https://nodejs.org/en/)
* [InvokeBuild](https://www.powershellgallery.com/packages/InvokeBuild/5.6.0)

### 2. Initialize the JavaScript Package

After installing Node, you will have access to the `npm` command. You will need to initialize the node package to start. This will create a `package.json` file in your directory. 

```text
npm init 
```

[Here is an example](https://github.com/ironmansoftware/ud-95/blob/master/package.json) `package.json` that you can also use as a starting point. 

### 3. Install JavaScript Packages

You will need several JavaScript packages to build your bundle. You will first want to install the dev dependencies. These are used to build your project.

```text
npm install @babel/core --save-dev
npm install @babel/plugin-proposal-class-properties --save-dev
npm install @babel/plugin-syntax-dynamic-import --save-dev
npm install @babel/polyfill --save-dev
npm install @babel/preset-env --save-dev
npm install @babel/preset-react --save-dev
npm install babel-loader --save-dev
npm install webpack --save-dev
npm install webpack-cli --save-dev
```

Next, you'll want to install the `universal-dashboard` package along with any other packages you wish to use in your component. We are using React95 in this example. We will build a control based on that library. 

```text
npm install universal-dashboard --save
npm install react95 --save
npm install styled-components --save
```

### 4. Configure Babel

You will need to create a `.babelrc` file to configure Babel for React.

```text
{
    "presets": ["@babel/preset-react"]
}
```

### 5. Configure Webpack

Webpack is extremely customizable and sometimes very hard to get right. Below is a basic `webpack.config.js` file you can use to configure Webpack. You can safely change the `ud95` entry key name and library value to one that matches your library. 

```text
var path = require('path');

var BUILD_DIR = path.resolve(__dirname, 'dist');

module.exports = (env) => {
  const isDev = env == 'development' || env == 'isolated';

  return {
    entry: {
      'ud95' : __dirname + '/index.js'
    },
    output: {
      library: "UD95",
      libraryTarget: "var",
      path: BUILD_DIR,
      filename: isDev ? '[name].bundle.js' : '[name].[hash].bundle.js',
      sourceMapFilename: '[name].[hash].bundle.map',
      publicPath: "/"
    },
    module : {
      rules : [
        { test: /\.(js|jsx)$/, exclude: [/node_modules/, /public/], loader: 'babel-loader'}
      ]
    },
    externals: {
      UniversalDashboard: 'UniversalDashboard',
      'react': 'react',
      'react-dom': 'reactdom'
    },
    resolve: {
      extensions: ['.json', '.js', '.jsx']
    }
  };
}
```

### 6. Component.jsx

Now you can build your first component. You will need to export a single function component from your component.jsx file. We suggest the use of functional React components rather than class-based React components. We need to wrap the component in withComponentFeatures to ensure the component has access to the Universal Dashboard platform features. 

```text
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

### 7. Index.js

Once your component is completed, you'll need to add it to an `index`.js file. The entry point for your library is the first place Webpack will look. It will discover all other components from import statements in your code. The index.js file is where you should register your components. You can use the `registerComponent` function to do so. 

```text
import { registerComponent } from 'universal-dashboard'
import UD95Button from './component';

registerComponent("ud95-button", UD95Button);
```

### 8. Bundle JavaScript

To bundle the JavaScript, run the following command to start webpack. This will output a file into the dist folder. 

```text
npm run build
```

### 9. PowerShell Script

Now you will need to create a PowerShell script that registers and creates your component. 

First, register the JavaScript with Universal Dashboard.

```text
$JsFile = Get-ChildItem "$PSScriptRoot\ud95.*.js"
$AssetId = [UniversalDashboard.Services.AssetService]::Instance.RegisterAsset($JsFile.FullName)
```

Next, create a function that returns a hashtable that defines which component we are creating and which props to set. 

The `type` property of your hashtable needs to match with the first parameter of `registerComponent` that you called in your JavaScript.  

```text
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

### 10. InvokeBuild \(optional\)

We suggest the use of InvokeBuild to create a build script to run all the steps of packaging and staging your module. The below build script deletes the dist folder, runs an NPM install to install packages, runs an NPM build to bundle the JavaScript and then copies the PS module to the dist folder. 

```text
task Clean {
    Remove-Item "$PSScriptRoot\dist" -Recurse -Force
}

task NpmInstall {
    & {
        $ErrorActionPreference = 'SilentlyContinue'
        
        Push-Location $PSScriptRoot
        npm install
        Pop-Location
    }
}

task NpmBuild {
    & {
        $ErrorActionPreference = 'SilentlyContinue'
        
        Push-Location $PSScriptRoot
        npm run build
        Pop-Location
    }
}

task Stage {
    Copy-Item "$PSScriptRoot\UniversalDashboard.95.*" "$PSScriptRoot\dist"
}

task . Clean, NpmInstall, NpmBuild, Stage
```

## Props

Props are values that are either passed from the PowerShell hashtable provided by the user or by the Universal Dashboard `withComponentsFeature` high-order function. 

### Standard 

The properties that you set in your hashtable in PowerShell will automatically be sent in as props to React component. 

For example, if you set the `text` property of the hashtable like this. 

```text
function New-UDText {
    param(
        [Parameter()]
        [string]$Text
    )
    
    @{
        type = "text"
        isPlugin = $true
        assetId = $AssetId 
        
        text = $Text
    }
}
```

Then you will have access to that prop in React. 

```text
import React from 'react';
import { withComponentFeatures } from 'universal-dashboard';

const UDText = props => {
    return <div>{props.text}</div>
}

export default withComponentFeatures(UDText);
```

### Endpoints

Endpoints are special in the way they are registered and the way that they are passed as props to your component. You will need to call `Register` on the endpoint in PowerShell and pass in the Id and PSCmdlet variables. 

```text
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

```text
New-UD95Button -Text 'Hello' -OnClick {
    Show-UDToast -Message 'Test' 
}
```

Universal Dashboard will automatically wire up the endpoint to a function within JavaScript. This means that you can use the props to call that endpoint.

Notice the `props.onClick` function call. This will automatically call the PowerShell script block on the server. 

```text
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

```text
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

## Publishing to the Marketplace

The [Universal Dashboard Marketplace](https://marketplace.universaldashboard.io/) is an aggregator of the PowerShell Gallery that lists Universal Dashboard components. The UD Marketplace automatically hooks into PowerShell Universal v1.3 or later where you can easily install additional components. 

To publish to the Marketplace, you simply need to publish to the PowerShell Gallery but include the `ud-component` tag in your module manifest. The marketplace syncs with the Gallery every hour and your component will be enabled for anyone to find after that. 



