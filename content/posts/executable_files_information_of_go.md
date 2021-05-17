---
title: "Executable files information of go"
date: 2021-05-16T23:00:43+09:00
draft: false
categories: ["Tech"]
tags: ["Go"]
---

`go version -m` can print module dependency of executable file's code.

```bash
> go version -m /usr/local/bin/peco
/usr/local/bin/peco: go1.14.5
        path    command-line-arguments
        mod     github.com/peco/peco    (devel)
        dep     github.com/google/btree v0.0.0-20161213163243-0c3044bc8bad      h1:IIXE5Gtu2VS7SL3lhB61iSliE+jpOwuYDYAH4HGxGwY=
        dep     github.com/jessevdk/go-flags    v1.1.0  h1:Geou1o2RJhW9nUu+puVL2ASZMWjfj6+uy97+byGKL98=
        dep     github.com/lestrrat-go/pdebug   v0.0.0-20180220043849-39f9a71bcabe      h1:S7XSBlgc/eI2v47LkPPVa+infH3FuTS4tPJbqCtJovo=
        dep     github.com/mattn/go-runewidth   v0.0.0-20161012013512-737072b4e32b      h1:idzeyUe3K4aU/SIZWMykIkJJyTD7CgDkxUQEjV07fno=
        dep     github.com/nsf/termbox-go       v0.0.0-20190817171036-93860e161317      h1:hhGN4SFXgXo61Q4Sjj/X9sBjyeSa2kdpaOzCO+8EVQw=
        dep     github.com/pkg/errors   v0.0.0-20161029093637-248dadf4e906      h1:aXc/AM323HlkOXjl3QuSO06wbXK45HrzBT+pwVOufXg=
```

https://golang.org/pkg/cmd/go/internal/version/