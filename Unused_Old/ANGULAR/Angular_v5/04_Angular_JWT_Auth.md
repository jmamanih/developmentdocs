# Angular 4 Authentication with JWT

Tutorial: https://www.youtube.com/playlist?list=PLZAiN3wmUtzUHBDUI6F5Ks3t-U-wVRIV2

Required infrastructure

* Git
* Laravel
* Faker
* Node JS
* npm
* Angular CLI
* TypeScript
* ReactiveX RxJS

Tutorial Source

[Tutorial Integrated JWT](https://www.youtube.com/watch?v=TOEm_WSS3bQ)
[Guide JWT Authentication Angular 2 and 4](http://jasonwatmore.com/post/2016/08/16/angular-2-jwt-authentication-example-tutorial)

## Backend Service API JWT Authentication

Laravel Backend:

user: admin
password: admin

*URL: http://lapazdigital.app/api/authenticate*
```json
{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbGFwYXpkaWdpdGFsLmFwcC9hcGkvYXV0aGVudGljYXRlIiwiaWF0IjoxNTExMjc0ODExLCJleHAiOjE1MTEyNzg0MTEsIm5iZiI6MTUxMTI3NDgxMSwianRpIjoib1dsRzZTUVhMZnYwU0I0YyIsInN1YiI6MSwicHJ2IjoiODdlMGFmMWVmOWZkMTU4MTJmZGVjOTcxNTNhMTRlMGIwNDc1NDZhYSJ9.gw3UhQMvL0aY93mPG_ovnOVIobooeN9upc1-Z9FHhTw",
    "response": "successful"
}
```
## Create Project Auth

```sh
ng new loginProject --prefix ng
ng serve -o
```

## User Model

Creating User Model

*Path: src/app/*
```sh
mkdir models
cd models
ng g cl User
```

*Path: src/app/models/user.ts*
```typescript
export class User {
    username: string;
    password: string;
}
```

## JWT Authentication Service

Creating Service Authentication

*Path: src/app/*
```sh
mkdir services
cd services
mkdir authentication
cd authentication
ng g s authentication
```
*Path: src/app/services/authentication/authentication.service.ts*
```typescript
import { Injectable } from '@angular/core';
import { Http, Headers, RequestOptions, Response } from '@angular/http';
import { Observable } from 'rxjs';
import 'rxjs/add/operator/map';
 
@Injectable()
export class AuthenticationService {
    
    public token: string;
    private apiUrl = "http://lapazdigital.app/api/";
    
    constructor(private http: Http) {
        // set token if saved in local storage
        var currentUser = JSON.parse(localStorage.getItem('currentUser'));
        this.token = currentUser && currentUser.token;
    }

    private getUrl(data: String) {
        return this.apiUrl + data;
    }

    login(username: string, password: string): Observable<boolean> {
        
        let body = "email=" + username + "&password=" + password;
        let headers = new Headers({'Content-Type':'application/x-www-form-urlencoded'});
        let options = new RequestOptions({'headers':headers});

        return this.http.post(this.getUrl('authenticate'), body, options).map((response: Response) => {
            // login successful if there's a jwt token in the response
            let token = response.json() && response.json().token;

            if (token) {
                // set token property
                this.token = token;
                // store username and jwt token in local storage to keep user logged in between page refreshes
                localStorage.setItem('currentUser', JSON.stringify({ username: username, token: token }));
                // return true to indicate successful login
                return true;
            } else {
                // return false to indicate failed login
                return false;
            }
        });
    } // End login

    logout(): void {
        // clear token remove user from local storage to log user out
        this.token = null;
        localStorage.removeItem('currentUser');
    }
}
```

## Login Component
 
Creating Login Component

*Path: src/app/components/*
```sh
ng g c login
```
Login Component

*Path: src/app/components/login.component.ts*
```typescript
import { Component, OnInit, ViewEncapsulation, HostListener} from '@angular/core';
import { Router } from '@angular/router';
import { AuthenticationService } from '../../services/authentication/authentication.service';

declare var require: any;

@Component({
  selector: 'ng-login',
  templateUrl: './login.component.html',
  styleUrls: ['./login.component.css'],
  encapsulation: ViewEncapsulation.None
})

export class LoginComponent implements OnInit {
    private imageLoginCard = require("./assets/login-card-lpd.png");
    private resol_X = 0;
    private resol_Y = 0;
    maxHeight = '100%';
    loginModel: any = {};
    loading = false;
    errorLogin: boolean = false;
    msgErrorLogin = '';

    constructor(private router: Router, private authenticationService: AuthenticationService) { }

    ngOnInit() {
        this.authenticationService.logout();   // reset login status
        this.resol_X = window.innerWidth;
        this.resol_Y = window.innerHeight;
        this.maxHeight = this.resol_Y + "px";
        console.log("Init Resolution: x = " + this.resol_X + ", y = " + this.resol_Y);
    }

    @HostListener('window:resize', ['$event'])
    onResize(event) {
      this.resol_Y = window.innerHeight;
      this.maxHeight = this.resol_Y + "px";
      console.log("Change Resolution: x = " + this.resol_X + ", y = " + this.resol_Y);
    }

    login() {
        this.loading = true;
        this.authenticationService.login(this.loginModel.username, this.loginModel.password).subscribe(result => {
            if (result === true) { // login successful
                console.log("Sucessful Login");
                this.errorLogin = false;
                this.router.navigate(['/']);
            } else {  // login failed
                console.error("Login Failed");
                this.msgErrorLogin = 'Nombre de Usuario ó Contraseña Incorrecto.';
                this.loading = false;
                this.errorLogin = true;
            }
        });
    }
}
```

Login Template

*Path: src/app/components/login.component.html*
```html
<div fxLayout="row" fxLayoutAlign="center center" class="main-content-login" [style.height]="maxHeight" >
    <mat-card class="login-card">
        <form name="form" (ngSubmit)="formLogin.form.valid && login()" #formLogin="ngForm" novalidate>
            <img mat-card-image [src]="imageLoginCard"/>
            <div class="center-items">
                <h4>INICIAR SESION</h4>
            </div>
            <div *ngIf="errorLogin" class="msg-error center-items">
                {{msgErrorLogin}}
            </div>
            <mat-card-content>
                <mat-form-field>
                    <input matInput placeholder="Usuario" name="username" [(ngModel)]="loginModel.username" #username="ngModel" required />
                </mat-form-field>
                <mat-form-field>
                    <input matInput placeholder="Contraseña" type="password" name="password" [(ngModel)]="loginModel.password" #password="ngModel" required />
                </mat-form-field>
            </mat-card-content>
            <mat-card-actions>
                <div class="center-items">
                    <button mat-raised-button color="primary" [disabled]="loading">Ingresar</button>
                </div>
            </mat-card-actions>
        </form> 
    </mat-card>
</div>
```
Login Style

*Path: src/app/components/login.component.css*
```css
.login-card {
	width: 280px;
	margin-top: 0px;		
}

.login-card .center-items {
	display: flex;
	flex-direction: row;
	box-sizing: border-box;
	justify-content: center;
	align-content: center;
	align-items: center;
}

.login-card img {
	box-sizing: border-box;
	margin-bottom: 5%;
}

.login-card .mat-card-actions button {
	margin-top: 5%;
	margin-bottom: 10%;
}

.login-card .msg-error {
	text-align: center;
	color: palevioletred;
	font-size: 13px;
	margin: 15px;
}

.login-card .mat-card-content {
	display: flex;
	flex-direction: column;
}

.main-content-login {
    display: flex; 
    flex-direction: row; 
    box-sizing: border-box; 
    justify-content: center; 
    align-content: center; 
    align-items: center;
    background-image: url('./assets/fondo.jpg');
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
}
```
*NOTE:* Before to Login Component [Install Material Design](003%20Angular%204%20Material%20Design.md)

## Home Component

Create Home Component

*Path: /src/app/*
```sh
cd components
ng g c home
```

*Path: src/app/components/home/home.component.ts*
```typescript
import { Component, OnInit, ViewEncapsulation } from '@angular/core';
import { User } from '../../models/user';
import { UserService } from '../../services/user/user.service';

@Component({
  selector: 'ng-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css'],
  encapsulation: ViewEncapsulation.None
})
export class HomeComponent implements OnInit {
    users: User[] = [];
    constructor(private userService: UserService) { }
    ngOnInit() {
        // this.service.section
     }
}
```

*Path: src/app/components/home/home.component.html*
```html
<div>
    <h1>Home</h1>
    <p>You're logged in with JWT!!</p>
    <div>
        Users from secure api end point:
        <ul>
            DATOS
        </ul>
    </div>
    <p><a [routerLink]="['/login']">Logout</a></p>
</div>
```

## Protecting Routes Using Guards

Creating Guards

*Path: src/app/*
```sh
mkdir guards
cd guards
ng g cl authGuard
```
*Path: src/app/guards/auth-guard.ts*
```typescript
import { Injectable } from '@angular/core';
import { Router, CanActivate } from '@angular/router';
 
@Injectable()
export class AuthGuard implements CanActivate {
    constructor(private router: Router) { }
    canActivate() {
        if (localStorage.getItem('currentUser')) {
            // logged in so return true
            return true;
        } else {
            // not logged in so redirect to login page
            this.router.navigate(['/login']);
            return false;
        }
    }
}
```

## App Routing

Creating Routes

*Path: src/app/*
```sh
ng g cl app.routing
```
*Path: src/app/app.routing.ts*
```typescript
import { Routes, RouterModule } from '@angular/router';
import { LoginComponent } from './components/login/login.component';
import { HomeComponent } from './components/home/home.component';
import { AuthGuard } from './guards/auth-guard';

const appRoutes: Routes = [
   { path: 'login', component: LoginComponent },
   { path: '', component: HomeComponent, canActivate: [AuthGuard] },
   { path: '**', redirectTo: '' } // otherwise redirect to home
];

export const routing = RouterModule.forRoot(appRoutes);
```

## App Modules

Add Declaration, Imports and Providers.

*Path: src/app/app.modules.ts*
```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';
import { AppComponent } from './app.component';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { MatToolbarModule, MatButtonModule, MatMenuModule, 
         MatIconModule, MatCardModule, MatFormFieldModule,
         MatInputModule 
       } from '@angular/material';

import { LoginComponent } from './components/login/login.component';
import { HomeComponent } from './components/home/home.component';
import { routing } from './app.routing';
import { AuthGuard } from './guards/auth-guard';
import { AuthenticationService } from './services/authentication/authentication.service';
import { UserService } from './services/user/user.service';

@NgModule({
  declarations: [
    AppComponent,
    LoginComponent,
    HomeComponent  
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule,
    BrowserAnimationsModule,
    MatToolbarModule,
    MatButtonModule,
    MatMenuModule,
    MatIconModule,
    MatCardModule,
    MatFormFieldModule,
    MatInputModule,
    routing
  ],
  providers: [
    AuthGuard,
    AuthenticationService,
    UserService
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

## Base Routing

*Path: src/app/index.html*
```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>La Paz Digital</title>
  <base href="/">   <!-- BASE REF -->
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
</head>
<body>
  <ng-root></ng-root>
</body>
</html>
```
## App Component

Change route default in template

*Path: src/app/app.component.html*
```html
<router-outlet></router-outlet>
```

*Path: src/app/app.component.ts*
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'ng-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})

export class AppComponent {
  ngOnInit(){
    console.log("La Paz Digital Frontend Initialized");
  }
}

```
## Protecting Routes in services app


https://scotch.io/tutorials/role-based-authentication-in-laravel-with-jwt