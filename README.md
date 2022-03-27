# go-func-cache
Simple cache go function with key/val storing...

install :
```

go get github.com/mrtdeh/go-func-cache

```

use:
```
// main.go

var c caching.Cache

func main() {

	for {
		testCacheFunc()
		time.Sleep(time.Second * 1)
	}
}

func testCacheFunc() {
	var s string
  
	c.DoTry(time.Second*5, func() {

		s = fmt.Sprint(rand.Int() + 1000)
		fmt.Println(sss)
		c.Save("myvar", s)

	})

	s = c.Get("myvar").(string)
	fmt.Println("my cached value : ", s)

}


```
