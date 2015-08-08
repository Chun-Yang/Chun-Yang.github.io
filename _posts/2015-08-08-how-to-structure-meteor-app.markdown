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

        I replace underscore with lodash here. , I use number
        prefix to maintian loading order in a folder.

      - constants.js

        ```Constant = {}```

    - schemas/
      - users.js

        ```Meteor.users.attachSchema(UserSchema)```
        I use [simple schema][simple-schema].

- client/
  - autoruns/
  - components/
  - config/
  - lib/
  - routes/
  - stylesheets/
  - template-helpers/
    - index.html
    - router.js
    - subscriptions.js
- collection-helpers/
- methods/
- private/
- public/
- server/
  - authorizations/
  - factories/
  - lib/
  - methods/
  - publications/
  - router.js

[doc]: [http://docs.meteor.com/#/full/structuringyourapp]
[simple-schema]: https://github.com/aldeed/meteor-simple-schema
