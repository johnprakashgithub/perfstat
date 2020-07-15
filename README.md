# bottler
Analyze and show tips about possible bottlenecks in Linux systems regarding to diskio, networking, cpu, swapping, memory etc

https://blog.appsignal.com/2018/03/06/understanding-cpu-statistics.html
https://www.cyberciti.biz/tips/linux-resource-utilization-to-detect-system-bottlenecks.html
http://web.archive.org/web/20101028025942/https://anchor.com.au/hosting/development/HuntingThePerformanceWumpus
https://www.tecmint.com/command-line-tools-to-monitor-linux-performance/

## Brainstorm

## Existing tools

* CPU stats by CPU (%idle %wait etc): mpstat -P ALL 2 5
* RAM stats (free, cache, buffer, swap): vmstat -S M 2
* Disk stats by block device (wr/s rd/s etc): iostat -dx 1
* Network bandwidth by host: iftop
* Open files by process: lsof
* CPU usage by process: top
* Disk usage by process: iotop
* Network bandwidth by process: nethogs OR iftop with netstat -tup OR dstat --net --top-io-adv

## Awareness

### Bottlenecks

* Low idle CPU (overall)
  * top cpu eater processes
* Low idle CPU (single CPU)
  * top cpu eater processes
* High CPU wait (waiting for IO)
  * top io waiter processes
  * top "waited" disks
* Low available network bandwidth (when max bandwidth is set by the user)
  * top network eater processes
* High number of processes waiting for CPU
* Disk nr of block read/writes seems to be in a ceil limit (hist inference)
* Disk bandwidth of read/writes seems to be in a ceil limit (hist inference)
* Network interface bandwidth seems to be in a ceil limit (hist inference)

### Risks

* Low RAM
  * top ram eater processes
* Low Disk
  * mapped device with lowest space
* Low available files to be open (ulimit)
  * top files open eater processes
* RAM memory growing linearly for process - there maybe a memory leak
  * process with growing memory

### Harm

* High swap IO - few RAM, may slow system by using too much disk
* High %util in disk - disk is being hammered and may not handle well spikes when needed

### Top 5 (tips)

* Processes with high cpu wait
* Processes with high cpu usage
* Processes with high disk io
* Processes with high nr of open files
* Processes with high network usage
* Destination hosts with high network bandwidth
* Block devices with high reads/writes

