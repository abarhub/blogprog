+++
title = "Logger toutes les propriétés de Spring Boot"
date = "2020-10-05"
description = "Logger toutes les propriétés de Spring Boot"
tags = ["java", "log"]
summary = "Logger toutes les propriétés de Spring Boot"
+++

Classe pour logguer toutes les propriétés avec Spring boot :
```Java
package com.toto.myapp.util;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.boot.context.event.ApplicationPreparedEvent;
import org.springframework.context.ApplicationListener;
import org.springframework.core.env.ConfigurableEnvironment;
import org.springframework.core.env.EnumerablePropertySource;
import org.springframework.core.env.PropertySource;

import java.util.LinkedList;
import java.util.List;

public class PropertiesLogger implements ApplicationListener<ApplicationPreparedEvent> {
  private static final Logger log = LoggerFactory.getLogger(PropertiesLogger.class);

  private ConfigurableEnvironment environment;
  private boolean isFirstRun = true;

  @Override
  public void onApplicationEvent(ApplicationPreparedEvent event) {
    if (isFirstRun) {
      environment = event.getApplicationContext().getEnvironment();
      printProperties();
    }
    isFirstRun = false;
  }

  public void printProperties() {
    for (EnumerablePropertySource propertySource : findPropertiesPropertySources()) {
      log.info("******* " + propertySource.getName() + " *******");
      String[] propertyNames = propertySource.getPropertyNames();
      Arrays.sort(propertyNames);
      for (String propertyName : propertyNames) {
        String resolvedProperty = environment.getProperty(propertyName);
        String sourceProperty = propertySource.getProperty(propertyName).toString();
        if(resolvedProperty.equals(sourceProperty)) {
          log.info("{}={}", propertyName, resolvedProperty);
        }else {
          log.info("{}={} OVERRIDDEN to {}", propertyName, sourceProperty, resolvedProperty);
        }
      }
    }
  }

  private List<EnumerablePropertySource> findPropertiesPropertySources() {
    List<EnumerablePropertySource> propertiesPropertySources = new LinkedList<>();
    for (PropertySource<?> propertySource : environment.getPropertySources()) {
      if (propertySource instanceof EnumerablePropertySource) {
        propertiesPropertySources.add((EnumerablePropertySource) propertySource);
      }
    }
    return propertiesPropertySources;
  }
}
```


Classe permettant de lister toutes les propriétés
Pour l'utiliser, il faut utiliser : 
`Java 
public static void main(String[] args) {
        SpringApplication springApplication = new SpringApplication(MyApplication.class);
        springApplication.addListeners(new PropertiesLogger());
        springApplication.run(args);        
}`
ou alors : 
`Java
@SpringBootApplication
public class Application extends SpringBootServletInitializer {
    private static Class<Application> applicationClass = Application.class;
    @Override
    protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
        return application.sources(applicationClass).listeners(myListener());
    }

    private ApplicationListener< ApplicationStartedEvent> myListener() {
        ....
    }

}`

voir : 
[code](https://stackoverflow.com/questions/48212761/how-to-log-all-active-properties-of-a-spring-boot-application-before-the-beans-i/48212783#48212783)
ou
[code avec un war](https://github.com/spring-projects/spring-boot/issues/2636#issuecomment-78434103)