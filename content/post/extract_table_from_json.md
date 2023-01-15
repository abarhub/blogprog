+++
title = "Extraction d'une table à partir de json"
date = "2022-11-17"
description = "Extraction d'une table à partir de json"
tags = ["json"]
summary = "Extraction d'une table à partir de json"
+++
# Exemple 1 
```shell
echo '{"key1":"val1", "myarray":["abc", "def", "ghi"]}' | jq -r '[.key1, .myarray[0]] | @csv'
"val1","abc"
```

# Exemple 2
```shell
jq -r '.results[] |  ( .properties |map(select(.key[] contains ("prod")) '
```
                    