---
title: Components
layout: docs-layout
---

## Components

----

##### Menu

* Router Menu

  ```html
  <ui-menu router.bind="aurelia-router">
  </ui-menu>
  ```
  * used to create sidebar menu using child-routers
<br/><br/>


* Custom Menu

  ```html
  <ui-menu menuclick.trigger="fn($event)">
    <section>Header</section>
    <menu id="string" disabled="bool" icon="string">Label</menu>
    <divider></divider>
    <menu href="string" disabled="bool" icon="string">Label</menu>
  </ui-menu>
  ```

  * `section`: creates a section header
  * `divider`: insert a single line divider
  * `menu`: menu item
    * `href`: optional. navigation route
    * `id`: link id to identify the menu clicked
    * `icon`: icon glyph classname

  * `menuclick`: `$event.detail` contains the menu item `{id, text}`

----

##### Panel

```html
<ui-panel expanded.bind="bool" collapsed.bind="bool">

  <!-- optional -->
  <ui-header primary|secondary
    icon.bind="string"
    close.bind="bool"
    expand.bind="bool"
    collapse.bind="bool">Title</ui-header>

  <ui-body scroll padded flex></ui-body>

  <!-- optional -->
  <ui-toolbar></ui-toolbar>
</ui-panel>
```

  * `ui-header`: create a panel header with control buttons
    * `primary`: use primary color background
    * `secondary`: use secondary color background
    * `icon`: icon glyph classname
    * `close`: show close button, this will create a closable panel
    * `expand`: show expand button, this will create an expandable panel
    * `collapse`: show collapse button, this will create a collapsible panel

  * `ui-body`: main panel body
    * `scroll`: enables scrolling, cannot be used with `flex`
    * `padded`: apply default padding
    * `flex`: create a flexbox column layout

----

