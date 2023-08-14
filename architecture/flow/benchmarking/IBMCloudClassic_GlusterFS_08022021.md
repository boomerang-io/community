# FIO report on self-managed ICP - WDC3

Storage is GlusterFS.

## Test results

### Test1: Read IOPS

- Random reads, 1 concurrent job, 4K block size

```ini
    [job1]
    bs=4K
    iodepth=64
    direct=1
    verify=0
    ioengine=libaio
    group_reporting=1
    time_based
    runtime=60
    ramp_time=2s
    name=read_iops
    rw=randread
    size=10G
```

#### Results:

- IOPS: <b>4829</b>
- BW: <b>18.9MiB/s</b>

```
fio-read-iops-fio-storage-benchmark-job-l9gnt
read_iops: (g=0): rw=randread, bs=(R) 4096B-4096B, (W) 4096B-4096B, (T) 4096B-4096B, ioengine=libaio, iodepth=64
fio-3.25
Starting 1 process
read_iops: Laying out IO file (1 file / 10240MiB)

read_iops: (groupid=0, jobs=1): err= 0: pid=8: Mon Feb  8 07:37:16 2021
  read: IOPS=4829, BW=18.9MiB/s (19.8MB/s)(1132MiB/60006msec)
    slat (usec): min=17, max=15691, avg=136.91, stdev=204.30
    clat (msec): min=3, max=303, avg=13.12, stdev=14.44
     lat (msec): min=3, max=303, avg=13.25, stdev=14.44
    clat percentiles (msec):
     |  1.00th=[    6],  5.00th=[    7], 10.00th=[    7], 20.00th=[    8],
     | 30.00th=[    9], 40.00th=[    9], 50.00th=[   10], 60.00th=[   10],
     | 70.00th=[   11], 80.00th=[   13], 90.00th=[   24], 95.00th=[   40],
     | 99.00th=[   74], 99.50th=[   87], 99.90th=[  174], 99.95th=[  186],
     | 99.99th=[  292]
   bw (  KiB/s): min= 6616, max=24864, per=100.00%, avg=19352.59, stdev=3315.07, samples=119
   iops        : min= 1654, max= 6216, avg=4838.07, stdev=828.77, samples=119
  lat (msec)   : 4=0.01%, 10=63.16%, 20=25.51%, 50=8.87%, 100=2.12%
  lat (msec)   : 250=0.33%, 500=0.02%
  cpu          : usr=2.78%, sys=7.82%, ctx=372930, majf=0, minf=58
  IO depths    : 1=0.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=100.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.1%, >=64=0.0%
     issued rwts: total=289793,0,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=64

Run status group 0 (all jobs):
   READ: bw=18.9MiB/s (19.8MB/s), 18.9MiB/s-18.9MiB/s (19.8MB/s-19.8MB/s), io=1132MiB (1187MB), run=60006-60006msec
```

### Test2: Read Throughput

- Sequential reads, 1MB block size, 8 concurrent jobs

```ini
    [job1]
    bs=1M
    iodepth=64
    direct=1
    verify=0
    ioengine=libaio
    group_reporting=1
    time_based
    runtime=60
    ramp_time=2s
    numjobs=8
    name=read_throughput
    rw=read
    size=10G
```

#### Results:

- IOPS: <b>398</b>
- BW: <b>407MiB/s</b>

