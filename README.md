# Go Concurrency Bug: Race Condition and Unexpected Channel Closure

This repository demonstrates a common concurrency bug in Go involving a race condition and unexpected channel closure.  The code attempts to process numbers concurrently using goroutines and channels but faces issues due to incorrect synchronization and channel handling.

## Bug Description

The original code uses a `sync.WaitGroup` to synchronize the completion of goroutines. However, it does not correctly manage the channel closure, potentially leading to unexpected behavior and race conditions.  The `wg.Wait()` call should occur *before* closing the channel to ensure all goroutines have written to the channel before the range loop exits.

## Bug Solution

The solution code provides a corrected version that fixes the channel closure and race condition by ensuring `wg.Wait()` is called before `close(ch)`, guaranteeing all goroutines complete before the channel is closed. This avoids potential panics or unpredictable output.

## How to Run

1. Clone the repository.
2. Navigate to the repository directory.
3. Run `go run bug.go` to execute the buggy code and `go run bugSolution.go` to run the corrected code.
