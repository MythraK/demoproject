# Why Docker Is Used in SONiC — Simple Explanation

## 💡 What is Docker’s role in SONiC?

Think of **SONiC (the network OS)** as a **big house**.

Inside this house, there are many **rooms**, and each room has a separate job:

- One room manages the switch hardware  
- One room runs routing protocols  
- One room runs the database  
- One room handles management functions  

👉 **Docker gives each SONiC component its own room (container)**  
So they do not disturb each other.

---

# 🟦 Advantages of Using Docker in SONiC

## ✅ 1. Isolation — Each service runs separately
Each SONiC module (BGP, LLDP, DHCP, database, etc.) runs in its own container.

- If one service crashes, the others are safe.

### Example:
If LLDP has a problem, the BGP service will still work because they are in different containers.

---

## ✅ 2. Easy to update and fix
You can update or restart **just one container** instead of rebooting the whole switch.

### Example:
Update only the BGP container → No need to stop the entire SONiC system.

---

## ✅ 3. Flexibility
You can add, remove, or modify services easily.

### Example:
You can build your own container for a new SONiC feature and run it without touching other parts.

---

## ✅ 4. Consistency
All containers run in a standard environment.  
That means SONiC behaves the same across different hardware vendors.

### Example:
Whether the switch is Broadcom, Mellanox, or Marvell — Docker ensures each service runs the same way.

---

## ✅ 5. Faster development
Developers can work on each module independently.

### Example:
A team can improve only the PFC watchdog container while another team works on BGP container.

---

## ✅ 6. Security
Containers help limit what each service can access.

- If one container is compromised, the attacker cannot easily access the whole system.

---
# SONiC Source Code Directory Structure (Simple Explanation + Diagram)

This document explains the SONiC source code directory structure in a simple and easy-to-understand way, along with a visual diagram.

---

## 🗂 SONiC Directory Structure — Diagram

```text
SONiC/
│
├── buildimage/          ← Core build system (build scripts, rootfs, kernel)
│
├── src/                 ← Main SONiC source code
│   ├── sonic-swss/              (Switch State Service)
│   ├── sonic-utilities/         (CLI utilities: show, config, etc.)
│   ├── sonic-sairedis/          (SAI interface + syncd)
│   ├── sonic-platform-common/   (Common platform APIs)
│   ├── sonic-snmpagent/         (SNMP agent)
│   └── sonic-telemetry/         (Telemetry service)
│
├── dockers/             ← Dockerfiles for all SONiC containers
│   ├── docker-database/
│   ├── docker-orchagent/
│   ├── docker-lldp/
│   ├── docker-snmp/
│   ├── docker-dhcp-relay/
│   ├── docker-teamd/
│   └── docker-router-bgp/
│
├── rules/               ← Build rules for each container/module
│
├── files/               ← Scripts, service templates, configs used during build
│
├── platform/            ← Vendor/platform-specific code
│   ├── broadcom/
│   ├── mellanox/
│   ├── marvell/
│     ├── cisco/
│   └── dell/
│
├── device/              ← Per-device hardware configuration
│   ├── x86_64-accton-as7326/
│   ├── x86_64-dell-s5232/
│   ├── x86_64-mlnx_msn2700/
│   └── others...
│
├── tools/               ← Helper scripts (build, logs, tests)
│
└── testing/             ← SONiC test framework (pytest)
```
# Types of Builds in SONiC (Simple and Easy Explanation)

SONiC provides different ways to build the system depending on what you want.  
You can build the **entire SONiC OS**, or only **one container**, or a **special version** for hardware or virtual switch.

---


## ✅ 1. Full SONiC Image Build

Builds the **entire SONiC operating system**.

### 📌 Output:
A `.bin` image that can be installed on a switch.

### 📌 Command:
```bash
make target/sonic-<platform>.bin
```

### 👉 Example:
```bash
make target/sonic-barefoot.bin
```

### ⭐ Simple meaning:
Like baking a **full cake** 🍰 from scratch.

---

## ✅ 2. Individual Docker Container Build

Builds **only one specific SONiC Docker service** instead of the entire OS.

### 📌 Output:
A `.gz` Docker container image.

### 📌 Command:
```bash
make target/docker-<container>.gz
```

### 👉 Example:
```bash
make target/docker-database.gz
```

