---
layout: post
author: Mark
title: AWS Amplify, JavaScript, Angular
---

We have an existing Angular application.  Let's attempt to integrate AWS solutions via Amplify to utilize systems
such as Cognito for user authentication and DynamoDB for data persistence.

Let's use this AWS [Amplify JavaScript](https://aws-amplify.github.io/docs/js/angular) page as a reference.

## Install Amplify

````
$ npm install --save aws-amplify
$ npm install --save aws-amplify-angular
````

## Configure Amplify

````
$ amplify configure
````

## Angular 6+ Support

Resolve Amplify Angular 6+ Issue as per [AWS](https://aws-amplify.github.io/docs/js/angular)
1. Modify polyfills.ts  
````
(window as any).global = window;
````

2. Modify index.html
````
<script>
    if (global === undefined) {
        var global = window
    }
</script>
````

3. Modify tsconfig.app.json
````
"compilerOptions": {
    "types" : ["node"]
}
````

## Setup

````
$ amplify init

Note: It is recommended to run this command from the root of your app directory
? Enter a name for the project hvag
? Enter a name for the environment dev
? Choose your default editor: Visual Studio Code
? Choose the type of app that you're building javascript
Please tell us about your project
? What javascript framework are you using angular
? Source Directory Path:  src
? Distribution Directory Path: dist/hvag
? Build Command:  npm run-script build
? Start Command: ng serve
Using default provider  awscloudformation

For more information on AWS Profiles, see:
https://docs.aws.amazon.com/cli/latest/userguide/cli-multiple-profiles.html

? Do you want to use an AWS profile? Yes
? Please choose the profile you want to use amplify-user
⠇ Initializing project in the cloud...

$ amplify add auth

$ amplify add api

$ amplify push

````

##  Importing the Amplify Angular Module and the Amplify Provider

Import the configuration file and load it in main.ts:
````
import Amplify from 'aws-amplify';
import amplify from './aws-exports';
Amplify.configure(amplify);
````

In the app module src/app/app.module.ts import the Amplify Module and Service:
````
import { AmplifyAngularModule, AmplifyService } from 'aws-amplify-angular';

@NgModule({
  ...
  imports: [
    ...
    AmplifyAngularModule
  ],
  ...
  providers: [
    ...
    AmplifyService
  ]
  ...
});
````

## Components

Amplify provides UI components that can be used in our view templates.

Try `<amplify-authenticator></amplify-authenticator>`

## Styles

Add the following to your styles.css file to use the default styles: `@import '~aws-amplify-angular/Theme.css';`
