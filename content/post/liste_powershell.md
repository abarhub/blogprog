+++
title = "Récupération d'une liste avec des appels rest"
date = "2024-05-11"
description = "Récupération d'une liste avec des appels rest"
tags = []
summary = "Récupération d'une liste avec des appels rest"
+++
```powershell
$url = "https://jsonplaceholder.typicode.com/posts"

$n=0
$val=0

$res = @()


while($val -ne 100)
{
    $val++
    Write-Host $val

    $url2=$url+"?_start="+$n+"&_limit=5"
    Write-Host $url2

    $result = Invoke-RestMethod -uri "$url2" -UseDefaultCredentials -Method Get -ContentType "application/json"

    if($result.Count -eq 0) {
        break
    }
    
    $res += $result

    Write-Host "count", $res.Count

    $n=$n+5
}

Write-Host "res"

$res
```
                    