# REPORT 

OpenVPN Setup and Testing Steps
## 1. Environment Preparation
Kali Linux VM Setup
Used Kali Linux virtual machine as the testing environment

Verified internet connectivity before starting VPN setup

## 2. OpenVPN Installation
Installation Command
bash
sudo apt install openvpn --allow-unauthenticated
Installed OpenVPN package on Kali Linux

Used --allow-unauthenticated flag to bypass repository GPG key issues

## 3. ProtonVPN Account Setup
Account Registration
Created free account at protonvpn.com

Verified email address for account activation

Accessed ProtonVPN dashboard for configuration files

OpenVPN Credentials Setup
Logged into ProtonVPN account

Navigated to Account → OpenVPN / IKEv2 username

Set up dedicated OpenVPN credentials

Saved username and password for authentication

## 4. Configuration File Download
Download Process
Accessed Downloads section in ProtonVPN dashboard

Selected OpenVPN configuration files

Downloaded free server configurations:

NL-free-01.protonvpn.net.udp.ovpn (Netherlands)

US-free-01.protonvpn.net.udp.ovpn (United States)

JP-free-01.protonvpn.net.udp.ovpn (Japan)

Saved files to ~/Downloads/ directory

## 5. Authentication Setup
Creating Secure Auth File
bash

# Create authentication file
    echo "openvpn_username" > ~/Downloads/protonvpn-auth.txt
    echo "openvpn_password" >> ~/Downloads/protonvpn-auth.txt

# Set secure permissions
    chmod 600 ~/Downloads/protonvpn-auth.txt
Created dedicated authentication file

Set restrictive permissions (600) for security

Stored OpenVPN-specific credentials (not account login)

## 6. Pre-VPN Connection Testing
Baseline IP Information
bash
# Check original IP address
    curl ifconfig.me

# Get detailed location information
    curl ifconfig.me/country
    curl ipinfo.io/city
    curl ipinfo.io/org


## 7. VPN Connection Establishment
Initial Connection Command
bash
# Navigate to config directory
cd ~/Downloads

# Establish VPN connection
sudo openvpn --config NL-free-01.protonvpn.net.udp.ovpn --auth-user-pass protonvpn-auth.txt
Connection Process Observations
OpenVPN initialized TLS handshake

Authentication with ProtonVPN servers

TLS key negotiation and verification

Connection established with "Initialization Sequence Completed" message

Real-time logs showed encryption tunnel establishment

## 8. Post-Connection Verification
IP Address Verification
Opened new terminal window while VPN connection remained active:

bash
# Check new IP address
    curl ifconfig.me

# Verify virtual location
    curl ifconfig.me/country
    curl ipinfo.io/city

Web-Based Verification
Accessed https://whatismyipaddress.com/

Verified IP address change visually

Confirmed geolocation showed Netherlands

Observed that website detected VPN usage

## 9. Traffic Encryption Testing
Browser Testing
Navigated to http://example.com while VPN active

Website loaded successfully through encrypted tunnel

Verified normal browsing functionality

Confirmed DNS requests routed through VPN

Additional Verification
bash
# Test multiple IP information services
    curl ipinfo.io
    curl api.ip.sb/geoip
    curl ifconfig.co/country
All services reported consistent VPN server information

No IP or DNS leaks detected

## 10. Performance Observations
Speed Comparison
Direct Connection: Faster response times, lower latency

VPN Connection: Noticeable speed reduction, increased latency

Observable Delay: Encryption/decryption overhead visible

Connection Stability
VPN connection remained stable during testing

No unexpected disconnections

Consistent throughput after initial connection

## 11. Disconnection Process
Terminating VPN Connection
Returned to OpenVPN terminal session

Pressed Ctrl + C to gracefully disconnect

Observed connection termination logs

Verified return to original IP address

#  RESULTS 
![image alt](https://github.com/devyani-oops/VPN-Security-Lab/blob/7eb4f4a702d8cb686a92633bb59e0e140535f5e7/Screenshot%202025-10-31%20155916.png)
![image alt](https://github.com/devyani-oops/VPN-Security-Lab/blob/9de73f736c9dd3a3ce8e53e34d9d35c1d5906d59/Screenshot%202025-10-31%20160054.png)
![image alt]()
