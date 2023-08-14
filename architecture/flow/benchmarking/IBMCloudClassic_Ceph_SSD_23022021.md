# FIO report on self-managed OCP4 Running in IBM Cloud (Classic Infra)

Storage is RedHat Openshift Container Storage (CEPH) on 3 nodes with backing `400GB Locally attached SSD disks`

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

- IOPS: <b>15800</b>
- BW: <b>61.8MiB/s</b>

```
fio-read-iops-fio-storage-benchmark-job-fgb79
read_iops: (g=0): rw=randread, bs=(R) 4096B-4096B, (W) 4096B-4096B, (T) 4096B-4096B, ioengine=libaio, iodepth=64
fio-3.25
Starting 1 process
read_iops: Laying out IO file (1 file / 10240MiB)

read_iops: (groupid=0, jobs=1): err= 0: pid=9: Tue Feb 23 08:12:34 2021
  read: IOPS=15.8k, BW=61.8MiB/s (64.8MB/s)(3707MiB/60006msec)
    slat (usec): min=5, max=2167, avg=13.69, stdev=26.44
    clat (usec): min=650, max=56451, avg=4027.97, stdev=3424.22
     lat (usec): min=660, max=56459, avg=4042.88, stdev=3423.66
    clat percentiles (usec):
     |  1.00th=[ 1012],  5.00th=[ 1336], 10.00th=[ 1565], 20.00th=[ 1926],
     | 30.00th=[ 2245], 40.00th=[ 2573], 50.00th=[ 2966], 60.00th=[ 3458],
     | 70.00th=[ 4146], 80.00th=[ 5276], 90.00th=[ 7635], 95.00th=[10421],
     | 99.00th=[18744], 99.50th=[21890], 99.90th=[30540], 99.95th=[34866],
     | 99.99th=[42206]
   bw (  KiB/s): min=50696, max=75599, per=100.00%, avg=63285.60, stdev=5211.97, samples=120
   iops        : min=12674, max=18899, avg=15821.26, stdev=1302.99, samples=120
  lat (usec)   : 750=0.01%, 1000=0.88%
  lat (msec)   : 2=21.55%, 4=45.88%, 10=26.20%, 20=4.73%, 50=0.76%
  lat (msec)   : 100=0.01%
  cpu          : usr=6.88%, sys=22.23%, ctx=150159, majf=0, minf=58
  IO depths    : 1=0.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=100.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.1%, >=64=0.0%
     issued rwts: total=948817,0,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=64

Run status group 0 (all jobs):
   READ: bw=61.8MiB/s (64.8MB/s), 61.8MiB/s-61.8MiB/s (64.8MB/s-64.8MB/s), io=3707MiB (3887MB), run=60006-60006msec
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

- IOPS: <b>206</b>
- BW: <b>214MiB/s</b>

```
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

read_throughput: (groupid=0, jobs=8): err= 0: pid=9: Tue Feb 23 08:05:01 2021
  read: IOPS=206, BW=214MiB/s (224MB/s)(13.7GiB/65810msec)
    slat (usec): min=9, max=10911, avg=92.82, stdev=260.84
    clat (msec): min=10, max=12402, avg=2420.90, stdev=2832.36
     lat (msec): min=10, max=12402, avg=2421.01, stdev=2832.36
    clat percentiles (msec):
     |  1.00th=[   13],  5.00th=[   18], 10.00th=[   26], 20.00th=[   45],
     | 30.00th=[   78], 40.00th=[  165], 50.00th=[ 1116], 60.00th=[ 1821],
     | 70.00th=[ 4212], 80.00th=[ 6141], 90.00th=[ 6477], 95.00th=[ 6678],
     | 99.00th=[10268], 99.50th=[11208], 99.90th=[12013], 99.95th=[12147],
     | 99.99th=[12281]
   bw (  KiB/s): min=16374, max=857182, per=100.00%, avg=260730.10, stdev=21157.88, samples=854
   iops        : min=   14, max=  836, avg=253.78, stdev=20.66, samples=854
  lat (msec)   : 20=7.09%, 50=16.25%, 100=12.12%, 250=9.35%, 500=2.52%
  lat (msec)   : 750=1.22%, 1000=2.62%, 2000=11.83%, >=2000=40.71%
  cpu          : usr=0.03%, sys=0.23%, ctx=14163, majf=0, minf=466
  IO depths    : 1=0.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=100.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=99.9%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.1%, >=64=0.0%
     issued rwts: total=13568,0,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=64

