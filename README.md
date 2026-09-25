# Hypervisors

## Repository Structure

```text
cloud-computing-repo/
│
├── type1-hypervisor/
│   └── Implementation images
│
└── type2-hypervisor/
    └── Implementation images
```

## Type 1 Hypervisor

A **Type 1 hypervisor**, runs directly on the physical hardware without requiring a host operating system.

The `type1-hypervisor` folder contains images related to Type 1 hypervisors setup/working.

## Type 2 Hypervisor

A **Type 2 hypervisor**, runs as an application on top of an existing operating system.

The `type2-hypervisor` folder contains images related to Type 2 hypervisors and their setup/working.

## Objective

The objective of this repository is to document and understand:

* Types of hypervisors
* Differences between Type 1 and Type 2 hypervisors
* Virtual machine environments
* Hypervisor architecture and working
* Practical setup and observations

## 🔍 Type 1 vs Type 2

| Feature     | Type 1                                  | Type 2                         |
| ----------- | --------------------------------------- | ------------------------------ |
| Runs on     | Physical hardware                       | Host OS                        |
| Also called | Bare-metal                              | Hosted                         |
| Performance | Generally lower virtualization overhead | Generally higher overhead      |
| Common use  | Servers and data centers                | Desktops and development       |
| Examples    | ESXi, Hyper-V, Xen                      | VirtualBox, VMware Workstation |


