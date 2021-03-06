# rrequire
"Root Require": A nodejs module for requiring files in paths relative to one where a specific package.json is located. 

## Why is this needed?

Because NodeJS does not have a robust way of determining the root path of a running application. Sure, when your app is a couple of files you dont have problems, but as it starts growing, with modular parts and plugins, you want to be sure you can locate the actual root of your application.

https://stackoverflow.com/questions/10265798/determine-project-root-from-a-running-node-js-application


## How to use?

````bash
npm install rrequire --save
````

````node
const rrequire = require("rrequire")
const Client = rrequire("your-app", "./src/model/client.js", [optional, boolean] forceRecheck).Client;
````

rrequire will search the current folder of the file from which it is invoked and the entire upstream directory until the root of the filesystem. Whenever a `package.json` file is detected, it will attempt to parse it. 

 - If the `name` field in the package.json matches `your-app`, it will detect that folder as the root of the app.
 - If the file path `"./src/model/client.js"` exists, relatively to the detected root folder, it will require the file for you.

