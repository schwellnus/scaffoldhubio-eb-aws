# Deploying the backend

The contents of this folder are basically overlays to the backend folder included in the scaffoldhub.io backend folder.

The infos here are variations of what is described in this document:

https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_nodejs_express.html

Read that first and make sure you understand what's happening (and have prerequesites done, like having your AWS cli and EB cli installed).

## Steps

1. Create the .npmrc and .ebextensions/nodecommand.config files (see below) and commit them to your repo.

2. Create a EB repository with the eb init command.
```sh
~/your-application/backend$ eb init --platform node.js --region eu-west-1
```

3. Create an environment running _your_ with the eb create command.
```sh
~/your-application/backend$ eb create _your-application-environment_
```

This should already let your app run.  It's not configured, as you hopefully did not push your .env file.

4. Setup your database manually as described https://docs.scaffoldhub.io/deployment/database/sql, make sure to have that database accessible to your new environment.

5. Go to the AWS admin console to add the environment variables manually (@todo: i'm sure there's a way to set that stuff via an .ebextension using secrets manager, etc etc... feel free to file a pull request if you're doing that)

Whenever you make changes to your app, commit and deploy via 
```sh
~/your-application/backend$ eb deploy
```

_Warning_: When you do
```sh
~/your-application/backend$ eb terminate
```
the configuration files created during step 2 will be removed.


## .npmrc

This needs to be included in order to enable npm modules to install properly.  I don't know if I was doing something wrong, but i only got things installing properly with this.

## .ebextensions/nodecommand.config

this ensures that the elastic beanstalk node runner starts with ```npm start``` instead of trying to run ```index.js``` or ```app.js``` directly.


