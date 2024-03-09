+++
title = "Trie en Typescript d'un objet sur 2 champs"
date = "2023-06-05"
description = "Trie en Typescript d'un objet sur 2 champs"
tags = ["typescript"]
summary = "Trie en Typescript d'un objet sur 2 champs"
+++
Pour trier un objet sur 2 champs, il faut faire une fonction spéciale de trie :
```Typescript
interface Person {
  name: string;
  age: number;
}

const personnes: Person[] = [
  { name: "Alice", age: 25 },
  { name: "Bob", age: 30 },
  { name: "Charlie", age: 20 },
  { name: "Alice", age: 30 }
];

personnes.sort((a, b) => {
  if (a.age !== b.age) {
    return a.age - b.age; // Trie par âge en ordre croissant
  } else {
    return a.name.localeCompare(b.name); // Trie par nom en ordre alphabétique
  }
});
```
                    