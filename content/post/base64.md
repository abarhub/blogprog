+++
title = "Encode et décode en Base64"
date = "2022-04-11"
description = "Encode et décode en Base64 des fichiers sous Linux et Windows"
tags = ["shell", "windows", "linux"]
summary = "Encode et décode en Base64 des fichiers sous Linux et Windows"
+++

# Linux

Encode :
```shell
base64 data.txt > data.b64
```

Décode :
```shell
base64 -d data.b64 > data.txt
```

# Windows

Encode :
```shell
certutil -encode data.txt tmp.b64 && findstr /v /c:- tmp.b64 > data.b64
```

Décode :
```shell
certutil -decode data.b64 data.txt
```