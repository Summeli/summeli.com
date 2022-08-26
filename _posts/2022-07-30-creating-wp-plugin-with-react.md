---
layout: post
title: "Creating a Wordpress plugin with react"
author: Summeli
description: "Creating a Wordpress plugin with create react-app and craco"
categories:
    - wordpress
tags:
    - wordpress
    - wordpressplugin
    - php
    - react
---

This is a quick description how to create a wordpress plugin with create react-app

I divided the plugin in two parts, the plugin, and the react-app. The react-app is copyed from build directory into the wordpress plugin.

## Create Wordpress plugin

```php
<?php
/**
 * Plugin Name: Myapp React Plugin
 * Description: Experimental wordpress plugin withg react
 * Version: 1.0.0
 */

function myapp_shortcode() {

	return '<div id="myapp-react" ></div>';
}

add_shortcode('myapp-react', 'myapp_shortcode');

function myapp_load_assets() {
	
	$react_app_js  = plugin_dir_url( __FILE__ ) . 'app/static/js/myapp.js';
    $react_app_css = plugin_dir_url( __FILE__ ) . 'app/static/css/myapp.css';	
      
    // time stops stylesheet/js caching while in development, might want to remove later
    $version = time();	
    wp_enqueue_script( 'myapp-react', $react_app_js, array(), $version, true );         
    wp_enqueue_style( 'myapp-react', $react_app_css, array(), $version );
}

add_action( 'wp_enqueue_scripts', 'myapp_load_assets' );
?>
```

## Create React app
Just run create react-app with your own style:

```bash
yarn create react-app my-app --template typescript
```

### configuring the app with craco

In the plugin above we're using div 'myapp-react', and we should use the same in the react-app.

So let's change the index.tsx to the following
```typescript

const root = ReactDOM.createRoot(
  document.getElementById('myapp-react') as HTMLElement
);
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```
We can also change the root-div from index.html if we want to run the app in the "normal developement mode also"

### Building the app as single file
In wp plugin we used the myapp.js and myapp.css files, so we should make the build produce only these two files to keep the wordpress development easy, and simple. 

In this example I'm using craco (Create React App Configuration Override)

Add craco to the project:
```bash
yarn add @craco/craco   
```

Afer installation let's create craco.confix.js
```js
// craco.config.js
module.exports = {
    webpack: {
      configure: {
        output: {
          filename: "static/js/myapp.js",
        },
        optimization: {
          runtimeChunk: false,
          splitChunks: {
            chunks(chunk) {
              return false;
            },
          },
        },
      },
    },
    plugins: [
      {
        plugin: {
          overrideWebpackConfig: ({ webpackConfig }) => {
            webpackConfig.plugins[5].options.filename = "static/css/myapp.css";
            return webpackConfig;
          },
        },
        options: {},
      },
    ],
  };
```

then we can just add a new build target to the package.json like this:
```js
 "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "build:wp": "craco build"
```

Now running 
```bash
yarn build:wp 
```
will build the app as two files myapp.js, and myapp.css. We can later copy them into the wordpress directory to get the app to bind with new plugin.

## Running it
Now we can just add the plugin in wordpress admin console, and use the shorcode to add the app into a wordpress page. Enjoy! 

### Load the component with wordpress
The react-app can be now loaded from wordpress with shorcode 'myapp-react'

### Developing the app
We can still develop the app with normal react way, by running yarn start, and writing some code.

## Rerences
[https://www.green-box.co.uk/create-a-wordpress-plugin-that-uses-a-react-app/](https://www.green-box.co.uk/create-a-wordpress-plugin-that-uses-a-react-app/)
![]()