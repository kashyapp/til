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

# `nil` channels do stuff
Sends and receives on nil channels block. It seems they are useful.

Example: (http://dave.cheney.net/2013/04/30/curious-channels)
In a select statement, if a specific channel needs to opt out, then you nil the reference to it. From that point on, all sends and receives on that channel can never proceed and are therefore ignored for select post that.  
