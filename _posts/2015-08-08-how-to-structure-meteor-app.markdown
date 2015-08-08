---
layout: post
title:  "How to structure your meteor app"
date:   2015-08-08 09:48:00
categories: meteor
---

Prerequisite: [Meteor official doc on structuring your applications][doc]

# Major goals of structuring your meteor app
- Another developer should be able to understand your app structure in a
  short amount of time.
- When you see some code, e.g. a function call, you should be able to know the
  location of the file that contains the definition of the code immediately.
- Your files should be small.
- You should be able to easily reason the loading order of your app.
- A global namespace and its methods should be confined into one folder or one
  file.

# My way of structuring a meteor app
- before/
  - lib/  
    There are three and only three lib folders in the app. This will be loaded
    firstly. Therefore, it is loaded before any js files excluding packages.
    - before/  
      - 0-lodash.js  
        ```_ = lodash```  
        I replace underscore with lodash.  
        I use number prefix to maintian loading order in a folder.
      - constants.js  
        ```Constant = {}```
    - schemas/
      - users.js  
        ```Meteor.users.attachSchema(UserSchema)```  
        I use [simple schema][simple-schema].
- client/
  - lib/
    This file wil be loaded before any server side files. Do `NOT` nest folders
    more then two levels, since it will not ensure a lower loading order than
    the ```before/lib/``` folder. You can use number prefix to ensure loading
    order.  
    ```server/lib/helpers/format-time.js # GOOD```  
    ```server/lib/helpers/utils/formater.js # BAD```  
    - constant.js  
      ```Constant.CLIENT_CONST = true```  
      Define client side constants
  - config/  
    - iron-router.js  
      ```Router.onBeforeAction(hook)```  
      Configure packages. I use [iron router][iron-router]
  - routes/
    This folder is all the routes files. Each js and html pair represent a
    route I defined in ```client/router.js```. E.G.  
    ```client/routes/users/user-id/posts/post-id/post-id.js```
    ```client/routes/users/user-id/posts/post-id/post-id.html```
  - components/  
    This folder contains resusable components.  
    This folder should not have more than one level of nesting, since all
    components are independent to each other. E.G.:  
    ```client/components/current-time/current-time.js```  
    ```client/components/current-time/current-time.html```  
  - stylesheets/
  - index.html
  - router.js  
    Define routes here.
  - subscriptions.js  
    ```Meteor.subscribe('users')```
    ```Meteor.subscribe('categories')```
    I put all subscriptions in one file.
- methods/
- private/
- public/
- server/
  - lib/  
    This file wil be loaded before any server side files. Do `NOT` nest folders
    more then two levels, since it will not ensure a lower loading order than
    the ```before/lib/``` folder. You can use number prefix to ensure loading
    order.  
    ```server/lib/helpers/format-time.js # GOOD```  
    ```server/lib/helpers/utils/formater.js # BAD```  
    - constant.js  
      ```Constant.SERVER_CONST = true```  
      Define server side constants
  - publications/
    - users.js  
      Meteor.publish('users', function() { return Meteor.roles.find() })
      Publish a collection.
  - authorizations/
    - users.js  
      Meteor.users.allow(authorizationRules)
      Define authorizations for a collection.
- router.js  
  Server side routers. (Iron router require a server-side router to be shared
  by the front tned)

# I wrote a yeoman [generator][generator-meteor-poetic] to do the chore

[doc]: http://docs.meteor.com/#/full/structuringyourapp
[simple-schema]: https://github.com/aldeed/meteor-simple-schema
[iron-router]: https://github.com/iron-meteor/iron-router
[generator-meteor-poetic]: https://github.com/poetic/generator-meteor-poetic
