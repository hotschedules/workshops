# Agent apps

This guide serves as a quick start guide to creating an agent, and writing an agent app to run on it.

# Preparation

In order to begin installing and working with an agent, there are a few preparation stages required.

## Install node and npm

Head on over to [https://nodejs.org/en/download/](https://nodejs.org/en/download/)

Download the installer for your operating system.

Run the installer, and follow through the on screen steps to get node running on your computer.

Next, run the npm install command to make sure you have the latest version.

```sudo npm install npm -g```

## Install and setup npmrc

Install the npmrc module for node at the global level.

```sudo npm install -g npmrc```

Now, open up the npmrc file (If you are on mac or linux, this will be ~./npmrc, on windows it will be C:\Users\<username>\npmrc)

It needs to contain the following content.

```
registry=http://rbcplatform.artifactoryonline.com/rbcplatform/api/npm/npm-virtual
_auth=cmJjYWdlbnQ6QVA4WUJiUDJGdDhRa01iM3MyN3Y3VTdWOWRO
always-auth=true
email=developer@hotschedules.com
```

Save the file.

# Getting the agent tools

Now that you have a working node environment set up, with the correct npmrc profile - it is time to begin downloading the agent tools.

## Install

hs-agent-tools is a node module that essentially wraps various pieces of functionality for the agent, but also has functionality to do things like agent installs, app creation, etc.

to install the module, run the following command :

```npm install -g hs-agent-tools```

## Creating an agent and app

When using hs-agent-tools, you will create an agent, which is coupled with it's own app install.

### hs-agent-builder

To create an application, open a terminal (or adminstrator priveleged cmd if on windows) and navigate to the directory where you want to create your app.

Run the following command to create an app named "my-app"

```hs-agent-builder create-app -w ./my-app my-app --verbose```

This will give you a folder structure which has the app and agent together. The app doesn't really do anything yet, but the scaffolding is now in place to building something more useful.

### Ensuring the install worked

Before going into the task of writing a more useful application please make sure the install worked.

Run the app by navigating into the _my-app_ directory and running the following command :

```hs-agent-runner -w ./agent start```

The agent should now run, and will register with the platform.

#Creating a new store and data type

Today's task will involve using a store, and also a custom type for our data upload.

## Creating the store

Open up a browser and navigate to :

[https://tools.bodhi.space/#/](https://tools.bodhi.space/#/)

Login, and then open up _Bodhi Store Manager_ from the list of available applications.

In the top right of the user interface, you will see an _add store_ button. Click it.

You will be taken to a form which will ask for the details of your store. Fill this in, and click the _add store_ button at the bottom of the form.

You will be taken back to the store list, click on the one you created, and you will be navigated to it's profile page. In the URL at the top, you will see the id of this store, take note of it, you will need it soon.

## Creating the type

Go back to :

[https://tools.bodhi.space/#/](https://tools.bodhi.space/#/)

This time I want to create a type. In today's workshop, our type will be for temperature and air pressure.

So open up Bodhi Types from the list.

On the left hand side, you will see a menu item which says _New Type_.

You will see a text box at the top which says "Created Type Name" - Type "TemperatureAndAir" in here. as this is what we are going to call the type - in real world development scenario, you could call it whatever you want.

In properties, we are going to have four of them so fill out the form as follows.

* store_id, of type String.
* timestamp, of type DateTime.
* temperature, of type Integer.
* airPressure, of type Integer.

At the top of the form, click the publish icon, to have your type created.


# Writing more useful functionality

For the process of making this lab more easy to follow - Please get a copy of the agent app template located at the following bitbucket git repository:

[https://bitbucket.org/redbookplatform/agent_app_workshop](https://bitbucket.org/redbookplatform/agent_app_workshop)

This application can be broken down into key points which allow us to carry out certain tasks they are laid out as follows :

* package.json
    * Configutation of the application 
* index.js 
    *  This is the entry point of the application, as configured in package.json.
* lib/plugins.js
    * For bringing in additional services, handlers, modules etc.
* lib/handlers
    * Handlers are modules which we will write in order to call when things happen. They usually perform one main task each.
* lib/services
    * Services are modules of code which we will write with  the intention of exporting various functions for related functionality. These can be simple or complex.
    * they are also used to supply functioality that is exposed by the agent, such as registering with the platform, etc.
* lib/sources
    * Sources are for managing sources of data which are for incoming data, or things that we may wish to watch for changes.

# Walking through the code
In today's workshop - I will walk you through the code in this project, line by line.

Keep an eye on the repository of the repository going forward, because I will actually be publishing a video on this as well, it just hasn't been done yet!

# Run the application

Remember the store_id we took note od earlier? We need to associate this agent with that id before we run it. 

So open up the package.json inside the my-app directory, and change :

_"store_id":""_

to

_"store_id":"YOUR ID HERE"_

To run the agent with the application we have created, simply navigate to the directory of the app, and run the following command.

```hs-agent-runner -w ./agent start```

To kill the agent, run the following command

```hs-agent-runner -w ./agent stop```

# Register the agent
Now that you have the agent running, with an app that works, you need to actually register the agent, so that the API will allow it to authenticate and begin sending requests.

## Editing the .agent file
Navigate to the _my-app/agent_ directory.

there is a hidden file in this directory called agent.

If you are on windows, you might need to enable the _""view hidden files"_ feature. After which you will be able to see it, it can be opened in any standard text editor.

On linux / mac - hidden files are prefixed with a '.' to make them hidden. You can open it with any of the following commands. Any editor can edit them.

Once you open the file, you will see the registration key, copy it.

## Using the key to register
Now, go back to bodhi tools : 

[https://tools.bodhi.space/#/](https://tools.bodhi.space/#/)

Select the agent manager.

On the left, you will see an item on the left menu that says "Registration", select it.

You will see a list of your stores (You may only have the one you createdin this workshop at present).

In the text field to the right of your store, paste in the registration key, and click the _"request"_ key.

Now you need to restart your agent - First, navigate to your _my-app_ directory and run the following commands:

```hs-agent-runner -w ./agent stop```
```hs-agent-runner -w ./agent start```


The agent should run, and at then output a green line of output, which says :

_```agent signed on```_

# Running the test script
The particular app from this exercise, is bundled with a test script. Which basically just generates some dummy data.

Open up a second terminal and navigate to the _my-app_ directory.

Run the test script, using the following command :

```node test.js```

This will populate the file.txt (Which the app watches for changes). And upload them, line by line, to the API.


