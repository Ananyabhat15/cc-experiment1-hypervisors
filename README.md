# Hypervisors

A hypervisor, also called a Virtual Machine Monitor (VMM), is software or firmware that allows multiple virtual machines (VMs) to run on a single physical computer.

It manages and allocates the physical hardware resources—such as CPU, memory, storage, and network—among different virtual machines while keeping them isolated from each other.

## Objectives

The main objectives of this experiment are:

- To understand the difference between Type-1 and Type-2 hypervisors.
- To set up virtual machines using different hypervisor platforms.
- To measure and compare their performance.
- To analyze throughput and latency under the same workload.
  
## Type 1 Hypervisor

A **Type 1 hypervisor**, runs directly on the physical hardware without requiring a host operating system.

The `type1-hypervisor` folder contains images related to Type 1 hypervisors setup/working.

## Type 2 Hypervisor

A **Type 2 hypervisor**, runs as an application on top of an existing operating system.

The `type2-hypervisor` folder contains images related to Type 2 hypervisors and their setup/working.

<img width="800" height="800" alt="type1-type2-hypervisor" src="https://github.com/user-attachments/assets/8a0f1bde-8c59-4a38-9072-aa903f880d73" />


##  Type 1 vs Type 2

| Feature     | Type 1                                  | Type 2                         |
| ----------- | --------------------------------------- | ------------------------------ |
| Runs on     | Physical hardware                       | Host OS                        |
| Also called | Bare-metal                              | Hosted                         |
| Performance | Generally lower virtualization overhead | Generally higher overhead      |
| Common use  | Servers and data centers                | Desktops and development       |
| Examples    | ESXi, Hyper-V, Xen                      | VirtualBox, VMware Workstation |


## Performance Metrics

The following parameters were recorded during the experiment:

| Metric | Proxmox VE | VMware Workstation |
|---|---:|---:|
| Total Execution Time | 10.0030 s | 10.0013 s |
| Total Events | 14,548 | 6,399 |
| Events per Second | 1,453.98 | 639.70 |
| Average Latency | 0.69 ms | 1.56 ms |

## Graphs

<img width="1200" height="750" alt="events_per_second_comparison" src="https://github.com/user-attachments/assets/16b31c23-682c-4afb-bb12-f604c66af36d" />
<img width="1500" height="900" alt="latency_comparison" src="https://github.com/user-attachments/assets/a9ac86ff-555b-450c-b276-cff930336102" />
<img width="1600" height="1270" alt="overall_performance_dashboard" src="https://github.com/user-attachments/assets/233d2e74-cba4-4007-b012-290730cfae72" />
<img width="1200" height="750" alt="total_events_comparison" src="https://github.com/user-attachments/assets/106cab65-82d8-41cd-a7e7-3a43ead8adde" />

## 3. Virtual Machine Specifications
To guarantee scientific accuracy and eliminate resource skewing, identical configurations were assigned to both VMs during setup:

| Resource Parameter | Proxmox VE (Type-1) | VMware Workstation (Type-2) | 
| :--- | :--- | :--- | 
| **VM Name** | `CC-Experiment1-Type1` | `CC-Experiment1-Type2` | 
| **Guest OS** | Ubuntu 22.04 LTS (ISO) | Ubuntu 22.04 LTS (ISO) | 
| **CPU Allocation**| 2 vCPU (1 Socket, 2 Cores) | 2 vCPU (1 Processor, 2 Cores) | 
| **RAM Allocation**| 2048 MiB (2.0 GB) | 2048 MB (2.0 GB) | 
| **Virtual Disk** | 20.0 GB (`local-lvm`) | 20.0 GB (Single File) | 
| **Network Adapter**| Bridge (`vmbr0`) | NAT | 
| **Benchmark Tool** | `sysbench` | `sysbench` | 

---

## 4. Experimental Procedure & Pre-Setups

### Part A: Type-1 Hypervisor Setup (Proxmox VE)
1. **Access**: Logged into the Proxmox VE web interface via `https://<PROXMOX_SERVER_IP>:8006`.
2. **VM Creation Stages**: `General -> OS -> System -> Disks -> CPU -> Memory -> Network -> Confirm`
3. **Configuration**: 
   - **OS**: Selected `ubuntu-22.04.iso` from local storage.
   - **Disks**: Allocated 20 GB on `local-lvm`.
   - **CPU**: 1 Socket, 2 Cores (Total 2 vCPU).
   - **Memory**: 1024 MiB.
   - **Network**: Assigned to `vmbr0` bridge.
