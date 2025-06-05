# duckdb-win-vs-wsl2
Performance comparison of native Windows vs. WSL2 Linux DuckDB Python package using TPC-H benchmark.

## Hardware and Software
* Dell Tower Plus, Intel Core Ultra 285K (24 cores, 8p/16e), 64GB RAM
* Windows Server 2025 Standard
* Ubuntu 24.04.2 inside WSL2 for Linux runs
* Python 3.13.4
* DuckDB release 1.3.0 Python package
* All firmware, operating systems and other software are up to date as of 6/5/2025

## Benchmark script
The [python_tpch.py](python_tpch.py) script simply runs all 22 TPC-H tests and sums up the cpu and real time,
and calculates how much of a speedup the multi-thread processing generates.
It expects a file named **tpch-sf100.db** in the **~/Downloads** directory.
This file can be downloaded at [https://blobs.duckdb.org/data/tpch-sf100.db](https://blobs.duckdb.org/data/tpch-sf100.db).

## Results
The script is run two times each on Windows and Linux to allow the OS to cache the data used completely in memory so disk speed is not a factor.
By running them back to back, any time spent allocating memory to WSL2 from Windows should also not be a factor.

| OS | CPU Time | Actual Time | Multi-thread Speedup |
|----|----------|-------------|------------|
| Windows | 352.7 | 49.6 | 7.1 |
| Linux | 389.6 | 18.2 | 21.4|

* The Linux version runs in about 37% of the time the Windows version needs.
* The Linux version actually uses more CPU time.
* The Windows version multi-thread speedup is about 1/3 of the Linux version.

I do not know why this is.
