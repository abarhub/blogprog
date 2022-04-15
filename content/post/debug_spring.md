+++
title = "Débugage spring"
date = "2021-03-06"
description = "Débugage spring"
tags = ["java", "spring", "spring boot", "debug"]
summary = "Débugage spring"
+++

Pour débuguer Spring boot, il y a 2 options :
* --debug : affiche les modules de spring boot activés ou pas activé
* --trace : affiche plus d'information, notemment la recherche de fichiers et les paramètres de configuration

Exemple d'utilisation :
```shell
java -Ddebug monjar.jar
```
ou 
```shell
java monjar.jar --debug
```

On peut aussi augmenter le niveau de log (a mettre dans application.properties) :
```properties
logging.level.org.springframework=DEBUG
```

pour spring security, c'est dans le code :
```Java
// par annotation :
@EnableWebSecurity(debug = true)
public class SecurityConfiguration extends WebSecurityConfigurerAdapter {
   // etc...
}
```
```Java
// par code :
@EnableWebSecurity
public class WebSecurityConfiguration extends WebSecurityConfigurerAdapter {

    @Override
    public void configure(WebSecurity web) throws Exception {
        web.debug(true);
    }
}
```
et au niveau log :
```properties
logging.level.org.springframework.security=DEBUG
```