4. **Installation**: Started the VM, opened the Console, and completed the standard Ubuntu Normal Installation.
5. **Verification**: Used `hostnamectl`, `lscpu`, `free -h`, and `df -h` to verify 2 Cores, 2GB RAM, and 20GB Disk.

### Part B: Type-2 Hypervisor Setup (VMware Workstation)
1. **Access**: Launched VMware Workstation and selected "Create a New Virtual Machine" (Typical Configuration).
2. **Configuration**:
   - **OS**: Mounted `ubuntu-22.04.iso`.
   - **Disks**: Set Maximum Disk Size to 20 GB (Stored as a single file).
   - **Hardware Customization**: Set Memory to 2048 MB, Processors to 1 (with 2 Cores), and Network Adapter to NAT.
3. **Installation**: Powered on the VM, erased the virtual disk, and completed the standard Ubuntu Normal Installation.
4. **Verification**: Executed the same terminal commands (`lscpu`, `free -h`) to confirm the identical allocation of hardware resources.

### Part C: Benchmark Execution
On both machines, the following commands were executed to run the test:
```bash
sudo apt update
sudo apt install sysbench -y
sysbench cpu --cpu-max-prime=20000 run
```

### 5. Sysbench Screenshot Comparison

Raw console verification of the benchmark results:

* **Proxmox VE Output:** `images/1.png`
* **VMware Workstation Output:** `images/2.png`

---


## Performance Analysis

The benchmark was run for approximately **10 seconds** on both hypervisors.

Proxmox VE processed **14,548 events** at a rate of **1,453.98 events/second**, while VMware Workstation processed **6,399 events** at **639.70 events/second**.

The average latency was **0.69 ms** for Proxmox VE compared to **1.56 ms** for VMware Workstation.

Although the total execution time was almost identical for both systems, Proxmox VE processed significantly more events during the test period and showed lower average latency.

### Observation

The results from this experiment show that **Proxmox VE achieved higher event-processing throughput and lower average latency** than VMware Workstation under the tested configuration.

However, the results depend on factors such as hardware resources, VM configuration, CPU allocation, memory allocation, and workload. Therefore, these results represent the performance observed in this particular experimental setup.

## Conclusion

The experiment demonstrates the performance differences between Type-1 and Type-2 hypervisors.

Based on the measured results, Proxmox VE showed higher throughput and lower latency in the given test, while both hypervisors had nearly the same total execution time.

This experiment helped in understanding how the underlying hypervisor architecture can affect virtual machine performance.

## Repository Structure

```text
Repository
│
├── comparison/
│   ├── 01-hypervisor-performance-comparison.png
│   ├── events_per_second_comparison.jpeg
│   ├── latency_comparison.jpeg
│   ├── overall_performance_dashboard.jpeg
│   └── total_events_comparison.jpeg
│
├── results/
│   └── performance-analysis.md
│
├── screenshots/
│   ├── type1-proxmox/
│   │   ├── 01-proxmox-dashboard.jpeg
│   │   ├── 02-proxmox-vm-configuration.jpeg
│   │   ├── 03-proxmox-vm-running.jpeg
│   │   ├── 03-proxmox-vm-running2.jpeg
│   │   ├── 04-proxmox-ubuntu-console.jpeg
│   │   ├── 05-proxmox-vm-configuration.jpeg
│   │   ├── 06-proxmox-sysbench-result.png
│   │   ├── 07-01-proxmox-resource-monitoring.png
│   │   ├── 07-02-proxmox-resource-monitoring.png
│   │   ├── 07-03-proxmox-resource-monitoring.png
│   │   └── 07-04-proxmox-resource-monitoring.png
│   │
│   └── type2-vmware/
│       ├── 01-vmware-vm-configuration.png
│       ├── 02-vmware-vm-running.png
│       ├── 03-vmware-system-configuration.jpeg
│       └── 04-vmware-sysbench-result.jpeg
│
├── scripts/
│   ├── benchmark.sh
│   └── generate_plots.py
│
└── README.md
