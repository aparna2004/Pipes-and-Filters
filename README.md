# Pipe-Filter Architecture Pattern Example in Go

This repository contains a simple Go program that demonstrates the Pipe-Filter Architecture Pattern. The program processes a sequence of integers by passing them through a series of filters: one to square the integers and another to double them.

## Overview

The Pipe-Filter Architecture Pattern structures a system around a series of processing elements called filters that are connected by pipes. Each filter processes data and passes it to the next filter via a pipe.

### Advantages
- **Reusability**: Filters can be reused in different pipelines or applications.
- **Scalability**: Additional filters can be added to extend the functionality of the pipeline.
- **Parallelism**: Filters can be executed in parallel if they are stateless, thus improving performance.

### Disadvantages
- **Debugging Difficulty**: Identifying and debugging issues are difficult in long pipelines.
- **Data Format Constraints**: Filters must agree on the data format, requiring careful design and standardization.
- **Latency**: Data must be passed through multiple filters, which can introduce latency.

### Use Cases
- Data Processing Pipelines like Extract, Transform, Load (ETL) processes in data warehousing.
- Compilers.
- Stream-Processing like Apache Flink.
- Image and Signal Processing.

## Getting Started

### Prerequisites

- Go (version 1.16 or later)

### Running Online
```
https://go.dev/play/
```

### Installation

1. Clone the repository:
    ```sh
    git clone https://github.com/yourusername/pipe-filter-example.git
    ```

2. Change to the project directory:
    ```sh
    cd pipe-filter-example
    ```

3. Build the project:
    ```sh
    go build
    ```

### Running the Program

To run the program, use the following command:
```sh
./pipe-filter-example
```

### Example Output

The program processes a sequence of integers and prints the result. For example:
```
[2 8 18 32 50]
```

## Code Explanation

### 1. Filter Type

We define a `Filter` type as a function that takes an `int` and returns an `int`.

```go
// Define a type for the filter function
type Filter func(int) int
```

### 2. Pipeline Function

The `Pipeline` function takes a slice of integers and a variable number of filters. It processes each integer through all the filters in sequence and returns the resulting slice.

```go
// Pipeline function that connects filters
func Pipeline(numbers []int, filters ...Filter) []int {
    for _, filter := range filters {
        for i, number := range numbers {
            numbers[i] = filter(number)
        }
    }
    return numbers
}
```

### 3. Filters

We define two filters, `Square` and `Double`, to square and double the integers, respectively.

```go
// Square filter
func Square(n int) int {
    return n * n
}

// Double filter
func Double(n int) int {
    return n * 2
}
```

### 4. Main Function

In the `main` function, we create a sample slice of integers, process it through the pipeline with the `Square` and `Double` filters, and print the result.

```go
func main() {
    // Sample data
    numbers := []int{1, 2, 3, 4, 5}

    // Process the numbers through the pipeline
    result := Pipeline(numbers, Square, Double)

    // Print the result
    fmt.Println(result)
}
```
