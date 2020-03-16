# angulartutorial
MyAngularLearnings

#Use of if else:

app.component.ts

    ifelse = true;
    ifthenelse = false;
    
app.component.html

     <div *ngIf="ifelse; else elsecondition">[This is to show *ngif="condition; else alternate"]</div>
     <div *ngIf="ifthenelse; then thencondition; else elsecondition">[This is to show *ngif="condition; then whentrue; else alternate"]</div>
     <ng-template #thencondition>[thencondition: using ngtemplate #thencondid]</ng-template>
     <ng-template #elsecondition>[elsecondition: using ngtemplate #elsecondid]</ng-template>
     <button (click)="ifelse=!ifelse; ifthenelse=!ifthenelse">switch</button>
     
 #use of input output:
 app.component.ts
 
      pageno = 0;
      newpageno(newno){
         this.pageno=newno;
      }
  app.component.html
  
  <app-navbar [pageno]="pageno" (setpageno)="newpageno($event)"></app-navbar>

  <app-page1 [pageno]="pageno" [hidden]="pageno !== 0 && pageno !== 1"></app-page1>

  <app-page2 [pageno]="pageno" [hidden]="pageno !== 0 && pageno !== 2"></app-page2>

  <app-page3 [pageno]="pageno" [hidden]="pageno !== 0 && pageno !== 3"></app-page3>
  
  
  navbar.component.ts
  
  @Input() pageno: number;
  
  @Output() setpageno = new EventEmitter<Number>();
    
   setpagenumber(pageno){
   
   this.setpageno.emit(pageno);
   
   this.pageno = pageno;
  }

  navbar.component.html

  
        <a (click)="setpagenumber(1)">Page1</a>
     
          <a (click)="setpagenumber(2)">Page2</a>
     
          <a (click)="setpagenumber(3)">Page3</a>
      

   page1.component.ts
    @Input() pageno: number;

    page2.component.ts
     @Input() pageno: number;

    page3.component.ts
     @Input() pageno: number;
     
   ### Use of template for child communication
   ```
   child.component.ts
   childAttribute = 'Child Property';
  childBoolAttribute = true;
  constructor() { }

  ngOnInit() {
  }

  childMethod() {
    alert('Child Attribute value is '+ this.childAttribute);
  }

  toggleChildBoolAttr() {
    this.childBoolAttribute = ! this.childBoolAttribute;
  }
   ```
  ```
  app.component.html
  <div class="container">
    <div>Use of template with child</div>
    <app-child #child></app-child>
    <h3>{{child.childBoolAttribute}}</h3>
    <button (click)="child.childMethod()">Show Child Attribute</button>
    <button (click)="child.toggleChildBoolAttr()">Toggle Child Attribute</button>
  </div>
  ```
  ### Use of ElementRef, Renderer, @HostListener, @HostBinding
  
  - ElementRef => to access DOM element
  - Renderer => to work with DOM's element style
  - @HostListener => function decorator allows you to handle events of the host element 
  - @HostBinding => function decorator allows you to set the properties of the host element

 ### Creating custom directive
 ```
 @Directive({
    selector: '[appchangecolor]'
 })
 
 //Use it inside component
 <div appchangecolor>Content</div>
 
 //property value changes of host element using @HostBinding
 @HostBinding('style.width') widthmod: string;
 
 //directive constructor for using elementref, renderer
 constructor(private el: ElementRef, private renderer: Renderer) {}
 
 //handling event on host element in directive using @hostListener
 @HostListener('mouseover') onMouseMoveFunc() {
    this.renderer.setElementStyle(this.el.nativeElement, 'color','RED');
    this.widthmod = "100%";
 }
 //handling event on host element in directive using @hostListener
 @HostListener('mouseleave') onMouseLeaveFunc() {
    this.renderer.setElementStyle(this.el.nativeElement, 'color','BLACK');
    this.widthmod = "50%";
 }
 
 
 ```
 ### Use of Bootstrap
 ```
 npm install bootstrap@latest --save
 angular.json => styles: ['./node_modules/bootstrap/dist/css/bootstrap.min.css']
 header.component.html=>
 <nav class="navbar navbar-expand-lg navbar-dark">
    <a class="navbar-brand" href="#">Header</a>
    <div class="collapse navbar-collapse">
        <ul class="navbar-nav">
            <li class="nav-item">
                <a class="nav-link" routerLink="/admin/list">List</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" routerLink="/admin/list-create">List Create</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" routerLink="/admin/list-update">List Update</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" routerLink="/admin/login">Login</a>
            </li>
        </ul>
    </div>
 </nav>
 ```
### Login Page with bootstrap
```
login.component.html
<div class="container">
    <div class="row">
        <div class="col-md-6">
            <div class="card">
                <div class="card-header">
                    Login
                </div>
                <div class="card-body">
                    <div class="row">
                        <div class="col-md-4">
                            <img src="https://placeimg.com/128/128/nature">
                        </div>
                        <div class="col-md-6">
                            <input type="text" class="form-control" #email>
                            <input type="password" class="form-control" #password>
                            <button class="btn btn-primary" (click)="authService.login(email.value, password.value)">Login</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
```
### Use of firebase for authentication
```
1. copy app firebase config from console.firebase.google.com
app.module.ts

import { AngularFileModule } from '@angular/fire'
import { AngularFireAuthModule } from '@angular/fire/auth'
export
const firebaseconfig= {}
imports: [
    AngularFireModule.initializeApp(firbaseconfig),
    AngularFireAuthModule
]

auth.service.ts
import { Router} from '@angular/router'
import { User} from 'firebase'
import { auth} from 'firebase/app'
import {AngularFireAuth} from '@angular/fire/auth'
export
user:User
constructor(private afauth:AngularFireAuth, private router: Router) {
    this.afauth.authState.subscribe(user => {
        if(user) {
            this.user = user;
            localStorage.setItem("user", JSON.stringify(user))
        } else {
            localStorage.setItem("user", null)
        }
    });
}
//login method
async login(email: string, password: string) {
    try {
        await this.afauth.auth.signinWithEmailPassword(email, password);
        this.router.navigate(['admin/list'])
    } catch (e) {
        alert(e)
    }
}
async logout() {
    await this.afauth.auth.signout();
    localstorage.removeItem("user")
    this.router.navigate(['/admin/login']);
}
get isLoggedIn() {
    const user = JSON.parse(localstorage.getItem("user"))
    return user !== nil
}

header.component.ts
constructor(private authService: AuthService) {}
```
