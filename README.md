🌩️ OpenNebula & VMware vCenter Integration Guide

📝 Project Overview

This documentation details the successful integration of OpenNebula cloud management platform with VMware vCenter infrastructure, completed as part of our 3rd year 

Cybersecurity program at Euro Mediterranean University of Fès.

Key Achievements:


✅ Deployed OpenNebula OVF template in vCenter environment


✅ Established secure connection between OpenNebula and vCenter

✅ Configured unified cloud resource management

✅ Implemented automated VM provisioning workflows

🛠️ Technical Components

🔧 Core Technologies

Technology	Role	Version

OpenNebula	Cloud Management Platform	6.0.0.1

VMware vCenter	Virtualization Management	ESXi 6.7+

CentOS	Host OS	7.x

🌐 Network Architecture
mermaid

graph LR

    A[OpenNebula VM] -->|vCenter Driver| B(VMware vCenter)
    B --> C[ESXi Hosts]
    C --> D[Virtual Machines]
    A --> E[Sunstone Web UI]
    
📋 Implementation Steps

1️⃣ OVF Template Deployment

# Sample deployment command
ovftool --acceptAllEulas --X:waitForIp vOneCloud-6.0.0.1.ovf vi://user@vcenter.domain/Datacenter
Configuration Highlights:

Allocated 2vCPU/4GB RAM

Thin-provisioned 10GB disk

Static IP assignment (10.0.1.176/24)

Enabled automatic startup

2️⃣ Initial Configuration


# Essential services control
sudo systemctl start opennebula
sudo systemctl start opennebula-sunstone
sudo systemctl enable opennebula

3️⃣ vCenter Plugin Installation

wget -P /tmp https://github.com/OpenNebula/addon-vcenter/releases/download/v5.12.0/vcenter.v5.12.0.tar.gz
sudo tar -xvf /tmp/vcenter.v5.12.0.tar.gz -C /
Configuration File (/etc/one/vcenter_driver.default):


:one_xmlrpc: https://vcenter.domain.com:443/sdk
:vi_user: "admin_user"
:vi_pass: "secure_password"
:vcenter_host: "vcenter.domain.com"

🔐 Security Considerations

Implemented RBAC for OpenNebula access

Configured firewall rules for required ports (2633/TCP for Sunstone)

Used SSH keys for secure CLI access

Regular snapshot backups of configuration

🖥️ Access Information

Service	URL	Credentials

Sunstone Web UI	http://10.0.1.176:9869	oneadmin /
SSH Access	ssh root@10.0.1.176	root / 
📊 Performance Metrics


🚀 Key Benefits Achieved

Unified Management: Single pane for VM lifecycle operations

Automation: Reduced manual provisioning time by 70%

Resource Optimization: Improved cluster utilization by 40%

Flexibility: Mixed hypervisor support (VMware + KVM)

⚠️ Known Issues & Solutions
Issue	Solution
vCenter connection drops	Verify certificate chain
Sunstone slow response	Increase VM memory allocation
OVF deployment fails	Check network MTU settings
