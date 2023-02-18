# ANGULAR 4 MATERIAL DESIGN

## Create Project

```sh
ng new angular_material --prefix ng
```

## Resources and guides

https://www.youtube.com/watch?v=sgu0YQTKNLs

* [Material Angular](https://material.angular.io/)
* [Angular](https://angular.io/)
* [Angular/Flex-Layout](https://github.com/angular/flex-layout/wiki/API-Documentation)
* [Material Icons](https://www.materialpalette.com/icons)

Install 

```sh
cd angular_material
npm install --save @angular/material @angular/cdk
npm install --save @angular/animations
ng -v
```

## Import Modules to Project Angular

app/app.modules.ts

```js
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { FormsModule } from '@angular/forms'; 	// <---
import { HttpModule } from '@angular/http';   	// <---

import { AppComponent } from './app.component';

import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { MatButtonModule, 					// <---
  		 MatCardModule,
  		 MatToolbarModule, 
  		 MatMenuModule,
  		 MatIconModule 	} from '@angular/material';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,					// <---
    HttpModule,
    BrowserAnimationsModule,
    MatButtonModule,
    MatCardModule,
    MatToolbarModule,
    MatMenuModule,
    MatIconModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

```

app/styles.css

```js
@import '~@angular/material/prebuilt-themes/indigo-pink.css';

body {
    margin: 0;
    padding: 0;
}
```

## Include References in component app

Create Component header-page

```sh
mkdir components
cd components
mkdir page
cd page
ng g c header-page
```

components/page/header-page.component.ts

```js
import { Component, OnInit, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'ng-header-page',
  templateUrl: './header-page.component.html',
  styleUrls: ['./header-page.component.css'],
  encapsulation: ViewEncapsulation.None
})
export class HeaderPageComponent implements OnInit {
  constructor() {}
  ngOnInit() {
  }
}
```

components/page/header-page.component.html

```html
<mat-toolbar color="primary">
  <span>Mi primera aplicacion con Material</span>
</mat-toolbar>
```

app.component.html

```html
<ng-header-page></ng-header-page>
<div style="text-align:center">
  	<h1>
    	Bienvenidos a {{title}}
  	</h1>
</div>
```

## Include Materials Icons

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Lapaz Digital Frontend</title>
  <base href="/">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">

  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">   <!--  ADD -->

</head>
<body>
  <ng-root></ng-root>
</body>
</html>
```
