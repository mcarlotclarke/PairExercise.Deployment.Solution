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
