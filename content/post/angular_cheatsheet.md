+++
title = "Angular cheatsheet"
date = "2022-04-03"
description = "Angular cheatsheet"
tags = ["angular"]
summary = "Angular cheatsheet"
+++

Pour utilisation d'une enum dans un template, il faut ajouter le code suivant dans le composant :
```typescript
public readonly myEnum : typeof MyEnum = MyEnum;
```
Apres on peut l'utiliser dans le template ```MyEnum.VALUE1```

Le parent appel l'enfant :
Parent.component.ts :
```typescript
import {Subject} from 'rxjs/Subject';
...
export class ParentComp {
  changingValue: Subject<boolean> = new Subject();
        
  tellChild() {
    this.changingValue.next(true);
  }
}
```
Parent.component.html
```typescript
<my-comp [changing]="changingValue"></my-comp>
```
Child.component.ts
```typescript
...
export class ChildComp implements OnInit{
  @Input() changing: Subject<boolean>;
  
  ngOnInit(){
    this.changing.subscribe(v => { 
      console.log('value is changing', v);
    });
  }
}
```

