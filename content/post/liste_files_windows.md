+++
title = "Liste les fichiers plus grands qu'une certaine taille"
date = "2022-09-25"
description = "Liste les fichiers plus grands qu'une certaine taille"
tags = ["windows"]
summary = "Liste les fichiers plus grands qu'une certaine taille"
+++
# Liste des fichiers superieurs à une certaine taille

## Batch

```bat
forfiles /P C:\ /M *.* /S /C "CMD /C if @fsize gtr 524288000 echo @PATH @FSIZE"
```

## Powershell

```powershell
Get-ChildItem C:\ -recurse | where-object {$_.length -gt 524288000} | Sort-Object length | ft fullname, length -auto
```

## Nushell

```shell
ls | where size > 10mb | sort modified
```
                    