### ⭐ Simple meaning:
Instead of baking a whole cake, you bake **one single layer** 🍪.

---

## ✅ 3. Platform-Specific Build

Builds SONiC for a **specific hardware platform** based on ASIC vendor.

### 📌 Output:
A SONiC image customized for specific hardware.

### 📌 Command:
```bash
make configure PLATFORM=<platform> ASIC=<asic>
```

### 👉 Example:
```bash
make configure PLATFORM=x86_64-accton-as5835-54x ASIC=broadcom
```

### ⭐ Simple meaning:
Like making a **phone case** designed for a specific phone model 📱.

---

## ✅ 4. Virtual Switch Build (VS Build)

Builds SONiC for running inside a **virtual machine** instead of real hardware.

### 📌 Output:
A `.img` Virtual Switch image.

### 📌 Command:
```bash
make target/sonic-vs.img
```

### 👉 Example:
```bash
make target/sonic-vs.img
```

### ⭐ Simple meaning:
A **fake switch** you can run on your computer 🖥️.

---

## ✅ 5. Incremental Build (Fast Build)

Rebuilds **only the modified parts** of SONiC after the full build.

### 📌 Output:
A faster rebuilt version containing only changed components.

### 📌 Command:
```bash
make init
make
```

### 👉 Example:
```bash
make init
make
```

### ⭐ Simple meaning:
You don’t bake the whole cake again — you **only fix the part you changed** ⚙️.

# How to Build the SONiC Image From Source (Simple Explanation)

This guide explains the SONiC build process in the simplest possible way.

---

## 🟦 Overview

Building SONiC is like building a big software project.

You do these steps:

1. Prepare your system  
2. Download SONiC source code  
3. Run the build command  
4. Get the final SONiC image  

---

## ✅ 1. Prepare Your System

Before building SONiC, you need a few basic tools installed on your system.  
These tools help SONiC compile and package everything correctly.

### Required tools:
- Docker  
- make  
- git  
- python3  

SONiC also provides a script that automatically installs most of these dependencies.

---

## ✅ 2. Download the SONiC Source Code

Clone the official SONiC build repository from GitHub:

```bash
git clone --recurse-submodules https://github.com/sonic-net/sonic-buildimage.git
cd sonic-buildimage
```

This downloads all the necessary SONiC build files and components.

---

## ✅ 3. Run the Build Command

After preparing your system and downloading the source code, you're ready to build the SONiC image.

Choose which type of SONiC image you want to create.

---

## 👉 Build Virtual Switch (VS) Image

This image is used for running SONiC in a virtual environment (for testing and learning).

```bash
make target/sonic-vs.img
```

---

## 👉 Build Image for Real Hardware (Example: Broadcom)

This command builds SONiC for Broadcom-based physical switches.

```bash
make target/sonic-broadcom.bin
```

---

### ⏳ Build Duration

The build process usually takes **1–3 hours**, depending on your:

- CPU speed  
- RAM size  
- Disk performance  

Most of the heavy work is automatically handled by Docker.

---

## ✅ 4. SONiC Image Output

