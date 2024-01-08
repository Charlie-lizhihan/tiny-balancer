# tiny-balancer

TinyBalancer is a reverse proxy load balancer extended from the Go standard library's `net/http/httputil`. It is designed to be flexible, efficient, and easy to use, with support for both HTTP and HTTPS protocols.

## Features

- **Protocol Support:** Works with both HTTP and HTTPS.
- **Load Balancing Algorithms:** Supports a variety of load balancing algorithms, including:
  - [x] Round-Robin
  - [x] Random
  - [ ] Power of Two Random Choices
  - [ ] Consistent Hash
  - [ ] Consistent Hash with Bounded
  - [ ] IP Hash
  - [ ] Least Load
- **Health Checks and Fault Recovery:** Implements heartbeat checks for backend servers, enabling automatic recovery from failures.

## Getting Started

### Prerequisites

- Go (version 1.x or later)

### Installing

To start using TinyBalancer, install Go and run `go get`:

```bash
go get github.com/Charlie-lizhihan/tiny-balancer
