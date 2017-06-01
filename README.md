# JavaScript design pattern(s)

JavaScript design patterns you should know

 * Module
 * Prototype
 * Observer
 * Singleton


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
