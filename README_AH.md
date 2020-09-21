# SPAtext
single page app step by step

## next to do:
  jasmine in browser is behaving unexpectedly, not loading latest tests.
  do a nodejs install so can run from command line
https://jasmine.github.io/setup/nodejs.html

  npm init
  sudo npm install --save-dev jasmine
  npx jasmine init // creates spec directory and config json for me
  customize spec/support/jasmine.json to enumerate source files and spec files you want Jasmine runner to include
  //run tests
  npx jasmine //from root of project

## next actions after course

clean up the URL by giving the app its own domain name
map the domain name to the S3 bucket
do this by creating a CNAME entry with your DNS provider that uses the endpoint URL as the value for the record (see appendix 2 off text)

create a test environment

IAM lockdown - add fine grained policies

redirect users to help links depending on the question (do in click handler)
  using window.location.hash or checkAnswerClick handler

from chapter 4 - connect with facebook (go to facebook developer portal and create a new app)
connect with openId

from ch 6 - move each lambda function handler out into its own file (all in index.js)

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
https://www.freecodecamp.org/news/jasmine-unit-testing-tutorial-4e757c2cbf42/
 (for python) - pip install jasmine
http://jasmine.github.io
  see a list of matchers (with expect)
jasmine-jquery extension (html specific matchers like toExist, to HaveClass)
https://github.com/velesin/jasmine-jquery
other test doubles
http://xunitpatterns.com/Test%20Double.html
routing libraries
Director - https://github.com/flatiron/director
Page - https://visionmedia.github.io/page.js
javascript test alternatives
qunit - http://qunitjs.com/
sinon.js - http://sinonjs.org/
vows.js - http://vowsjs.org/ (async test framework)
hash change events - further reading (including getting old has value in event callback)  and can manipulate browser history using pushState and popState methods of window.history
https://developer.mozilla.org/en-US/docs/Web/API/Window/location
https://developer.mozilla.org/en-US/docs/Web/API/WindowEventhandlers/onhashchange


### ch 1
https://en.wikipedia.org/wiki/CAP_theorem
https://sdk.amazonaws.com/builder/js
https://www.npmjs.com/package/grunt-livereload
http://getskeleton.com
http://getskeleton.com/examples/landing/
http://console.aws.amazon.com

### ch 2 routing views with hash events
jasmine doc (21)
to trigger the event - load app then spy on the showView function
then can assert that the spy was invoked with the right arguments

in app, register our listenerby assigning a function to the onhashchange property on the window object (browser API provides this property)
the function will be invoked whenever the hash changes

### chapter 3 essentials of single page apps
extract the markup for the problem view to an html template
  flexible, easily testable and require no special libraries or tools
  easier than building the markup programmatically using jQuery
  once we've created a template, we'll add a title element

  templates will live inside the 'templates' div
  use jQuery's clone() function to make a copy
  update the text for teh title element
  now hide the templates div from the user (with a little css)
  add a rule for .templates to display:none

using templates to manage markup, keeps app flixible and dynamic enough to show any content
using jQuery makes it easy to clone, change, append the templates without having to use a templating library

add description of the problem, teh problem code, and a place for the users to provide an answer

data will come from a data model

use low object mapping impedance (avoid map back and forth to underlying datastore)
if we mix data and behavior on the objects in the model, we'll have to separate them out again when we go serialize them to/from the db
instead will use more direct mapping from model objects to the db and not use object model

use data binding
  one way data binding - data inserted into markup automatically (for readonly)
  two-way data binding - insert into markup and then read back out to model, 
    ie when an event is triggered that signals the data was changed
  in markup - add data attributes to the elements in the view to specify what properties should be bound to those elements
  then write function that apply the properties of the javascript object to an element.

  click handler using jquery (don't want to reload the page and reset the state of the app)

use jQuery Effects API
  fadeOut
  fadeIn

take you to landing page when you are out of problems to solve by extracting function to test the end condition directly

create a shell - the visible markup outside the templates and view container, visible in every view, eg navigation bars, logos, sidebars, menus for app, parent for fixed position elements available in any view

custom events to send messages to our views
  have view register event listener so i can trigger behavior without breaking encapsulation

  remove the view before moving on to the next one
  use jQuery's empty function cleans up associated data and event handlers (ie don't have to worry about cleaning up the cleanup function)

  https://www.w3.org/standards/webdesign/accessibility
  http://itstiredinhere.com/accessibility

  links to web apps as home screen buttons
  ios:
  https://developer.apple.com/library/ios/documentation/AppleApplications/Reference/SafariWebContent/ConfiguringWebApplications/ConfiguringWebApplications.html

  https://developer.chrome.com/multidevice/android/installtohomescreen

  css animations

  form validation - validate.js and parse.ly

  https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_data_attirbutes

  https://api.jquery.com/data/#data-html5

  http://underscorejs.org

  http://ramdajs.com

 https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/Sending_and_retrieving_form_data

 http://api.jquery.com/category/effects 

 https://developer.mozilla.org/en-US/docs/Web/CSS/animation

