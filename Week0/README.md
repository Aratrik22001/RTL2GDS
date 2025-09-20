# VSD Hardware Design Program

## Week 0: Tool Setup

Welcome to my **VLSI System Design (VSD) Program** repository!
Installing the essential open-source tools for the software and setting up the development setup took up this week. The goal is to create a reliable and effective environment for doing design, simulation, and synthesis tasks.

#### <ins>Follow the steps below to set up all the required tools:</ins>

### **Minimum System Configuration**
- RAM: 6 GB
- Storage: 50 GB free space
- OS: Ubuntu 20.04 (or later)
- CPU: 4 cores

### **Adjusting Ubuntu display to full screen**
```bash
$ sudo apt update
$ sudo apt install build-essential dkms linux-headers-$(uname -r)
$ cd /media/<username>/VBox_GAs_7.1.8/
$ ./autorun.sh
```
### **TOOL CHECK**

#### <ins>**Yosys**</ins>
```bash
$ sudo apt-get update
$ git clone https://github.com/YosysHQ/yosys.git
$ cd yosys
$ sudo apt install make    # install make if missing
$ sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
$ make config-gcc
# Note: Yosys needs the abc submodule. Initialize it before compiling:
$ git submodule update --init --recursive
$ make
$ sudo make install
```

#### <ins>**Iverilog**</ins>
```bash
$ sudo apt-get update
$ sudo apt-get install iverilog
```

#### <ins>**gtkwave**</ins>
```bash
$ sudo apt-get update
$ sudo apt-get install gtkwave
```
