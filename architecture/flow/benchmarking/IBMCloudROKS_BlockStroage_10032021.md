# FIO report - ROKS managed OCP Cluster on VPCv2 - OCP001

Name in IBM Cloud: <b>ess-roks-vpc-wdc-001</b>

Storage is Platform provided Storage Class `ibmc-vpc-block-10iops-tier`

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

- IOPS: <b>2993</b>
- BW: <b>11.7MiB/s</b>

```
fio-read-iops-fio-storage-benchmark-job-rngsp
read_iops: (g=0): rw=randread, bs=(R) 4096B-4096B, (W) 4096B-4096B, (T) 4096B-4096B, ioengine=libaio, iodepth=64
fio-3.25
Starting 1 process
read_iops: Laying out IO file (1 file / 10240MiB)

read_iops: (groupid=0, jobs=1): err= 0: pid=9: Wed Mar 10 14:55:22 2021
  read: IOPS=2993, BW=11.7MiB/s (12.3MB/s)(702MiB/60021msec)
    slat (usec): min=2, max=12057, avg=10.21, stdev=74.60
    clat (usec): min=493, max=42505, avg=21362.02, stdev=2576.65
     lat (usec): min=497, max=42520, avg=21372.44, stdev=2575.23
    clat percentiles (usec):
     |  1.00th=[11731],  5.00th=[17957], 10.00th=[20317], 20.00th=[20841],
     | 30.00th=[21103], 40.00th=[21365], 50.00th=[21365], 60.00th=[21365],
     | 70.00th=[21627], 80.00th=[21890], 90.00th=[22152], 95.00th=[24773],
     | 99.00th=[31327], 99.50th=[32375], 99.90th=[36439], 99.95th=[37487],
     | 99.99th=[40109]
   bw (  KiB/s): min=11728, max=12240, per=100.00%, avg=11986.00, stdev=57.51, samples=119
   iops        : min= 2932, max= 3060, avg=2996.44, stdev=14.40, samples=119
  lat (usec)   : 500=0.01%, 750=0.01%
  lat (msec)   : 2=0.01%, 4=0.01%, 10=0.29%, 20=7.17%, 50=92.55%
  cpu          : usr=1.46%, sys=4.71%, ctx=60278, majf=0, minf=63
  IO depths    : 1=0.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=100.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.1%, >=64=0.0%
     issued rwts: total=179690,0,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=64

Run status group 0 (all jobs):
   READ: bw=11.7MiB/s (12.3MB/s), 11.7MiB/s-11.7MiB/s (12.3MB/s-12.3MB/s), io=702MiB (736MB), run=60021-60021msec

Disk stats (read/write):
  vdd: ios=188044/1422, merge=0/17, ticks=3938946/29817, in_queue=3968763, util=99.75%
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

- IOPS: <b>45</b>
- BW: <b>49.2MiB/s</b>

```
read_throughput: (groupid=0, jobs=8): err= 0: pid=10: Wed Mar 10 15:38:25 2021
  read: IOPS=45, BW=49.2MiB/s (51.6MB/s)(3042MiB/61821msec)
    slat (usec): min=57, max=882092, avg=171270.90, stdev=170186.42
    clat (msec): min=1225, max=15178, avg=9935.43, stdev=2354.47
     lat (msec): min=1407, max=15444, avg=10099.00, stdev=2368.47
    clat percentiles (msec):
     |  1.00th=[ 2165],  5.00th=[ 4212], 10.00th=[ 6678], 20.00th=[ 9060],
     | 30.00th=[ 9597], 40.00th=[10000], 50.00th=[10402], 60.00th=[10805],
     | 70.00th=[11073], 80.00th=[11476], 90.00th=[12147], 95.00th=[12818],
     | 99.00th=[14026], 99.50th=[14429], 99.90th=[14832], 99.95th=[15100],
     | 99.99th=[15234]
   bw (  KiB/s): min=16299, max=122880, per=97.61%, avg=49182.97, stdev=3113.88, samples=845
   iops        : min=   11, max=  120, avg=47.83, stdev= 3.05, samples=845
  lat (msec)   : 2000=0.71%, >=2000=107.32%
  cpu          : usr=0.01%, sys=0.09%, ctx=2305, majf=0, minf=1450
  IO depths    : 1=0.0%, 2=0.0%, 4=0.0%, 8=0.5%, 16=2.5%, 32=6.9%, >=64=90.1%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=99.7%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.3%, >=64=0.0%
     issued rwts: total=2815,0,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=64

Run status group 0 (all jobs):
   READ: bw=49.2MiB/s (51.6MB/s), 49.2MiB/s-49.2MiB/s (51.6MB/s-51.6MB/s), io=3042MiB (3190MB), run=61821-61821msec

Disk stats (read/write):
  vdd: ios=9128/23, merge=0/80, ticks=15956046/8374, in_queue=15964420, util=99.81%
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

