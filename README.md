# DateValueAccessor for Angular
[![NPM version][npm-image]][npm-url]
[![Tests][tests-image]][tests-url]

A custom value accessor for Angular.  
Now you can use `<input type="date">` (provides real JavaScript date objects) directly with two-way data bindings (ngModel) as well as with reactive forms (formControlName/formControl).

## Demo

Here you can see the `DateValueAccessor` - the binding works!
Changes to the input field are propagated to the model.

![Example: works](https://johanneshoppe.github.io/angular-date-value-accessor/assets/reactive-works.gif)

And here you can see the `LocalDateValueAccessor`.
Please notice how the date is adjusted due to the German time zone (UTC+1) and how the time offset works.

![Example: works](https://johanneshoppe.github.io/angular-date-value-accessor/assets/reactive-works-local.gif)

And this shows a not working form field (the default behaviour).
Changes in the input field are propagated to the model, but unfortunately the date becomes a string which is not very useful for any further processing.

![Example: does not work](https://johanneshoppe.github.io/angular-date-value-accessor/assets/reactive-does-not-work.gif)

**You can try out the demo at the following page:**  
http://johanneshoppe.github.io/angular-date-value-accessor/

## Usage

You have to explicitly opt-in by adding the attribute `useValueAsDate` or `useValueAsLocalDate` to a date input control:

```html
<!-- DateValueAccessor (UTC) --->

<input type="date"
       name="myBirthday"
       ngModel
       useValueAsDate>

OR

<input type="date"
       name="myBirthday"
       [(ngModel)]="myBirthday"
       useValueAsDate>

OR

<input type="date"
       formControlName="myBirthday"
       useValueAsDate>

<!-- LocalDateValueAccessor (Local Time) --->

<input type="date"
       name="myBirthday"
       ngModel
       useValueAsLocalDate>

OR

<input type="date"
       name="myBirthday"
       [(ngModel)]="myBirthday"
       useValueAsLocalDate>

OR

<input type="date"
       formControlName="myBirthday"
       useValueAsLocalDate>

```

## Installation

Download the package via NPM:

```bash
npm install angular-date-value-accessor
```

## UTC Time and Local Time
When working with Dates in Javascript you either operate in UTC or Local Time.

* UTC is has no timezone offset.
* Local Time depends on the host system time zone and offset.

Javascript Dates support both the UTC and the Local Time representation.
Depending on the requirements of your application you can choose from these Value Accessors:
* [DateValueAccessor (UTC)](#datevalueaccessor-utc)
* [LocalDateValueAccessor (Local Time)](#localdatevalueaccessor-local-time)


## DateValueAccessor (UTC)

The `DateValueAccessor` operates in UTC (Coordinated Universal Time).
The HTML date input will read the UTC representation of the Date Object. When you select a date it will output an UTC date with the time set to 00:00 (UTC).

Import the module via NgModule:

```js
// app.module.ts

import { DateValueAccessorModule } from 'angular-date-value-accessor';

@NgModule({
  imports: [
    DateValueAccessorModule
  ]
})
export class AppModule { }
```

Now you can apply the `useValueAsDate` to your date input controls.

## LocalDateValueAccessor (Local Time)

If you prefer to work with Local Dates then you can use the `LocalDateValueAccessorModule`.

The HTML date input will read the Local Time representation of the Date Object. When you select a date it will output a Local Date with the time set to 00:00 (Local Time).

Import the module via NgModule:

```js
// app.module.ts

import { LocalDateValueAccessorModule } from 'angular-date-value-accessor';

@NgModule({
  imports: [
    LocalDateValueAccessorModule
  ]
})
export class AppModule { }
```

Now you can apply the `useValueAsLocalDate` to your date input controls.

> **ℹ️ Hint:** Most UI component libraries like Angular Material, Kendo Angular, PrimeNG implement their DatePickers operating in Local Time. The Angular Date Pipe uses the Local Time representation of the Date Object by default, too.


## IE11 Support

This package works great on modern browsers.
But Internet Explorer 11 does not support `<input type="date">` out of the box.
If you want to support this browser, you need an additional polyfill:
https://www.npmjs.com/package/date-input-polyfill

![IE11 Demo](https://johanneshoppe.github.io/angular-date-value-accessor/assets/ie11.png)
> Demo in IE11 using the `date-input-polyfill`. `LocalDateValueAccessor` works as expected. Please note that all input fields operate in local time. This means that `DateValueAccessor` does not behave as specified.


[npm-url]: https://npmjs.org/package/angular-date-value-accessor
[npm-image]: https://badge.fury.io/js/angular-date-value-accessor.svg
[tests-url]: https://github.com/JohannesHoppe/angular-date-value-accessor/actions?query=workflow%3ATests
[tests-image]: https://github.com/JohannesHoppe/angular-date-value-accessor/workflows/Tests/badge.svg