```
fio-read-throughput-fio-storage-benchmark-job-4chcq
read_throughput: (g=0): rw=read, bs=(R) 1024KiB-1024KiB, (W) 1024KiB-1024KiB, (T) 1024KiB-1024KiB, ioengine=libaio, iodepth=64
...
fio-3.25
Starting 8 processes
read_throughput: Laying out IO file (1 file / 10240MiB)
job1: Laying out IO file (1 file / 10240MiB)
job1: Laying out IO file (1 file / 10240MiB)
job1: Laying out IO file (1 file / 10240MiB)
job1: Laying out IO file (1 file / 10240MiB)
job1: Laying out IO file (1 file / 10240MiB)
job1: Laying out IO file (1 file / 10240MiB)
job1: Laying out IO file (1 file / 10240MiB)

read_throughput: (groupid=0, jobs=8): err= 0: pid=8: Mon Feb  8 08:27:53 2021
  read: IOPS=398, BW=407MiB/s (427MB/s)(23.9GiB/60034msec)
    slat (usec): min=875, max=265188, avg=20029.14, stdev=14811.37
    clat (msec): min=17, max=1674, avg=1250.54, stdev=140.62
     lat (msec): min=32, max=1690, avg=1270.58, stdev=141.05
    clat percentiles (msec):
     |  1.00th=[  634],  5.00th=[ 1099], 10.00th=[ 1133], 20.00th=[ 1183],
     | 30.00th=[ 1200], 40.00th=[ 1217], 50.00th=[ 1250], 60.00th=[ 1267],
     | 70.00th=[ 1301], 80.00th=[ 1334], 90.00th=[ 1401], 95.00th=[ 1452],
     | 99.00th=[ 1536], 99.50th=[ 1569], 99.90th=[ 1620], 99.95th=[ 1636],
     | 99.99th=[ 1670]
   bw (  KiB/s): min=223232, max=522367, per=98.06%, avg=409028.77, stdev=6273.96, samples=953
   iops        : min=  218, max=  510, avg=399.29, stdev= 6.13, samples=953
  lat (msec)   : 20=0.02%, 50=0.05%, 100=0.03%, 250=0.27%, 500=0.40%
  lat (msec)   : 750=0.46%, 1000=0.47%, 2000=100.41%
  cpu          : usr=0.07%, sys=0.91%, ctx=221070, majf=0, minf=474
  IO depths    : 1=0.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=100.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.1%, >=64=0.0%
     issued rwts: total=23943,0,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=64

Run status group 0 (all jobs):
   READ: bw=407MiB/s (427MB/s), 407MiB/s-407MiB/s (427MB/s-427MB/s), io=23.9GiB (25.6GB), run=60034-60034msec
```

### Test3: Write IOPS

- Random writes, 4K block size, 1 concurrent job

```ini
    [job1]
    bs=4K
    iodepth=64
    direct=1
    verify=0
    ioengine=libaio
    group_reporting=1
    time_based
    runtime=60
    ramp_time=2s
    name=write_iops
    rw=randwrite
    size=10G
```

#### Results:

- IOPS: <b>276</b>
- BW: <b>1112KiB</b>

```
fio-write-iops-fio-storage-benchmark-job-gj44b
write_iops: (g=0): rw=randwrite, bs=(R) 4096B-4096B, (W) 4096B-4096B, (T) 4096B-4096B, ioengine=libaio, iodepth=64
fio-3.25
Starting 1 process
write_iops: Laying out IO file (1 file / 10240MiB)

write_iops: (groupid=0, jobs=1): err= 0: pid=8: Mon Feb  8 08:37:02 2021
  write: IOPS=276, BW=1112KiB/s (1139kB/s)(65.4MiB/60256msec); 0 zone resets
    slat (usec): min=22, max=5986, avg=105.58, stdev=151.99
    clat (msec): min=148, max=448, avg=230.60, stdev=35.06
     lat (msec): min=148, max=448, avg=230.71, stdev=35.06
    clat percentiles (msec):
     |  1.00th=[  176],  5.00th=[  188], 10.00th=[  194], 20.00th=[  203],
     | 30.00th=[  209], 40.00th=[  215], 50.00th=[  224], 60.00th=[  234],
     | 70.00th=[  245], 80.00th=[  255], 90.00th=[  275], 95.00th=[  296],
     | 99.00th=[  342], 99.50th=[  351], 99.90th=[  409], 99.95th=[  426],
     | 99.99th=[  447]
   bw (  KiB/s): min=  792, max= 1440, per=99.99%, avg=1112.84, stdev=135.05, samples=120
   iops        : min=  198, max=  360, avg=278.16, stdev=33.72, samples=120
  lat (msec)   : 250=75.63%, 500=24.75%
  cpu          : usr=0.35%, sys=0.96%, ctx=35025, majf=0, minf=58
  IO depths    : 1=0.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=100.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.1%, >=64=0.0%
     issued rwts: total=0,16690,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=64

Run status group 0 (all jobs):
  WRITE: bw=1112KiB/s (1139kB/s), 1112KiB/s-1112KiB/s (1139kB/s-1139kB/s), io=65.4MiB (68.6MB), run=60256-60256msec
```

