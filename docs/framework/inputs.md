---
title: Inputs
layout: docs-layout
---

## Input Elements

----


##### Form

```html
<ui-form submit.trigger="fn()" busy.bind="boolean" auto-grid>
  <!-- .... -->
</ui-form>
```

* `auto-grid`: create a form with a default two-column layout
* `busy`: bindable property to disable all input elements and display loader overlay when busy to prevent changes
* `submit`: event triggered when enter key pressed on any input, except textarea

----

##### Button

* __Basic Button__

  ```html
  <ui-button label.bind="string"
    click.trigger="fn()"
    icon.bind="string"
    theme.bind="theme"
    theme-property
    size-property
    style-property></ui-button>
  ```
  * `theme.bind` or `theme-property`: `default` `primary` `secondary` `info` `danger` `success` `warning`
  * `size-property`: `normal` `small` `large`
  * `style-property`: `round` `square` `icon-top`

<br/>

* __Dropdown Button__

  ```html
  <ui-button dropdown value.bind="string">
    <section>Title</section>
    <menu id="" icon="string">label</menu>
    <divider></divider>
    <menu id="" icon="string">label</menu>
  </ui-button>
  ```
  * Creates a non-editable dropdown styled button, the button label will be updated to selected menu text

<br/>

* __Button with Menu__

  ```html
  <ui-button menu>
    <section>Title</section>
    <menu id="" icon="string">label</menu>
    <divider></divider>
    <menu id="" icon="string">label</menu>
  </ui-button>
  ```
  * Creates a button with a menu, unlike the dropdown the button label does not change, useful for creating extra options like button

----

##### Switch

```html
<ui-switch
  checked.bind="boolean"

  label-on="On"
  label-off="Off"

  width="number"

  change.trigger="fn()"
  theme-property>Label</ui-switch>
```

  * `width` em size

----

##### Basic Input

* Single Input

  ```html
  <ui-input
    value.bind="any"
    name.bind="string"

    change.trigger="fn()"

    disabled.bind="boolean"
    readonly.bind="boolean"

    dir.bind="ltr|rtl"

    placeholder.bind="string"
    help-text.bind="string"

    prefix-icon="string"
    prefix-text="string"

    suffix-icon="string"
    suffix-text="string"

    button-icon="string"
    button-text="string"
    buttonclick.trigger="fn()"

    input-type
    required
    clear
    checkbox
    auto-width
    label-top
    label-hide>Label</ui-input>
  ```

    * `input-type`: `text` `password` `number` `decimal` `file` `email` `url` `search` `capitalize`
    * `checkbox`: add a checkbox add-on to enable/disable input
    * `help-text`: small text to be displayed below the input element
    * `prefix`/`suffix`: addon icon/text to be displayed to the left/right of the input element
    * `button`: addon button to displayed
    * `required`: add a `*` indicator to the end of the label
    * `clear`: add an `x` overlay to clear inputted text

    <br/>

* Double Input
_inherits attributes from `ui-input`_

  ```html
  <ui-input-dual
    value-second.bind="string"
    name-second.bind="string"

    placeholder-second.bind="string"

    center-icon="string"
    center-text.bind="string">Label</ui-input-dual>
  ```

    * `center`: addon icon/text to be displayed in between the two input elements
    * __NOTE__ input-type must be same for both input elements

----

##### Textarea
_inherits attributes from `ui-input`_

```html
<ui-textarea rows="5">Label</ui-textarea>
```

* all input attributes applicable, except input-type

---

##### ComboBox
_inherits attributes from `ui-input`_

```html
<ui-combo
  options.bind="Array"
  value-property="string"
  display-property="string"
  icon-property="string"
  icon-class="string"
  empty-text="string"
  select.trigger="fn()">Label</ui-combo>
```

* `options`: list of options for the combo box
* `value-property`: object property to used as option value
* `display-property`: object property to used as display text
* `icon-property`: object property to used as icon class, e.g displaying country flag 'iso3'
* `icon-class`: class to appended to option icon, e.g displaying country flag 'ui-flag'

----

##### Tag Input
_inherits attributes from `ui-input`_

```html
<ui-tags
  options.bind="Array"
  value.bind="Array of IDs or comma-separated-string"
  value-property="string"
  display-property="string"
  icon-property="string"
  icon-class="string"
  empty-text="string"
  select.trigger="fn()">Label</ui-tags>
```

----

##### List

```html
<ui-list
  options.bind="Array"
  value.bind="Array of IDs or comma-separated-string"
  value-property="string"
  display-property="string"
  icon-property="string"
  icon-class="string"
  empty-text="string"
  copy searchable>Label</ui-list>
```

A multiple selection list

* `copy`: allow multiple selection of single item
* `searchable`: enable search

----

##### Date

* __Date Input__
_inherits attributes from `ui-input`_

  ```html
  <ui-date
    date.bind="string | Date | Moment"
    date-end.bind="string | Date | Moment"
    format.bind="DD MMM YYYY"
    options.bind="DateOptions"
    range>Label</ui-date>
  ```

  * `range`: enable date range input
  * `date-end`: applies to end date value only if range input
  * `options`:

    ```ts
    DateOptions = {
      // to disable min/max dates set null
      minDate: string | Date | Moment;
      maxDate: string | Date | Moment;

      // enable time input
      showTime = false;

      // Array or callback method to check valid dates
      validDates: Array<any> | Function;

      // Array or callback method to check invalid dates
      invalidDates: Array<any> | Function;
    }
    ```

* __Inline Date View__

  ```html
  <ui-date-view
    date.bind="string | Date | Moment"
    format.bind="DD MMM YYYY"
    options.bind="DateOptions">Label</ui-date>
  ```

----

##### File
A multiple file drag-drop input

```html
<ui-file>Label></ui-file>
```

* Creates a drop-zone for dragging files onto, allows adding of multiple files
* Use with [UIHttpService.upload](/docs/framework/utilities.html#http-service)

----

##### Phone
_inherits attributes from `ui-input`_

```html
<ui-phone
  value.bind="full phone number"
  country.bind="phone country"
  isd-code.bind="international dialing code"
  area-code.bind="phone area code"
  phone.bind="phone number"
  extension.bind="phone extension"
  international>Label</ui-date>
```

* `value`: full phone number with international prefix
* `country`: country ISO-2 code for using when input is for national numbers only
* `international`: ignore ISO-2 country code and accept input starting with international dialing code
* `isd-code` `area-code` `phone` `extension`: phone number parts
