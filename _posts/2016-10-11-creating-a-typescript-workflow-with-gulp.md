---
layout: post
title: Creating a TypeScript Workflow with Gulp
categories:
- blog
---

## Creating the Application Folders and Files

1. Create a new folder where your project code will live. You can name it anything you’d like but I’ll call it **typescriptDemo** in this post.
2. Create the following folders inside of typescriptDemo:
	- src
	- src/app
	- src/js

3. Open a command-prompt in the root of the typescriptDemo folder and run the following npm command (you’ll need to have Node.js installed) to create a file named package.json.

	**npm init**

4. Answer the questions that are asked. For this example you can go with all of the defaults it provides. After completing the wizard a new file named **package.json** will be added to the root of the folder.
Create the following files in the typescriptDemo folder:
 - gulpfile.js
 - gulpfile.config.js
 - tslint.json

## Installing Gulp, Gulp Modules and TSD

1. Now let’s get Gulp installed globally on your machine. Open a command-prompt and run the following command:

	**npm install gulp –g**

2. Open **package.json** and add the following **devDependencies** property into it. The location of the property in the file doesn’t really matter but I normally put it at the bottom.

	**Note:** The module versions shown here will certainly change over time. You can visit http://npmjs.org to find the latest version of a given module.

```json
"devDependencies": {
	    "gulp": "^3.8.11",
	    "gulp-debug": "^2.0.1",
	    "gulp-inject": "^1.2.0",
	    "gulp-sourcemaps": "^1.5.1",
	    "gulp-tslint": "^1.4.4",
	    "gulp-typescript": "^2.5.0",
	    "gulp-rimraf": "^0.1.1"
	}
```

3. Ensure that your command window path is at the root of the **typescriptDemo** folder and run the following command to install the dependencies:

	**npm install**

4. The http://definitelytyped.org site provides a Node.js module named **tsd** that can be used to install TypeScript type definition files that are used to provide enhanced code help in various editors. Install the **tsd** module globally by running the following command:

	**npm install tsd@next -g**

5. Run the following command:

	**tsd init**

6. Open the **tsd.json** file that is generated in the root of **typescriptDemo** and change the following properties to include “tools” in the path as shown next:

	**"path": "tools/typings",**
	**"bundle": "tools/typings/tsd.d.ts"**

7. Let’s use **tsd** to install a TypeScript definition file for Angular (an angular.d.ts file) and update the **tsd.json** file with the Angular file details as well. Run the following command:

	**tsd install angular --save**

	**Note:** You can install additional type definition files for other JavaScript libraries/frameworks by running the same command but changing the name from “angular” to the appropriate library/framework. See http://definitelytyped.org/tsd for a list of the type definition files that are available.

8. Let’s now install the jQuery type definition as well since the Angular type definition file has a dependency on it:

	**tsd install jquery --save**

9. If you look in the **typescriptDemo** folder you’ll see a new folder is created named **tools**. Inside of this folder you’ll find a file named **typings** that has an **angular/angular.d.ts** type definition file and a **jquery/jquery.d.ts** file in it. You’ll also see a file named **tsd.json**.

10. Create a file named **typescriptApp.d.ts** in the **typescriptDemo/tools/typings** folder. This file will track all of the TypeScript files within the application to simplify the process of resolving dependencies and compiling TypeScript to JavaScript.

11. Add the following into the **typescriptApp.d.ts** file and save it (the comments are required for one of the Gulp tasks to work properly):

```json
	//{
	//}
```
