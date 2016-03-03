## Embed sync.Mutex in a global variable
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

## `nil` channels do stuff
Sends and receives on nil channels block. It seems they are useful.

Example: (http://dave.cheney.net/2013/04/30/curious-channels)
In a select statement, if a specific channel needs to opt out, then you nil the reference to it. From that point on, all sends and receives on that channel can never proceed and are therefore ignored for select post that.  

## Stacked Channels (is what the author calls it)
http://gowithconfidence.tumblr.com/post/31426832143/stacked-channels

Using a Buffered channel of size 1, don't do channel send, but use a custom method `Stack(item)` which uses a `select` operation to either do a successful send (or) receive the current value, accumulate with the new one and goes back into select to send it.
