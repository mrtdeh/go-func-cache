# go-funcacher
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

Benchmarking :
```golang
func TestGoCacherBench(t *testing.T) {
	for i := 0; i < 5; i++ {

		sss := time.Now()
		var s string

		// wrap your code you want to cache into DoTry func
		// and set duration for recaching
		c.DoTry(time.Second*5, func() {
			time.Sleep(time.Second)
			s = fmt.Sprint(rand.Int() + 1000)
			// save new value in cache store
			c.Save("myvar", s)

		})

		// retrive and print cached value
		s = c.Get("myvar").(string)
		fmt.Println("my cached value : ", s)

		time.Sleep(time.Second)

		elapsed := time.Since(sss)
		log.Println(elapsed)
	}
}

```
run test with verbose mode : `-v`
and then result:
```
=== RUN   TestGetAgentHash
my cached value :  5577006791947780410
2022/03/29 08:24:02 2.000389789s
my cached value :  5577006791947780410
2022/03/29 08:24:03 1.000136586s
my cached value :  5577006791947780410
2022/03/29 08:24:04 1.000151866s
my cached value :  5577006791947780410
2022/03/29 08:24:05 1.000137946s
my cached value :  5577006791947780410
2022/03/29 08:24:06 1.000124832s
--- PASS: TestGetAgentHash (6.00s)
PASS
ok      command-line-arguments  6.004s
```
