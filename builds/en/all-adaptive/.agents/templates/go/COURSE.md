<!-- Example for Go: copy this file and replace the topics with your own. -->

# Course: Go — from basics to an HTTP service

## Learning goal

Write idiomatic Go: command-line utilities and a small HTTP service with tests, enough to pass an interview for a junior Go developer.

## Student context

- Current level: confident in Python, has not written Go
- Why learning: interview
- Time and pace: 4–5 hours per week
- Format: practice in this project, theory along the way
- Practice: self-study

## What you will be able to do

- write code in Go idioms: errors as values, interfaces, packages
- work with goroutines and channels without data races
- cover code with table-driven tests and run `go test -race`
- stand up an HTTP service with a JSON API

## Out of scope

- gRPC, Kubernetes, infrastructure and deployment

## When a topic counts as done

- the assignment works, `go test ./...` passes
- the student has explained the solution in their own words

## Program

### Module 1. Language basics

1. Variables, types, constants
2. Conditionals, loops, switch
3. Functions and multiple return values
4. Errors as values

### Module 2. Data and structures

5. Arrays, slices, maps
6. Structs and methods
7. Pointers and receivers

### Module 3. Code organization

8. Interfaces
9. Packages and modules (`go mod`)
10. Standard library: `fmt`, `strings`, `errors`, `time`

### Module 4. Concurrency

11. Goroutines
12. Channels and select
13. `sync`, `context`, cancellation

### Module 5. Tests and tooling

14. `go test` and table-driven tests
15. Benchmarks, `go vet`, `golangci-lint`

### Module 6. Practice: an HTTP service

16. `net/http`: routing and handlers
17. JSON and API errors
18. Testing HTTP handlers

## Materials

- A Tour of Go — https://go.dev/tour/
- Effective Go — https://go.dev/doc/effective_go
- Go roadmap — https://roadmap.sh/golang

---

Updated: 2026-10-10 (example; check the current Go and library versions before use)