- IOPS: <b>2000</b>
- BW: <b>8007KiB</b>

```
fio-write-iops-fio-storage-benchmark-job-4qljd
write_iops: (g=0): rw=randwrite, bs=(R) 4096B-4096B, (W) 4096B-4096B, (T) 4096B-4096B, ioengine=libaio, iodepth=64
fio-3.25
Starting 1 process
write_iops: Laying out IO file (1 file / 10240MiB)

write_iops: (groupid=0, jobs=1): err= 0: pid=9: Wed Mar 10 15:45:40 2021
  write: IOPS=2000, BW=8007KiB/s (8199kB/s)(469MiB/60022msec); 0 zone resets
    slat (usec): min=7, max=28729, avg=24.51, stdev=154.41
    clat (usec): min=787, max=1024.1k, avg=32011.34, stdev=56437.17
     lat (usec): min=1104, max=1024.1k, avg=32036.07, stdev=56438.47
    clat percentiles (msec):
     |  1.00th=[    3],  5.00th=[   13], 10.00th=[   18], 20.00th=[   21],
     | 30.00th=[   22], 40.00th=[   22], 50.00th=[   22], 60.00th=[   22],
     | 70.00th=[   22], 80.00th=[   24], 90.00th=[   42], 95.00th=[   90],
     | 99.00th=[  251], 99.50th=[  468], 99.90th=[  785], 99.95th=[  852],
     | 99.99th=[  978]
   bw (  KiB/s): min=  232, max=24952, per=99.62%, avg=7976.96, stdev=5283.07, samples=119
   iops        : min=   58, max= 6238, avg=1994.19, stdev=1320.82, samples=119
  lat (usec)   : 1000=0.01%
  lat (msec)   : 2=0.17%, 4=2.48%, 10=1.54%, 20=10.59%, 50=76.58%
  lat (msec)   : 100=5.07%, 250=2.63%, 500=0.57%, 750=0.29%, 1000=0.14%
  lat (msec)   : 2000=0.01%
  cpu          : usr=1.56%, sys=7.34%, ctx=80678, majf=0, minf=63
  IO depths    : 1=0.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=100.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.1%, >=64=0.0%
     issued rwts: total=0,120082,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=64

Run status group 0 (all jobs):
  WRITE: bw=8007KiB/s (8199kB/s), 8007KiB/s-8007KiB/s (8199kB/s-8199kB/s), io=469MiB (492MB), run=60022-60022msec

Disk stats (read/write):
  vdd: ios=0/120421, merge=0/5679, ticks=0/3937385, in_queue=3937385, util=99.43%
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

- IOPS: <b>45</b>
- BW: <b>49.1MiB/s</b>

```
write_throughput: (groupid=0, jobs=8): err= 0: pid=9: Wed Mar 10 15:52:25 2021
  write: IOPS=45, BW=49.1MiB/s (51.5MB/s)(3011MiB/61356msec); 0 zone resets
    slat (usec): min=119, max=2484.5k, avg=174815.23, stdev=314336.77
    clat (msec): min=501, max=1
    8067, avg=9906.25, stdev=3058.99
     lat (msec): min=1676, max=18464, avg=10072.97, stdev=3075.57
    clat percentiles (msec):
     |  1.00th=[ 2366],  5.00th=[ 4597], 10.00th=[ 5336], 20.00th=[ 7684],
     | 30.00th=[ 8658], 40.00th=[ 9463], 50.00th=[10134], 60.00th=[10537],
     | 70.00th=[11208], 80.00th=[12281], 90.00th=[13892], 95.00th=[15234],
     | 99.00th=[16845], 99.50th=[17113], 99.90th=[17113], 99.95th=[17113],
     | 99.99th=[17113]
   bw (  KiB/s): min=16243, max=418774, per=100.00%, avg=60912.66, stdev=8139.56, samples=674
   iops        : min=   11, max=  407, avg=59.18, stdev= 7.94, samples=674
  lat (msec)   : 750=0.29%, 2000=0.29%, >=2000=107.77%
  cpu          : usr=0.04%, sys=0.08%, ctx=2009, majf=0, minf=523
  IO depths    : 1=0.0%, 2=0.0%, 4=0.0%, 8=0.5%, 16=2.3%, 32=6.9%, >=64=90.2%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=99.7%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.3%, >=64=0.0%
     issued rwts: total=0,2779,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=64

Run status group 0 (all jobs):
  WRITE: bw=49.1MiB/s (51.5MB/s), 49.1MiB/s-49.1MiB/s (51.5MB/s-51.5MB/s), io=3011MiB (3157MB), run=61356-61356msec

Disk stats (read/write):
  vdd: ios=0/9118, merge=0/1375, ticks=0/14210844, in_queue=14210844, util=99.77%
```