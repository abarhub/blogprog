+++
title = "A simple grep implementation in Go"
date = "2023-05-07"
description = "A simple grep implementation in Go"
tags = ["golang","grep"]
summary = "A simple grep implementation in Go"
+++
```golang
package main

import(
  "bufio"
  "fmt"
  "log"
  "os"
  "regexp"
)

func handleLine(line string) {
  matched, err := regexp.MatchString(os.Args[1], line)

  if err != nil {
    log.Fatal(err)
  } else if matched {
    fmt.Println(line)
  }
}

func main() {
  scanner := bufio.NewScanner(os.Stdin)

  for scanner.Scan() {
    handleLine(scanner.Text())
  }

  if err := scanner.Err(); err != nil {
    log.Fatal(err)
  }
}
```
                    