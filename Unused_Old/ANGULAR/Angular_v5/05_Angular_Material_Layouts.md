# ANGULAR MATERIAL DESIGN LAYOUTS

Custom theme material: https://alligator.io/angular/angular-material-custom-theme/
https://www.youtube.com/watch?time_continue=83&v=kHbMm7psBag

## Custom Themes Angular Material

Resources:

[Material Design Color Guidelines](https://material.io/guidelines/style/color.html)

Create custom theme
themes.scss

*Path: src/themes.scss*
```scss
@import '~@angular/material/theming';
@include mat-core();

$custom-primary:mat-palette($mat-grey, 900);
$custom-accent: mat-palette($mat-amber, 600, 900, A700);
$custom-warn:   mat-palette($mat-pink);
$custom-theme:  mat-light-theme($custom-primary, $custom-accent, $custom-warn);
/*$custom-theme: mat-dark-theme($custom-primary, $custom-accent, $custom-warn);*/

@include angular-material-theme($custom-theme);

.alternate-theme {
    $alternate-primary: mat-palette($mat-amber, 600);
    $alternate-accent:  mat-palette($mat-grey, 900);
    $alternate-theme:   mat-light-theme($alternate-primary, $alternate-accent);
    @include angular-material-theme($alternate-theme);
}
```
Usage alternative theme
```html
<div class="alternate-theme">
    <p color="primary">
        :::
    </p>
</div>
```

*Path: .angular-cli.json*
```json
"styles": [
    "styles.css",
    "themes.scss"
],
```
## Flex Layout for Angular

Install Flex-Layout

```sh
npm install @angular/flex-layout --save
```
Import the Angular Flex-Layout NgModule

*Path: src/app/app.module.ts*
```typescript
import { FlexLayoutModule } from '@angular/flex-layout';
// other imports 
@NgModule({
  imports: [FlexLayoutModule],
  
})
```
## [Sidenav] Open sidenav from another component

Step 01: In your Sub component, put the custom event as below,

```html
<button mat-raised-button color="accent" (click)="navOpen()">
```

Step 02:Change your typescript file as fallows,

```typescript
import {Component} from '@angular/core';
import {EventEmitter} from '@angular/core';

@component({
    selector:'sub-component',
    styleUrls: ['./sub.component.css'],
    templateUrl: './sub.component.html',
    outputs:['navToggle']
})

export class SubComponent{
    navToggle=new EventEmitter();

    navOpen(){
        this.navToggle.emit(true);
    }
}
```

Step 03: In your main component you can put ,

```html
<sub-component (navToggle)="sidenav.open()">
```

(NOTE:Don't forget to add "#sidenav" to your mat-sidenav .)
Then it should work.
