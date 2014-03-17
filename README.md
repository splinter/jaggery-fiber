jaggery-fiber
=============


Initializing an App
-------------------
The Fiber script considers an app as a collection of packages and allows individual files to be required.It will look for a package.json file in root directory of your app;

```javascript
  {
    "subPackages":["Packages you want to deploy"]
  }
```

Creating an App instance
-----------------------
Fiber creates a virtual model of your application when it is initializes and allows the logic that you write to reference the app context from a single point.

```javascript
  var fiber=require('fiber');
  fiber.app.init(function(context){
      //Any initialization logic for your app
  });
```


Using Components
----------------
The Fiber script allows you to define reusable bundles of logic called components.A component is some piece of logic that creates, alters or checks data presented to the user.

###Creating a component
All components are tracked on a per app basis

```javascript
  var fiber=require('fiber');
  fiber.app.components.register('c1',function(){
    
  });
```
