# SPAtext
single page app step by step

## next actions
clean up the URL by giving the app its own domain name
map the domain name to the S3 bucket
do this by creating a CNAME entry with your DNS provider that uses the endpoint URL as the value for the record (see appendix 2 off text)

create a test environment

IAM lockdown - add fine grained policies
## further reading
### intro
http://learnjs.benrady.com
learn to code html and css by shay howe
http://learn.shayhowe.com/html-css/
eloquent javascript by marijn haverbeke
http://eloquentjavascript.net/
apps and examples from the book here:
https://pragprog.com/book/brapps/serverless-page-apps
https://github.com/benrady/learnjs

### ch 1
https://en.wikipedia.org/wiki/CAP_theorem
https://sdk.amazonaws.com/builder/js
https://www.npmjs.com/package/grunt-livereload
http://getskeleton.com
http://getskeleton.com/examples/landing/
http://console.aws.amazon.com

### ch 2 routing views with hash events
jasmine doc (21)


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

## to deploy
(rather than our own Apache or Nginx web server)
Amazon's Simple Storage Service (S3)

### set up the AWS command-line interface (AWS CLI)
```
pip install awscli

```
create AWS user with access keys my

IAM - identity and access managementd
  use this to create individual users who have access to the services under your account
  have to sign up for the S3 service (create a bucket) from services/s3
  learnjs.dream2do.ca (could not do from command line)
  endpoint(I think) is http://learnjs.dream2do.ca.s3-website-us-east-2.amazonaws.com
  
```
./sspa deploy_bucket learnjs.dream2do.ca
```
debug error
https://aws.amazon.com/premiumsupport/knowledge-center/s3-access-denied-error-kms/
add permission to the kms:GenerateDataKey action - 
go back to setup since I couldn't create the bucket from the command line

https://docs.aws.amazon.com/AmazonS3/latest/gsg/GetStartedWithS3.html
https://docs.aws.amazon.com/AmazonS3/latest/gsg/PuttingAnObjectInABucket.html
aws configure (do again)
aws s3 ls
now has learnjs.dream2do.ca
aws sts get-caller-identity
account 040939238419:user/avhenders

ultimate solution: had to make my permissions on my bucket public (vs the private default when creating the bucket)


## notes and quotes
your first and most important challenge is to figure out what the market wants to buy and what it's willing to pay.  product/market fit, is key to building a successful product or service

build a product and try to sell it - validate the demand and your ability to connect with those customers via a sales or marketing channel - asap

landing page - quickly explain what the app is and provides a clear path to get started with it (often with button - the call to action)

until your application is in the hands of your users, from their perspective, you havne't really done anything, no matter how much code you've written

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

### ch 2
  tests - to trigger events, inspect markup
  event loop - invokes callbacks
  javascript - modify markup, make requests
  html - read values

  http://learnjs.dream2do.ca.s3-website.us-east-2.amazonaws.com/tests/index.html
  (at beginning, no tests found)
  can have user browse to /tests and copy/paste the error they are experiencing in the tests

  1. create view container in the markup to give the router a place to add the views
  2. create the showView function and have it create a minimal version of the problem view
  3. create a namespace where the router function can live

markup goes nowhere - create view container
to have tests access the markup in the app 
SpecHelper.js - copies markup in app in an element with the markup class, then appends it to the body of the test runner's page, making it available to all our tests.
also need to add view-container class to the <div> with the skeleton container class on it

debugging via console:
document.querySelector('.view-container')
var element = document.querySelector('.view-container')
element.__proto__
$('.view-container').empty()
$('.view-container').append(problemView)
$('.view-container').append('<h1>Angela</h1><p>is learning</p>'))

is equivalent to 
var element = document.createElement("h1")
element.innerText = "Angela"
document.querySelector('.view-container').appendChild(element)

in console can do $('.view-container)

adding view parameters - split hash into 2 parts, name and a parameter
(could be other kinds of identifiers, like primary db keys, UUIDs, crypto hashes, raw data as plain text or encoded e.g. json)

create spies - to test the interactions between 2 pieces of code
  is a test double that stand in for real objects or functions
  

## approach and purpose
-  build a single page web app, moving logic normally found in the server down into a web client built with javascript, html, css
-  use Amazon web services to build a serverless back end
  (replaces servers, dbs, and load balancers of traditional web app with cloud services)

## issues encountered

### ch 1

### ch 2
DevTools failed to load SourceMap: Could not load content for chrome-extension://liecbddmkiiihnedobmlmillhodjkdmb/js/content.js.map: HTTP error: status code 404, net::ERR_UNKNOWN_URL_SCHEME

DevTools failed to load SourceMap: Could not load content for chrome-extension://liecbddmkiiihnedobmlmillhodjkdmb/js/intercom-link-expand-loader.js.map: HTTP error: status code 404, net::ERR_UNKNOWN_URL_SCHEME

Synchronous XMLHttpRequest on the main thread is deprecated because of its detrimental effects to the end user's experience. For more help, check https://xhr.spec.whatwg.org/. jquery-2.1.4.js

