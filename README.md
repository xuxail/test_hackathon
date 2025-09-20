<div align="center">
  <img src="https://i.postimg.cc/FHBrPm10/Gemini-Generated-Image-gbe1vlgbe1vlgbe1-removebg-preview.png" alt="TestCore Logo" width="150" height="150"> <h1>Thermal-Aware Spatio-Temporal Scheduler with Microwatt PowerPC Coprocessor</h1>
  <p>
    <i>Revolutionizing data center efficiency by eliminating thermal hotspots with intelligent hardware-accelerated scheduling.</i>
  </p>

  <p align="center">
    <a href="#about-the-project"><strong>Explore the project »</strong></a>
    <br />
    <br />
    <a href="https://github.com/ThermalCoreLabs/thermal-scheduler/issues">Report Bug</a>
    ·
    <a href="https://github.com/ThermalCoreLabs/thermal-scheduler/issues">Request Feature</a>
  </p>
</div>

![Status](https://img.shields.io/badge/status-proposal-lightgrey)
![License](https://img.shields.io/badge/license-MIT-blue)
---

## 🚀 Project Overview

**Team Name:** ThermalCore Labs  
**Hackathon Category:** Hardware & Systems  
**Track:** Innovative Computing Solutions

### Problem Statement

Modern data centers face a dual performance crisis:

CPU Overhead from Software Scheduling: Traditional OS schedulers like Linux CFS consume 5-15% of CPU cycles just for scheduling decisions, with latencies ranging from 1-10ms. This overhead scales poorly - Google's research shows that software schedulers create performance jitter and waste valuable CPU cycles that could be used for actual computation.
Thermal Management Blind Spot: Current schedulers lack real-time thermal awareness, creating hotspots that trigger CPU throttling and reduce performance by 15-30%. The thermal feedback loop is too slow (100ms+ response time) to prevent damage.

The Core Issue: Every scheduling decision made in software steals CPU cycles from your applications. In high-frequency trading, microservices, and HPC workloads, this overhead is devastating to performance.
### Our Solution: Hardware-Accelerated Thermal Scheduling

Inspired by Google's Coriolis research (achieving <1μs scheduling latency) and Microsoft's Catapult project (95% performance improvements), we propose a dedicated Microwatt PowerPC coprocessor that:

Eliminates CPU Overhead: Moves all thermal scheduling logic to dedicated hardware, freeing up 5-15% of host CPU cycles for applications
Achieves Sub-Millisecond Response: Hardware scheduling with <500μs latency vs 1-10ms software scheduling
Real-time Thermal Awareness: Continuous thermal monitoring and prediction impossible with software-only solutions
Predictable Performance: Eliminates scheduling jitter that plagues software schedulers

Expected Impact: Following industry research patterns, we anticipate 20-30% overall system performance improvement through the combination of eliminated CPU scheduling overhead and optimized thermal management.

---

## 🎯 What We're Building

### Core Innovation

* **External Hardware Coprocessor:** Dedicated Microwatt OpenPOWER softcore running on FPGA
* **Real-time Thermal Monitoring:** Sub-millisecond response to thermal events
* **Intelligent Scheduling:** Advanced spatio-temporal algorithms for optimal task placement
* **Seamless Integration:** Works with existing Linux systems via PCIe or Ethernet

### Key Features

* 🌡️ **Thermal Prediction:** Spatio-temporal thermal-aware scheduling algorithm using Spatial and Temporal correlation.
* 🗺️ **Spatial Optimization:** CPU topology-aware task placement for balanced heat distribution.
* ⏱️ **Temporal Load Balancing:** Time-staggered execution to prevent sudden thermal spikes.
* 🔌 **Hot-pluggable:** External coprocessor ensures zero impact on host CPU performance.
* 📊 **Real-time Telemetry:** 1000Hz monitoring of temperature, power, and utilization.

---

## 🏗️ Technical Architecture

### High-Level Design

The system comprises a Host Server interacting with a Microwatt Coprocessor to offload and optimize thermal-aware scheduling.

![Thermal-Aware Spatio-Temporal Scheduler Architecture](https://i.postimg.cc/y6tTz35G/u-P-drawio.png) 

### Data Flow

1.  **Collection:** Host gathers CPU temperature, power, and utilization data from `/sys/class/thermal/`, `/proc/stat`, and RAPL interfaces.
2.  **Transmission:** Telemetry is sent to the Microwatt coprocessor via PCIe DMA (or UDP for prototype).
3.  **Processing:** The OpenPOWER core on the coprocessor executes advanced scheduling algorithms, incorporating real-time thermal prediction.
4.  **Decision:** Optimized task placement decisions are returned to the host.
5.  **Application:** The Linux scheduler applies these decisions using `sched_setaffinity()` or cgroups.

---

## 🛠️ Technical Specifications

### Performance Targets
| Metric | Our Target | Current Software | Industry Research |
| :--- | :--- | :--- | :--- |
| **Scheduling Latency** | **<500µs** | 1-10ms (Linux CFS) | Google Coriolis: <1µs |
| **CPU Scheduling Overhead**| **0%** | 5-15% CPU cycles | NVIDIA BlueField: 30% savings |
| **Thermal Response Time** | **<1ms** | 100ms+ | Real-time prevention vs reaction |
| **Performance Improvement**| **20-30%** | N/A | Microsoft Catapult: 95% gains |
| **Thermal Hotspot Reduction**| **>25%** | N/A | Proactive vs reactive thermal mgmt |


### Software Stack

* **Coprocessor OS:** Bare-metal C or Linux on Microwatt
* **Host Integration:** Linux kernel module + userspace daemon
* **Communication:** PCIe DMA or UDP/IP stack
* **APIs:** IOCTL, sysfs, netlink for control

---
### 🧪 Testing & Validation

* **Test Environment**

    **Hardware:** Virtual machine or Dell PowerEdge R750 (2x Intel Xeon Gold 6338) (as per availibility)
    **Workloads:** SPEC CPU2017, PARSEC, stress-ng
    **Monitoring:** Intel PCM, ``perf``,

* **Benchmarking Plan** 

  **Baseline:** Measure thermal distribution with Linux CFS
  **Integration:** Deploy coprocessor and measure improvement
  **Stress Testing:** Run thermal stress workloads
  **Performance Impact:** Measure application throughput change
  **Power Analysis:** Compare total system power consumption

## 📖 References & Resources

### 📄 Technical Documentation

* [Microwatt GitHub Repository](https://github.com/antonblanchard/microwatt)
* [OpenPOWER ISA Specification](https://openpowerfoundation.org/specifications/isa/)
* [Linux Thermal Subsystem Documentation](https://www.kernel.org/doc/Documentation/thermal/index.html)
* [PCIe DMA Programming Guide for FPGAs](https://www.xilinx.com/support/documentation/ip_documentation/xdma/v4_1/pg195-xdma.pdf)

### 🔬 Related Work & Research
* [Spatio-temporal thermal-aware scheduling for homogeneous high-performance computing datacenters](https://www.researchgate.net/publication/313406742_Spatio-temporal_thermal-aware_scheduling_for_homogeneous_high-performance_computing_datacenters)
* [Intel RAPL: Power Monitoring Framework](https://www.intel.com/content/www/us/en/developer/articles/technical/intel-power-governor.html)
* [Analysis of the Linux Completely Fair Scheduler (CFS)](https://www.kernel.org/doc/Documentation/scheduler/sched-design-CFS.txt)
* [Academic Papers on Thermal-Aware Task Scheduling](https://scholar.google.com/scholar?q=thermal-aware+task+scheduling)
* [Case Studies in FPGA-based System Acceleration](https://scholar.google.com/scholar?q=FPGA-based+system+acceleration+case+studies)

### 📝 License & Open Source
This project is released under the MIT License to encourage adoption and collaboration.
<br>
<div align="center">
Built with ❤️ for better, more efficient computing
<br>
#Hackathon2024 #FPGA #OpenPOWER #ThermalManagement #SystemOptimization
</div>
