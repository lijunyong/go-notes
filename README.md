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
# go context
```
func main()  {
	ctx, cancel := context.WithCancel(context.Background())
	go go1(ctx)
	time.Sleep(5 * time.Second)
	cancel()
	time.Sleep(5 * time.Second)
	fmt.Println("main done")
}

func go1(ctx context.Context)  {
	c, cancel := context.WithTimeout(ctx, 1 * time.Second)
	defer cancel()
	go go2(c)
	for{
		select {
		case <- ctx.Done():
			fmt.Println("ctx go1 done")
			return
		case <-time.After(500 * time.Millisecond):
			fmt.Println("go1")
		}
	}
}

func go2(ctx context.Context)  {
	for{
		select {
		case <-ctx.Done():
			fmt.Println("ctx go2 done")
			return
		case <-time.After(500 * time.Millisecond):
			fmt.Println("go2")
		}
	}
}
```
