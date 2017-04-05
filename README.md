# Readme

A shell script to install VPN using SoftEther on Ubuntu VPS like DigitalOcean
now requires Ubuntu 16.04 or Debian Jessie or higher

Some parts adapted to Google Cloud Engine VMs

## Execution

* Execution for installation and setup

```shell
sudo su
wget -O - bit.ly/sevpnsetup | sh
```

This script fetches the SoftEtherVPN Server Source Code from github
After SE-VPN is built, it setups the SE-VPN server.

The following are done:
* adds a VirtualHub named VPN
* adds a user to the hub VPN with the username vpn and password vpn
* Creates a tap device called soft for local bridging
* And bridges it to the hub VPN.
* The tap device is initialized with ip address of 172.16.0.1
 
DNSMasq is installed to provide DNS and DHCP to the VPN Clients

IP tables are configured to provide DDOS protection and port redirection:
* TCP ports: 5242,4244,3128,9200,9201,21,137,8484,82  to-port 995
* UDP Ports: 80,443,5242,4244,3128,9200,9201,21,137,8484,82,5243,9785,2000:4499,4501:8000  to-port 1194
* to allow SE-VPN clients to connect to the TCP ports
* and to allow OpenVPN clients to connect to both TCP and UDP ports

Haproxy is installed to share port 80,443,8080 to squid, ssh and SE-VPN

Lastly: It outputs a URL with the Sample OpenVPN config which can be modified to connect to various ports.

Then it prompts you to set a server password