## ch 4 identity as a service with amazon cognito
treat identity management as another web service to separate concerns
use identities from a variety of identity providers (google, facebook, our own app) and link them with a single identity record provided by Cognito
auth becomes a concern of the infrastructure rather than the app
vs store users in a db, and salt and hash passwords
avoid the security concerns inherent in managing others' passwords
will create an identity pool to act as a repository for user identities
connect app with 3rd party identity providers
then create profiles that let our app directly access any amazon web service from the browser,
then store user data in a db

based on the oauth2 standard
oauth2 has some serious problems

google+ sign-in
create and configure a google project in the google developers console (google api console)

steps:
1. open google developers console and login using your google account
2. click create project button
3. give project a name
4. open the project detail page and select enable and manage apis under use google apis in dashboard
5. find google+ api and enable it
6. select credentials in left sidebar
7. click tab that says oauth consent screen and fill out form
will be presented to users when they are asked to connect to your app with google (only need a product name)
8. click add credentials button and select oauth 2.0 client id
9. select web application as app type and click create
(set this up under aviak.ca as dream2dojs and created a clientid)

next - review api.jquery.com

then create an identity pool in the Cognito AWS console
  holds a list of users, shows what credentials they used to connect
  use the sspa script (create_pool action) based on the config directory you specify
  ie in conf/cognito/identity_pools/learnjs/config.json

  ./sspa create_pool conf/cognito/identity_pools/learnjs

  cognito uses amazon's security token service (STS) to generate temporary aws credentials for our users

add button to navbar to let users connect using their google accounts

use id_token from response object in googleUser to create the cognitoIdentityCredentials object
to test this, spy on the CognitoIdentityCredentials constructor function, return the spy object instead, and use andCallFake to delegate to a function that is passed in, which invokes the callback to turn it into a synchronous function

## ch 5 - storig data in dynamodb
./sspa create_table conf/dynamodb/tables/learnjs/ learnjs
says created
(then I modified the table_info.json but I think I botched it)
original error:
(base) Michaels-MacBook-Pro:SPAtext angela$ ./sspa create_table conf/dynamodb/tables/learnjs/ learnjs
Waiting for table creation..........done!

An error occurred (NoSuchEntity) when calling the PutRolePolicy operation: The role with name learnjs_cognito_authenticated cannot be found.

after I tried to fix it:
(base) Michaels-MacBook-Pro:SPAtext angela$ ./sspa create_table conf/dynamodb/tables/learnjs/ learnjs

An error occurred (NoSuchEntity) when calling the PutRolePolicy operation: The role with name learnjs_cognito_authenticated cannot be found.


==
when user enters correct answer, we're going to save it

sendDbRequrest 
- create new deberred object so you can chain this with other async requests
attach 2 event handlers via on method - error and success

==
fetch answer, answer is saved when a user gets the right answer for the problem

==
next add IAM policy so user can look at others answers
added a group to IAM - authgroup that has this policy
AmazonCognitoDeveloperAuthenticatedIdentities
but not sure what to do with it after that
come back to learnjs/5500/policy/table_policy_condition.json

additional reading:
jquery 3 and promise/A+ deferred
policy simulator
allowing s3 access - images, sounds, video best stored in services meant to store large media objects