#### Test4: Write throughput

- Sequential writes, 1MB block size, 8 concurrent jobs

```ini
  fio.job: |-
    [job1]
    bs=1M
    iodepth=64
    direct=1
    verify=0
    ioengine=libaio
    group_reporting=1
    time_based
    runtime=60
    ramp_time=2s
    numjobs=8
    name=write_throughput
    rw=write
    size=10G
```

#### Results:

- IOPS: <b>68</b>
- BW: <b>70MiB/s</b>

```
fio-write-throughput-fio-storage-benchmark-job-j6f8x
write_throughput: (g=0): rw=write, bs=(R) 1024KiB-1024KiB, (W) 1024KiB-1024KiB, (T) 1024KiB-1024KiB, ioengine=libaio, iodepth=64
...
fio-3.25
Starting 8 processes
write_throughput: Laying out IO file (1 file / 10240MiB)
job1: Laying out IO file (1 file / 10240MiB)
job1: Laying out IO file (1 file / 10240MiB)
job1: Laying out IO file (1 file / 10240MiB)
job1: Laying out IO file (1 file / 10240MiB)
job1: Laying out IO file (1 file / 10240MiB)
job1: Laying out IO file (1 file / 10240MiB)
job1: Laying out IO file (1 file / 10240MiB)

write_throughput: (groupid=0, jobs=8): err= 0: pid=8: Mon Feb  8 08:41:38 2021
  write: IOPS=68, BW=70.0MiB/s (74.4MB/s)(4277MiB/60248msec); 0 zone resets
    slat (msec): min=28, max=442, avg=116.41, stdev=32.11
    clat (msec): min=113, max=8371, avg=6930.96, stdev=1358.92
     lat (msec): min=227, max=8498, avg=7047.08, stdev=1356.74
    clat percentiles (msec):
     |  1.00th=[  701],  5.00th=[ 3440], 10.00th=[ 6611], 20.00th=[ 6879],
     | 30.00th=[ 7013], 40.00th=[ 7080], 50.00th=[ 7148], 60.00th=[ 7282],
     | 70.00th=[ 7483], 80.00th=[ 7684], 90.00th=[ 7886], 95.00th=[ 8020],
     | 99.00th=[ 8154], 99.50th=[ 8221], 99.90th=[ 8356], 99.95th=[ 8356],
     | 99.99th=[ 8356]
   bw (  KiB/s): min=26619, max=94252, per=95.93%, avg=69734.71, stdev=1486.86, samples=886
   iops        : min=   25, max=   92, avg=67.75, stdev= 1.48, samples=886
  lat (msec)   : 250=0.24%, 500=0.53%, 750=0.32%, 1000=0.39%, 2000=1.50%
  lat (msec)   : >=2000=100.70%
  cpu          : usr=0.12%, sys=0.16%, ctx=36753, majf=0, minf=475
  IO depths    : 1=0.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=2.3%, 32=6.2%, >=64=91.5%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=99.8%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.2%, >=64=0.0%
     issued rwts: total=0,4125,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=64

Run status group 0 (all jobs):
  WRITE: bw=70.0MiB/s (74.4MB/s), 70.0MiB/s-70.0MiB/s (74.4MB/s-74.4MB/s), io=4277MiB (4485MB), run=60248-60248msec
```