# SPAtext
single page app step by step

## next actions

## further reading
http://learnjs.benrady.com
learn to code html and css by shay howe
http://learn.shayhowe.com/html-css/
eloquent javascript by marijn haverbeke
http://eloquentjavascript.net/
apps and examples from the book here:
https://pragprog.com/book/brapps/serverless-page-apps
https://github.com/benrady/learnjs

## tips and recommendations
  consider using an automated page-reloading tool as you work e.g. livepage plugin for google chrome
  or livereload (standalone web server and protocol that is used to reload web apps automatically during dev.  whenever server detects a file has changed, communicates the change to the js lib or browser plugin in the client)
  or livereloadX, livereload app, live-server or grunt-livereload (node)

## concepts used here
TDD - Red Green Refactor
no yak shaving

## environment and libraries used
Normalize CSS - ensures base style is the same across all browsers
Skeleton - responsive css boilerplate
Skeleton's default font - Raleway
jQuery 2 - for building application views, visual effects, listening to events
vendor.js - libraries customized to the app or aren't popular enough to be available on a content delivery network (CDN) including:
  CognitoIdentity
  CognitoSync
  DynamoDB
  Lambda
  STS
app.js - will have the application logic in javascript
  will have domain-specific logic of the app, and router, template functions and code for data binding
style - can pull into its own css at some point
public/tests - contains a test runner and an empty test suite in app_spec.js
sspa - wrapper script to do simple tasks like config AWS services, build code bundles, deploy the application

## to run locally
start a local development server that serves the content of the public directory:
```
./sspa server
```


## notes and quotes
your first and most important challenge is to figure out what the market wants to buy and what it's willing to pay.  product/market fit, is key to building a successful product or service

build a product and try to sell it - validate the demand and your ability to connect with those customers via a sales or marketing channel - asap

landing page - quickly explain what the app is and provides a clear path to get started with it (often with button - the call to action)

in N-Tier design - application server does most of the heavy lifting
  - storing user data 
  - issue security creds
  - control navigation
  - web portion = provide interface to back end

  - db
  - app server - auth, navigation, validation, data i/o
  - web server - application load
  - load balancer - connection mgmt
  - browser - navigation, validation

Serverless design
  - application logic to the browser
  - Oauth2 identity providers e.g. facebook, google, twitter so not have to store passwords
  - data - connect to Amazon Dynamo DB from browser
  - any fn that can't be done in the browser can be handled by amazon Lamdba microservice

  benefits
  - no more servers - applying security patches, monitoring cpu/memory use, rolling log files, running out of disk space, operational issues
  - can focus on the app, not the infrastructure
  - easy to scale via cloud service providers
  - highly available - don't have to bring down server to deploy or upgrade
  - low cost
  - microservice friendly - can intro specialty services to do custom auth, validation, asynchronous data processing
  - inherently distributed (pass messages via requests and responses) between nodes in a network and are limited in how they can do this (see CAP theorem)
  
  limitations
  - vendor lock-in
  - new logs to read
  - different security model - can't mix application validation with security validation
  - different identity model - e.g. join to user table with id not apply anymore
  - big scale costs

## approach and purpose
-  build a single page web app, moving logic normally found in the server down into a web client built with javascript, html, css
-  use Amazon web services to build a serverless back end
  (replaces servers, dbs, and load balancers of traditional web app with cloud services)

