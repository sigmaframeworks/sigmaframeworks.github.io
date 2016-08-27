---
title: Core Elements
layout: docs-layout
---

## Core Elements

----

##### Viewport

```html
<ui-viewport
  router.bind="aurelia-router"

  subtitle.bind="string"  
  copyright.bind="string"

  icon.bind="<path to image>"
  icon-class.bind="string"

  show-menu.bind="bool"
  show-options.bind="bool"
  show-taskbar.bind="bool"

  logout.trigger="fn()"

  menu-start/menu-end>

  <!-- any button/input element to be displayed in options box -->

  <!-- if using multi dialog taskbar add quick links -->
  <div slot="quick-links"></div>

</ui-viewport>
```

* __Attributes__

  `router`: Main app router for building navigation menu

  `subtitle`: Application header subtitle

  `copyright`: Copyright message displayed on the footer

  `icon`: Image path for logo

  `icon-class`: Logo image classname

  `show-menu`: Display side menu

  `show-options`: Display options box in header

  `show-taskbar`: Display taskbar for multi dialog display

  `menu-start`: Display menu and menu toggle left for ltr, right for rtl.

  `menu-end`: Display menu and menu toggle right for ltr, left for rtl.

  __NOTE__ Default is menu location `menu-start`, provide either `icon` or `icon-class`


* __Events__

  `logout`: Logout event fired from options box button/menu link for logout.

* __Router Options__

  Router config options

  ```ts
  configureRouter(config, router: Router) {
    // Show logo in side menu
    config.options.showLogo = true;
    // Show logout link in side menu
    config.options.showAuthentication = true;
    // Add when using authorization
    config.addPipelineStep('authorize', AuthInterceptor);
  }
  ```

  Route extras, add settings to individual routes that have `nav:true`

  ```ts
  settings: {
    // Disable route menu link
    disabled: 'bool',

    // Title to used for menu, this allows the route to show a different title in menu and the standard title is used for document title
    menuTitle: 'string',

    // Create a section
    sectionStart: 'bool',
    sectionTitle: 'string',

    // Icon to displayed
    icon: 'classname'
  }
  ```

----

##### Page Components

  * __Page__

    ```html
    <ui-page page-title.bind="string" view-model.ref="page">
      <!-- section / content -->
    </ui-page>
    ```
    Show toast using `view-model.ref`, `page.toast(message)`

    See [Utils](/docs/framework/utilities.html#toast-options) for toast options


  * __Section__

    ```html
    <ui-section row|column>
      <!-- sidebar / toolbar / content -->
    </ui-section>
    ```
    `row`: row layout for having sidebar

    `column`: default layout


  * __Content__

    ```html
    <ui-content auto scroll padded>
    </ui-content>
    ```
    `auto`: auto height

    `scroll`: enable scrolling

    `padded`: add default padding


  * __Sidebar__

    ```html
    <ui-sidebar width.bind="" collapsible scroll>
        <!-- ui-menu with a bound child router -->
        <!-- or any content -->
    </ui-sidebar>
    ```
    `width`: default `220px`

    `scroll`: enable scrolling, must enable when using `ui-menu` for child-routers

    `collapsible`: allow collapse, when collapsed clicking the panel overlays the sidebar


  * __Toolbar__

    ```html
    <ui-toolbar submit.trigger="">
      <!--
      ui-button or any ui-input element,
      ui-input elements must have auto width -->
    </ui-toolbar>
    ```
    `submit`: event fired on enter-press when containing input elements


  * __StatsBar__

    A simple display for statistical counts

    ```html
    <ui-statsbar>
      <ui-stat icon.bind="string" value.bind="string">label</ui-stat>
    </ui-statsbar>
    ```
    `icon`: a glyphicon classname

    `value`: stat value, must be a pre-formatted string

    `label`: stat label

----

##### Grid Layout

  * __Row__

    Flexbox display wrapper, default layout direction `row`

    ```html
    <ui-row row|column>
        <!-- ui-column -->
    </ui-row>
    ```

    * Horizontal alignment for row layout
      * `start`
      * `end`
      * `center`
      * `spaced`
    * Vertical alignment for row layout
      * `top`
      * `bottom`
      * `middle`
      * `stretch`

    * To read more about CSS3 FlexBox visit [CSS Tricks](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

  * __Column__

    Flexbox element, default basis `auto`.

    ```html
    <ui-column auto|fill|fit size="" width="css_width">
        <!-- content -->
    </ui-column>
    ```

    * Self Alignment
      * `top`
      * `bottom`
      * `middle`
      * `stretch`
    * Sizing
      * `auto`: auto fit to content size
      * `fill`: fill available space
      * `full`: wrap if necessary and take 100% space
      * `width`: sets the `flex-basis` property

    Applicable sizes `xs`,`sm`,`md`,`lg`,`xl` `1-12`.

    eg. `size='xl-3 lg-4 md-6'`: 25% width on X-Large, 33.33% width on Large, 50% width on Medium views