## ch 6
building microservices with lambda
e.g. enforcing data constraints that can't be specified in an access policy
using amazon lambda service can create web services that run in dedicated containers that only cost when they are handling requests
(don't need web servers for this)
- other examples:
- filter query results before send them back to the browser
- enable 3rd party access to app
- cache data 
- create lambda to provide the most common answer provided by our users to one of the programming puzzles, securely, without compromising access to other user data, and also reduces the amount of data sent to browser
- define service using AWS command line
then 2 methods for invoking the service - authenticated method using credentials, and one that is public method using http

steps:
javascript function that takes 2 arguments
  first arg = payload (json) as a parsed javascript object
  2nd arg - context - to interact with the lambda environment, including methods to respond to the request or fail with an error
package the function and its dependencies in a zip file
choose a name and settings like resource limits
upload the zip that contains the function to AWS

note on Node.js
javascript runtime based on v8
uses event driven model to prevent blocking on I/O and other long running operations
(could also use Java and Python lambda functions)

note on lambdas:
don't necessarily exit when function returns
use context to respond or fail
async tasks may not complete by time the function returns - want to avoid!
invoke callback to finish the request
useful actions:
- write to filesystem (512MB) at /tmp, but only when fn is running (not persisted)
- run linux commands from function (shell) so can use node.js libraries with native extensions
limits:
-number of processes can spawn, number of file descriptors have open
-number of concurrent invocations of function (default 100)
-300 sections for execution
memory, time, cost:
pay by gigabyte second, longer and more memory = pay more

deploy lambda fn:
use AWS CLI lambda create-function

```
./sspa build_bundle
./sspa create_service conf/lambda/functions/echo
```

create copy of echo folder for popularAnswers then 
```
./sspa create_service conf/lambda/functions/popularAnswers
```

```
aws --profile admin iam list-policies
```

## tips and recommendations
  consider using an automated page-reloading tool as you work e.g. livepage plugin for google chrome
  or livereload (standalone web server and protocol that is used to reload web apps automatically during dev.  whenever server detects a file has changed, communicates the change to the js lib or browser plugin in the client)
  or livereloadX, livereload app, live-server or grunt-livereload (node)
  https://github.com/MikeRogers0/LivePage (load unpacked extension in browser), forked from repo

## concepts used here
TDD - Red Green Refactor
no yak shaving
functional programming
aws


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

## to run tests

http://localhost:9292/tests/index.html#


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

 http://learnjs.dream2do.ca.s3-website.us-east-2.amazonaws.com/


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

sign in as root user (angela@aviak.ca)

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

handling parameters in view functions
make tests FIRE-y
fast, informative, reliable and exhaustive
so if introduce a bug it causes exactly one test to fail

loading the applicaaitn
  when enter URL the browser fetches the file and downloads it
  if it's html - browser will download other assets specified in the markup
    e.g. css, javascript, fonts, images, videos

test coverage:
  don't assume a particular implementation
  favor testability over encapsulation
  assume someone else knows how to test it. how would you discover their approach
  write tests for untested code before you'll change it
  when all else fails, isolate untested code from testable code

loading process for single page app - you're not done
  event listeners to be added
  data structures to initialize
  other assets to fetch

could put it in a script in the page, but the browser might run it as soon as it can, even before the browser has created the html hierarchy

to avoid this, attach a listener that is notified once the page is ready
add script tag to end of page and attach listener using jquery's .ready() function
and use the DOMContentLoaded event

respond to hash events - add a listener for the hashchange event using jquery trigger event
  to trigger, load the app then spy on the showView function, then call trigger and pass in the name of the even we want to trigger ie hashchange

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

title includes problem # test - does not pass as written, even though it returns the matching string

invokes router when loaded - does not pass, does not even run

# ch 5 
learnjs new folder created, deleted it
google auth doesn't seem to work in cloud
locally, says it is signed in, but your profile is empty
expected: should have email address and name at a minimum displayed
in cloud - google icon does not change to signed in
all tests (in cloud) run as passed
all tests (locally) run as passed

# ch 6
test functions through aws console
not sure, check this out:
https://docs.aws.amazon.com/lambda/latest/dg/getting-started-create-function.html
not sure where is the settings page for the lambda function, and don't see test icon or actions icon text refers to...

## future plans
have a true function evaluator, see hackerrank for an idea of how
add ability to create test cases with the functionality, and have the tests evaluate properly too
add ability to see previous answers

did research into gradients and more ideas around cards and making visuals and making it creative 