# yggdrasil

A Node.js client for doing requests to yggdrasil, the Mojang authentication system, used for Minecraft and Scrolls, with support for TheAltening

# Usage
    $ npm install yggdrasil

## Client
```js
//init
const ygg = require('yggdrasil')({
  //Optional settings object
  host: 'https://authserver.mojang.com' //Optional custom host. No trailing slash.
});

//Authenticate a user
ygg.auth({
  token: '', //Optional. Client token.
  agent: '', //Agent name. Defaults to 'Minecraft'
  version: 1, //Agent version. Defaults to 1
  user: '', //Username
  pass: '', //Password
  requestUser: false //Optional. Request the user object to be included in response
}, function(err, data){});

//Refresh an accessToken
ygg.refresh(oldtoken, clienttoken, true, function(err, newtoken, response body){});
// Note that requestUser is an optional parameter. If set to true, it requests the user object from Mojang's authentication servers as well.

//Validate an accessToken
ygg.validate(token, function(err){});

//Invalidate all accessTokens
ygg.signout(username, password, function(err));
```

## Server
```js
const yggserver = require('yggdrasil').server({
  //Optional settings object
  host: 'https://authserver.mojang.com' //Optional custom host. No trailing slash.
});

//Join a server (clientside)
yggserver.join(token, profile, serverid, sharedsecret, serverkey, function(err, response body){});

//Join a server (serverside)
yggserver.hasJoined(username, serverid, sharedsecret, serverkey, function(err, client info){});
```
## Proxy Support
```js
const ProxyAgent = require('proxy-agent');

const ygg = require('yggdrasil')({
  //Any type of HTTP Agent 
  agent: new ProxyAgent('https://example.com:8080')
});
```

## With ES6 Named Exports
```js
/**
 * Import Client or Server from 'yggdrasil/es6'.
 * Note that the library is stateless when imported this way vs the CommonJS way.
 */
import { Client as ygg, Server as yggServ } from 'yggdrasil/es6'

// Use it like you normally would.

ygg.validate(token, function(err){})

yggServ.join(token, profile, serverid, sharedsecret, serverkey, function(err, response body){});
```

# Further Reading
* [Authentication protocol documentation](http://wiki.vg/Authentication)
* [node-minecraft-protocol](https://github.com/PrismarineJS/node-minecraft-protocol), a Minecraft client and server in Node.js
