+++
title = "Formation Angular 17 (02/2024)"
date = "2024-02-15"
description = "Formation Angular 17 (02/2024)"
tags = ["angular"]
summary = "Formation Angular 17 (02/2024)"
+++
# Formation Angular

## Ne jamais faire de subscrib dans un subscrib

Il ne faut jamais faire de :
```typescript
this._bookRepository.getBookList()
this._bookRepository.getBookList()
.subscribe(bookList => {
this.bookList = bookList
let autre=this.other.get().subscribe(bookList => {
  // autre traitement
});
})
```
Si on fait comme ça, on n'est pas sur de l'ordre des appels. Exemple [ici](http://getgoingit.blogspot.com/2018/05/passing-value-from-one-observable-to.html).
Il faut utiliser un switchMap pour ne prendre que le dernier, et faire un seul appel.
Il faut aussi penser à retourner quelque chose s'il y a une erreur pour éviter d'arreter le flux.

## Libération d'un observable

Pour liberer un observable, il faut utiliser takeUntileDestroy().


                    