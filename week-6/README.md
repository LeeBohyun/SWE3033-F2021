# Week 6

## Frequently asked questions
- RocksDB memory size: write_buffer_size (Number of bytes to buffer in memtable before compacting) default: 67108864 bytes
- DBBench # of concurrent threads : 1 default thread
- make static_lib

## Overview

This week you will install RocksDB and run DB_Bench on your own system.

Follow the guide below. If you have any questions, don't hesitate to contact me via email 

> NOTE: This lab is based on the Linux environment. If you don't have a Linux machine, use [VirturalBox](https://www.virtualbox.org/). (Recommend Ubuntu 18.04)

## Instructions

### 1. Install pre-requisites:

**Linux - Ubuntu**
- Upgrade gcc version at least 4.8
- gflags: `sudo apt-get install libgflags-dev`
  If this doesn't work, here's a nice tutorial:
  (http://askubuntu.com/questions/312173/installing-gflags-12-04)
- snappy: `sudo apt-get install libsnappy-dev`
- zlib: `sudo apt-get install zlib1g-dev`
- bzip2: `sudo apt-get install libbz2-dev`

**[Other platform](https://github.com/facebook/rocksdb/blob/master/INSTALL.md#supported-platforms)**

### 2. Build and install RocksDB

```bash
$ git clone https://github.com/facebook/rocksdb
$ cd rocksdb
$ make
$ make check
```

### 3. Run DB_Bench

```bash
$ ./db_bench
```

You can see options of `db_bench` using below command ([Details](https://github.com/facebook/rocksdb/wiki/Benchmarking-tools)):

```bash
$ ./db_bench --help
```

For the report, run the below command and measure the performance of RocksDB on your system:

> Update `-db="/path/to/datadir"` path according to your experimetal environment

```bash
$ ./db_bench --benchmarks="readrandomwriterandom" \
  -db="/path/to/datadir" \
  -use_direct_io_for_flush_and_compaction=true \
  -use_direct_reads=true \
  -duration=600 \
  -statistics \
  -stats_interval_seconds=10 2>&1 | tee result.txt
```

### 4. Record the experimental result

At the end of the benchmark, you can see the below result:

```bash
...
readrandomwriterandom :      53.084 micros/op 18838 ops/sec; ( reads:10172700 writes:1130299 total:1000000 found:4076910)
...
```

- `micros/op`: Microseconds spent processing one operation
- `ops/sec`: Processed operations per second

Show all of the above results in your report.

## Report Submission

1. Run DB_Bench to benchmark RocksDB on your system
2. Present the experimental results

Organize the results into a single report and submit it. Follow the [submission guide](../report-submission-guide.md) for your report.

## Reference
- [RocksDB GitHub](https://github.com/facebook/rocksdb) 
- [RocksDB Installation](https://github.com/facebook/rocksdb/blob/main/INSTALL.md)
- [RocksDB Benchmarking tools](https://github.com/facebook/rocksdb/wiki/Benchmarking-tools)
- [Mijin An, How to use db_bench](https://github.com/meeeejin/til/blob/master/rocksdb/how-to-use-db_bench.md)
