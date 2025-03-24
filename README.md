# Technical Documentation: Homelab Setup

## Overview
This document outlines the setup and configuration of a homelab designed for cybersecurity research, penetration testing, and security monitoring. The lab simulates an enterprise network with multiple VLANs, vulnerable machines, and security tools. This setup allows security professionals and enthusiasts to practice exploitation, network defense, and incident response in a controlled environment.

## Hardware & Virtualization

### Host Server
To ensure optimal performance, the host server should meet the following specifications:
- **CPU:** Multi-core processor (Intel Xeon or AMD Ryzen recommended)
- **RAM:** At least 32GB (more is preferable for running multiple VMs)
- **Storage:** SSDs for faster VM operations; recommended capacity: 1TB+
- **Network Interface Cards (NICs):** Multiple NICs or VLAN-capable switches for proper network segmentation
- **Power Supply:** UPS for power backup to prevent sudden shutdowns

### Virtualization Platform
A hypervisor is required to manage virtual machines efficiently. Some options include:
- **VMware ESXi:** Enterprise-grade hypervisor, good for large-scale virtual networks
- **Proxmox:** Open-source alternative with strong community support
- **VirtualBox:** Suitable for lightweight, small-scale setups
- **Hyper-V:** Microsoft’s hypervisor, useful for Windows-dominated environments

## Networking & Firewall Setup

### PFsense Firewall
PFsense serves as the core firewall and router for the homelab. It provides features such as:
- VLAN creation and isolation
- Firewall rules to control traffic flow between VLANs
- VPN configuration for remote access
- Intrusion detection/prevention via Snort or Suricata
- NAT and port forwarding

### VLAN Configuration & Purpose

| VLAN ID | Name              | Purpose                                                | Machines Hosted                                      |
|---------|-------------------|--------------------------------------------------------|------------------------------------------------------|
| 1       | Security Tools    | Security monitoring, penetration testing, and incident response | Kali Linux, Wazuh, Security Onion, Nessus, Caldera, The Hive, Cortex |
| 10      | Vulnerable Machines | Intentionally insecure systems for penetration testing practice | Metasploitable 2, Buggy Web App, VulnHub Images      |
| 20      | Windows Environment | Simulated enterprise Windows environment               | Active Directory Server, Windows 10/11 Clients       |
| 30      | Docker & Containers | Containerized applications and services                | Ubuntu Server, Docker, Portainer                     |

#### VLAN 1: Security Tools
This VLAN hosts security tools used for vulnerability assessments, network monitoring, and adversary simulation.
- **Kali Linux**
- **Wazuh**
- **Caldera**
- **Security Onion**
- **Nessus**
- **The Hive & Cortex**

#### VLAN 10: Vulnerable Machines
This VLAN contains intentionally vulnerable systems for cybersecurity training and testing.
- **Metasploitable 2**
- **Buggy Web App**
- **Down Vulnerable Web App**
- **VulnHub Images**

#### VLAN 20: Windows Environment
A Windows-based enterprise environment for Active Directory testing, Windows security assessments, and endpoint monitoring.
- **Active Directory Server**
- **Windows 10 Client**
- **Windows 11 Client**

#### VLAN 30: Docker & Containers
A dedicated environment for running and managing containerized applications.
- **Ubuntu Server**
- **Docker**
- **Portainer**

### Firewall & Network Configuration

#### PFsense Setup & Security Controls
1. **VLAN Assignments:**
   - Configure VLAN interfaces within PFsense.
   - Assign appropriate subnets (e.g., 192.168.1.0/24 for Security Tools, 192.168.10.0/24 for Vulnerable Machines).
2. **Firewall Rules:**
   - Restrict unnecessary traffic between VLANs.
   - Allow controlled access for testing purposes.
3. **VPN Configuration:**
   - Configure OpenVPN or WireGuard for remote access.
4. **DHCP & DNS Setup:**
   - Assign static IPs to critical machines.
   - Configure internal DNS resolution for hostname lookups.

## Logging & Monitoring

### Security Monitoring Tools
- **Security Onion:** Monitors network traffic and detects anomalies.
- **Wazuh:** Logs security events and provides SIEM capabilities.
- **PFsense Logs:** Captures firewall activity and system events.

### Best Practices for Logging
- Enable centralized logging for easy monitoring.
- Regularly review security logs for suspicious activity.
- Set up alerts for critical security events.

## Additional Considerations

### Snapshots & Backups
- Take regular **snapshots** of virtual machines before testing new exploits.
- Implement **automated backups** for key systems.

### Access Controls
- Limit administrative access to critical machines.
- Implement **role-based access controls (RBAC)**.

### Performance Optimization
- Monitor **CPU, RAM, and disk usage**.
- Allocate resources effectively based on VM requirements.
- Use **SSD storage** for faster VM operations.

### Future Expansion
- Consider adding **cloud integration** for hybrid security testing.
- Deploy additional **vulnerable machines** for varied attack scenarios.
- Experiment with **Red vs. Blue team exercises**.

## Conclusion
This homelab provides a structured environment for security testing and research, emphasizing network segmentation, vulnerability exploitation, and security tool integration. By maintaining proper configurations and monitoring, it serves as an invaluable resource for cybersecurity learning and practical experience.
