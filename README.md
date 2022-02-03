# parallelSort vs. sort

A micro-benchmark to compare the throughput of two sorting methods provided by the ``java.util.Arrays`` class, 
``parallelSort`` and ``sort``. The benchmark generates an array of _n_ random numbers. The 
resulting unsorted array is then sorted by each method.

Built with [Maven](https://maven.apache.org/) and [JMH](https://openjdk.java.net/projects/code-tools/jmh/).

## Executing the Benchmark

_Tested with: Maven 3.8.4 and Amazon Corretto JDK 17_

* Step 1: ``$ git clone git://github.com/rharri/streams-benchmark.git``
* Step 2: ``$ cd array-sort-bench``
* Step 3: ``$ mvn clean verify``
* Step 4: ``$ java -jar target/benchmarks.jar``

## Test Machine

|                         | Machine                                                                                |
|-------------------------|----------------------------------------------------------------------------------------|
| **Operating System**    | Ubuntu 20.04.3 LTS</br>                                                                |
| **CPU**                 | 3.7GHz 6-Core AMD Ryzen 5 5600X                                                        |
| **RAM**                 | 32 GB 3200 MHz DDR4                                                                    |
| **JVM**                 | OpenJDK 64-Bit Server VM Corretto-17.0.2.8.1 (build 17.0.2+8-LTS, mixed mode, sharing) |

## Results

The `size` represents the number of random numbers generated, and thus number of elements to be sorted by each
method. In this case: 1 Hundred, 1 Thousand, 4 Thousand, 10 Thousand, 100 Thousand, 1 Million, and 10 Million.

| Benchmark        | (size)   | Mode  | Cnt |   Score |   Error | Units |
|------------------|----------| ------|-----|-------|---------|-------|
| testParallelSort | 100      | thrpt  | 8   | 2065213.082 | ± 597319.145 | ops/s |
| testParallelSort | 1000     | thrpt  | 8   | 135466.730 | ± 6844.356 | ops/s |
| testParallelSort | 4000     | thrpt  | 8   | 17151.777 | ± 1572.506 | ops/s |
| testParallelSort | 10000    | thrpt  | 8   | 7061.721 | ± 2213.384 | ops/s |
| testParallelSort | 100000   | thrpt  | 8   | 1371.719 | ± 18.590 | ops/s |
| testParallelSort | 1000000  | thrpt  | 8   | 159.374 | ± 15.976 | ops/s |
| testParallelSort | 10000000 | thrpt  | 8   | 14.856 | ± 0.066 | ops/s |
| testSort         | 100      | thrpt  | 8   | 1941952.830 | ± 392573.519 | ops/s |
| testSort         | 1000     | thrpt  | 8   | 128412.026 | ± 4753.738 | ops/s |
| testSort         | 4000     | thrpt  | 8   | 17166.564 | ± 2639.573 | ops/s |
| testSort         | 10000    | thrpt  | 8   | 3936.256 | ± 7.219 | ops/s |
| testSort         | 100000   | thrpt  | 8   | 288.131 | ± 3.097 | ops/s |
| testSort         | 1000000  | thrpt  | 8   | 24.575 | ± 0.336 | ops/s |
| testSort         | 10000000 | thrpt  | 8   | 2.036 | ± 0.166 | ops/s |

_thrpt = Throughput_, _ops/s = Operations per second_

### A helpful reminder from JMH...
The numbers above are just data. To gain reusable insights, you need to follow up on
why the numbers are the way they are. Use profilers (see -prof, -lprof), design factorial
experiments, perform baseline and negative tests that provide experimental control, make sure
the benchmarking environment is safe on JVM/OS/HW level, ask for reviews from the domain experts.
Do not assume the numbers tell you what you want them to tell.