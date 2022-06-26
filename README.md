[![GoDoc](https://godoc.org/facette.io/natsort?status.svg)](https://godoc.org/facette.io/natsort)


# natsort: natural strings sorting in Go

This is NOT an implementation of the "Alphanum Algorithm" by [Dave Koelle][0] in Go, but something slightly better.

## Benchmark

This was modified to use something else than chunks and Dave Koelle's algorithm. Not only the previous version used regular expressions to detect numbers, but it would also allocate extra memory to store the parsed values and was not optimized at all. This version is more optimized.

### Before

```
goos: linux
goarch: amd64
pkg: github.com/MagicalTux/natsort
cpu: Intel(R) Core(TM) i7-8700K CPU @ 3.70GHz
BenchmarkSort1-12    	    6136	    300245 ns/op
PASS
```

### After

```
goos: linux
goarch: amd64
pkg: github.com/MagicalTux/natsort
cpu: Intel(R) Core(TM) i7-8700K CPU @ 3.70GHz
BenchmarkSort1-12    	  606818	      2013 ns/op
PASS
```

## Usage

```go
package main

import (
    "fmt"
    "strings"

    "facette.io/natsort"
)

func main() {
    list := []string{
        "1000X Radonius Maximus",
        "10X Radonius",
        "200X Radonius",
        "20X Radonius",
        "20X Radonius Prime",
        "30X Radonius",
        "40X Radonius",
        "Allegia 50 Clasteron",
        "Allegia 500 Clasteron",
        "Allegia 50B Clasteron",
        "Allegia 51 Clasteron",
        "Allegia 6R Clasteron",
        "Alpha 100",
        "Alpha 2",
        "Alpha 200",
        "Alpha 2A",
        "Alpha 2A-8000",
        "Alpha 2A-900",
        "Callisto Morphamax",
        "Callisto Morphamax 500",
        "Callisto Morphamax 5000",
        "Callisto Morphamax 600",
        "Callisto Morphamax 6000 SE",
        "Callisto Morphamax 6000 SE2",
        "Callisto Morphamax 700",
        "Callisto Morphamax 7000",
        "Xiph Xlater 10000",
        "Xiph Xlater 2000",
        "Xiph Xlater 300",
        "Xiph Xlater 40",
        "Xiph Xlater 5",
        "Xiph Xlater 50",
        "Xiph Xlater 500",
        "Xiph Xlater 5000",
        "Xiph Xlater 58",
    }

    natsort.Sort(list)

    fmt.Println(strings.Join(list, "\n"))
}
```

Output:

```
10X Radonius
20X Radonius
20X Radonius Prime
30X Radonius
40X Radonius
200X Radonius
1000X Radonius Maximus
Allegia 6R Clasteron
Allegia 50 Clasteron
Allegia 50B Clasteron
Allegia 51 Clasteron
Allegia 500 Clasteron
Alpha 2
Alpha 2A
Alpha 2A-900
Alpha 2A-8000
Alpha 100
Alpha 200
Callisto Morphamax
Callisto Morphamax 500
Callisto Morphamax 600
Callisto Morphamax 700
Callisto Morphamax 5000
Callisto Morphamax 6000 SE
Callisto Morphamax 6000 SE2
Callisto Morphamax 7000
Xiph Xlater 5
Xiph Xlater 40
Xiph Xlater 50
Xiph Xlater 58
Xiph Xlater 300
Xiph Xlater 500
Xiph Xlater 2000
Xiph Xlater 5000
Xiph Xlater 10000
```

[0]: http://davekoelle.com/alphanum.html
