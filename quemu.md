## Show me golang example code how can i write a simple application which can run on QEMU

Sure, here is an example of a simple Go program that you can run on QEMU:

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, QEMU!")
}
```

To run this program on QEMU, you will need to first install Go and QEMU on your system. Once you have those set up, you can compile the program using the go build command:

```
go build hello.go
```
This will create an executable binary file called hello in the current directory. You can then run the binary on QEMU using the following command:

```
qemu-arm ./hello
```
This will start QEMU and run the hello program inside it. You should see the output "Hello, QEMU!" printed to the console.

Note that the above example assumes that you are running QEMU in ARM mode. If you are running QEMU in a different mode (e.g. x86), you will need to specify the appropriate target architecture when compiling the Go program. You can do this by setting the GOARCH environment variable before running the go build command, e.g.

```
GOARCH=amd64 go build hello.go
```
I hope this helps! Let me know if you have any questions.
