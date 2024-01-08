# tiny-balancer

TinyBalancer is a reverse proxy load balancer extended from the Go standard library's `net/http/httputil`. It is designed to be flexible, efficient, and easy to use, with support for both HTTP and HTTPS protocols.

## Features

- **Protocol Support:** Works with both HTTP and HTTPS.
- **Load Balancing Algorithms:** Supports a variety of load balancing algorithms, including:
  - [x] Round-Robin
  - [x] Random
  - [x] Power of Two Random Choices
  - [x] Consistent Hash
  - [x] Consistent Hash with Bounded
  - [x] IP Hash
  - [x] Least Load
- **Health Checks and Fault Recovery:** Implements heartbeat checks for backend servers, enabling automatic recovery from failures.

## Getting Started

### Prerequisites

- Go (version 1.x or later)

### Installing

To start using TinyBalancer, install Go and run `go get`:

```bash
go get github.com/Charlie-lizhihan/tiny-balancer
```

### Usage
Here's a quick example of how to set up and test a load balancer:
```go
package main

import (
	"fmt"
	"log"

	"github.com/Charlie-lizhihan/tiny-balancer/balancer"
)

func main() {
	hosts := []string{
		"http://192.168.11.101",
		"http://192.168.11.102",
		"http://192.168.11.103",
		"http://192.168.11.104",
	}

	//  the balancer support
	// 	IPHashBalancer         = "ip-hash"
	// 	ConsistentHashBalancer = "consistent-hash"
	// 	P2CBalancer            = "p2c"
	// 	RandomBalancer         = "random"
	// 	R2Balancer             = "round-robin"
	// 	LeastLoadBalancer      = "least-load"
	// 	BoundedBalancer        = "bounded"
	lb, err := balancer.Build(balancer.R2Balancer, hosts)
	if err != nil {
		log.Fatal("Error building balancer:", err)
	}

	clientAddr := "172.160.1.5" // Example client IP

	for i := 0; i <= 5; i++ {
		targetHost, err := lb.Balance(clientAddr)
		if err != nil {
			log.Fatal("Error balancing:", err)
		}

		// Simulate routing the request to 'targetHost'
		fmt.Printf("Routing request from %s to %s\n", clientAddr, targetHost)
		lb.Inc(targetHost)
		defer lb.Done(targetHost)
	}

}
```
