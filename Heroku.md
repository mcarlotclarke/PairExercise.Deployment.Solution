## What is Heroku

A cloud platform that lets companies build, deliver, monitor and scale apps — we're the fastest way to go from idea to URL, bypassing all those infrastructure headaches.

Heroku is a hosting platform, a place where your apps can live and any internet user can visit. Have you ever tried to show someone not at Fullstack what you were working on at Fullstack? If you tried to give them your IP address, that didn't work because their computer cannot find a route to your computer. Heroku is configured so that any internet user can view an app running on its platform.

Heroku calls its basic unit of computation a dyno which you can think of as an internet accessible server. Although it is a server, it might not be running on dedicated hardware

- Uses the 12 factor app to design apps https://12factor.net/

## Installing Heroku CLI

You can run Heroku locally thru the installation of its command line interface
Follow steps https://devcenter.heroku.com/articles/heroku-cli : 1. Download and install 2. Verify installation

\*\*Must see the following for confirmation:
[user@localhost]$ heroku
CLI to interact with Heroku
VERSION
heroku/7.14.4 darwin-x64 node-v10.9.0
USAGE
$ heroku [COMMAND]
COMMANDS
access manage user access to apps
addons tools and services for developing, extending, and operating your app
apps manage apps on Heroku
auth check 2fa status
authorizations OAuth authorizations
...

\*\* These steps are done right from your terminal

## Log in to Heroku

To use the Heroku platform you must log in. `heroku login` then enter your Heroku credentials.

Ex.
[user@localhost]\$ heroku login
heroku: Enter your login credentials
Email: cool.guy55@cool.example.com
Password: **\*\***\***\*\***
Logged in as cool.guy55@cool.example.com

## Create your app

Pick an app name (you can change it later). Remember the article on bikshedding http://bikeshed.com/
Once you have your name run `heroku create your-app-name`

Confirmation
[user@localhost]\$ heroku create your-app-name
Creating ⬢ your-app-name... done
https://your-app-name.herokuapp.com/ | https://git.heroku.com/your-app-name.git

You can visit your Heroku url to see your app!

## Deploy

Heroku has a copy of your repository. It maintains its own history of your app, and you can only deploy by pushing to its `master` branch. But to push to that repository, it needs to be registered as a remote in your own, local, git repository. (Look at the remotes we currently have using `git remote -v`)

Ex.
[user@localhost]\$ git remote -v
heroku https://git.heroku.com/your-app-name.git (fetch)
heroku https://git.heroku.com/your-app-name.git (push)
origin git@github.com:your-github-username/your-app-name.git (fetch)
origin git@github.com:your-github-username/your-app-name.git (push)

## My workshop steps:

Miosotiss-MBP:~ miosotis$ heroku create miosotis-app
Creating ⬢ miosotis-app... done
https://miosotis-app.herokuapp.com/ | https://git.heroku.com/miosotis-app.git
Miosotiss-MBP:~ miosotis$ git remote -v
fatal: not a git repository (or any of the parent directories): .git
Miosotiss-MBP:~ miosotis$ git remote -version
fatal: not a git repository (or any of the parent directories): .git
Miosotiss-MBP:~ miosotis$

- Deploy
  Make sure to commit to your master prior to git push heroku master

- Logs
  You can check out your logs from the dashboard, next to open app, more, view logs
  Also from the command line: `heroku logs` - The advantage of this method is that you can filter the output for a particular form of message using bash pipelining. https://stackoverflow.com/questions/8607568/can-i-get-heroku-logs-to-return-only-lines-outlining-errors Additionally, you can get a live view of the logs by using the --tail flag. Then as messages are generated on your dyno they will appear in your terminal.

- Deploying build artifacts
  Your bundle is not being served on your app site, because of these lines in the .gitignore file: bundle.js bundle.js.map

So you need to send those files to Heroku. For the purposes of this workshop, and in the future with Boilermaker, you should use npm run deploy. This script creates a deploy branch, runs webpack, adds these files to the branch, commits these changes, deploys them to Heroku by git push heroku deploy:master and finally deletes the deploy branch. For a closer look at what this script is doing and how it works, see the seventh Boilermaker review video.

- heroku add-ons (heroku postgres and herokt run bash -> for npm run seed
  In order to connect your database, Heroku has a default add-on that will do the trick:

\*\* Heroku Postgres
First navigate to "Configure Add-ons" in the Heroku dashboard for your app. Then search for postgres and click Heroku Postgres:

Then select the "Hobby Dev -- Free" option

Video tutorial https://www.youtube.com/watch?v=fAedA9LS9nM&t=2m
When you add an add-on, your app will restart. Your app will also restart if we update any environment variables, or "Config Vars" as Heroku calls them.

\*\* Heroku run bash

To create your schema and load the initial data into your database you need to run npm run seed but how do you do that on Heroku? You can get a bash session on your dyno by using the heroku run command. This command runs a command on Heroku, but if the command is bash then you can get an interactive shell session on your dyno. Note that running heroku run bash will take a bit of time the first time.

- Continuous integration and deployment
  https://stackoverflow.com/questions/28608015/continuous-integration-vs-continuous-delivery-vs-continuous-deployment/44798079

- Travis
  When changes are made to the master branch of your repository, Travis will build and test your app on their platform

- Travis.yml
  .travis.yml

Take a look at the .travis.yml file in your repository. First off, it is a YAML file, which is a serialization format that is a little more flexible than JSON (a superset, in fact), but less flexible than full on JavaScript.

Hint:
Key reference via dot syntax
Click to toggle hint
Due to the close relationship between YAML and JavaScript, values are often referred to using dot syntax, for example, the key addons.postgresql has the value '9.6' in this screenshot:

Look at the install key and notice that it is using npm ci for installation. Here ci stands for Continuous Integration, and this will install dependencies based on your package-lock.json file. This is why this file must be committed and kept up to date.

Hint:
Optional: Resolving merge conflicts in package-lock.json
Click to toggle hint
You can run into merge conflicts in package-lock.json if multiple people add new dependencies. This file is generated, so it is best not to edit this file manually, and in Boilermaker we use npm-merge-driver to resolve these conflicts. You should not run into any such conflicts in this workshop. If something goes very wrong, you can always delete the app's node_modules folder and package-lock.json and subsequently run npm install to generate a new one.

Be sure that the create database line contains the correct name for your project: it should match the nameattribute in package.json concatenated with -test so in our case your-app-name-test.

You can look at the official Travis docs for more information on other specific clauses.

Since this .travis.yml descends from the same file in the Boilermaker workshop, the information in the .travis.yml portion of the seventh Boilermaker review video applies to this project.

- Encripting your heroku auth token
