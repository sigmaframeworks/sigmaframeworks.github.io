---
title: Utilities
layout: docs-layout
---

## Utility Classes

----

##### Application

`import {UIApplication} from 'sigma-ui-framework'`

`@inject(UIApplication)`

* __Properties__
  * `IsAuthenticated`: Property used to enable/disable authentication driven elements like main side-menu
  * `Username`: Username to be display in side menu
  * `AuthUser`, `AuthToken`: To be used when sending basic authentication header
* __Methods__
  * `login(authUser, authToken?)`: create authenticated session, and navigate to default route.
  * `logout()`: clear authenticated session, and navigate to login. Must have a route named `login`

  * `shared(key, value)`: share objects across views, these wont be available across sessions
  * `session(key, value)`: get/save objects from session storage
  * `persist(key, value)`: get/save objects from local storage
  * `clearSession()`: clear session storage

  * `info(tag, msg, ...rest)`: print info log
  * `warn(tag, msg, ...rest)`: print warning log
  * `debug(tag, msg, ...rest)`: print debug log
  * `error(tag, msg, ...rest)`: print error log

  * `toast(ToastOptions)`: show toast
  * `toastSuccess(message | ToastOptions)`: show success toast
  * `toastError(message | ToastOptions)`: show error toast

  ```ts
  ToastOptions = {
    message:string;
    icon:string;
    theme:string;
    extraClass:string;
    autoHide:boolean;
  }
  ```

  * `alert(message | AlertConfig)`: display simple alert box

  ```ts
  AlertConfig = {
    message:string;
    type:string = "info | error | exclaim";
    button:string = "OK";
  }
  ```
  * `confirm(message | ConfirmConfig):Promise<boolean>`: display simple confirm box

  ```ts
  ConfirmConfig = {
    message:string;
    yesLabel:string = "Yes";
    noLabel:string = "No";
  }
  ```

----

##### Http Service

`import {UIHttpService} from 'sigma-ui-framework'`

`@inject(UIHttpService)`

* __Methods__
  * `setBaseUrl(url)`: override default base url. the default base url can be set in plugin config.
  * `get(api):Promise<JSON>`: get content as JSON
  * `text(api):Promise<string>`: get content as text
  * `put(api, body):Promise<JSON>`
  * `post(api, body):Promise<JSON>`
  * `delete(api):Promise<JSON>`
  * `upload(api, FormElement):Promise<any>`: upload files from form using WebAPI FormData. For more information [read this](https://developer.mozilla.org/en-US/docs/Web/API/FormData/Using_FormData_Objects)

----

##### Event

`import {UIEvent} from 'sigma-ui-framework'`

_Inject not needed, all methods are static_

* __Methods__
  * `broadcast(event:string, data:any)`: broadcast an event using `EventAggregator`
  * `subscribe(object:any, callback:Function):Subscription`: subscribe for broadcasted events `EventAggregator`
  * `observe(object:any, propertyName:string):PropertyObserver`: observe property changes using `BindingEngine.propertyObserver`

----

##### Model

`export class MyModel extends UIModel {}`

* __Override Methods__
  * Override these methods with Rest API calls for each model
  * `get()`
  * `post()`
  * `put()`
  * `delete()`
* __Methods__
  * `dispose()`: dispose the model
  * `isDirty()`: check if model properties have changed
  * `saveChanges()`: update the original values with current values, note this does not call the Rest API
  * `discardChanges()`: discard any changes made to the model properties

----

##### Converters & Formatters

* __Global Value Converters__
  * __Dates (using [momentjs](http://momentjs.com))__
    * `date:<format>`: format date to string, default format 'DD MMM YYYY hh:mm A'
    * `fromNow`: format date to string relative to current time, e.g. '1 day ago'
  * __Numbers (using [numeraljs](http://numeraljs.com))__
    * `number:<format>`: format number to string, default format '0,0[.]00'
    * `currency:<symbol>:<format>`: format number to currency string, default symbol '$', default format '$ 0,0[.]00'
    * `percent`: format number to percentage string
    * All formats are returned as HTML strings, must be used as `innerhtml.bind="345 | currency"`
  * __Object Converters (using [lodash](https://lodash.com))__
    * `keys`: return array of property keys of Object
    * `group:<property>`: return object grouped by property in array of objects
    * `sort:<property>`: return object sorted by property in array of objects
  * __Other Converters__
    * `markdown`: Parse markdown to HTML. (using [kramed](https://www.npmjs.com/package/kramed))
    * `json`: returns JSON object as string
    * `isString`
    * `isArray`
    * `isObject`
    * `isTrue`
    * `isFalse`

* __Formatters, (usage `UIFormat.date(date)`)__
  * `date(date:string | Date | Moment, format:string)`
  * `toISOString(date:string | Date | Moment)`
  * `fromNow(date:string | Date | Moment)`
  * `number(value:Number, format:string)`
  * `currency(value:Number, symbol:string, format:string)`
  * `percent(value:Number)`

----

##### Utilities

* Global Methods attached to window object
  * `isTrue(YES | Y | ON | 1 | true)`
  * `isEmpty(object:any)`
  * `isFunction(object:any)`
  * `getParentByTag(el:HTMLElement, tag:string):HTMLElement`
  * `getParentByClass(el:HTMLElement, class:string, stopAtClass:string)`
* Countries

  ```ts
  window.countries = [{
    // ISO country codes
    iso2: string;
    iso3: string;

    name: string;
    continent: string;

    // ISO currency code
    currency: string;
    // International dialing code
    phone: number;
    // Country tld
    tld: string;
  }]
  ```
* Currencies

  ```ts
  window.currencies = {
    ISO_code: name
  };
  ```

----

###### Toast options

```ts
ToastOptions = {
  message: '',
  icon: '',
  theme: 'default',
  autoHide: true,
  extraClass: ''
}
```
