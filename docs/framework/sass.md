---
title: SASS Variables
layout: docs-layout
---

## SASS Variables

----

##### Theme Colors

```scss
$primary                    : $lapis-lazuli !default;
$primary-text               : $white !default;

$secondary                  : $crockery-blue !default;
$secondary-text             : $black !default;

$info                       : $blue-green !default;
$danger                     : $cadmium-red !default;
$success                    : $mistletoe !default;
$warning                    : $cadmium-orange !default;

$bg-primary                 : $greenish-blue !default;
$bg-info                    : $new-blue !default;
$bg-danger                  : $peach !default;
$bg-success                 : $lime-green !default;
$bg-warning                 : $reddish-yellow !default;
```

##### Base Variables

```scss
// fonts
$base-font-size             : .95em !default;
$base-line-height           : 1.1 !default;
$base-font-family-input     : 'Lato', 'Trebuchet MS', Tahoma, san-serif !default;
$base-font-family-serif     : 'Source Code Pro', 'Georgia', 'Times New Roman', serif !default;
$base-font-family-sans-serif: 'Open Sans', 'Segoe UI', 'Roboto', 'Helvetica Neue', Arial, sans-serif !default;
$base-font-family           : $base-font-family-sans-serif !default;

// colors
$base-bg                    : $white-sp !default;
$base-text                  : $black !default;
$base-bg-image              : 'back/bg-light.png' !default;
$base-splash-image          : 'loader-spinner.gif' !default;

// borders
$base-border-color          : $wg-5 !default;
$base-border-radius         : .2em !default;
$base-shadow-color          : $wg-8 !default;

// padding
$base-padding               : .3em .8em !default;
```

##### Typography

```scss
// font weights
$font-weight-normal         : 400 !default;
$font-weight-strong         : 600 !default;
$font-weight-bold           : 800 !default;

// text colors
$text-link                  : $primary !default;
$text-muted                 : $wg-5 !default;
$text-primary               : $primary !default;
$text-info                  : $info !default;
$text-danger                : $danger !default;
$text-success               : $success !default;
$text-warning               : $warning !default;

$inline-code-bg             : $tg-0 !default;
$inline-code-text           : $lipstick-red !default;

$pre-code-bg                : $wg-2 !default;
$pre-code-text              : $wg-9 !default;
$pre-code-border            : $wg-4 !default;

$hr-highlight               : $white !default;
$hr-shadow                  : $ng-3 !default;
```

##### Grid Layout

```scss
$grid-xs-min                : 320px !default; // 320 - 480
$grid-sm-min                : 480px !default; // 480 - 768
$grid-md-min                : 768px !default; // 768 - 1024
$grid-lg-min                : 1024px !default; // 1024 - 1536
$grid-xl-min                : 1536px !default; // 1536 - ∞
```

##### App Viewport

```scss
$app-header-bg              : $agate !default;
$app-header-text            : $white !default;
$app-header-subtitle        : $white !default;
$app-header-font-size       : 1.5em !default;

$app-footer-bg              : $ng-9 !default;
$app-footer-text            : $ng-1 !default;
$app-footer-font-size       : .5em !default;

$app-menu-bg                : $black !default;
$app-menu-text              : $white !default;
$app-menu-link              : $primary !default;
$app-menu-font-size         : 1.2em !default;
$app-menu-bg-image          : 'back/bg-menu.png' !default;
$app-menu-shim              : $cg-00 !default;

$app-menu-hover-bg          : rgba($primary, .5) !default;
$app-menu-hover-text        : $primary-text !default;

$app-menu-active-bg         : $primary !default;
$app-menu-active-text       : $primary-text !default;
$app-menu-active-border     : $primary-text !default;
```

##### Page

```scss
$page-title-bg              : $night-blue !default;
$page-title-text            : $white !default;

$sidebar-bg                 : rgba($wg-0, .5) !default;
$sidebar-text               : $base-text !default;

$toolbar-bg                 : $ng-0 !default;
$toolbar-text               : $ng-9 !default;

$statsbar-bg                : $ice-blue !default;
$statsbar-text              : $antwerp-blue !default;
$statsbar-label             : $wg-7 !default;
```

