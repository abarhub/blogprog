+++
title = "Suppression des branches mergées"
date = "2022-03-20"
description = "Suppression des branches mergées"
tags = ["linux", "windows", "shell", "powershell", "git"]
summary = "Suppression des branches mergées"
+++
# Linux

Fetch pour mettre à jour les branches
```shell
git fetch -p
```

Suppression des branches locales
```shell
git branch --merged | grep -v '\*\|master\|main\|develop' | xargs -n 1 git branch -d
```

Suppression des branches distantes
```shell
git branch -r --merged | grep -v '\*\|master\|main\|develop' | sed 's/origin\///' | xargs -n 1 git push --delete origin
```

# Windows

Suppression des branches locales mergées
```Powershell
git branch --format "%(refname:short)" -r --merged develop | Select-String "develop|master|HEAD" -notMatch | Out-GridView -PassThru | % { git branch -d $_ }
```

Suppression des branches distantes mergées (ne marche pas)
```Powershell
git branch --format "%(refname:short)" -r --merged develop | Select-String "develop|master|HEAD" -notMatch | Out-String -Stream  | ($_) -replace "\(origin\/\)","" | Out-GridView -PassThru | % {  echo $_  }
```

cf :
[StackOverflow](https://stackoverflow.com/a/24558813/14275002)
[PowerShell](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/select-string?view=powershell-7.2)