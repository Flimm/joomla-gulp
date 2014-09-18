# Gulp build system for Joomla!

Develop faster

1. [What is this?](#whats-this)
2. [How does it work?](#how-works)
3. [Install](#install)
    1. [Clone this repo in your project](#clone)
    2. [Install node.JS](#install-node)
    3. [Install Gulp](#install-gulp)
    4. [Initialise your project's package.json file](#initialise-package)
    5. [Install joomla-gulp requirements](#install-joomla-gulp)
    6. [Install your favorite Gulp plugins](#install-gulp-plugins)
    7. [Create your joomla-gulp-extensions folder](#create-gulp-extensions)
    8. [Create your config](#create-config)
    9. [Create your gulpfile.js](#create-gulpfile)
    10. [Start writing extensions](#start-writing-extensions)
4. [Naming conventions](#naming.conventions)

## <a name="whats-this"></a>1. What is this?

Most Joomla! extensions out there still use a [Phing](http://www.phing.info/) based build system that makes the job but without using the latest technologies. [Gulp](http://gulpjs.com/) is a modern [Node.JS](http://nodejs.org/) based build system incredibly fast and easy to understand because it uses javascript code.

### <a name="plugins"></a>Some of the cool plugins available for Gulp:

* Compile LESS ([gulp-less](https://github.com/plus3network/gulp-less)) & Sass ([gulp-sass](https://www.npmjs.org/package/gulp-sass)) files on the fly
* Minify CSS ([gulp-minify-css](https://www.npmjs.org/package/gulp-minify-css)), JS ([gulp-uglify](https://www.npmjs.org/package/gulp-uglify)) files on the fly
* Concatenate files ([gulp-concat](https://www.npmjs.org/package/gulp-concat)) to mix various resources (i.e. CSS files) into one single file (and HTTP request)
* Run [CodeSniffer](http://pear.php.net/package/PHP_CodeSniffer/redirected) validations ([gulp-phpcs](https://github.com/JustBlackBird/gulp-phpcs))
* Run [JSHint](http://www.jshint.com/) validations ([gulp-jshint](https://www.npmjs.org/package/gulp-jshint))
* Run [CoffeeScript](http://coffeescript.org/) validations ([gulp-coffee](https://www.npmjs.org/package/gulp-coffee))
* Reload your browser automatically when you edit any file (including php, sass, less, js... ) ([browser-sync](http://www.browsersync.io/docs/gulp/)).
* Minify the size of the images ([gulp-imagemin](https://www.npmjs.org/package/gulp-imagemin)) on the fly.

These are mainly the tools I use and the tools I think we should move forward but are you missing something? Suggest it!

## <a name="how-works"></a>2. How does it work?

This is a reusable base Gulp system for Joomla! extension development. Do not expect something magical here except that and task naming conventions. This repo is just a base system to allow you to add your extensions build scripts in a standard way so you can focus on the project specific stuff. 

This base build system does not depend on any project structure because you specify it on your extension build scripts.

The main idea of this build system is that you always develop your extensions within your extensions main folder (your project's repository). The build system copies files to your test site and reloads your browser when anything that you want to watch changes. It's easy to adapt to any workflow (like symblink folders) but it's not the native way it works.

## <a name="install"></a>3. Install

### <a name="clone"></a>3.1. Clone this repo in your project

In your project's root:

`git clone git@github.com:phproberto/joomla-gulp.git`

### <a name="install-node"></a>3.2. Install node.js

I won't extend here. Visit http://nodejs.org/ or search google.

### <a name="install-gulp"></a>3.3. Install Gulp
Install Gulp globally so it's available in all your projects:  
`sudo npm install -g gulp`  

Install Gulp on your project's folder:  
`npm install --save-dev gulp`  

### <a name="initialise-package"></a>3.4. Initialise your project's package.json file

On your project's folder run:

`npm init`

That will create a package.json file with the information that you provide.  

### <a name="install-joomla-gulp"></a>3.5. Install joomla-gulp requirements

This project only has 3 dependencies. You can install them from your project's root:

`npm install browser-sync --save-dev`  
`npm install gulp-zip --save-dev`  
`npm install require-dir --save-dev`  

### <a name="install-gulp-plugins"></a>3.6. Install your favorite Gulp plugins

I recommend you to look at this [readme's list of available extensions](#plugins). to start with. You can install any of them with:

`npm install {EXTENSION} --save-dev`

For example to install the Sass compiler:

`npm install gulp-sass --save-dev`

### <a name="create-gulp-extensions"></a>3.7. Create your joomla-gulp-extensions folder

Copy the `joomla-gulp-extensions-sample` folder inside this repo into your project's root folder and rename it to `joomla-gulp-extensions`. That folder contains a sample  structure.  

Note: You can rename folders to anything you want. For example I prefer to use `gulp` instead of `joomla-gulp` (I clone it directly to the `gulp` folder) and I use `gulp-extensions` instead of `joomla-gulp-extensions`. You only have to ensure that your `gulpfile.js` require dirs point to the right folders.

### <a name="create-config"></a>3.8. Create your config file

Copy the file `gulp-config.json.sample` into your project's root folder and rename it to `gulp-config.json` and customise the params inside to fit your project requirements.

#### Configuration options

* **wwwDir**           : The local folder where your website is hosted  
* **browserSyncProxy** : The host to use for browser-sync. You can create a virtualhost or directly use localhost.  
* **extensions**       : Object containing the list of extensions available on your repository  

Sample extensions definition:

```
	"extensions"       : {
		"components" : ["content"],
		"libraries"  : ["joomla"],
		"media"      : ["joomla"],
		"modules"    : {
			"backend"        : ["quickicon"]
			"frontend"       : ["latest-articles"]
		},
		"plugins"    : {
			"authentication" : ["joomla"],
			"content"        : ["emailcloak"],
			"system"         : ["languagecode"]
		},
		"templates"  : {
			"frontend"       : ["tudomus"]
		}
	}
```