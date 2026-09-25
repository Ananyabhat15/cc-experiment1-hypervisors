# Performance Analysis

The benchmark was run for approximately **10 seconds** on both hypervisors.

- **Proxmox VE (Type-1)** processed **14,548 events** at **1,453.98 events/second**.
- **VMware Workstation (Type-2)** processed **6,399 events** at **639.70 events/second**.
- The average latency was **0.69 ms** for Proxmox VE and **1.56 ms** for VMware Workstation.
- The total execution time was almost the same for both, at around **10 seconds**.

## Observation

From the results, Proxmox VE processed **more than twice as many events per second** and had a **lower average latency** in this test. This indicates better event-processing performance under the tested configuration.

> **Note:** The results depend on the VM resources, hardware, and test configuration used, so they represent performance for this specific experimental setup.
