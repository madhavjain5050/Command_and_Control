# Havoc C2 Server Installation Guide

## Table of Contents

- [Introduction](#introduction)
- [What is a C2 Server?](#what-is-a-c2-server)
- [Prerequisites](#prerequisites)
- [Cloning the Havoc Repository](#cloning-the-havoc-repository)
- [Installing Dependencies](#installing-dependencies)
- [Installing Python 3.10](#installing-python-310)
- [Building and Running the Havoc Team Server](#building-and-running-the-havoc-team-server)
- [Building and Running the Havoc Client](#building-and-running-the-havoc-client)
- [Configuring a Listener](#configuring-a-listener)
- [Generating and Deploying Payloads](#generating-and-deploying-payloads)
- [Managing Sessions](#managing-sessions)
- [Conclusion](#conclusion)

## Introduction

Havoc is a modern and powerful Command and Control (C2) framework used for red team operations and penetration testing. This guide will help you set up and configure the Havoc C2 framework on your system, enabling you to manage compromised systems effectively.

## What is a C2 Server?

A Command and Control (C2) server is a backend system used by red teams and adversaries to manage compromised machines. C2 servers allow attackers to execute commands, exfiltrate data, and maintain access to the target system.

Havoc is a modern C2 framework providing features such as:

- Secure encrypted communications
- Modular payloads
- Multi-user team collaboration
- Customizable listeners and profiles

## Prerequisites

Ensure your system meets the following requirements:

- Linux-based operating system (Debian/Ubuntu recommended)
- Administrative privileges
- Required packages and dependencies installed

## Cloning the Havoc Repository

Clone the official Havoc repository from GitHub and navigate into the directory:

```bash
git clone https://github.com/HavocFramework/Havoc.git
```

```bash
cd Havoc
```

## Installing Dependencies

Install all required dependencies:

```bash
sudo apt update && sudo apt install -y \
    git build-essential apt-utils cmake \
    libfontconfig1 libglu1-mesa-dev libgtest-dev libspdlog-dev \
    libboost-all-dev libncurses5-dev libgdbm-dev libssl-dev \
    libreadline-dev libffi-dev libsqlite3-dev libbz2-dev \
    mesa-common-dev qtbase5-dev qtchooser qt5-qmake \
    qtbase5-dev-tools libqt5websockets5 libqt5websockets5-dev \
    qtdeclarative5-dev golang-go libboost-all-dev \
    mingw-w64 nasm
```

## Installing Python 3.10

To install Python 3.10 manually:

```bash
wget https://www.python.org/ftp/python/3.10.0/Python-3.10.0.tgz
```

```bash
tar -xf Python-3.10.0.tgz && cd Python-3.10.0
```

```bash
./configure --enable-optimizations
```

```bash
make -j $(nproc)
sudo make altinstall
```

```bash
python3.10 --version
```

## Building and Running the Havoc Team Server

### Download Required Go Modules

Navigate to the `teamserver` directory and download necessary Go modules:

```bash
cd teamserver
go mod download golang.org/x/sys
go mod download github.com/ugorji/go
cd ..
```

## Build the Team Server

Compile the team server:

```bash
make ts-build
```

## Run the Team Server

Start the Havoc team server with a specified profile:

```bash
./havoc server --profile ./profiles/havoc.yaotl -v --debug
```

## Building and Running the Havoc Client

### Build the Havoc Client

Compile the client:

```bash
make client-build
```

## Run the Havoc Client

Launch the client:

```bash
./havoc client
```

## Configuring a Listener

### Open the Client and Add a Listener

1. Navigate to `View` > `Listeners`
2. Click `Add`
3. Configure the following settings:

    Name: <title>
    Host: <192.168.x.x>
   
4. Save the listener configuration.
