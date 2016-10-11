---
layout: post
title: Creating a TypeScript Workflow with Gulp
categories:
- blog
---

TypeScript provides a lot of great functionality that lets you leverage many of the features available in ES6 today but how do you get started using it in your favorite editor? If you’re using Visual Studio or WebStorm then TypeScript support can be used directly and everything happens magically without much work on your part. But, if you’re using Sublime Text, Brackets, Atom, or another editor you’ll have to find a plugin to compile .ts files to JavaScript or create your own custom workflow.

While several plugins exist to compile TypeScript and even provide code help as you’re writing TypeScript code in different editors, I generally prefer to use my own custom workflow. There are multiple benefits associated with going with this approach including the ability to standardize and share tasks across team members as well as being able to tie the workflow into a custom build process used in continuous integration scenarios. In this post I’ll walk through the process of creating a custom TypeScript workflow using Gulp (a JavaScript task manager). It’s a workflow setup that my friend Andrew Connell and I created when we recently converted an application to TypeScript. Throughout the post you’ll learn how to setup a file named gulpfile.js to compile TypeScript to JavaScript and also see how you can “lint” your TypeScript code to make sure it’s as clean and tidy as possible.

## Getting Started Creating a Custom TypeScript Workflow

I talked about using Gulp to automate the process of transpiling ES6 to ES5 in a previous post. The general process shown there is going to be used here as well although I’ll be providing additional details related to TypeScript. If you’re new to Gulp, it’s a JavaScript task manager that can be used to compile .ts files to .js files, lint your TypeScript, minify and concatenate scripts, and much more. You can find additional details at http://gulpjs.com.

Here’s a step-by-step walk-through that shows how to get started creating a TypeScript workflow with Gulp. Although there are several steps to perform, it’s a one-time setup that can be re-used across projects. If you’d prefer to use a starter project rather than walking through the steps that are provided in this post then see the project at https://github.com/DanWahlin/AngularIn20TypeScript or download the project associated with the exact steps shown in this post here. 

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
