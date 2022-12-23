## Give me golang code example for creating persistent Linux container using multiple namespaces (mount,pid,uts,user,cgroup,network) 

> Here is an example of how you might create a persistent Linux container using multiple namespaces in Go:

```go
package main

import (
	"fmt"
	"os"
	"syscall"
)

func main() {
	// Create a new mount namespace
	if err := syscall.Unshare(syscall.CLONE_NEWNS); err != nil {
		fmt.Println(err)
		return
	}

	// Mount an empty directory as the root filesystem for the container
	if err := syscall.Mount("/path/to/empty/directory", "/", "", syscall.MS_BIND, ""); err != nil {
		fmt.Println(err)
		return
	}

	// Create a new PID namespace
	if err := syscall.Unshare(syscall.CLONE_NEWPID); err != nil {
		fmt.Println(err)
		return
	}

	// Create a new UTS namespace
	if err := syscall.Unshare(syscall.CLONE_NEWUTS); err != nil {
		fmt.Println(err)
		return
	}

	// Create a new user namespace
	if err := syscall.Unshare(syscall.CLONE_NEWUSER); err != nil {
		fmt.Println(err)
		return
	}

	// Create a new cgroup namespace
	if err := syscall.Unshare(syscall.CLONE_NEWCGROUP); err != nil {
		fmt.Println(err)
		return
	}

	// Create a new network namespace
	if err := syscall.Unshare(syscall.CLONE_NEWNET); err != nil {
		fmt.Println(err)
		return
	}

	// Change the root directory for the container
	if err := syscall.PivotRoot("/path/to
```

## Another example
```go

package main

import (
	"fmt"
	"syscall"
)

func main() {
	// Create new namespaces for the container
	err := syscall.Unshare(syscall.CLONE_NEWNS | syscall.CLONE_NEWPID | syscall.CLONE_NEWUTS | syscall.CLONE_NEWUSER | syscall.CLONE_NEWCGROUP)
	if err != nil {
		fmt.Println(err)
		return
	}

	// Create a new mount namespace
	err = syscall.Unshare(syscall.CLONE_NEWNS)
	if err != nil {
		fmt.Println(err)
		return
	}

	// Mount an empty directory as the root filesystem for the container
	err = syscall.Mount("/path/to/empty/directory", "/", "", syscall.MS_BIND, "")
	if err != nil {
		fmt.Println(err)
		return
	}

	// Change the root directory for the container
	err = syscall.PivotRoot("/path/to/empty/directory", "/oldroot")
	if err != nil {
		fmt.Println(err)
		return
	}

	// Change the current working directory to the new root directory
	err = syscall.Chdir("/")
	if err != nil {
		fmt.Println(err)
		return
	}

	// Unmount the old root filesystem
	err = syscall.Unmount("/oldroot", syscall.MNT_DETACH)
	if err != nil {

```
