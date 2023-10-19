
# TypeScript coding 


## Table of contents

* [Typescript coding style guide](#typescript-coding-style-guide)
  * [Naming](#naming)
  * [Naming Conventions](#naming-conventions)
  * [Naming Booleans](#naming-booleans)
  * [File names](#file-names)
  * [Brackets](#brackets)
  * [Spaces](#spaces)
  * [Semicolons](#semicolons)
  * [Code Comments](#code-comments)
  * [Barrels](#barrels)
  * [S-I-D](#sid)
  *   [Avoid contractions](#avoid-contractions)
  *   [Avoid context duplication](#avoid-context-duplication)
  *   [Reflect the expected result](#reflect-the-expected-result)
  *   [A/HC/LC Pattern](#a-hc-lc-pattern)
  *   [Actions](#actions)
      *   [get](#get)
      *   [set](#set)
      *   [reset](#reset)
      *   [fetch](#fetch)
      *   [remove](#remove)
      *   [delete](#delete)
      *   [compose](#compose)
  *   [Context](#context)
  *   [Prefixes](#prefixes)
      *   [is](#is)
      *   [has](#has)
      *   [should](#should)
      *   [min/max](#min-max)
* [Nest coding style guide](#nest-coding-style-guide)
  * [Organize imports](#organize-imports)
  * [Use typescript aliases](#use-typescript-aliases)
  * [Specify component member accessor explicitly](#specify-component-member-accessor-explicitly)
  * [Component structure](#component-structure)
  * [private Subject, public Observable pattern](#private-subject,-public-observable-pattern)
  * [Services inside HTML templates](#services-inside-HTML-templates)
  * [Manage Subscriptions Declaratively](#manage-subscriptions-declaratively)
* [Postgresql](#postgresql)
  * Names
## Typescript coding style guide

### Naming

The name of a variable, function, or class, should answer all the big questions. It should tell you why it exists, what it does, and how it is used. If a name requires a comment, then the name does not reveal its intent.

**Use meaningful variable names.**

Distinguish names in such a way that the reader knows what the differences offer.

Bad:

 ``` typescript
 function isBetween(a1: number, a2: number, a3: number): boolean {
   return a2 <= a1 && a1 <= a3;
 }
```

Good: 

``` typescript
 function isBetween(value: number, left: number, right: number): boolean {
   return left <= value && value <= right;
 }

```

**Use pronounceable variable names**

If you can't pronounce it, you can't discuss it without sounding weird.

Bad:

``` typescript
class Subs {
  public ccId: number;
  public billingAddrId: number;
  public shippingAddrId: number;
}

const primerNombre = 'Gustavo'
const amigos = ['Kate', 'John']
```

Good:

``` typescript
class Subscription {
  public creditCardId: number;
  public billingAddressId: number;
  public shippingAddressId: number;
}

const primerNombre = 'Gustavo'
const amigos = ['Kate', 'John']

```

**Avoid mental mapping**

Explicit is better than implicit.<br />
*Clarity is king.*

Bad:

``` typescript
const u = getUser();
const s = getSubscription();
const t = charge(u, s);
```

Good:

``` typescript
const user = getUser();
const subscription = getSubscription();
const transaction = charge(user, subscription);
```

**Don't add unneeded context**

If your class/type/object name tells you something, don't repeat that in your variable name.

Bad:

``` typescript
type Car = {
  carMake: string;
  carModel: string;
  carColor: string;
}

function print(car: Car): void {
  console.log(`${car.carMake} ${car.carModel} (${car.carColor})`);
}
```

Good:

``` typescript
type Car = {
  make: string;
  model: string;
  color: string;
}

function print(car: Car): void {
  console.log(`${car.make} ${car.model} (${car.color})`);
}
```

### Naming Conventions

* Use camelCase for variable and function names

Bad:

``` typescript
var FooVar;
function BarFunc() { }
```

Good:

``` typescript
var fooVar;
function barFunc() { }
```

* Use camelCase of class members, interface members, methods and methods parameters

Bad:

``` typescript
class Foo {
  Bar: number;
  Baz() { }
}
```

Good:

``` typescript
class Foo {
  bar: number;
  baz() { }
}
```

* Use PascalCase for class names and interface names.

Bad:

``` typescript
class foo { }
```

Good:

``` typescript
class Foo { }
```

* Use PascalCase for enums and camelCase for enum members

Bad:

``` typescript
enum notificationTypes {
  Default = 0,
  Info = 1,
  Success = 2,
  Error = 3,
  Warning = 4
}
```

Good:

``` typescript
enum NotificationTypes {
  default = 0,
  info = 1,
  success = 2,
  error = 3,
  warning = 4
}
```

### Naming Booleans

* Don't use negative names for boolean variables.

Bad:

``` typescript
const isNotEnabled = true;
```

Good:

``` typescript
const isEnabled = false;
```

* A prefix like is, are, or has helps every developer to distinguish a boolean from another variable by just looking at it

Bad:

``` typescript
const enabled = false;
```

Good:

``` typescript
const isEnabled = false;
```

### File names

* File names must be all lowercase and may include underscores (_) or dashes (-), but no additional punctuation. Follow the convention that your project uses. Filenames’ extension must be .ts,.js
```
app.js
utils.js
product-utils.js

```

* Directory names
  
```
/components/
/utils/
```

### Brackets

* **OTBS** (one true brace style). [Wikipedia](https://en.wikipedia.org/wiki/Indentation_style#Variant:_1TBS_(OTBS))

The one true brace style is one of the most common brace styles in TypeScript, in which the opening brace of a block is placed on the same line as its corresponding statement or declaration.

``` typescript
if (foo) {
  bar();
}
else {
  baz();
}
```

* Do not omit curly brackets
  
* **Always** wrap the body of the statement in curly brackets.

### Spaces

Use 2 spaces. Not tabs.

### Semicolons

Use semicolons.

### Code Comments

> So when you find yourself in a position where you need to write a comment, think it through  and  see  whether  there  isn't  some  way  to  turn  the  tables  and  express  yourself  in code. Every time you express yourself in code, you should pat yourself on the back. Everytime you  write  a  comment,  you  should  grimace  and  feel  the  failure  of  your  ability of expression.

**Bad Comments**

Most comments fall into this category. Usually they are crutches or excuses for poor code or justifications for insufficient  decisions, amounting to little more than the programmer talking to himself.

**Mumbling**

Plopping in a comment just because you feel you should or because the process requires it, is a hack. If you decide to write a comment, then spend the time necessary to make sure it is the best comment you can write.

**Noise Comments**

Sometimes you see comments that are nothing but noise. They restate the obvious and provide no new information.

``` typescript
// redirect to the Contact Details screen
this.router.navigateByUrl(`/${ROOT}/contact`);
```

``` typescript
// self explanatory, parse ...
this.parseProducts(products);
```

**Scary noise**

``` typescript
/** The name. */
private name;

/** The version. */
private version;

/** The licenceName. */
private licenceName;

/** The version. */
private info;
```

Read these comments again more carefully. Do you see the cut-paste error? If authors aren't  paying attention when comments are  written (or pasted), why should  readers be expected to profit from them?

**TODO Comments**

In general, TODO comments are a big risk. We may see something that we want to do later so we drop a quick **// TODO: Replace this method** thinking we'll come back to it but never do.

If you're going to write a TODO comment, you should link to your external issue tracker.

There are valid use cases for a TODO comment. Perhaps you're working on a big feature and you want to make a pull request that only fixes part of it. You also want to call out some refactoring that still needs to be done, but that you'll fix in another PR.

``` typescript
// TODO: Consolidate both of these classes. PURCHASE-123
```

This is actionable because it forces us to go to our issue tracker and create a ticket. That is less likely to get lost than a code comment that will potentially never be seen again. 

**Comments can sometimes be useful**

* When explaining why something is being implemented in a particular way.
* When explaining complex algorithms (when all other methods for simplifying the algorithm have been tried and come up short).

**Comment conventions**

* Write comments in *English*.
  
* Do not add empty comments
  
* Begin single-line comments with a single space
  
Good:

``` typescript
// Single-line comment
```

Bad:

``` typescript
//Single-line comment
//  Single-line comment
```

* Write single-line comments properly
  
  * Single-line comments should always be preceded by a single blank line.
  * Single-line comments should never be followed by blank line(s).

Good:

``` typescript
const x;

// This comment is valid
const y;
```

Bad:

``` typescript
const x;

// This comment is not valid

const y;
```
``` typescript
const x;
// This comment is not valid

const y;
```

* Do not write embedded comments

  * Do not write comments between declaration of statement and opening curly brackets.
  * Place comments above statements, or within statement body.

Good:

``` typescript
// This method does something..
public method() {
}
```

Bad: 

``` typescript
public method() { // This method does something..
}
```

``` typescript
public method() {
// This method does something..
}
```

### Barrels

> A barrel is a way to rollup exports from several modules into a single convenience module. The barrel itself is a module file that re-exports selected exports of other modules.

> **import noise** - this is an issue seen in languages where there are dependencies that need to be "imported", "required", or "included" and the first (1 - n) lines are non functional code.

Example of a barrel file:

``` typescript
export * from './product-added-dialog.component';
export * from './website-selector.component';
export * from './product-family-selector.component';
export * from './individual-product-selector.component';
export * from './license-type-selector.component';
export * from './period-and-quantity-selector.component';
```

How to use it inside components:

Good:

``` typescript
import { CartsService, PaidSupportService, SettingsService } from '@modules/services';
```

Bad:

``` typescript
import { SettingsService } from './settings/settings.service';
import { CartsService } from './carts/carts.service';
import { PaidSupportService } from './paid-support/paid-support.service';
```

* Barrel files are named index.ts by convention
* Do not import a barrel in the files that are already used in that barrel because this leads to circular dependency

### S.I.D
* Short. A name must not take long to type and, therefore, remember;
* Intuitive. A name must read naturally, as close to the common speech as possible;
* Descriptive. A name must reflect what it does/possesses in the most efficient way.

Bad:
  ```

const a = 5 // "a" could mean anything
const isPaginatable = a > 10 // "Paginatable" sounds extremely unnatural
const shouldPaginatize = a > 10 // Made up verbs are so much fun!
```
Good:
```
const postCount = 5
const hasPagination = postCount > 10
const shouldPaginate = postCount > 10 // alternatively
```
### Avoid contractions
-------------------------------------------

Do **not** use contractions. They contribute to nothing but decreased readability of the code. Finding a short, descriptive name may be hard, but contraction is not an excuse for not doing so.

    /* Bad */
    function getUsrNme() {
      // ...
    }
    
    /* Good */
    function getUserName() {
      // ...
    }
    
### Avoid context duplication
---------------------------------------------------------

A name should not duplicate the context in which it is defined. Always remove the context from a name if that doesn't decrease its readability.

    class UserService {
      /* Method name duplicates the context (which is "User") */
      getUserSettings(event) { 
        // ...
      }
    
      /* Reads nicely as `userService.getSettings()` */
      getSettings(event) { 
        // ...
      }
    }

### Reflect the expected result
-------------------------------------------------------------

A name should reflect the expected result.

    /* Bad */
    const isEnabled = itemCount > 3
    if(!isEnabled) {
      // ...
    }
    
    /* Good */
    const isDisabled = itemCount <= 3
    if(isDisabled) {
      // ...
    }

* * *

### Naming functions
=======================================

### A/HC/LC Pattern
-------------------------------------

There is a useful pattern to follow when naming functions:

    prefix? + action (A) + high context (HC) + low context? (LC)
    

Take a look at how this pattern may be applied in the table below.

Name

Prefix

Action (A)

High context (HC)

Low context (LC)

`getUser`

`get`

`User`

`getUserMessages`

`get`

`User`

`Messages`

`shouldDisplayMessage`

`should`

`Display`

`Message`

`isPaymentEnabled`

`is`

`Enabled`

`Payment`

* * *

### Actions
---------------------

The verb part of your function name. The most important part responsible for describing what the function _does_.

### `get`

Accesses data immediately (i.e. shorthand getter of internal data).

    function getUserFullName() {
      return this.firstName + ' ' + this.lastName;
    }
      

> See also [compose](#compose).

### `set`

Sets a variable in a declarative way, with value `A` to value `B`.

    let fruits = 0;
    
    function setFruits(nextFruits) {
      fruits = nextFruits;
    }
    
    setFruits(5);
    console.log(fruits); // 5

### `reset`

Sets a variable back to its initial value or state.

    const initialFruits = 5
    let fruits = initialFruits
    setFruits(10)
    console.log(fruits) // 10
    
    function resetFruits() {
      fruits = initialFruits
    }
    
    resetFruits()
    console.log(fruits) // 5

### `fetch`

Request for some data, which takes some indeterminate time (i.e. database request).

    function getUsers() {
      return this.userRepository.createQueryBuilder()
        .where('user.isActive = :isActive', { isActive: true })
        .getMany();
    }


### `remove`

Removes something _from_ somewhere.

For example, if you have a collection of selected filters on a search page, removing one of them from the collection is `removeFilter`, **not** `deleteFilter` (and this is how you would naturally say it in English as well):

    function removeFilter(filters, filterName) {
      return filters.filter((name) => name !== filterName)
    }
    
    const selectedFilters = ['price', 'availability', 'size']
    removeFilter(selectedFilters, 'price')

> See also [delete](#delete).

### `delete`

Completely erases something from the realms of existence.

Imagine you are a content editor, and there is that notorious post you wish to get rid of. Once you clicked a shiny "Delete post" button, the CMS performed a `deletePost` action, **not** `removePost`.

    function deleteUser(id) {
       return this.userRepository.delete(id);
    }

> See also [remove](#remove).

### `compose`

Creates new data from the existing one. Mostly applicable to strings, objects, or functions.

    function composePageUrl(pageName, pageId) {
      return (pageName.toLowerCase() + '-' + pageId)
    }

> See also [get](#get).

* * *

### Context
---------------------

A domain that a function operates on.

A function is often an action on _something_. It is important to state what its operable domain is, or at least an expected data type.

    /* A pure function operating with primitives */
    function filter(list, predicate) {
      return list.filter(predicate)
    }
    
    /* Function operating exactly on posts */
    function getRecentPosts(posts) {
      return filter(posts, (post) => post.date === Date.now())
    }

> Some language-specific assumptions may allow omitting the context. For example, in JavaScript, it's common that `filter` operates on Array. Adding explicit `filterArray` would be unnecessary.

\--

### Prefixes
-----------------------

Prefix enhances the meaning of a variable. It is rarely used in function names.

### `is`

Describes a characteristic or state of the current context (usually `boolean`).

    const color = 'blue'
    const isBlue = color === 'blue' // characteristic
    const isPresent = true // state
    
    if (isBlue && isPresent) {
      console.log('Blue is present!')
    }
### `has`

Describes whether the current context possesses a certain value or state (usually `boolean`).

    /* Bad */
    const isProductsExist = productsCount > 0
    const areProductsPresent = productsCount > 0
    
    /* Good */
    const hasProducts = productsCount > 0
   

### `should`

Reflects a positive conditional statement (usually `boolean`) coupled with a certain action.

    function shouldUpdateUrl(url, expectedUrl) {
      return url !== expectedUrl
    }
    
### `min`/`max`

Represents a minimum or maximum value. Used when describing boundaries or limits.

    /**
     * Renders a random amount of posts within
     * the given min/max boundaries.
     */
    function renderPosts(posts, minPosts, maxPosts) {
      return posts.slice(0, randomBetween(minPosts, maxPosts))
    }
## NestJs coding style guide

### Organize imports

With clean and easy to read import statements you can quickly see the dependencies of current code. Make sure you apply following good practices for import statements:

* Unused imports should be removed.
* Groups of imports are delineated by one blank line before and after.
* Groups must respect following order:
  * Angular imports (i.e. import { HttpClient } from '@angular/common/http')
  * Angular material imports (i.e. import { MatSelectChange } from '@angular/material/select')
  * 3rd party imports except rxjs (i.e. import { SessionStorageService } from 'ngx-webstorage')
  * rxjs imports (i.e import { skipWhile } from 'rxjs/operators')
  * application imports sorted by type (services, classes, interfaces, enums)

Bad:

``` typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { MatSelectChange } from '@angular/material/select';
import { SessionStorageService } from 'ngx-webstorage';

import { merge, Observable, BehaviorSubject } from 'rxjs';
import { filter, tap } from 'rxjs/operators';
import { INumberToTypeDictionary, Utils } from '@shared/classes';

import { ProductUtils } from '@modules/services/products/classes';

import { AdditionalServicesApi } from './additional-services-api';
```

Good:

``` typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { MatSelectChange } from '@angular/material/select';
import { SessionStorageService } from 'ngx-webstorage';

import { merge, Observable, BehaviorSubject } from 'rxjs';
import { filter, tap } from 'rxjs/operators';

import { INumberToTypeDictionary, Utils } from '@shared/classes';
import { ProductUtils } from '@modules/services/products/classes';
import { AdditionalServicesApi } from './additional-services-api';
```
### Use typescript aliases

This will avoid long relative paths when doing imports.

Bad:

``` typescript
import { UserService } from '../../../services/UserService';
```

Good:

``` typescript
import { UserService } from '@services/UserService';
```

### Specify component member accessor explicitly

TypeScript supports public (*default*), protected and private accessors on class members.

Bad:

``` typescript
export class ConsultingEntryComponent {
  quantities: number[] = [];
  isBeingRemoved = false;

  destroyed$ = new Subject<void>();

  constructor(private productsService: ProductsService) { }

  get isBeingProcessed(): boolean {
    return this.disabled || this.isBeingRemoved;
  }

  get isDiscountedPriceAvailable(): boolean {
    return !(Utils.isNullOrUndefined(this.fullPrice) || Utils.isNullOrUndefined(this.discounts));
  }

  onPeriodSelectionChanged(event: MatSelectChange): void {
    this.changeMade.next();
  }
}
```

Good:

``` typescript
export class ConsultingEntryComponent {
  public quantities: number[] = [];
  public isBeingRemoved = false;

  private destroyed$ = new Subject<void>();

  constructor(private productsService: ProductsService) { }

  public get isBeingProcessed(): boolean {
    return this.disabled || this.isBeingRemoved;
  }

  private get isDiscountedPriceAvailable(): boolean {
    return !(Utils.isNullOrUndefined(this.fullPrice) || Utils.isNullOrUndefined(this.discounts));
  }

  public onPeriodSelectionChanged(event: MatSelectChange): void {
    this.changeMade.next();
  }
}
```

Use the private or protected accessor as much as you can because it provides a better encapsulation.

### Component structure

Use the following component structure:

1. data members (i.e. public isBeingRemoved = false)
2. constructor
3. lifecycle hooks (following their execution order)
4. getters/setters
5. event handlers
6. other methods

Use the following component accessors order:

1. private
2. protected
3. public

* Separate each group with a whitespace before and after


### Barrels

Barrels can cause circular dependencies when they are used to import stuff from the same module.
Given the structure:
```
module/
|- a.component.ts
|- b.component.ts
|- b.model.ts
|- index.ts
```

index.ts
```
export * from 'b.component.ts';
export * from 'a.component.ts';
export * from 'b.model.ts';
```
Trying to import b.component.ts inside a.component.ts through index.ts will cause a circular dependency. 
To solve this issue we have to import b.component.ts directly.

### private Subject, public Observable pattern

Utilizing a private Subject and a public Observable allows us to lock down access to our Subject and prevent its modification.

The goal is to emit changes only from the service that the Subject belongs to and make the value emitted available through an observable. This allows us to have a SSOT (single source of truth).

Bad:

``` typescript
export class AdditionalServicesService extends AdditionalServicesApi {
  public escrowCartEntries$ = new BehaviorSubject<OrderItemModel[]>([]);
}
```

* The Subject is made public so it can be changed outside the service.

Good:

``` typescript
export class AdditionalServicesService extends AdditionalServicesApi {
  public escrowCartEntries$: Observable<OrderItemModel[]>;

  private escrowCartEntriesSubject$ = new BehaviorSubject<OrderItemModel[]>([]);
  
  constructor() {
    this.escrowCartEntries$ = this.escrowCartEntriesSubject$.asObservable();
  }
}
```

*  Here we utilize a Subject and an Observable derived from the Subject. We emit changes to the Subject from the service, and expose it to the outside world through the Observable


### Services inside HTML templates

Avoid referencing services in HTML templates.

Bad:

``` HTML
<div class="price">pricingService.articlePrice</div>
```

Good:

``` HTML
<div class="price">articlePrice</div>
```

Why to avoid it?

* It couples the service implementation with the HTML template
* It breaks the LoD (Law of Demeter)
* VS Code does not support it (cannot find service reference inside template) so it makes refactoring not that fun anymore
* 
### Postgresql
* Names in SQL must begin with a letter (a-z) or underscore (_). Subsequent characters in a name can be letters, digits (0-9), or underscores. The system uses no more than NAMEDATALEN-1 characters of a name;   longer names can be written in queries, but they will be truncated. By default, NAMEDATALEN is 32 so the maximum name length is 31 (but at the time the system is built, NAMEDATALEN can be changed in src/include/postgres_ext.h).

* Names containing other characters may be formed by surrounding them with double quotes ("). For example, table or column names may contain otherwise disallowed characters such as spaces, ampersands, etc. if quoted. Quoting a name also makes it case-sensitive, whereas unquoted names are always folded to lower case. For example, the names FOO, foo and "foo" are considered the same by Postgres, but "Foo" is a different name.

* Double quotes can also be used to protect a name that would otherwise be taken to be an SQL keyword. For example, IN is a keyword but "IN" is a name.
