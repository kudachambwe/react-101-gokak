# Part 2. React: Digging a little deeper  🕳️
* * *
## 1. Few things before we start - React

- VSCode - Editor
	- My prefered editor, easy to use customizable, fast and stable
	- [Download here](https://code.visualstudio.com/download) ⬇️
	- Many good alternatives like; Atom, Sublime, Brackets.
- Github - Version Control & Hosting Code
	- Host code for version control and collaboration and so much more 
	- [Signup/sign in here](https://github.com/) 👤
- Node (`v.16.15.0`)
	- ...
	- **WHY?** - To run javascript outside the browser. 
- NPM 
	- Think "Limewire"
	- Software registry for many things; download packages, tools, create packages for specific few/many/all etc.
	- Three ses/components: 
		- Website - browse packages and read docs
		- CLI (Command Line Interface) - access to npm via the terminal
		- The registry - large public database for JS software and packages (public or private)
	- **WHY?** - To install necessary packages, run and build code. 
- - NVM (Node Version Manager) = version manager for node.js 🤠
	- Lets you switch between versions 
	- Install instructions [here](https://github.com/nvm-sh/nvm#installation) ⬇️
	- **WHY?** - 
- (HomeBrew/Choco) 🤠
	- Nice thing to have. Choose between: 
		- Homebrew = easy-to-install hack to install software on consoles solely for MacOS machines, i.e. command line  [Install here](https://docs.brew.sh/Installation) ⬇️
		- Chocolatey = same as Homebrew essentially - but for Windows. [Install here](https://chocolatey.org/install) ⬇️
	- **WHY?** - Because reasons...


* * *
## 2. Walkthrough: Setting up the Environment 🖥️

### 2.1. Do we really need to? 
* "Well... No"🤥
* React support the "Use as little or as much as you need" thinking
* Sometimes you need a little, sometimes a bit more
* Based on simple HTML document: 
```html
<!doctype html>
<html>
 <head>
  <title>Our Basic HTML Page</title>
  <meta name="description" content="Our first page">
 </head>
 <body>
	 <h1> Hello World!</h1>
 </body>
</html>
```
* We can simply add 3 CDNs to directly write React in HTML like this:

```html
<!doctype html>
<html>
  <head>
	<title>Our slightly fancier React HTML Page</title>
    <script src="https://unpkg.com/react@18/umd/react.development.js" crossorigin></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js" crossorigin></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  </head>
  <body>

    <div id="mydiv">
	  	<!-- This element's contents will be replaced with your component. -->
	 </div>

    <script type="text/babel">
      function Hello() {
        return <h1>Hello World!</h1>;
      }

      ReactDOM.render(<Hello />, document.getElementById('mydiv'))
    </script>

  </body>
</html>
```

So whats really happening here: 
1. The first two scripts let us write React code into our JS `<script/>` 
	1. `react@18` = Holds the **react source** for components, state, props etc. - to switch version; replace 18 with the version number.
	2. `react-dom@18` = Th **glue** between React and the DOM (i.e. mounting the app to index i.e. `ReactDOM.render()`) 
2. Babel (JS compiler) allows us to write JSX syntax and ES6 in older browsers 


⚠️ **Warning: This isn't suitable for production releases!**

### 2.2 Spoiler Alert: Yep, we do.. 😬

* "[Create React App](https://create-react-app.dev/docs/getting-started/)" or `create-react-app` 
* Easy-to-setup environment for React, and according to docs; "[...] best way to start building a new single-page application in React."
* An official way to create single page React Apps
* Bolierplate setup for a quick start
* Provides modern build setup w/ zero config
* "Start & get going" approach
* Basic info: 
	* Doesn't handle backend logic or databases - just frontend build pipeline. You use whatever you want! 
	* Under the hood; Babel (JS **compiler**) and `webpack` (JS **bundler**) 🥴
	* However - you don't need to know anything about them! 🤩

1. Run the following command to create a React Application named `my-first-app`: 
The `create-react-app` will set up everything you need to run a React application. 
```shell
$ npx create-react-app my-first-app
```


2. Now run this command to move into the project directory CRA just created for you: 
```shell
$ cd my-first-app
```

3. Run this command to run the React application `my-first-app`
```shell
$ npm start
```

A new browser window should open with your brand new React App. If not, then try typing `localhost:3000` in the adress bar. 

* * *
## 3. Exercise 0: Getting started 🧩

After running the application, go to your preferred edtior and open the folder `/my-first-app`
You should a folder structure that looks something like this: 

```text
my-first-app
├── README.md
├── node_modules
├── package.json
├── .gitignore
├── public
│   ├── favicon.ico
│   ├── index.html
│   ├── logo192.png
│   ├── logo512.png
│   ├── manifest.json
│   └── robots.txt
└── src
    ├── App.css
    ├── App.js
    ├── App.test.js
    ├── index.css
    ├── index.js
    ├── logo.svg
    ├── serviceWorker.js
    └── setupTests.js
```
*\* `serviceWorker.js` = scripts separate from the main thread & not DOM related; run mainly by the browser. For network related features enabling such features as **push notifications,** retrieving stuff from **cache** etc etc.* 

Some noteworthy scripts you need to know to run, test and build the app: 

1. `$ npm start`
Runs the app in development mode. 
Note that the page will automatically reload if you make changes to the code. 

If you make a mistake/typo/error you will see the build errors and lint warnings in the console: 

![e33f94bd22f8a204b0f16adee9b58995.png](:/859c04c116724c8bbf1ca236804a8ef0)

2. `$ npm test`

Runs a test watcher in an interactive mode. The default is that it runs the tests related to the previous changes since last commit. 

This is something you can read/learn more about [here](https://create-react-app.dev/docs/running-tests)

3. `$ npm build`

Builds the app for production to the `/build` folder It bundles the React and optimizes the build for best performance. 

The build is minified and the filenames include the hashes. 

Minified = minimizing code and markup in code to reduce load time and bandwidth usage. Formats  code into a something that provides the best user experience basically. 
* * *
## 4. Walkthrough: How to structure things nicely 🗂️
* Many ways to best structure, it boils down to preference combined with best practices
* But most people would agree on these following: 
	* Break large components into smaller ones. Think Separation of Concern Principle. 
	* Decouple logic from UI
	* Single Responsibility Principle - a component should have ONE reason to change, one specific purpose. 
	* Keep your code DRY. Don't Repeat Yourself, but sometimes code duplicates are a "necessary evil"
	* Use Functional Components (FC) instead of Class 
	* Follow the React way of creating separate folders for all files related to component
	* Allways follow namin conventions e.g. `PascalCase` for Components etc. `const visible = true` < `const isVisible = true`
	* Keep Components as simple as possible - see Single Responsibility Principle
	* Consider using Typescript (*not so important in the beginning*)
* Many more others but these are the most common
* Final advice: Don't overthink it.  
* My recommendation: features/pages and components

```txt
src/
├── feature/
│   ├── User/
│   ├── Error/
│   └── User/
│	│── User.jsx
│	│── User.css
│	└── User.test.js
└── components/
    ├── App/
    ├── Button/
    └── List/
```

**Good references:** 
[React Recommendations/tips](https://reactjs.org/docs/faq-structure.html)
[Atomic Design](https://bradfrost.com/blog/post/atomic-web-design/)
[Good blog from Robin Wieruch](https://www.robinwieruch.de/react-folder-structure/)