Run status group 0 (all jobs):
   READ: bw=214MiB/s (224MB/s), 214MiB/s-214MiB/s (224MB/s-224MB/s), io=13.7GiB (14.8GB), run=65810-65810msec
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

- IOPS: <b>3547</b>
- BW: <b>13.9MiB</b>

```
fio-write-iops-fio-storage-benchmark-job-c8jzk
write_iops: (g=0): rw=randwrite, bs=(R) 4096B-4096B, (W) 4096B-4096B, (T) 4096B-4096B, ioengine=libaio, iodepth=64
fio-3.25
Starting 1 process
write_iops: Laying out IO file (1 file / 10240MiB)

write_iops: (groupid=0, jobs=1): err= 0: pid=9: Tue Feb 23 08:18:55 2021
  write: IOPS=3547, BW=13.9MiB/s (14.5MB/s)(832MiB/60011msec); 0 zone resets
    slat (usec): min=6, max=3356, avg=14.63, stdev=17.50
    clat (msec): min=2, max=167, avg=18.03, stdev=15.88
     lat (msec): min=2, max=167, avg=18.04, stdev=15.88
    clat percentiles (msec):
     |  1.00th=[    5],  5.00th=[    6], 10.00th=[    7], 20.00th=[    8],
     | 30.00th=[    9], 40.00th=[   11], 50.00th=[   12], 60.00th=[   14],
     | 70.00th=[   17], 80.00th=[   25], 90.00th=[   46], 95.00th=[   57],
     | 99.00th=[   69], 99.50th=[   73], 99.90th=[   85], 99.95th=[   96],
     | 99.99th=[  161]
   bw (  KiB/s): min= 8248, max=17691, per=100.00%, avg=14194.82, stdev=1511.86, samples=120
   iops        : min= 2062, max= 4422, avg=3548.62, stdev=377.95, samples=120
  lat (msec)   : 4=0.39%, 10=39.70%, 20=35.16%, 50=16.73%, 100=8.00%
  lat (msec)   : 250=0.05%
  cpu          : usr=1.81%, sys=5.77%, ctx=51915, majf=0, minf=58
  IO depths    : 1=0.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=100.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.1%, >=64=0.0%
     issued rwts: total=0,212868,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=64

Run status group 0 (all jobs):
  WRITE: bw=13.9MiB/s (14.5MB/s), 13.9MiB/s-13.9MiB/s (14.5MB/s-14.5MB/s), io=832MiB (872MB), run=60011-60011msec
```

### Test4: Write throughput

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

- IOPS: <b>102</b>
- BW: <b>110MiB/s</b>

```
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

write_throughput: (groupid=0, jobs=8): err= 0: pid=9: Tue Feb 23 08:25:32 2021
  write: IOPS=102, BW=110MiB/s (115MB/s)(7256MiB/65899msec); 0 zone resets
    slat (usec): min=50, max=316579, avg=326.44, stdev=5311.57
    clat (msec): min=42, max=17423, avg=4731.96, stdev=4951.46
     lat (msec): min=42, max=17423, avg=4732.34, stdev=4951.45
    clat percentiles (msec):
     |  1.00th=[   62],  5.00th=[   82], 10.00th=[  101], 20.00th=[  155],
     | 30.00th=[  236], 40.00th=[  768], 50.00th=[ 2735], 60.00th=[ 3910],
     | 70.00th=[ 8658], 80.00th=[10805], 90.00th=[11879], 95.00th=[12818],
     | 99.00th=[15100], 99.50th=[16040], 99.90th=[17113], 99.95th=[17113],
     | 99.99th=[17113]
   bw (  KiB/s): min=16364, max=411754, per=100.00%, avg=144444.01, stdev=11287.18, samples=770
   iops        : min=   12, max=  402, avg=139.96, stdev=11.03, samples=770
  lat (msec)   : 50=0.28%, 100=10.22%, 250=22.81%, 500=7.97%, 750=1.69%
  lat (msec)   : 1000=1.39%, 2000=3.64%, >=2000=59.46%
  cpu          : usr=0.12%, sys=0.12%, ctx=7012, majf=0, minf=466
  IO depths    : 1=0.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=100.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=99.9%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.1%, >=64=0.0%
     issued rwts: total=0,6752,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=64

Run status group 0 (all jobs):
  WRITE: bw=110MiB/s (115MB/s), 110MiB/s-110MiB/s (115MB/s-115MB/s), io=7256MiB (7608MB), run=65899-65899msec
```