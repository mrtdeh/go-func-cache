# go-func-cache
Simple cache go function with key/val storing...

install :
```

go get github.com/mrtdeh/go-func-cache

```

use:
```golang
// main.go

var c caching.Cache

func main() {

	// run priodicly cached function
	for {
		testCacheFunc()
		time.Sleep(time.Second * 1)
	}
}

func testCacheFunc() {
	var s string
  	
	// wrap your code you want to cache into DoTry func
	// and set duration for recaching
	c.DoTry(time.Second*5, func() {

		s = fmt.Sprint(rand.Int() + 1000)
		// save new value in cache store
		c.Save("myvar", s)

	})

	// retrive and print cached value
	s = c.Get("myvar").(string)
	fmt.Println("my cached value : ", s)

}


```
