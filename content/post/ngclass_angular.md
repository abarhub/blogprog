+++
title = "Exemple de ngclass"
date = "2021-04-25"
description = "Exemple de ngclass"
tags = ["angular"]
summary = "Exemple de ngclass"
+++

# Exemple de ngclass :

```html
<p [ngClass]="'first second'">...</p>

<p [ngClass]="['first', 'second']">...</p>
  
<p [ngClass]="{'first': true, 'second': false}">...</p>
  
<p [ngClass]="stringExp|arrayExp|objExp">...</p>
  
<p [ngClass]="{'class1 class2 class3' : true}">...</p>
```

Pour d'autres exemples, voir [ici](https://malcoded.com/angular-cheat-sheet/) ou [ici](https://angular.io/guide/cheatsheet)