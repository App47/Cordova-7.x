# Cordova-7.x
App47 plugin for Cordova (PhoneGap) version 7.x

## Supported Platforms

* iOS Version 8.0+
* Android API Version 19 (KitKat)

## Installation

Navigate to your project directory and if you haven't already, set the platforms you want to support:
```
$ cordova platform add ios android 
``` 

Install the plugin with:
```
$ cordova plugin add https://github.com/App47/Cordova-7.x
``` 

## Configuring the Agent
The agent can now be initialized in Javascript alone so that the platform directories do not need to be modified.  
```
app47.configureAgent("578f8287db8fe908ba0004d7");
```

Your javascript will also have to be sure to pass onResume and onPause events to the Agent.  The following is a snippet of code to configure the agent, set notification handlers and pass along the events:
```
    onDeviceReady: function() {
        // configure the agent
        app47.configureAgent("578f8287db8fe908ba0004d7");

        // set up onResume, onPause event handlers to pass to Agent
        document.addEventListener('resume', this.onResume.bind(this), false);
        document.addEventListener('pause', this.onPause.bind(this), false);
    },


    onResume: function() {
        app47.onResume();
    },

    onPause: function() {
        app47.onPause();
    },
```

## Using the Agent
The name `app47` will essentially be injected into your app's JS files. Thus, you can access corresponding methods like so:

```
app47.genericEvent("awesome event");
```

Where the code above invokes a generic event named "awesome event". Note, the Cordova plugins make better use of Cordava JavaScript callbacks like so:

```
app47.timedEvent("button pressed", function(timedEventId){
  //timedEventId is the ID from starting a timed event
  //code to press a button, etc
  //App47 PG plugin will automatically stop the timed event
});
``` 

Note in the code above, there is no need to start nor stop a timed event -- the code in the callback (which is passed in the event's id) will be invoked and after a successful invocation, the timed event will be stopped. You can optionally pass in a 2nd function that'll be invoked upon some error.



