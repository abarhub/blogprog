+++
title = "Exemple de loggeur avec slf4j"
date = "2020-06-24"
description = "Exemple de loggeur avec slf4j"
tags = ["java", "log", "slf4j"]
+++


```Java
public class ExempleLogger {

    private static final Logger LOGGER = LoggerFactory.getLogger(ExempleLogger.class);

    public void exemple(){
      LOGGER.info("test {}", 52);
    }
}
```
