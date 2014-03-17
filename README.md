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
  fiber.app(function(context){
      //Any initialization logic for your app
  });
```


Components
----------------
The Fiber script allows you to define reusable bundles of logic called components.A component is some piece of logic that creates, alters or checks data presented to the user.

###Creating a component
There are two types of  components that can be deployed by users;

1. Logic components
2. Error handling components


####Logical components

```javascript
  var fiber=require('fiber');
  fiber.app.component('myComponent',function(context,handlers){
      handlers(); //Make sure to invoke the other handlers
  });
```

####Error handling components

```javascript
  var fiber=require('fiber');
  fiber.app.component('errHandler', function(err,context,handlers){
       handlers(err); //Allow other error handlers to process the request
  });
```

###Using components
Components can be connected together to form a chain of execution that transforms a data object;

```javascript
  var fiber=require('fiber');
  var data={};
  fiber.app.components.chain('myComponent').
                  chain('errHandler').
                  resolve(data,req,res,session);
```

There is also two other syntax types that are supported by fiber;

```javascript
  fiber.app.components.chain(function(context,handlers){
        //Some logic
  }).
  chain('myComponent').
  resolve(data,req,res,session);
  
```

You can defin multiple components in one line using;
```javascript
  fiber.app.components.chain('myComponent,errHandler').resolve(data,req,res,session);
```

####Running some logic at the end of a chain

You will often want to run some piece of logic at the end of a component chain.Fiber allows this through the finally method;

```javascript
  fiber.app.components.chain('myComponent').
                  chain('errHandler').
                  finally(function(context,req,res,session){
                  }).
                  resolve(data,req,res,session);
```
