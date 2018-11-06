# What's here?

### A prototype of the Alexa skill for Salesforce Marketing Cloud

## Setup

### 1. Setup API Integration in Marketing Cloud

See [API Integration](https://developer.salesforce.com/docs/atlas.en-us.mc-app-development.meta/mc-app-development/api-integration.htm) for more details.

#### Add an API Integration component

Add an `API Integration` component in Marketing Cloud.
- Make sure *Perform server-to-server requests* is *checked*.
- Select the appropriate Marketing Cloud scope for your API calls.

#### Put the API Key in Environment Variables

Get the `ClientID` and `ClientSecret` from API Integration component and put in the environment variables below on your local computer:
- `SFMC_API_CLIENTID=YOUR_CLIENTID`
- `SFMC_API_CLIENTSECRET=YOUR_CLIENTSECRET`

See [Get an API Key](https://developer.salesforce.com/docs/atlas.en-us.noversion.mc-getting-started.meta/mc-getting-started/get-api-key.htm) for more details.

### 2. Setup local dev environment

The steps below are for MacOS. Modify as needed for your specific operating system.

#### Pre-requisites

Install these on your local computer (skip what you already have!)

- [Git](https://git-scm.com/downloads)
- [Visual Studio Code](https://code.visualstudio.com/download)
- [Node.js](https://nodejs.org/en/download/)

Next:
- Register for an [AWS Account](https://aws.amazon.com/)
- Register for an [Amazon Developer Account](https://developer.amazon.com/)
- Check out the [Alexa Skills Kit Developer Console](https://developer.amazon.com/alexa/console/ask)
- Install and setup [ASK CLI](https://developer.amazon.com/docs/smapi/quick-start-alexa-skills-kit-command-line-interface.html)

> *NOTE:* Use the `default` profile when you setup the `ASK CLI`

## Local development

The steps below are for MacOS. Modify as needed for your specific operating system.

### Get the source code

Open a `Terminal` window and type the commands below:
```bash
$ cd ~
$ git clone https://github.com/ajaykumar127/Alexa_Integration_SF-tryout_by_Ajay.git
```

### Install dependencies
In the `Terminal` window, type the commands below to install Node package dependencies:

```bash
$ cd ~/sfmc-alexa
$ npm install
```

## Run locally on yur computer

During development, it's a pain to have to deploy your intent handler code to AWS Lambda everytime you make a change.

There's a better way! You can connect Alexa to your local development environment and not use AWS Lambda at all. This avoids deploying to AWS Lambda every time you make changes to your intent handler code. Your code changes are available to Alexa instantly.

This approach is super useful for local debugging & testing, and for demos too!

There are many *free* tools that provide this magic sauce such as [ngrok](https://ngrok.com) and [Serveo](http://serveo.net).

We will use [Serveo](http://serveo.net) in our case because it needs nothing other than `ssh` and lets us specify a fixed custom domain name for our Alexa skill to use.

### Here's how this works

- When this prototype starts, it runs a local `Express` server on your computer
- Run `ssh` on your local computer to expose `http://localhost:3000` as `https://innovationday2018.serveo.net` using `serveo`
- Configure your Alexa skill to connect to `https://innovationday2018.serveo.net`
- `serveo` proxies all Alexa requests to the `Express` server running on your computer
- Your local `Express` server uses the same Lambda functions to satisfy Alexa intents
- Life is good!

### Open the project in Visual Studio Code

- Launch Visual Studio Code
- Click `Open` and choose the folder `~/sfmc-alexa`
- In VS Code, click `View -> Terminal` to open a `Terminal` window
- In the VS Code `Terminal` window, type `npm install`

### Start `serveo`

- In the VS Code `Terminal` window, click `+` to start a 2nd `Terminal` window
- In the 2nd `Terminal` window, type `./run-serveo.sh` (or `./run-serveo.bat` for Windows)
- This starts `ssh` and traffic from `https://sfmchackday2018.serveo.net` is proxied to your local server.
- `ssh` is happily running in this 2nd `Terminal` window. You can switch to other windows as usual

### Configure the endpoint for the Alexa skill

- Switch back to the 1st terminal window in VS Code
- Type the following command to deploy the Alexa skill:

```bash
$ npm run-script deploy
```

### Start the local `Express` server

- In the VS Code terminal window, switch back to the 1st terminal window
- Type the following command:

```bash
$ npm start
```
