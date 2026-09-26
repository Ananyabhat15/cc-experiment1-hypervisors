# Hypervisors

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



## 🔍 Type 1 vs Type 2

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
cc-experiment1-hypervisors/
│
├── screenshots/
│   ├── type1-proxmox/
│   │   ├── 01-proxmox-dashboard.png
│   │   ├── 02-proxmox-vm-configuration.png
│   │   ├── 03-proxmox-vm-running.png
│   │   ├── 04-proxmox-ubuntu-console.png
│   │   ├── 05-proxmox-system-configuration.png
│   │   ├── 06-proxmox-sysbench-result.png
│   │   └── 07-proxmox-resource-monitoring.png
│   │
│   ├── type2-vmware/
│   │   ├── 01-vmware-vm-configuration.png
│   │   ├── 02-vmware-vm-running.png
│   │   ├── 03-vmware-system-configuration.png
│   │   └── 04-vmware-sysbench-result.png
│   │
│   └── comparison/
│       └── 01-hypervisor-performance-comparison.png
│
├── results/
│   └── performance-analysis.md
│
└── README.md


