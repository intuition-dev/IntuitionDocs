
# Metabake

## 'All my friends KNOW the low-coder'

#### Metabake is open source and extensible low-code productivity tool for programmers.

## Overview

Metabake(mbake) provides all the necessary tools for a developer to write cleaner code faster, with `pug` templating and livereload out of the box.

You can gradually adopt it while it allows you to develop faster - and with clean simplicity - Static Websites, Web Components, custom CMS/E-Commerce, CRUD and all sorts of dynamic web-apps.

### Prerequisites

You should know HTML, CSS and JavaScript - that is all we use. If you need to catch up, we recommend this book: 'Design and Build Websites' by Jon Duckett.


## Quick start
```sh
yarn global add mbake
mbake -w . /* for a base website */
cd website
mbakeX -w . /* to run the watcher/livereload */
```


## Metabake in 4 Minutes

Building sites take a few moments, just add `index.pug` and `dat.yaml` files in the folder, and compile it with `mbake .` from the root folder of your site.


### Example
Create a folder called 'one'.
In the folder 'one', create file index.pug

```pug

header
body
   p Hello #{key1}

```

and create file dat.yaml
```yaml
key1: World
```
> Note: to create a new page|screen in mbake, create a new folder with an index.pug and day.yaml in each folder.


### Now make with mbake:

```sh
mbake .
```

This will create `index.html`. Of course you can use regular Pug syntax to include other Pug files or Markdown. (Metabake Markdown flavor includes CSS support):
```pug
body
   div
      include:metaMD comment.md
```

And example Markdown file with CSS nested classes. Title is nested in 2 levels, .column class CSS and second level .stick CSS class
```
:::: column col-2
::: stick
Title 
:::
::::

```



So if you write a Markdown file comment.md, it will be included in index.html
---


### Watcher

This will start a webserver and auto-refresh browser, and watch for file changes to auto build:
```sh
mbakeX -w .
```

Instead of `.` you can specify any path.
Also, the fact that we are generating this static content allows us to have the entire webapp served by a CDN


## SASS
CSS can be hard to work with, so people use Sass/Scss. Create a `style.scss` file:
```css
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
   font: 100% $font-stack;
   color: $primary-color;
}
```
Create file `assets.yaml` in assets folder, to compile your scss to css

```
css:
- style.scss
```

and run
```sh
mbake -s .
```

It will create a css file in `assets/css` with auto-prefixes.

So the structure of asset folder should look something like that:
```folder
assets/
   css/style.css /* this is going to be compiled from style.scss */
   scss/style.scss /* your working area */
   assets.yaml /* with `scss` files that need to be compiled */
	...
```

## TypeScript

TypeScript is supper-set of JavaScript. Write a ts file, like foo.ts:
```ts
foo(i:number) {
	console.log('oh hi')
}
```

and run
```sh
mbake -t .
```

It will create a `.js` and `min.js` files. It will output ES5 to support IE11, so feel free to use class { } syntax.
If there is no `.ts`, than it will simply slightly mimifify js files into min.js (but no ES5 conversion).


## Examples - Website

There are 12 very different examples included in the mbake CLI. One is just a website:
```sh
mbake -w
```

That will extract an example website in the current folder. ( Obviously you can create any layout with any combination of css and other libraries, but here is how we laid out an example/starter website).


## Dynamic data/CRUD/'ViewModel'

This relates to dynamic data, not static content (static eg: CMS or eCommerce). To extract an example CRUD web-app in the current folder:

```sh
mbake -u
```

It has a README.md in root of the website that you can glance.


## CMS/Itemize example

### Itemize (eg CMS)

Lets build a folder called `Items` and in that folder create a blank file `dat_i.yaml,` with nothing there.
- In the folder called `Items` create folder `Page1` and folder `Page2`. In each page folder create `index.pug` and `dat.yaml`. So you have `Page1` and `Page2` folder under `Items`.

- In each Page's `dat.yaml` add
```
title: Page name
```
And add a few more key/value words in each dat.yaml, but make each pages values a bit different.

- And now, in the folder `Items` run

```sh
mbake -i .
```
It will create `items.json`. This allows you to fetch that json and search for content, CMS, items, etc.

# Todo
