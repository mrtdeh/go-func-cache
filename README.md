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

benchmarking :
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

		elapsed := time.Since(sss)
		log.Println(elapsed)

		time.Sleep(time.Second)
	}
}

```
run test with verbose mode : `-v`

and then result:
```
=== RUN   TestGetAgentHash
my cached value :  5577006791947780410
2022/03/29 08:31:53 1.000210903s
my cached value :  5577006791947780410
2022/03/29 08:31:54 20.754µs
my cached value :  5577006791947780410
2022/03/29 08:31:55 17.763µs
my cached value :  5577006791947780410
2022/03/29 08:31:56 23.756µs
my cached value :  5577006791947780410
2022/03/29 08:31:57 17.136µs
--- PASS: TestGetAgentHash (6.00s)
PASS
ok      command-line-arguments  6.003s
```
