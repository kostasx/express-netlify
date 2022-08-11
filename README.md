# Deploying an Express app to Netlify as a Serverless Function (Lambda)

## INITIAL SETUP

```bash
npm init -y
npm i express serverless-http netlify-lambda
```

mkdir functions

vim netlify.toml

`netlify.toml:`

```toml
[build]

    functions = "functions"
```

vim src/api.js

`src/api.js:`

```js
const express    = require('express');
const serverless = require("serverless-http");
const app        = express();
const router     = express.Router();
router.get("/", (req,res)=> res.json({ message: "Express deployed to Netlify!" }));
app.use( "/.netlify/functions/api", router );
module.exports.handlers = serverless( app );	
```

Edit `package.json:`

```json
"start" : "./node_modules/.bin/netlify-lambda serve src",
"build" : "./node_modules/.bin/netlify-lambda build src",
```

Run `npm start` and you are ready to go!

Visit: `http://localhost:9000/.netlify/functions/api`

## Deploy to Netlify

Settings:

Branch to deploy: main
Base Directory
Build command: npm run build
Publish directory: <- IMPORTANT! This needs to be empty and NOT dist/
Functions directory: functions