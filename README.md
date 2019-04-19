# LoginPageMEANStack

This project was generated with [Angular CLI](https://github.com/angular/angular-cli).

This is a simple login page made with MEAN stack (MongoDB, ExpressJS, Angular 6, NodeJS).
## This project includes:
- User registration.
- User login.
- User Authorization.

## Basic working of login page
1. When user enters email and password and when both of them are correct we return an access token (generated with jwt)
2. This access token is stored in localstorage of the browser.
3. Now if user leaves the page and opens the same site again we check to see if there is any access token present in user's localstorage.
4. if access token is present - > we verify that access token and redirect user to the profile page.
5. if access token is not present - > we keep user on the same page.

## About Directories
- NodeJS and ExpressJS is inside `restApi/`
- MongoDB database is in `user_db/`
- Angular Components are in `src/app`

## Prerequisites to understand the project
- MEAN stack (Angular 2+)
- ES6 Javascript (specially promises)
- JWT: Json Web Token it is a libray to generate random token it has 2 function jwt.sign() to create token and jwt.verify() to verify
- bcrypt - Library to hash passwords, I've used two functions in this project bcrypt.hash() to hash password and bcrypt.compare to compare string with hashed password.

## Tools / Libraries / Softwares required.
1. Install [npm](https://nodejs.org/) and Angular Client `npm install @angular/cli` (ignore if already installed)
2. In command prompt type `npm install` to download starter packages.
3. `cd restApi` and type `npm install bcrypt,jsonwebtoken,mongoose,express`
4. Install [MongoDB](http://www.mongodb.com/)
5. Go to bin folder in your mongodb directory, Mine is in `c:/program files/mongodb/server/3.6/bin` and type `mongostore <path of user_db folder>`

## How to Run
1. Change directory to your project and `ng serve` to start angular server
2. Change directory to bin folder of your mongodb installation folder, Mine is `c:/program files/mongodb/server/3.6/bin` and type `mongod` then open new command prompt and type `mongo`
3. Change directory to `restApi/` and type `node index.js` to start Node Server

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `-prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).

selenium jenkins error troubleshooting


error:


possible fix1:

* In your Jenkins settings add a global property  key : DISPLAY
* value:0:0
* 
* On your server start Xvfb in the background:  Xvfb :0 -ac -screen 0 1024x768x24 &
* 

fix2:

Run following commands to start selenium web server

Xvfb :99 -ac -screen 0 1280x1024x24 &
export DISPLAY=:99
nice -n 10 x11vnc 2>&1 &

start google chrome via selenium driver
ng e2e --serve true --port 4200 --watch true

Protractor.conf file:
capabilities: {
    'browserName': 'chrome',
    'chromeOptions': {
        'args': ['no-sandbox']
    }
},

insert new argument as seen below

{hromeOptions options = new ChromeOptions();
        ...
        options.addArguments("--no-sandbox");
        options.addArguments("--disable-dev-shm-usage");}

fix3:
workaround  is to cleanup the temp files before running tests:
rm -rf /tmp/.org.chromium.Chromium*

https://stackoverflow.com/questions/22424737/unknown-error-chrome-failed-to-start-exited-abnormally

generating chrome log

ptions = webdriver.ChromeOptions()
options.binary_location = '/opt/google/chrome/google-chrome'
service_log_path = "{}/chromedriver.log".format(outputdir)
service_args = ['--verbose']
driver = webdriver.Chrome('/path/to/chromedriver',
        chrome_options=options,
        service_args=service_args,
        service_log_path=service_log_path)
note:
by just changing from driver = webdriver.Chrome('/usr/local/bin/chromedriver') to driver = webdriver.Chrome(), I was able to make my code run.

fix4:
https://github.com/heroku/heroku-buildpack-google-chrome/issues/56

update chrome config as this

capabilities: {
browserName: 'chrome',
ignoreProtectedModeSettings: true//,
chromeOptions: {
args: [ "--headless","--disable-gpu","--window-size=800,600","--no-sandbox","--disable-dev-shm-usage" ] // to comment / uncomment for headless
}
driver = webdrive.Chrome('/usr/local/bin/chromedriver',chrome_options=chrome_options)
}

what is protractor?


Protractor is an end-to-end test framework for Angular and AngularJS applications. Protractor is a Node.js program built on top of WebDriverJS. Protractor runs tests against your application running in a real browser, interacting with it as a user would.
By default, Protractor uses the Jasmine test framework for its testing interface.
how to configure protractor?

http://www.protractortest.org/#/browser-setup

what is jasmine?
Jasmine is a behavior-driven development framework for testing JavaScript code. It does not depend on any other JavaScript frameworks. It does not require a DOM. And it has a clean, obvious syntax so that you can easily write tests.

Advantages of using protractor

https://www.thoughtworks.com/insights/blog/testing-angularjs-apps-protractor

testing with protractor

http://www.jhipster-book.com/#!/news/entry/adding-protractor-tests

How to configure Protractor with Selenium webdriver
https://youtu.be/nerfBTEC3Hs

AngularJS Protractor Tutorial FrameworkSetup

https://youtu.be/57134cHJlAs

update chrome driver
Update Protractor to use Latest Chromedriver (Otherwise it can't run against Chrome v65)

ode_modules/protractor/bin/webdriver-manager update
command. After that I ran my tests and all worked as expected with latest version of chromedriver.


Update Protractor to use Latest Chromedriver (Otherwise it can't run against Chrome v65) 
https://github.com/angular/protractor/issues/4728

The local solution to this is to go download Chromedriver 2.36 and then point your config files to this - and thus override Protractor's Chromedriver choice (2.33.x).
chromeDriver: './location/of/your/chromedriver.exe'

'directConnect: true' has issues for Chrome Driver
https://github.com/angular/protractor/issues/4887

0:02 / 30:22




Install Protractor + Jasmine + Typescript +VSCode [All Free Tools] [CherCher Tech]
https://youtu.be/W-m2mbGf1tM

https://chercher.tech/protractor/install-protractor

Install and configure Mongodb

https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x-tarball/

auto deploy using jenkins

deploy batch script
#!/bin/sh
ssh ezderman@NODE.SERVER.IP <<EOF
 cd ~/node-app
 git pull
 npm install — production
 pm2 restart all
 exit
EOF

setup ci cd for node.js app in jenkins

https://medium.com/@mosheezderman/how-to-set-up-ci-cd-pipeline-for-a-node-js-app-with-jenkins-c51581cc783c

ci-cd for Angular js and node js application
https://app.pluralsight.com/player?course=continuous-integration-deployment-angularjs-nodejs&author=alex-zanfir&name=continuous-integration-m01&clip=0&mode=live

jenkins in mac os

install jenkins on macOS-x
https://jenkins.io/doc/book/installing/

1.Mac OS X
Log files should be at /var/log/jenkins/jenkins.log, unless customized in org.jenkins-ci.plist

2.https://www.fourkitchens.com/blog/article/trigger-jenkins-builds-pushing-github/
3.https://jenkins.io/solutions/github/

4.https://wiki.jenkins.io/display/JENKINS/Github+OAuth+Plugin#GithubOAuthPlugin-Setup
5./Users/Shared/Jenkins/Home

6.Start and Stop Jenkins on OSX
# start	
	sudo launchctl load /Library/LaunchDaemons/org.jenkins-ci.plist
	
	
# stop	sudo launchctl unload /Library/LaunchDaemons/org.jenkins-ci.plist
7.How to uninstall Jenkins from MAC
1. Go to /Applications --> Delete the Jenkins folder.
2. Delete /Users/Shared/Jenkins.
3. Delete Jenkins user(there will be a standard user with no name username for the first time when jenkins is installed) from "Users & Groups"
8.uninstall jenkins from mac os-x

$sudo /Library/Application\ Support/Jenkins/Uninstall.command

9. using jenkins
https://jenkins.io/doc/book/using/

10 perform this on jenkins tomorrow
https://youtu.be/QvFungzXI5s

11.Continuous Integration With Jenkins For MEAN Stack App

https://www.agiratech.com/continuous-integration-jenkins-mean-stack-app/

12Continuous Integration and deployment (CI/CD Pipeline) with Jenkins and Node.js

https://codeforgeek.com/2019/03/continuous-integration-deployment-jenkins-node-js/

/users/shared/workspace/test_proj

CICD of mean-stack on Azure Devops

https://medium.com/@easonlai888/warrior-series-making-mean-stack-work-with-azure-devops-2497ebd727d9

Create a Node.js web app in Azure

https://docs.microsoft.com/en-gb/azure/app-service/app-service-web-get-started-nodejs


export PATH=/usr/local/bin:$PATH
cd /Users/Shared/Jenkins/Home/workspace/test_proj
npm install
ng build --prod

Angular jenkins dev build

export PATH=/usr/local/bin:$PATH
npm install
ng build

Angular jenkins prod build

export PATH=/usr/local/bin:$PATH
npm install
npm run ng build --prod

deploying Angular App

https://youtu.be/nxV3weqMzYo

git clone git@github.com:https://github.com/devanand73/MEAN-Stack-loginPage.git

	Github Webhook | Integrating Jenkins With Github 
http://49.204.209.163:8080/github-webhook-  payload url

https://youtu.be/PhxZamqYJws

