# Embed sync.Mutex in a global variable
```go
var count = struct {
  n int
  mu sync.Mutex
}

func foo() {
  count.Lock()
  count.n++
  count.Unlock()
}
```
