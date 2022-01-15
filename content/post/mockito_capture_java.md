+++
title = "Capture des paramètres avec Mockito "
date = "2020-06-18"
description = "Capture des paramètres avec Mockito "
tags = ["java", "mockito"]
+++


```Java
ArgumentCapto<Person> peopleCaptor = ArgumentCaptor.forClass(Person.class);
verify(mock, times(2)).doSomething(peopleCaptor.capture());
        
List<Person> capturedPeople = peopleCaptor.getAllValues();
assertEquals("John", capturedPeople.get(0).getName());
assertEquals("Jane", capturedPeople.get(1).getName());
```
