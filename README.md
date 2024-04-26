Democracy.io
============

[![Build Status](https://travis-ci.org/EFForg/democracy.io.svg?branch=master)](https://travis-ci.org/EFForg/democracy.io)

Express & Angular app for sending messages to Senate and House members

(c) 2015 Electronic Frontier Foundation

## Table of Contents

* [Background Info](#background-info)
* [Getting Started](#getting-started)
* [App Configuration](#app-configuration)
* [Run tests](#run-tests)
* [Running the server](#running-the-server)
* [Angular App](#angular-app)

## Background Info

Democracy.io is an app for contacting Senate & House members. It provides a user friendly wrapper around the individual member contact forms.

It uses APIs from:
* [Smarty Streets](https://smartystreets.com/docs)
* [Phantom of the Capitol](https://github.com/EFForg/phantom-of-the-capitol)

## Getting started

### Redis

Ensure that Redis is running locally:
```
sudo apt-get install redis-server
```
or install manually via http://redis.io/topics/quickstart - making sure to read the "Securing Redis" section, especially if you install Redis manually.

### App dependencies & build

#### Notes Per Spencer to Get the Dependencies Installed Correctly (since they are very old)

In thise project, need to install node version that is in package.json file (v8.12.0)...
```
nvm install 8.12.0
```

```
nvm use 8.12.0
```

Make sure the npm version is the version that works with the old node version (npm v6.4.1).
npm -v in terminal should show 6.4.1 . If you get an error running an npm command, then try uninstalling the node 8.12.0 version and reinstalling it. The correct, compatible version should automatically be installed and activated with the node version install 

Install the correct version of simple-swizzle that is a dependency of a dependency...

```
npm install simple-swizzle@^0.2.2
```

Now try running gulp serve in the terminal, and the app should pop up in a localhost window

#### End Spencer's notes

```
npm install
npm run build
```

### credentials

You can generate required creds by running

```
node bin/gen-creds.js
```

or:

After you've run `npm install` generate a salt for encrypting IP addresses and store it in your local.json file, under: SERVER > CREDENTIALS > IP > SALT

```
var bcrypt = require('bcrypt');
var salt = bcrypt.genSaltSync(10);
console.log(salt);
```

Set a session secret and store it in your local.json file, under: SERVER > CREDENTIALS > SESSION > SECRET

## App Configuration

App config is controlled via the [node-config](https://github.com/lorenwest/node-config) module.

To set credentials, create a local-dev.json file under the [config dir](/config) and override the SERVER.CREDENTIALS setting.

Alternately, you can use:
* [Environment variables](https://github.com/lorenwest/node-config/wiki/Environment-Variables)
* [Command line options](https://github.com/lorenwest/node-config/wiki/Command-Line-Overrides)

## Run tests

```
npm run test
```

## Running the server locally

Spins up a local server to serve the app, including proxying browsersync on top of the express server.

```
gulp serve
```

## Deploying

To deploy the server, simply run:

```
pm2 deploy ecosystem.json5 production
```

For more instructions on setting up a production server, check [/deployment/README.md](deployment/README.md).

## Angular app

See the [www/README.md](/www/README.md) for details