##### Menus

```scss
$menu-link-bg               : transparent !default;
$menu-link-text             : $primary !default;

$menu-hover-bg              : rgba($primary, .5) !default;
$menu-hover-text            : $primary-text !default;

$menu-click-bg              : rgba($primary, .7) !default;
$menu-click-text            : $primary-text !default;

$menu-active-bg             : $ng-1 !default;
$menu-active-border         : $primary !default;
$menu-active-text           : $primary !default;
```

##### Buttons

```scss
$button-default-bg          : $tg-0 !default;
$button-default-text        : $tg-8 !default;
$button-primary-bg          : $primary !default;
$button-primary-text        : $primary-text !default;
$button-info-bg             : $info !default;
$button-info-text           : $white !default;
$button-danger-bg           : $danger !default;
$button-danger-text         : $white !default;
$button-success-bg          : $success !default;
$button-success-text        : $white !default;
$button-warning-bg          : $warning !default;
$button-warning-text        : $white !default;
```

##### Inputs

```scss
$input-bg                   : $white-sp !default;
$input-text                 : $wg-9 !default;
$input-label                : $wg-7 !default;
$input-label-width          : 10em !default;
$input-border               : $wg-4 !default;
$input-placeholder-text     : $wg-3 !default;

$input-invalid-border       : $danger !default;
$input-focus-border         : $ultramarine !default;

$input-readonly-bg          : #fefcfa !default;
$input-disabled-bg          : $ng-0 !default;

$input-addon-bg             : $cg-00 !default;
$input-addon-text           : $cg-7 !default;

$input-button-bg            : $secondary !default;
$input-button-text          : $secondary-text !default;
```

##### Date Input

```scss
$date-weekday-bg            : $secondary !default;
$date-weekday-text          : $secondary-text !default;

$date-control-text          : $primary !default;
$date-control-hover-bg      : $primary !default;
$date-control-hover-text    : $primary-text !default;

$date-active                : $base-text !default;
$date-muted                 : $cg-5 !default;
$date-week                  : $night-blue !default;
$date-disabled              : $cg-3 !default;
$date-selected-bg           : $primary !default;
$date-selected-text         : $primary-text !default;

$date-icon                  : $font-ui-calendar !default;
$date-prev                  : $font-ui-page-prev-line !default;
$date-next                  : $font-ui-page-next-line !default;
```

##### Tabs

```scss
$tab-bg                     : $wg-00 !default;
$tab-text                   : $wg-9 !default;
$tab-border                 : $wg-3 !default;

$tab-active-bg              : $white !default;
$tab-active-text            : $ng-9 !default;
$tab-active-border          : $primary !default;
```

##### Toasts

```scss
$toast-default              : $wg-9 !default;
$toast-info                 : $process-blue !default;
$toast-danger               : $carmine !default;
$toast-success              : $mistletoe !default;
$toast-warning              : $atoll !default;
$toast-text                 : $white !default;
```

##### Datagrid

```scss
$datagrid-header-bg         : $cg-0 !default;
$datagrid-header-hover-bg   : $cg-2 !default;
$datagrid-footer-bg         : $ng-0 !default;
$datagrid-odd-bg            : $white !default;
$datagrid-even-row          : $tg-1 !default;
$datagrid-text              : $tg-9 !default;

$datagrid-button-view       : $font-ui-preview-thick !default;
$datagrid-button-edit       : $font-ui-edit-thick !default;
$datagrid-button-delete     : $font-ui-delete-black !default;

$datagrid-hover-bg          : $aqua-blue !default;
$datagrid-active-bg         : $smoky-blue !default;
$datagrid-indicator-color   : $wg-7 !default;

$pager-first-glyph          : $font-ui-page-first-black !default;
$pager-prev-glyph           : $font-ui-page-prev-black !default;
$pager-next-glyph           : $font-ui-page-next-black !default;
$pager-last-glyph           : $font-ui-page-last-black !default;
```

##### Component Z-Index

```scss
$z-index-splash             : 50000 !default;
$z-index-notify             : 10000 !default;
$z-index-floating           : 500 !default;
$z-index-ribbon             : 200 !default;
```
