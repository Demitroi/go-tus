你好！
很冒昧用这样的方式来和你沟通，如有打扰请忽略我的提交哈。我是光年实验室（gnlab.com）的HR，在招Golang开发工程师，我们是一个技术型团队，技术氛围非常好。全职和兼职都可以，不过最好是全职，工作地点杭州。
我们公司是做流量增长的，Golang负责开发SAAS平台的应用，我们做的很多应用是全新的，工作非常有挑战也很有意思，是国内很多大厂的顾问。
如果有兴趣的话加我微信：13515810775  ，也可以访问 https://gnlab.com/，联系客服转发给HR。
# go-tus [![Build Status](https://travis-ci.org/eventials/go-tus.svg?branch=master)](https://travis-ci.org/eventials/go-tus) [![Go Report Card](https://goreportcard.com/badge/github.com/eventials/go-tus)](https://goreportcard.com/report/github.com/eventials/go-tus) [![GoDoc](https://godoc.org/github.com/eventials/go-tus?status.svg)](http://godoc.org/github.com/eventials/go-tus)

A pure Go client for the [tus resumable upload protocol](http://tus.io/)

## Example

```go
package main

import (
    "os"
    "github.com/eventials/go-tus"
)

func main() {
    f, err := os.Open("my-file.txt")

    if err != nil {
        panic(err)
    }

    defer f.Close()

    // create the tus client.
    client, _ := tus.NewClient("https://tus.example.org/files", nil)

    // create an upload from a file.
    upload, _ := tus.NewUploadFromFile(f)

    // create the uploader.
    uploader, _ := client.CreateUpload(upload)

    // start the uploading process.
    uploader.Upload()
}
```

## Features

> This is not a full protocol client implementation.

Checksum, Termination and Concatenation extensions are not implemented yet.

This client allows to resume an upload if a Store is used.

## Built in Store

Store is used to map an upload's fingerprint with the corresponding upload URL.

| Name | Backend | Dependencies |
|:----:|:-------:|:------------:|
| MemoryStore  | In-Memory | None |
| LeveldbStore | LevelDB   | [goleveldb](https://github.com/syndtr/goleveldb) |

## Future Work

- [ ] SQLite store
- [ ] Redis store
- [ ] Memcached store
- [ ] Checksum extension
- [ ] Termination extension
- [ ] Concatenation extension
