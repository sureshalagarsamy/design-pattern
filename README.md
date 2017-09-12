# JavaScript design pattern(s)

JavaScript design patterns you should know

 * Module
 * Prototype
 * Observer
 * Singleton


### Singleton

 simplest/cleanest way to implement singleton pattern in JavaScript

```javascript
var myInstance = {
  method1: function () {
    // ...
  },
  method2: function () {
    // ...
  }
};
```

If you want private members on your singleton instance, you can do something like this:

```javascript
var myInstance = (function() {
  var privateVar = '';

  function privateMethod () {
    // ...
  }

  return { // public interface
    publicMethod1: function () {
      // all private members are accesible here
    },
    publicMethod2: function () {
    }
  };
})();
```

This is has been called the module pattern, it basically allows you to encapsulate private members on an object, by taking advantage of the use of closures.

Good enough i guess..

Still not clear :( ok I will give more information... Pleae stay back.

### Singleton

A Singleton only allows for a single instantiation, but many instances of the same object. The Singleton restricts clients from creating multiple objects, after the first object created, it will return instances of itself.

One example is using an office printer. If there are ten people in an office, and they all use one printer, ten computers share one printer (instance). By sharing one printer, they share the same resources.

```javascript
var printer = (function () {
  var printerInstance;
  function create () {
    function print() {
      // underlying printer mechanics
    }
    function turnOn() {
      // warm up
      // check for paper
    }
    return {
      // public + private states and behaviors
      print: print,
      turnOn: turnOn
    };
  }
  return {
    getInstance: function() {
      if(!printerInstance) {
        printerInstance = create();
      }
      return printerInstance;
    }
  };
  function Singleton () {
    if(!printerInstance) {
      printerInstance = intialize();
    }
  };

})();
```

The create method is private because we do not want the client to access this, however, notice that the getInstance method is public. Each officer worker can generate a printer instance by interacting with the getInstance method, like so:


```javascript
var officePrinter = printer.getInstance();
```

In AngularJS, Singletons are distributed over a large area, the most notable being services, factories, and providers.

### Module

The module pattern is probably the most widely used pattern in JavaScript. Let's walk through an example to see how it works.

```javascript
var robot = {
    identity: "Suresh",
    workIn: function () {
        console.log("Do automated jobs!");
    },
    kill: function () {
        console.log(this.identity + "kill anyone");
    }
};
```

This version of ```robot``` is perfectly serviceable. It can perform a task as per the command. However, it has a serious weakness. This ```robot``` identity property is publicly accessible.

Any code in your application could potentially overwrite it and cause ```robot``` to malfunction. For example:

```javascript
// Some joker put this in your codebase
robot.identity = "virus";

// Outputs: "virus kill anyone"
robot.kill();
```

So to avoid these sorts of situations we need a way to keep certain pieces of data private. JavaScript gives us just such a tool the immediately invoked function expression (IIFE).

A standard IIFE looks like this:

```javascript
(function () {
    // Code goes here
})();
```

The advantage of the IIFE is that any vars declared inside it are inaccessible to the outside world. So how does that help us? The key is that an IIFE can have a return value just like any other function.

```javascript
var robot = (function() {
    var identity = "Suresh";
    return {
        workIn: function () {
            console.log("Do automated jobs!");
        },
        kill: function () {
            console.log(identity + "kill anyone");
        }
    };
})();
console.log(robot.identity);	// Output: undefined
robot.workIn();                 // Output: Do automated jobs!
```

As you can see, we were able to use the IFFE's return value to make ```robot```'s utility functions publicly accessible. And at the same time we were able to ensure that ```robot```'s ```identity``` remains a secret from outside.

You might be wondering when using the module pattern is a good idea. The answer is that it works well for situations like if you need to both enforce ```privacy for some of your data``` and ```provide a public interface```, then the module pattern is probably a good fit.
