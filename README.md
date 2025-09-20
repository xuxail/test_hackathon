<div align="center">
  <img src="https://i.imgur.com/your-logo-here.png" alt="ThermalCore Labs Logo" width="150" height="150"> <h1>Thermal-Aware Spatio-Temporal Scheduler with Microwatt PowerPC Coprocessor</h1>
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

---

## 🚀 Project Overview

**Team Name:** ThermalCore Labs  
**Hackathon Category:** Hardware & Systems  
**Track:** Innovative Computing Solutions

### Problem Statement

Modern data centers suffer from thermal hotspots that cause CPU throttling and reduce server performance by **15-30%**. Traditional OS schedulers like Linux CFS lack real-time thermal awareness, leading to uneven heat distribution and energy inefficiency.

### Our Solution

We propose a dedicated **Microwatt PowerPC coprocessor** that implements thermal-aware spatio-temporal scheduling algorithms to optimize CPU task placement in real-time, preventing thermal hotspots while maintaining system performance.

---

## 🎯 What We're Building

### Core Innovation

* **External Hardware Coprocessor:** Dedicated Microwatt OpenPOWER softcore running on FPGA
* **Real-time Thermal Monitoring:** Sub-millisecond response to thermal events
* **Intelligent Scheduling:** Advanced spatio-temporal algorithms for optimal task placement
* **Seamless Integration:** Works with existing Linux systems via PCIe or Ethernet

### Key Features

* 🌡️ **Thermal Prediction:** ML-based temperature forecasting to anticipate hotspots.
* 🗺️ **Spatial Optimization:** CPU topology-aware task placement for balanced heat distribution.
* ⏱️ **Temporal Load Balancing:** Time-staggered execution to prevent sudden thermal spikes.
* 🔌 **Hot-pluggable:** External coprocessor ensures zero impact on host CPU performance.
* 📊 **Real-time Telemetry:** 1000Hz monitoring of temperature, power, and utilization.

---

## 🏗️ Technical Architecture

### High-Level Design

The system comprises a Host Server interacting with a Microwatt Coprocessor to offload and optimize thermal-aware scheduling.

![Thermal-Aware Spatio-Temporal Scheduler Architecture](https://i.imgur.com/h5HjT20.png) ### Data Flow

1.  **Collection:** Host gathers CPU temperature, power, and utilization data from `/sys/class/thermal/`, `/proc/stat`, and RAPL interfaces.
2.  **Transmission:** Telemetry is sent to the Microwatt coprocessor via PCIe DMA (or UDP for prototype).
3.  **Processing:** The OpenPOWER core on the coprocessor executes advanced scheduling algorithms, incorporating real-time thermal prediction.
4.  **Decision:** Optimized task placement decisions are returned to the host.
5.  **Application:** The Linux scheduler applies these decisions using `sched_setaffinity()` or cgroups.

---

## 📋 Implementation Plan

### Phase 1: Rapid Prototype (Week 1-2)

* **Platform:** Arty A7 FPGA Development Board
* **Communication:** UDP over Ethernet
* **Goal:** End-to-end validation
* **Deliverables:**
    * ✅ Microwatt running on FPGA
    * ✅ Host telemetry collection (Python)
    * ✅ Basic thermal-aware scheduler (C on PowerPC)
    * ✅ UDP communication working
    * ✅ Live demo with temperature reduction

### Phase 2: PCIe Integration (Week 3-4)

* **Platform:** Xilinx VCU118 or AMD Alveo U50
* **Communication:** PCIe Gen3 x16 with DMA
* **Goal:** Production-ready low-latency implementation
* **Deliverables:**
    * [ ] PCIe endpoint with XDMA integration
    * [ ] Linux kernel driver (`/dev/thermal_scheduler`)
    * [ ] Ring buffer DMA for high-throughput
    * [ ] MSI-X interrupts for <500μs latency
    * [ ] VFIO userspace API

### Phase 3: Advanced Algorithms (Week 5-6)

* **Goal:** Sophisticated thermal modeling and ML integration
* **Deliverables:**
    * [ ] Predictive thermal modeling
    * [ ] Online ML model training
    * [ ] Multi-socket NUMA awareness
    * [ ] Container/cgroup integration
    * [ ] Performance benchmarking

---

## 🛠️ Technical Specifications

### Hardware Requirements

* **FPGA:** Xilinx 7-series or UltraScale+ (35K+ LUTs)
* **Memory:** 2MB BRAM + 4GB DDR4 (optional)
* **I/O:** PCIe Gen3 x16 or Gigabit Ethernet
* **Power:** <15W additional consumption

### Performance Targets

| Metric                       | Target     | Current Best (Linux CFS) |
| :--------------------------- | :--------- | :----------------------- |
| Scheduling Latency           | `<500μs`    | `~10ms`                  |
| Thermal Hotspot Reduction    | `>25%`     | `N/A`                    |
| CPU Performance Overhead     | `<2%`      | `N/A`                    |
| Telemetry Processing Rate    | `1000Hz`   | `~100Hz`                 |

### Software Stack

* **Coprocessor OS:** Bare-metal C or Linux on Microwatt
* **Host Integration:** Linux kernel module + userspace daemon
* **Communication:** PCIe DMA or UDP/IP stack
* **APIs:** IOCTL, sysfs, netlink for control

---

## 📊 Data Structures

### Telemetry Packet (Host → Coprocessor)

```c
struct __attribute__((packed)) telemetry_packet {
    uint64_t timestamp_us;      // Microsecond timestamp
    uint32_t cpu_id;            // Physical CPU identifier
    float temperature_c;        // Core temperature (°C)
    float power_w;             // Power consumption (W)
    float utilization;         // CPU usage (0.0-1.0)
    uint32_t runqueue_len;     // Waiting tasks
    uint32_t context_switches; // Switch rate
    uint32_t checksum;         // CRC32 integrity
};
```
<br>
<div align="center">
Built with ❤️ for better, more efficient computing
<br>
#Hackathon2024 #FPGA #OpenPOWER #ThermalManagement #SystemOptimization
</div>
