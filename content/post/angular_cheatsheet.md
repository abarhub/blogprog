+++
title = "Angular cheatsheet"
date = "2022-04-03"
description = "Angular cheatsheet"
tags = ["angular","cheatsheet"]
summary = "Angular cheatsheet"
+++

# Enum dans un Template

Pour utilisation d'une enum dans un template, il faut ajouter le code suivant dans le composant :
```typescript
public readonly myEnum : typeof MyEnum = MyEnum;
```
Apres on peut l'utiliser dans le template ```MyEnum.VALUE1```

# Communication parent/enfant

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

# Fermer un observable

Pour fermer un observable de façon automatique
```typescript
@Component({...})
export class AppComponent implements OnInit, OnDestroy {
    over$ = new Subject();
    
    ngOnInit () {
        var observable$ = Rx.Observable.interval(1000);
        observable$
          .pipe(takeUntil(this.over$))
          .subscribe(x => console.log(x));
    }    
    
    ngOnDestroy() {
        this.over$.next();
        this.over$.complete();
    }
}
```
Pour d'autres façon de le faire, voir ici :
[StackOverflow](https://blog.bitsrc.io/6-ways-to-unsubscribe-from-observables-in-angular-ab912819a78f)

