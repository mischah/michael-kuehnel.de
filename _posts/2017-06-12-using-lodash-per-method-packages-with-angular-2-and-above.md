---
layout: post
lang: en_GB
title:  "Quick Tip: Using Lodash per method packages with Angular (2 and above)"
date:   2017-06-12 11:00:00
category: Angular
tags: "Angular, Lodash, Quick Tip, npm, types, import"
image: ""
excerpt: "I didn’t get how to import per method packages and how to include the types in my project. It’s not that hard but I invested some time to get this straight. Hope this little tip can save you half an hour :blush:"
disqusIdentifier: 2017-06-13-using-lodash-per-method-packages-with-angular-2-and-above
---

# Problems with using Lodash per method packages

I didn’t get how to import per method packages and how to include the types in my project.

Therefore I encountered on or another of the following error Messages:

```bash
ERROR in /path/to/project/src/app/my.component.ts (3,10): Module '"/path/to/project/node_modules/@types/lodash/index"' has no exported member 'lodash'.
```

```bash
ERROR in /path/to/project/src/app/my.component.ts (3,22): Module '"/path/to/project/node_modules/@types/lodash.drop/index"' resolves to a non-module entity and cannot be imported using this construct.
```

```bash
ERROR in /path/to/project/src/app/my.component.ts (71,24): Cannot find name 'dropRight'.
```

```bash
ERROR in Cannot read property 'getLineAndCharacterOfPosition' of undefined
```

It’ actually pretty much straight forward to fix these errors like described below

## Installing Lodash per method packages

In addition to the Lodash packages you have to install the type definitions:

```bash
npm install --save lodash.drop
npm install --save @types/lodash.drop

npm install --save lodash.dropright
npm install --save @types/lodash.dropright
```

## Add type definitions to your project

Add just the one and only item to the `types` array in `src/tsconfig.app.json`:

```javascript
{
  "compilerOptions": {
    "types": [
      "lodash"
    ]
  }
}
```

*Note: No need to add each and every installed lodash method in here.*

## Import methods where you need them

Just act like you have installed the whole Lodash package:

```javascript
import { drop, dropRight } from 'lodash';

// […]
visiblePages = dropRight(totalPages, PagesAboveVisible);
```

----

Looks easy, but I invested some time to get this straight. Hope this little tip can save you half an hour :blush:
