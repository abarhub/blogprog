+++
title = "Commandes équivalentes aux commandes Linux sous Windows"
date = "2025-05-31"
description = "Commandes équivalentes aux commandes Linux sous Windows"
tags = []
summary = "Commandes équivalentes aux commandes Linux sous Windows"
+++
# Commandes Linux équivalentes sous Windows

## Recehrche de fichiers contenant un texte

```bat 
DOS> findstr text *.*
DOS> findstr text c:\repertoire\*.txt
# dans les sous répertoires
DOS> findstr /S text *.*
```
```powershell
PowerShell> Select-String -Path "C:\repertoire\*.csv" -Pattern "texte" 
PowerShell> Get-ChildItem -Path C:\repertoire\*.txt -Recurse | Select-String -Pattern 'Texte' -CaseSensitive
```

## Recherche de fichiers par le nom

```bat 
DOS> dir /b/s *.txt
DOS> dir /s *foo*
```
```powershell
PowerShell> Get-ChildItem -Path .\* -Include *.mp4 -Recurse
PowerShell> Get-ChildItem -Recurse -Path C:\ | Where-Object {$_.Length gt 1MB}
PowerShell> Get-ChildItem -Path .\* -Include *.mp4 -Recurse | Where-Object { $_.CreationTime -lt '2024-01-01' }
# exclu des fichiers. Semble ne fonctionner que pour les fichiers, et pas pour les répertoires
PowerShell> Get-ChildItem -Path . -Recurse -Exclude ('node_modules', 'node', 'target','*.jar') -File
```

## Appel url / telechargement de fichiers

```powershell
PowerShell> Invoke-WebRequest https://www.google.fr
PowerShell> Invoke-WebRequest -Proxy "http://proxy.hostname:8090/" https://www.google.fr 
PowerShell> Invoke-WebRequest -NoProxy https://www.google.fr
PowerShell> Invoke-WebRequest -SkipCertificateCheck https://www.google.fr
PowerShell> Invoke-WebRequest [$myDownloadUrl](https://www.google.fr) -OutFile c:\temp\file.html
PowerShell> Invoke-WebRequest "https://httpbin.org/ip"
```

## Commandes équilavantes à jq

```powershell
# curl "https://api.example.com/data" | jq '.someField'

# URL de l'API
$url = "https://api.example.com/data"

# Appeler l'API et obtenir l'objet JSON
# Invoke-RestMethod convertit automatiquement la réponse JSON en un objet PowerShell
$jsonData = Invoke-RestMethod -Uri $url

# Accéder au champ souhaité (remplacez 'someField' par le nom de votre champ)
$fieldValue = $jsonData.someField

# Afficher la valeur du champ
Write-Host "La valeur du champ est : $fieldValue"

# Si le champ est imbriqué, par exemple .data.item
# $fieldValue = $jsonData.data.item
```

```powershell
PowerShell> (Invoke-RestMethod -Uri "https://api.example.com/data").someField(Invoke-RestMethod -Uri "https://api.example.com/data").someField
```
                    