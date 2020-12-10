# Timber Tailwind Starter

For Wordpress projects using a simple NPM script setup

## Links

- [Using Tailwind CSS In Your WordPress Theme](https://paulund.co.uk/using-tailwind-css-in-your-wordpress-theme)
- [Tailwind CSS with Timber for WordPress Theme Development](https://buildawesomewebsites.com/tailwind-css-with-timber-for-wordpress-theme-development/)
- [Twig for Timber cheatsheet](https://notlaura.com/the-twig-for-timber-cheatsheet/)
- [The power of extending Twig files](https://ffwagency.com/en-uk/learning/blog/power-extending-twig-templates)

## Setup

### Copy files from Timber starter theme

[The Timber Starter Theme](https://github.com/timber/starter-theme)

### Set up default package.json

`npm init -y`

### Install Tailwind and dependencies

`npm install tailwindcss postcss autoprefixer postcss-cli`

`npm install cross-env --save-dev`

### Add Tailwind as a PostCSS plugin

`touch postcss.config.js`

```
module.exports = {
  plugins: [
    require('tailwindcss'),
    require('autoprefixer'),
  ]
}
```

### Create Tailwind config file

`npx tailwind init`

And purge Twig files:

```
purge: [
  '**/*.twig',
],
```

### Setup CSS

The Timber starter theme has a "static" folder where we add CSS

`touch static/tailwind.css`

```
/*
 * Theme Name:
 * Theme URI: https://github.com/curiousways/
 * Author: Curious Ways
 * Description: A Wordpress site built with Wordpress and Timber
 * Version: 1.0
 * Text domain:
*/

@tailwind base;
@tailwind components;
@tailwind utilities;
```

### Set up NPM build scripts

Add to package.json

```
"scripts": {
  "watch": "cross-env NODE_ENV=development postcss static/css/tailwind.css -o style.css --watch",
  "build": "cross-env NODE_ENV=production postcss static/css/tailwind.css -o style.css"
},
```

Run scripts:

```
npm run build
npm run watch
```

### Extras

#### Add ACF JSON folder

`mkdir acf-json`

#### Enqueue assets example

```
// --------------------------------------------------
// Enqueue Assets
// --------------------------------------------------

function site_assets() {
  wp_enqueue_style( 'slick', get_template_directory_uri() . '/inc/slick/slick.css', 'all');
  wp_enqueue_script( 'slick', get_template_directory_uri() . '/inc/slick/slick.min.js', array('jquery'), '1.0.0', true );
  wp_enqueue_script( 'site-js', get_template_directory_uri() . '/dist/js/site.min.js', array('jquery'), '1.0.0', true );
  wp_enqueue_script( 'alpine', 'https://cdn.jsdelivr.net/gh/alpinejs/alpine@v2.3.5/dist/alpine.min.js', null, null, true );
  // wp_enqueue_style( 'typography-css', 'https://cloud.typography.com/7073312/6919812/css/fonts.css');
}
```