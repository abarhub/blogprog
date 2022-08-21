+++
title = "Unsubscribe des observables"
date = "2022-05-27"
description = "Unsubscribe des observables"
tags = ["angular","web"]
summary = "Unsubscribe des observables"
+++
Il faut penser à unsubscribe les observables.

```typescript
import { interval } from 'rxjs';

const data$ = interval(1000);


const subscription = data$.subscribe({
    next: value => console.log(value),
    error: error => console.error(error),
    complete: () => console.log('DONE!')
});

// dans le ngOnDestroy()
subscription.unsubscribe();
```

Une façon simple de le gérer, c'est d'utiliser takeUntil
```typescript
import { Component, OnInit, OnDestroy } from '@angular/core';

import { Subject, interval } from 'rxjs';
import { takeUntil } from 'rxjs/operators';

@Component({ ... })
export class AppComponent implements OnInit, OnDestroy {
  isOver$: Subject<boolean> = new Subject<boolean>();

  constructor(private apollo: Apollo) {}

  ngOnInit() {
    this.myService.getAll()
           .pipe(takeUntil(this.isOver$))
           .subscribe(data => {
              console.info(data);
           },(e)=>{
              console.error("Error", e);
           });    
  }

  ngOnDestroy() {
    this.isOver$.next(true);
    this.isOver$.unsubscribe();
  }
}

```

