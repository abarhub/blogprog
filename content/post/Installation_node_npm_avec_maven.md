+++
title = "Installation de node et npm avec maven"
date = "2021-10-09"
description = "Installation de node et npm avec maven"
tags = ["maven", "npm", "build"]
+++

# Installation de node et npm avec maven

Il faut utiliser l'outils : [frontend-maven-plugin](https://github.com/eirslett/frontend-maven-plugin)

Exemple :

```xml
<plugin>
    ...
    <executions>
        <execution>
            <!-- optional: you don't really need execution ids, but it looks nice in your build log. -->
            <id>install node and npm</id>
            <goals>
                <goal>install-node-and-npm</goal>
            </goals>
            <!-- optional: default phase is "generate-resources" -->
            <phase>generate-resources</phase>
        </execution>
    </executions>
    <configuration>
        <nodeVersion>v4.6.0</nodeVersion>

        <!-- optional: with node version greater than 4.0.0 will use npm provided by node distribution -->
        <npmVersion>2.15.9</npmVersion>
        
        <!-- optional: where to download node and npm from. Defaults to https://nodejs.org/dist/ -->
        <downloadRoot>http://myproxy.example.org/nodejs/</downloadRoot>
    </configuration>
</plugin>
```