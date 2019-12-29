
## A Beginner’s Guide to npm — the Node Package Manager

### Installing Node.js

Long Term Support (LTS) version of Node.

### 检查版本

	[mac@node4 ~]$ which node
	/usr/local/lib/nodejs/node-v10.16.0-linux-x64/bin/node
	[mac@node4 ~]$ 
	[mac@node4 ~]$ node --version
	v10.16.0
	
	
	[mac@node4 ~]$ which npm
	/usr/local/lib/nodejs/node-v10.16.0-linux-x64/bin/npm
	[mac@node4 ~]$ 
	[mac@node4 ~]$ npm --version
	6.9.0

### Updating npm

Linux/Mac OS:

	[mac@node4 ~]$ npm install npm@latest -g

Windows:

	npm install --global --production npm-windows-upgrade
	npm-windows-upgrade --npm-version latest

### Node Packaged Modules



### Changing the Location of Global Packages

Let’s see what output npm config gives us.

	[mac@node4 ~]$ npm config list
	; cli configs
	metrics-registry = "https://registry.npmjs.org/"
	scope = ""
	user-agent = "npm/6.9.0 node/v10.16.0 linux x64"
	
	; node bin location = /usr/local/lib/nodejs/node-v10.16.0-linux-x64/bin/node
	; cwd = /home/mac
	; HOME = /home/mac
	; "npm config ls -l" to show all defaults.
	
For now it’s important to get the current global location.

	[mac@node4 ~]$ npm config get prefix
	/usr/local/lib/nodejs/node-v10.16.0-linux-x64
	[mac@node4 ~]$ 

This is the prefix we want to change, so as to install global packages in our home directory. 

	[mac@node4 ~]$ cd ~ && mkdir .node_modules_global
	[mac@node4 ~]$ 
	[mac@node4 ~]$ pwd
	/home/mac
	
	[mac@node4 ~]$ npm config set prefix=$HOME/.node_modules_global
	[mac@node4 ~]$ 
	[mac@node4 ~]$ npm config get prefix
	/home/mac/.node_modules_global
	[mac@node4 ~]$ 


This also creates a .npmrc file in our home directory

	[mac@node4 ~]$ npm config get prefix
	/home/mac/.node_modules_global
	[mac@node4 ~]$ 
	[mac@node4 ~]$ cat .npmrc
	prefix=/home/mac/.node_modules_global
	[mac@node4 ~]$ 


Finally, we need to add .node_modules_global/bin to our $PATH environment 

	export PATH="$HOME/.node_modules_global/bin:$PATH"

Now our .node_modules_global/bin will be found first and the correct version of npm will be used.

	[mac@node4 ~]$ which npm
	~/.node_modules_global/bin/npm
	[mac@node4 ~]$ 
	[mac@node4 ~]$ npm --version
	6.11.2
	[mac@node4 ~]$ 

### Installing Packages in Global Mode

	[mac@node4 ~]$ npm install uglify-js --global
	/home/mac/.node_modules_global/bin/uglifyjs -> /home/mac/.node_modules_global/lib/node_modules/uglify-js/bin/uglifyjs
	+ uglify-js@3.6.0
	added 3 packages from 38 contributors in 5.256s
	[mac@node4 ~]$ 

### Listing Global Packages

use　npm list --global will list lot of things.

	[mac@node4 ~]$ npm list --global --depth=0
	/home/mac/.node_modules_global/lib
	├── npm@6.11.2
	└── uglify-js@3.6.0
	
	[mac@node4 ~]$ 

use the Uglify package to minify example.js into example.min.js:

	$ wget https://vuejs.org/js/vue.js
	$ uglifyjs vue.js -o vue.min.js 
	$ ls
	vue.js  vue.min.js

### Installing Packages in Local Mode

When you install packages locally, you normally do so using a package.json file. 

	[mac@node4 npm_test]$ npm init
	This utility will walk you through creating a package.json file.
	It only covers the most common items, and tries to guess sensible defaults.
	
	See `npm help json` for definitive documentation on these fields
	and exactly what they do.
	
	Use `npm install <pkg>` afterwards to install a package and
	save it as a dependency in the package.json file.
	
	Press ^C at any time to quit.
	package name: (npm_test) etax
	version: (1.0.0) 
	description: Demo of package.json
	entry point: (index.js) 
	test command: 
	git repository: 
	keywords: 
	author: mac
	license: (ISC) 
	About to write to /home/mac/vue_demo/npm_test/package.json:
	
	{
	  "name": "etax",
	  "version": "1.0.0",
	  "description": "Demo of package.json",
	  "main": "index.js",
	  "scripts": {
	    "test": "echo \"Error: no test specified\" && exit 1"
	  },
	  "author": "mac",
	  "license": "ISC"
	}
	
	
	Is this OK? (yes) yes
	[mac@node4 npm_test]$ 

Let's check it:

	[mac@node4 npm_test]$ cat package.json 
	{
	  "name": "etax",
	  "version": "1.0.0",
	  "description": "Demo of package.json",
	  "main": "index.js",
	  "scripts": {
	    "test": "echo \"Error: no test specified\" && exit 1"
	  },
	  "author": "mac",
	  "license": "ISC"
	}
	[mac@node4 npm_test]$ 

If you want a quicker way to generate a package.json file use npm init --y

	[mac@node4 npm_test2]$ npm init --y
	Wrote to /home/mac/vue_demo/npm_test2/package.json:
	
	{
	  "name": "npm_test2",
	  "version": "1.0.0",
	  "description": "",
	  "main": "index.js",
	  "scripts": {
	    "test": "echo \"Error: no test specified\" && exit 1"
	  },
	  "keywords": [],
	  "author": "",
	  "license": "ISC"
	}

Let's check it:

	[mac@node4 npm_test2]$ cat package.json 
	{
	  "name": "npm_test2",
	  "version": "1.0.0",
	  "description": "",
	  "main": "index.js",
	  "scripts": {
	    "test": "echo \"Error: no test specified\" && exit 1"
	  },
	  "keywords": [],
	  "author": "",
	  "license": "ISC"
	}
	[mac@node4 npm_test2]$ 

Now let’s try and install [Underscore](https://underscorejs.org/ "https://underscorejs.org/").

	[mac@node4 npm_test2]$ npm install underscore
	npm notice created a lockfile as package-lock.json. You should commit this file.
	npm WARN npm_test2@1.0.0 No description
	npm WARN npm_test2@1.0.0 No repository field.
	
	+ underscore@1.9.1
	added 1 package from 1 contributor and audited 1 package in 2.268s
	found 0 vulnerabilities
	
	[mac@node4 npm_test2]$ ls
	node_modules  package.json  package-lock.json
	[mac@node4 npm_test2]$ 


> Note that a lockfile is created. We’ll be coming back to this later.

Now if we have a look in package.json we will see that a dependencies field has been added:

	[mac@node4 npm_test2]$ cat package.json 
	{
	  "name": "npm_test2",
	  "version": "1.0.0",
	  "description": "",
	  "main": "index.js",
	  "scripts": {
	    "test": "echo \"Error: no test specified\" && exit 1"
	  },
	  "keywords": [],
	  "author": "",
	  "license": "ISC",
	  "dependencies": {
	    "underscore": "^1.9.1"
	  }
	}
	[mac@node4 npm_test2]$ 

### Managing Dependencies with package.json


### Uninstalling Local Packages


### Installing a Specific Version of a Package


### Updating a Package


### Searching for Packages


### Re-installing Project Dependencies


### Managing the Cache


### Audit


### Aliases


### Version Managers


### Conclusion