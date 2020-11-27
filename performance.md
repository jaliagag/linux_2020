# Brendan Gregg

<https://www.youtube.com/watch?v=FJW8nGV4jxY>

## Observability Tools

watch activity. Safe, usually, depending on resource overhead.

### Basic

- uptime
- top or htop, atop: % CPU, command - on the CPU part of the top command, where it says sys, it's something the kernel is doing.
- ps -ef f --> tree thing
- vmstat --> procs, r --> cpus have tasks running, memory, cpu usage
- **iostat** - iostat -xmdz 1; read/second, write/s, %util - disk utilization
- mpstat -P ALL 1 : see CP balance
- free -m
- sar -n DEV 1 : checks network i/o

### Intermediate

- strace: system call tracer - CAREFUL WHEN USING IN PROD!!! - to figure out the system time. it slows things down. **strace -tp `pgrep <processname>` 2>&1 | head -100** - how many bytes is the process consuming.
- tcpdump: sniff network packets for psot analysis - trace of the packets; tcpdump -nr /tmp/out.tcpdump | head
- netstat : things happening at the tcp level.
- nicstat : similar to iostat
- pidstat : `-t 1` or `-d 1` per thread breakdown use time and system time for each process. User time is related to the app, system time is related to system calls, iostat for device uses.
- swapon
- lsof : too many file descriptor open - who is ocnnected to who, which application on which port is connected to what, where.
- sar, dstat 
- collectl

## Advanced Observability Tools

<https://www.youtube.com/watch?v=zrr2nUln9Kk>

## Benchmarking

load test. caution! production tests can cause issues due to contention

## Tuning

Change! Danger! changes could hurt performance, now or later with load

## Static

check configuration. should be safe