##### Dialog

  * Dialog View

    ```html
    <template>
      <ui-content>
        <!-- Dialog body -->
      </ui-content>
      <ui-toolbar>
        <!-- Dialog Footer -->
        <ui-button label="Close" click.trigger="close()"></ui-button>
      </ui-toolbar>
    </template>
    ```

  * Dialog View-Model

    ```ts
    import {autoinject} from "aurelia-framework";
    import {UIDialog} from "sigma-ui-framework";

    @autoinject()
    export class MyDialog extends UIDialog {

      icon:string;
      title:string;

      width:string = '600px';
      height:string = '400px';

      modal: boolean = false;
      drag: boolean = true;
      resize: boolean = true;
      maximize: boolean = true;

      constructor() {
        super();
      }

      canActivate(model) {
        // return promise or boolean
        return true;
      }

      attached() {
        this.focus();
      }
    }
    ```

  * __Properties__
    * `icon`: icon glyph classname
    * `title`: dialog title
    * `width`: dialog width, (em | rem | px)
    * `height`: dialog height, (em | rem | px)
    * `modal`: open dialog as modal when true, default false
    * `drag`: enable dragging
    * `resize`: enable resizing
    * `maximize`: enable maximizing

  * __Methods__
    * `close`: close this dialog
    * `toast`: show a toast message, for options see [Utils](/docs/framework/utilities.html#toast-options)
    * `focus`: Move focus to first input element found

<br/>

  * Open dialog from page view

    ```ts
    import {autoinject} from "aurelia-framework";
    import {UIDialogService} from "sigma-ui-framework";
    import {MyDialog} from "./my-dialog";

    @autoinject()
    export class PageView {

      constructor(public dialogService:UIDialogService) {
      }

      openDialog() {
        this.dialogService.show(MyDialog, model);
      }
    }
    ```

----

##### Tab Panel

```html
<ui-tab-panel>
  <ui-tab label.bind="string" icon.bind="glyph" scroll|flex padded>
    <!-- content examples -->
    <!-- Compose a view or view-model
    <compose view-model="./my-view"></compose>
    -->
    <!-- Add a row layout section (requires flex layout)
    <ui-section row>
      <ui-sidebar></ui-sidebar>
      <ui-content></ui-content>
    </ui-section>
    -->
    <!-- Add a datagrid (requires flex layout)
    <ui-datagrid>....</ui-datagrid>
    -->
  </ui-tab>
</ui-tab-panel>
```

* `scroll`: enables scrolling, cannot be used with `flex`
* `padded`: apply default padding
* `flex`: create a flexbox column layout

* __TODO__ ability to add/close a tab dynamically via script

----

##### Login Panel

```html
<ui-login
  error.bind="string"
  busy.bind="bool"
  login.trigger="fn($event)"
  row-layout>
  <!-- Login message to be displayed -->
</ui-login>
```

* __Attributes__
  `error`: Error message to be displayed

  `busy`: Indicator to enable/disable input elements

  `row-layout`: Display login message and form side-by-side, default display is column

* ###### Events
  `login`: Login event, `$event.detail = LoginModel`

* ###### i18n Translation
  ```json
  {
    "login":{
      "username": "Username",
      "password": "Password",
      "remember": "Remember Me",
      "button"  : "Login",
      "version" : "Version {% raw %}{{Version}}{% endraw %}",
      "design_message": "This app is designed to run on desktop and tablets"
    }
  }
  ```

* ###### LoginModel
  - _Properties_
    * `username`
    * `password`
    * `remember`

  - _Methods_
    * `save`: Persist username/password in local storage, password is only saved when `remember` is true

----

##### Datagrid

```html
<ui-datagrid
  data-list.bind="array"
  empty-text.bind="string"
  summary-row.bind="bool | model"
  default-sort="<column_id>"
  default-order="asc | desc"
  rowselect.trigger="fn($event)"
  linkclick.trigger="fn($event)"
  selectable auto-height>
    <ui-data-column
      data-id="string"
      data-sort="string"

      use-virtual="boolean"

      format="string"
      symbol="string"
      summary="string"
      labels="array"

      class="string"
      width="string"
      min-width="string"

      button-title="string"
      button-icon="string"
      button-theme="string"
      button-menu="array"

      value.call="fn($model)"
      display.call="fn($model)"
      button.call="fn($model)"

      locked sortable resizeable
      (align) [start | center | end]
      (button-type) [view | edit | delete]
      (data-type) [text | date | datetime| from-now | number | currency | link | button]>
        Label</ui-data-column>
    ...
</ui-datagrid>
```

  * __DataGrid Attributes__
    * `data-list`: Array of data models
    * `use-virtual`: Use `aurelia-ui-virtualization` for rendering large data-set
    * `empty-text`: text to be displayed when data-list is empty
    * `default-sort`: default sort column id
    * `default-order`: default sort order
    * `summary-row`: if passed true summary will be calculated, if passed a data model values from model will be used instead
    * `selectable`: allow row selection
    * `auto-height`: default style if flex stretched, use auto-height to remove flex stretch
    * `rowselect`: event trigger, access row model `$event.detail`
    * `linkclick`: event trigger when button/link/menu clicked, `$event.detail = {dataId:column_id, model: row_model}`

  *	__Column Attributes__
    * `data-id`: model property or a unique identifier
    * `data-sort`: model property to be used as secondary sort field
    * `format`: date formatting uses `momentjs`, number formatting using `numeraljs`
    * `symbol`: symbol prefix to used in number format if required
    * `summary`: enables summary on this column, types available `sum`, `avg`
    * `labels`: array or object of strings to be used to display labels
    * `value.call($model)`: a callable function that will return custom value which will be formatted as per column settings. `$model={ value: value, column: column, model: model }`
    * `display.call($model)`: a callable function that will return custom display, this will skip the column formatting. `$model={ value: value, column: column, model: model }`
    * `button.call($model)`: a callable function to display custom buttons, return string to display in place of button, else return `{icon: string, title: string, theme: string, disabled: bool}`


##### Pager

```html
<ui-pager
  current.bind="number"
  total.bind="number"
  pagechanged.trigger="fn($event)"></ui-pager>
```

* `pagechanged`: passes current page in `$event.detail`, use this instead of observing the current bound value

----

##### Tree Panel

```html
<ui-tree
  value.bind="string"
  model.bind="treeModel"
  options.bind="treeOptions"
  change.trigger="fn($event)"
  checked.trigger="fn($event)"></ui-tree>
```
* `change.tigger`: event fired when tree item is selected, `$event.detail` will contain selected node
* `checked.tigger`: event fired when checkboxes enabled, `$event.detail` will contain all checked items

```ts
UITreeOptions = {
  // show maximum of ? levels
  maxLevels: number;

  // show checkboxes
  showCheckbox: boolean;
  // show checkbox only at ? level, -1/null all levels
  checkboxLevel: number;

  showRoot: boolean;
  rootLabel: string;
}
```

```ts
UITreeModel = {
  id: any;
  name: string;
  leaf: boolean;
  children:Array<UITreeModel>;

  iconGlyph: string;

  checked: boolean;
  expanded: boolean;
  isVisible: boolean;
}
```

----

##### Chart Panel

> Chart panels use [amCharts](https://amcharts.com)

* Generic chart panel

  ```html
  <ui-chart chart-title=""
    chart-options="<AmChart Options>"
    height="<number>">
    <!-- panel header buttons -->
  </ui-chart>
  ```
  * generic chart element accepts complete amCharts chart option.
  * See amChart [demos](https://www.amcharts.com/demos/) or [documentation](https://docs.amcharts.com/3/javascriptcharts/AmChart)

<br/>

* Bar/Column chart panel

  ```html
  <ui-bar chart-title="string"
    chart-options="UIBarChartOptions"
    height="number"
    chart-data="array"
    legend="bottom | right"
    bar|column export>
    <!-- panel header buttons -->
  </ui-bar>
  ```
  * `bar`: bar chart
  * `column`: column chart
  * `export`: enable amChart export

  ```ts
  UIBarChartOptions = {
    chartTitle: string;
    valueAxisTitle: string;
    valueAxisUnit: string;
    categoryAxisTitle: string;
    categoryField: string;
    theme: string;
    series: Array<AmCharts.AmGraph>;
  }
  ```

<br/>

* Pie chart panel

  ```html
  <ui-pie chart-title="string"
    height="number"
    chart-data="array"
    value-property="string"
    title-property="string"
    color-property="string"
    theme="pie">
    <!-- panel header buttons -->
  </ui-pie>
  ```
  * `value-property`: model property for slice value
  * `title-property`: model property for slice legend label
  * `color-property`: model property for slice color, this will override the theme color
  * `theme`: available themes

  <div>
        <p>
          <span class="chart-theme-name">default:</span>
          <span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="756" style="background-color: rgb(213, 53, 48); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="756" style="background-color: rgb(239, 107, 40); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="756" style="background-color: rgb(157, 110, 75); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="756" style="background-color: rgb(237, 236, 71); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="756" style="background-color: rgb(93, 175, 67); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="756" style="background-color: rgb(56, 208, 70); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="756" style="background-color: rgb(39, 159, 121); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="756" style="background-color: rgb(90, 197, 196); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="756" style="background-color: rgb(51, 142, 189); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="756" style="background-color: rgb(55, 95, 167); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="756" style="background-color: rgb(124, 83, 162); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="756" style="background-color: rgb(166, 33, 106); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="756" style="background-color: rgb(223, 128, 151); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><!--anchor-->
        </p>
        <p>
          <span class="chart-theme-name">pie:</span>
          <span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="758" style="background-color: rgb(181, 47, 48); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="758" style="background-color: rgb(246, 143, 49); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="758" style="background-color: rgb(143, 198, 73); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="758" style="background-color: rgb(160, 196, 200); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="758" style="background-color: rgb(165, 71, 151); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="758" style="background-color: rgb(151, 126, 109); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="758" style="background-color: rgb(149, 77, 67); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="758" style="background-color: rgb(251, 204, 46); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="758" style="background-color: rgb(92, 129, 88); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="758" style="background-color: rgb(93, 134, 163); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="758" style="background-color: rgb(177, 13, 95); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="758" style="background-color: rgb(14, 107, 168); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="758" style="background-color: rgb(11, 104, 72); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><!--anchor-->
        </p>
        <p>
          <span class="chart-theme-name">red:</span>
          <span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="760" style="background-color: rgb(124, 39, 34); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="760" style="background-color: rgb(167, 58, 33); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="760" style="background-color: rgb(218, 57, 38); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="760" style="background-color: rgb(222, 72, 52); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="760" style="background-color: rgb(228, 106, 106); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="760" style="background-color: rgb(235, 137, 140); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="760" style="background-color: rgb(237, 150, 155); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><!--anchor-->
        </p>
        <p>
          <span class="chart-theme-name">blue:</span>
          <span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="762" style="background-color: rgb(18, 123, 179); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="762" style="background-color: rgb(32, 148, 198); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="762" style="background-color: rgb(104, 183, 220); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="762" style="background-color: rgb(126, 193, 220); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="762" style="background-color: rgb(176, 217, 228); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="762" style="background-color: rgb(184, 222, 229); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="762" style="background-color: rgb(220, 235, 230); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><!--anchor-->
        </p>
        <p>
          <span class="chart-theme-name">pink:</span>
          <span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="764" style="background-color: rgb(128, 54, 75); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="764" style="background-color: rgb(170, 45, 82); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="764" style="background-color: rgb(200, 35, 93); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="764" style="background-color: rgb(222, 34, 101); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="764" style="background-color: rgb(230, 99, 149); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="764" style="background-color: rgb(235, 127, 165); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="764" style="background-color: rgb(239, 150, 178); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><!--anchor-->
        </p>
        <p>
          <span class="chart-theme-name">green:</span>
          <span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="766" style="background-color: rgb(10, 77, 68); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="766" style="background-color: rgb(17, 129, 115); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="766" style="background-color: rgb(23, 153, 135); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="766" style="background-color: rgb(28, 180, 161); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="766" style="background-color: rgb(59, 188, 173); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="766" style="background-color: rgb(103, 196, 184); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="766" style="background-color: rgb(150, 213, 204); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><!--anchor-->
        </p>
        <p>
          <span class="chart-theme-name">orange:</span>
          <span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="768" style="background-color: rgb(111, 54, 16); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="768" style="background-color: rgb(148, 66, 22); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="768" style="background-color: rgb(189, 82, 27); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="768" style="background-color: rgb(245, 107, 35); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="768" style="background-color: rgb(252, 149, 79); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="768" style="background-color: rgb(253, 178, 126); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="768" style="background-color: rgb(251, 206, 168); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><!--anchor-->
        </p>
        <p>
          <span class="chart-theme-name">violet:</span>
          <span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="770" style="background-color: rgb(78, 35, 84); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="770" style="background-color: rgb(96, 42, 130); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="770" style="background-color: rgb(115, 47, 151); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="770" style="background-color: rgb(134, 80, 159); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="770" style="background-color: rgb(155, 101, 167); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="770" style="background-color: rgb(186, 135, 189); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="770" style="background-color: rgb(203, 162, 202); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><!--anchor-->
        </p>
        <p>
          <span class="chart-theme-name">spectrum:</span>
          <span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="772" style="background-color: rgb(133, 5, 9); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="772" style="background-color: rgb(203, 37, 21); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="772" style="background-color: rgb(226, 73, 26); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="772" style="background-color: rgb(254, 119, 34); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="772" style="background-color: rgb(254, 156, 39); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="772" style="background-color: rgb(255, 205, 66); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><span class="chart-theme-dot au-target" css.bind="{background: col}" au-target-id="772" style="background-color: rgb(255, 238, 84); background-position: initial initial; background-repeat: initial initial;">&nbsp;</span><!--anchor-->
        </p>
        <p>&nbsp;</p>
      </div>
