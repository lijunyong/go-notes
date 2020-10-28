# go-notes
go基础笔记

# module lookup disabled by -mod=vendor
```
#在对go mod项目执行go build的报错，可以通过：
export GOFLAGS=""
go build
```

# rm -rf 删除GOPATH下目录报Permission denied
```
https://github.com/golang/go/issues/27161
go clean -modcache
```
