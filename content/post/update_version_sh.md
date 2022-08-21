+++
title = "Changement de version des pom"
date = "2020-06-18"
description = "Changement de version des pom"
tags = ["java", "maven", "version"]
+++


```shell
# changement de version des pom
mvn versions:set -DnewVersion=1.0.0.0-SNAPSHOT

# changement de version des pom sans backup
mvn versions:set -DnewVersion=1.0.0.0-SNAPSHOT -DgenerateBackupPoms=false
```

<!--more-->
