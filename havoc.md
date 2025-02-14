Havoc C2 Server Installation Guide

Table of Contents

Introduction

What is a C2 Server?

Prerequisites

Cloning the Havoc Repository

Installing Dependencies

Installing Python 3.10

Building and Running the Havoc Team Server

Building and Running the Havoc Client

Configuring a Listener

Generating and Deploying Payloads

Managing Sessions

Conclusion

Introduction

Havoc is a modern and powerful Command and Control (C2) framework used for red team operations and penetration testing. This guide will help you set up and configure the Havoc C2 framework on your system, enabling you to manage compromised systems effectively.

What is a C2 Server?

A Command and Control (C2) server is a backend system used by red teams and adversaries to manage compromised machines. C2 servers allow attackers to execute commands, exfiltrate data, and maintain access to the target system.

Havoc is a modern C2 framework providing features such as:

Secure encrypted communications

Modular payloads

Multi-user team collaboration

Customizable listeners and profiles

Prerequisites

Ensure your system meets the following requirements:

Linux-based operating system (Debian/Ubuntu recommended)

Administrative privileges

Required packages and dependencies installed

Cloning the Havoc Repository

Clone the official Havoc repository from GitHub and navigate into the directory:

git clone https://github.com/HavocFramework/Havoc.git
cd Havoc

Installing Dependencies

Install all required dependencies:

sudo apt update && sudo apt install -y \
    git build-essential apt-utils cmake \
    libfontconfig1 libglu1-mesa-dev libgtest-dev libspdlog-dev \
    libboost-all-dev libncurses5-dev libgdbm-dev libssl-dev \
    libreadline-dev libffi-dev libsqlite3-dev libbz2-dev \
    mesa-common-dev qtbase5-dev qtchooser qt5-qmake \
    qtbase5-dev-tools libqt5websockets5 libqt5websockets5-dev \
    qtdeclarative5-dev golang-go libboost-all-dev \
    mingw-w64 nasm

Installing Python 3.10

To install Python 3.10 manually:

wget https://www.python.org/ftp/python/3.10.0/Python-3.10.0.tgz

tar -xf Python-3.10.0.tgz && cd Python-3.10.0

./configure --enable-optimizations

make -j $(nproc)
sudo make altinstall

Verify the installation:

python3.10 --version

Building and Running the Havoc Team Server

Download Required Go Modules

Navigate to the teamserver directory and download necessary Go modules:

cd teamserver
go mod download golang.org/x/sys
go mod download github.com/ugorji/go
cd ..

Build the Team Server

Compile the team server:

make ts-build

Run the Team Server

Start the Havoc team server with a specified profile:

./havoc server --profile ./profiles/havoc.yaotl -v --debug

Building and Running the Havoc Client

Build the Havoc Client

Compile the client:

make client-build

Run the Havoc Client

Launch the client:

./havoc client

Configuring a Listener

Open the Client and Add a Listener

Navigate to View > Listeners

Click Add

Configure the following settings:

Name: admin-payload

Host: 192.168.1.142

Save the listener configuration.

Generating and Deploying Payloads

Generate Payload

In the Havoc client, go to Attack > Payload > Generate

Save the generated payload.

Deploy and Execute Payload on Target Machine

Transfer the payload to the target machine and execute it:

scp payload.exe user@target:/path/to/destination

Execute the payload on the target system. Once the payload is executed, it will establish a connection back to the Havoc C2 server.

Managing Sessions

Check for Active Sessions

Once the payload is executed, check for active shells in the Havoc client.

Removing Old Sessions

To clear previous session data:

rm -rf data/loot/* && rm -f data/teamserver.db

For persistent Havoc installation:

rm /home/$(whoami)/.havoc/data/teamserver.db && rm -rf /home/$(whoami)/.havoc/data/loot/*

Conclusion

By following this guide, you have successfully:

Installed and configured the Havoc C2 server

Built and launched the team server and client

Configured listeners for payload communication

Generated, deployed, and executed payloads on a target system

For further information and advanced configurations, refer to the official Havoc documentation: Havoc Framework Documentation.

Quick Havoc Installation via APT

If you prefer an easier installation, use APT:

sudo apt install havoc

Modify the default profile settings:

vim /usr/share/havoc/profiles/havoc.yaotl

Set the administrator credentials:

admin: admin

Start the server and client:

havoc server --profile ./profiles/havoc.yaotl -v --debug
havoc client

Configure a listener and deploy the payload:

View > Listeners > Add

Name: admin-payload

Host: 192.168.1.142

Save the listener

Attack > Payload > Generate

Deploy and execute the agent on a Windows machine

Once executed, access the remote shell from the Havoc client

To remove previous sessions:

rm /home/$(whoami)/.havoc/data/teamserver.db && rm -rf /home/$(whoami)/.havoc/data/loot/*

This guide ensures a seamless setup of the Havoc C2 framework for effective red teaming and penetration testing operations.
