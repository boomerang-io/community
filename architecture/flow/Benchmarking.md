# Benchmarking

This document is meant to records the process of testing performance and the various test results

## Storage

Test parameters were taken from the recommendations here: https://cloud.google.com/compute/docs/disks/benchmarking-pd-performance

### Prerequisites

- Kubernetes/OCP Cluster
- Knowledge of the storage classes available in the cluster (`kubectl get sc`)

### Testing process

For benchmarking we decided to use the `fio` tool since it is platform-independent so we can run the same tests regardless of K8S cluster type and storage classes. That way, we can compare values under similar conditions and have a more accurate view of what to expect when running production workloads.

### Test details & results:

- [IBM Cloud Classic Infra with GlusterFS - 08.02.2021](./benchmarking/IBMCloudClassic_GlusterFS_08022021.md)
- [IBM Cloud Classic Infra with Ceph on SSD - 23.02.2021](./benchmarking/IBMCloudClassic_Ceph_SSD_23022021.md)
- [IBM Cloud ROKS with Block Storage - 10.03.2021](./benchmarking/IBMCloudROKS_BlockStorage_10032021.md)