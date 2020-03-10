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
