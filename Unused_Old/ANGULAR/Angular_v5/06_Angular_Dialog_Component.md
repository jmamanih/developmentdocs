# ANGULAR DIALOG COMPONENT
## Version 4 & 5

Reference tutorial:

https://blog.thoughtram.io/angular/2017/11/13/easy-dialogs-with-angular-material.html

## Creating dialogs with MatDialog

*Example: User Dialog Component*

```sh
cd src/app/components/users
ng g c user-dialog
```

*path: src/app/components/users/user-dialog.component.ts*

```typescript
import { Component, OnInit, ViewEncapsulation } from '@angular/core';
import { MatDialog, MatDialogRef } from '@angular/material';

@Component({
  selector: 'ng-user-dialog',
  templateUrl: './user-dialog.component.html',
  styleUrls: ['./user-dialog.component.css'],
  encapsulation: ViewEncapsulation.None
})
export class UserDialogComponent implements OnInit {

  //constructor(public dialogRef:  ) { }
  constructor(public dialogRef: MatDialogRef<UserDialogComponent>) {}

  ngOnInit() {
  }
  
  closeDialog(): void {
    console.log("Cerrando dialogo");
    this.dialogRef.close();
  }
}
```
*path: src/app/components/users/user-dialog.component.html*
```html
<mat-toolbar>
    <span>{{title}}</span>
    <span class="head-menu-spacer"></span>
    <button mat-icon-button mat-dialog-close>
        <mat-icon>close</mat-icon>
    </button>
</mat-toolbar>  
<mat-dialog-content>
    Content goes here
</mat-dialog-content>
<mat-dialog-actions>
    <button mat-button mat-dialog-close>No</button>
    <button mat-button [mat-dialog-close]="true">Yes</button>
</mat-dialog-actions>
```
*path: src/app/app.modules.ts*

```typescript
import { MatDialogModule } from '@angular/material';
import { UserDialogComponent } from './components/admin/users/user-dialog/user-dialog.component';

@NgModule({
  declarations: [
    //...
    UserDialogComponent      
  ],
  imports: [
    //...
  ],
  providers: [
      //...
  ],
  entryComponents: [UserDialogComponent]
})
```

## Sharing data with dialogs 

Parameters

*path: src/app/components/users/user.component.html*

```html
<mat-cell *matCellDef="let user">
    <mat-icon (click)="openDialog(user.id,'Modificar Datos del Usuario')">edit</mat-icon>
    <mat-icon aria-label="Inhabilitar Usuario">block</mat-icon>
    <mat-icon aria-label="Cambiar Contraseña">vpn_key</mat-icon>
</mat-cell>
```

Inside our component

*path: src/app/components/users/user.component.ts*

```typescript
import { Component, OnInit, Inject } from '@angular/core';
import { User } from '../../../models/user';
import { MatPaginator,  MatTableDataSource, MatSort, MatDialog, MatDialogRef } from '@angular/material';

declare var require: any;

@Component({
    selector: 'ng-users',
    templateUrl: './users.component.html',
    styleUrls: ['./users.component.css'],
    encapsulation: ViewEncapsulation.None
})

export class UsersComponent implements OnInit {

    public users: User[];
    displayedColumns = ['id', 'actions', 'name', 'email'];
    dataSource: any;
    userDialogRef: MatDialogRef<UserDialogComponent>;

    constructor(private router: Router, private userService: UserService, public dialog: MatDialog) { }

    ngOnInit() {
        // ...
    }
    
    openDialog(id: number, title: string) {
        console.log("Open Dialog: ", id);
        this.userDialogRef = this.dialog.open(UserDialogComponent, {
            hasBackdrop: false,
            width:'550px',
            data: { titleDialog: title}
        });

        this.userDialogRef.afterClosed().subscribe(result=>{
            console.log("Luego de cerrar el dialogo");
        });
    }
}
```

Inject data using the MAT_DIALOG_DATA.

*path: src/app/components/users/user-dialog.component.ts*

```typescript
import { Component, OnInit, ViewEncapsulation, Inject } from '@angular/core';
import { MatDialog, MatDialogRef, MAT_DIALOG_DATA } from '@angular/material';

@Component({
  selector: 'ng-user-dialog',
  templateUrl: './user-dialog.component.html',
  styleUrls: ['./user-dialog.component.css'],
  encapsulation: ViewEncapsulation.None
})
export class UserDialogComponent implements OnInit {
  title: string;

  constructor(public dialogRef: MatDialogRef<UserDialogComponent>, @Inject(MAT_DIALOG_DATA) private data) {}

  ngOnInit() {
    this.title = this.data.titleDialog;
  }
  
  closeDialog(): void {
    console.log("Cerrando dialogo");
    this.dialogRef.close();
  }
}
```