After the build completes, your output SONiC image will be located inside the **target/** directory.

---

## 📁 Output Examples

### Virtual Switch Image
```
sonic-vs.img
```

### Broadcom Hardware Image
```
sonic-broadcom.bin
```

# SONiC Docker Containers (Simple Explanation)

SONiC uses many small Docker containers. Each container does one specific job.

---

## 1. database (the main memory)
- Stores all SONiC information  
- All services read/write here  
➡️ Like SONiC’s central storage.

## 2. swss (the translator)
- Reads config from the database  
- Converts it into hardware instructions  
➡️ Translates SONiC settings into actions for the switch chip.

## 3. syncd (the hardware driver)
- Talks directly to the ASIC  
- Programs the hardware  
➡️ Like a driver controlling the chip.

## 4. bgp (the routing brain)
- Runs routing protocols (BGP, OSPF, EVPN)  
➡️ Decides where packets should go.

## 5. teamd (port-channel manager)
- Manages LAG / port-channels  
➡️ Handles combined ports.

## 6. lldp (neighbor info)
- Sends/receives LLDP packets  
➡️ Shows which device is connected on each port.

## 7. pmon (hardware health checker)
- Monitors fans, temperature, power, optics  
➡️ Checks hardware health.

## 8. dhcp_relay (DHCP helper)
- Forwards DHCP requests to servers  
➡️ Helps devices get IP addresses.

## 9. snmp (monitoring agent)
- Provides SNMP monitoring  
➡️ Allows monitoring tools to read switch data.

## 10. telemetry
- Sends live switch data using gNMI/gRPC  
➡️ Real-time metrics streaming.

## 11. mgmt-framework
- Provides REST API, CLI, gNMI  
➡️ Enables automation and external control.

## 12. nat
- Handles Network Address Translation  
➡️ Converts private ↔ public IPs.

## 13. router-advertiser
- Sends IPv6 Router Advertisements  
➡️ Helps IPv6 devices learn network info.

---

# Summary Table

| Container | Simple Meaning |
|----------|----------------|
| database | SONiC’s memory |
| swss | Converts config → hardware actions |
| syncd | Talks to switch chip |
| bgp | Routing brain |
| teamd | Port-channel controller |
| lldp | Learns neighbors |
| pmon | Hardware health monitor |
| dhcp_relay | Helps devices get IP |
| snmp | Monitoring service |
| telemetry | Live data streaming |
| mgmt-framework | API & CLI server |
| nat | IP translation |
| router-advertiser | IPv6 announcements |

# 📍 Where Are SONiC Docker Images Located After the Build?

When you build SONiC using commands like:

```bash
make target/sonic-vs.img
```

or

```bash
make target/sonic-broadcom.bin
```

SONiC builds multiple Docker containers (database, swss, syncd, lldp, snmp, etc.).

---

# 📁 Location of the Built Docker Images

After the build completes, all SONiC Docker images are stored in:

```
./target/docker
```

Inside this folder, you will find image files such as:

```
docker-database.gz
docker-lldp.gz
docker-sflow.gz
docker-teamd.gz
docker-snmp.gz
docker-swss.gz
docker-syncd-broadcom.gz
```

These `.gz` files are compressed Docker images used during SONiC boot.

---

## 🧠 Why Are They Stored Here?

- The SONiC build system creates each container separately.
- They are kept in `target/docker` so they can be packaged into the final SONiC `.bin` or `.img` file.
- They can also be loaded manually for debugging or testing.

---

## 🧪 Example: How to Load a Docker Image

To load the database container manually:

```bash
docker load < target/docker/docker-database.gz
```
# How to Build One Docker Container in SONiC (Simple Guide)

## 1. Go to your SONiC build folder
```bash
cd sonic-buildimage
```

## 2. Delete the old container file (optional)
This forces a clean rebuild.
```bash
rm -f target/docker-<container>.gz
```
Example:
```bash
rm -f target/docker-swss.gz
```

## 3. Build only that container
```bash
make target/docker-<container>.gz
```
Example:
```bash
make target/docker-swss.gz
```

## 4. Load the built image into Docker
```bash
docker load -i target/docker-<container>.gz
```
Example:
```bash
docker load -i target/docker-swss.gz
```

## Summary
- SONiC keeps each Docker container as a `.gz` file inside `target/`
- Delete old → build new → load into Docker
# Purpose of Database Docker & Management Docker in SONiC

## 🗄️ Database Docker (redis)

### What it does:
- Stores all SONiC configuration (interfaces, VLANs, routes, QoS, etc.)
- Stores state information (link status, counters, neighbors)
- Acts as the central data store for all SONiC services

### Why it is important:
- Provides one common place for configuration
- Ensures consistency across all SONiC components
- Redis database makes read/write operations very fast

### Simple example:
```
config vlan add 10
```
This VLAN info is stored in the Database Docker and read by the VLAN service.

---

## 🧑‍💼 Management Docker (mgmt-framework)

### What it does:
- Handles CLI, REST API, gNMI, NETCONF commands
- Validates input using YANG models
- Converts user commands into database updates
- Writes configuration into the Database Docker

### Why it is important:
- Ensures all settings are correct and conflict-free
- Provides standardized API-based management
- Connects external tools to SONiC configuration

### Simple example:
REST API to add VLAN:
1. Request goes to Management Docker  
2. Validates VLAN ID  
3. Writes to Database Docker  
4. Services apply the change  

---


