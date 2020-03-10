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