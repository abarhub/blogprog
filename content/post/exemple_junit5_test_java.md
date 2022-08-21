+++
title = "Exemple de test paramétré"
date = "2020-10-30"
description = "Exemple de test paramétré"
tags = ["java", "junit5", "test"]
summary = "Exemple de test paramétré"
+++

Exemple de test paramétré :
```Java
class ParametreTest {
  
  @ParameterizedTest
  @MethodSource("provideStringsForIsBlank")
  void isBlank_ShouldReturnTrueForNullOrBlankStrings(String input, boolean expected) {
    assertEquals(expected, Strings.isBlank(input));
  }

  private static Stream<Arguments> provideStringsForIsBlank() {
    return Stream.of(
      Arguments.of(null, true),
      Arguments.of("", true),
      Arguments.of("  ", true),
      Arguments.of("not blank", false)
    );
  }
  
}
```
Code basé sur le site [Baeldung](https://www.baeldung.com/parameterized-tests-junit-5)
