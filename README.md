############## Openstack Local Host Single Node Deployment ######################


This is your host IP address: 192.168.122.217
This is your host IPv6 address: ::1
Horizon is now available at http://192.168.122.217/dashboard
Keystone is serving at http://192.168.122.217/identity/
The default users are: admin and demo
The password: secret

Services are running under systemd unit files.
For more information see: 
https://docs.openstack.org/devstack/latest/systemd.html

DevStack Version: 2026.1
Change: f9448d8978ebd7862a5019e8e023836aee248a18 Merge "Revert "Cap stable/2025.2 network, swift, volume api_extensions for tempest"" 2025-11-25 14:01:51 +0000
OS Version: Ubuntu 24.04 noble
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
VIM Specification:
 OS:Ubuntu 24.04.3 (Noble Numbat)
 RAM:8 GB
 HDD:80GB
 Newtork:Bridge (Static IP )
 hypervisor: Linux KVM
 
 ## How To Add Static IP in linux #############
To set a static IP for interface enp1s0 on your Ubuntu machine (currently 192.168.122.217/24 via DHCP), follow the steps below.
🔧 Step-1: Check Netplan config file
You will see a file such as:
00-installer-config.yaml
01-network-manager-all.yaml
🔧 Step-2: Edit the file
sudo nano /etc/netplan/00-installer-config.yaml
🔧 Step-3: Replace DHCP config with static IP
Copy–paste this configuration (modify if needed 👇)

network:
  version: 2
  renderer: NetworkManager
  ethernets:
    enp1s0:
      dhcp4: no
      addresses:
        - 192.168.122.217/24
      gateway4: 192.168.122.1
      nameservers:
        addresses:
          - 8.8.8.8
          - 1.1.1.1

🔧 Step-4: Apply Configuration
sudo netplan apply

If you're using SSH and want a safe apply:
sudo netplan try
🔧 Step-5: Verify

ip a
ip route
systemd-resolve --status
 
 =======================================================================
  Instalation Guideline ****************
 
 Step1:In Root fresh VM Machine : 
 1. #apt install git -y
 2. #lsmem (check the Memory should be not Less the 8GB )
 3. sudo useradd -s /bin/bash -d /opt/stack -m stack
 4. Ensure home directory for the stack user has executable permission for all, as RHEL based distros create it with 700 and Ubuntu 21.04+ with 750 which can cause issues             during   deployment.
 #sudo chmod +x /opt/stack (Set Pemission ) 
 5. Since this user will be making many changes to your system, it should have sudo privileges:
   #echo "stack ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/stack
 6. sudo -u stack -i
 7. Download DevStack: 
       #git clone https://opendev.org/openstack/devstack
     The devstack repo contains a script that installs OpenStack and templates for configuration files.
 8. #cd devstack
 9. Create a local.conf file with four passwords preset at the root of the devstack git repo.
    1. vim local.conf 
    [[local|localrc]]
ADMIN_PASSWORD=secret
DATABASE_PASSWORD=password
RABBIT_PASSWORD=password
SERVICE_PASSWORD=password

wq!

This is the minimum required config to get started with DevStack.
10. Start the install # ./stack.sh

It will take as per Network Speed 20-30min final Output will be that.

This is your host IP address: 192.168.122.217
This is your host IPv6 address: ::1
Horizon is now available at http://192.168.122.217/dashboard
Keystone is serving at http://192.168.122.217/identity/
The default users are: admin and demo
The password: secret

Services are running under systemd unit files.
For more information see: 
https://docs.openstack.org/devstack/latest/systemd.html

DevStack Version: 2026.1
Change: f9448d8978ebd7862a5019e8e023836aee248a18 Merge "Revert "Cap stable/2025.2 network, swift, volume api_extensions for tempest"" 2025-11-25 14:01:51 +0000
OS Version: Ubuntu 24.04 noble

#############################################################################

 
 
