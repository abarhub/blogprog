+++
title = "Injection un fichier dans du json en l'encodant en base64"
date = "2022-05-14"
description = "Injecter un fichier dans du json en l'encodant en base64"
tags = ["curl", "json"]
summary = "Injecter un fichier dans du json en l'encodant en base64"
+++
# Injection d'un fichier (Methode 1)

```shell
jq -Rn '.instances[0].image.b64 = inputs' < <(base64 volunteers.jpg | tr -d \\n) > input.json
```

cf [stakoverflow](https://stackoverflow.com/a/59578821/6577778)

# Injection d'un fichier (Methode 2)

```shell
jq -Rs --rawfile pub id_rsa.pub '{pem: ., pub: $pub}' id_rsa
```

cf [stakoverflow](https://stackoverflow.com/a/60422509/6577778)

# Encodage en base 64


```shell
jq '"Basic " + ("\(.user):\(.pass)"|@base64)' <basic.json
```

cf [stakoverflow](https://unix.stackexchange.com/a/590254)




