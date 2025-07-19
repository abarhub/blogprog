+++
title = "Configuration logback"
date = "2024-03-17"
description = "Configuration logback"
tags = ["log","java"]
summary = "Configuration logback"
+++
# Configuration logback

## Exemple simple 

Utilisation en Java avec SLF4J
```Java
public class Slf4jExample {

    private static final Logger LOGGER = LoggerFactory.getLogger(Slf4jExample.class);

    public static void main(String[] args) {
        LOGGER.debug("Debug log message");
        LOGGER.info("Info log message");
        LOGGER.error("Error log message");
    }
}
```

Configuration simple sur la console
```xml
<configuration>

    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <layout class="ch.qos.logback.classic.PatternLayout">
            <Pattern>
                %d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n
            </Pattern>
        </layout>
    </appender>

    <logger name="com.mkyong" level="debug" additivity="false">
        <appender-ref ref="CONSOLE"/>
    </logger>

    <root level="error">
        <appender-ref ref="CONSOLE"/>
    </root>

</configuration>
```

## Configuration en reprenant le pattern de spring boot

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration scan="true">
    <!-- use Spring default values -->
    <include resource="org/springframework/boot/logging/logback/defaults.xml"/>

    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>${CONSOLE_LOG_PATTERN}</pattern>
            <charset>utf8</charset>
        </encoder>
    </appender>
    …
</configuration>
```


## Séparation de certains log dans un fichier séparé

Pour mettre les logs dans un fichier séparé :
```xml
<?xml version="1.0"?>
<configuration>
    <appender name="FILE" class="ch.qos.logback.core.FileAppender">
        <file>logfile.log</file>
        <append>true</append>
        <encoder>
            <pattern>%-4relative [%thread] %-5level %logger{35} - %msg %n</pattern>
        </encoder>
    </appender>
    <appender name="ANALYTICS-FILE" class="ch.qos.logback.core.FileAppender">
        <file>analytics.log</file>
        <append>true</append>
        <encoder>
            <pattern>%-4relative [%thread] %-5level %logger{35} - %msg %n</pattern>
        </encoder>
    </appender>
    <!-- additivity=false ensures analytics data only goes to the analytics log -->
    <logger name="analytics" level="DEBUG" additivity="false">
        <appender-ref ref="ANALYTICS-FILE"/>
    </logger>
    <root>
        <appender-ref ref="FILE"/>
    </root>
</configuration>
```

Pour l'utiliser
```Java
Logger analytics = LoggerFactory.getLogger("analytics");
```

## Pour indiquer ou se trouve le fichier de log

```shell
-Dlogging.config=file:///your/file/location/logback.xml
```

## Configuration d'un appender dans un fichier avec rollback

```xml
<configuration>
  <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
    <file>logFile.log</file>
    <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
      <!-- daily rollover -->
      <fileNamePattern>logFile.%d{yyyy-MM-dd}.log</fileNamePattern>

      <!-- keep 30 days' worth of history capped at 3GB total size -->
      <maxHistory>30</maxHistory>
      <totalSizeCap>3GB</totalSizeCap>

    </rollingPolicy>

    <encoder>
      <pattern>%-4relative [%thread] %-5level %logger{35} -%kvp- %msg%n</pattern>
    </encoder>
  </appender> 

  <root level="DEBUG">
    <appender-ref ref="FILE" />
  </root>
</configuration>
```

## syntaxe des pattern

La documentation est [ici](https://logback.qos.ch/manual/layouts.html#conversionWord)

* %X{ABC} : pour afficher un MDC. Si le {} n'est pas présent, c'est pour le MDC qui est affiché
* ${PID} : le pid du processus. C'est spécifique à Spring Boot
                    