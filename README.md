# SOC-Lab-environment
Building a SOC environment from scratch for incident response and alert triage
# Screenshots 
Downloading VirtualBox 7.2.4 on my Windows Host

<img width="1392" height="684" alt="image" src="https://github.com/user-attachments/assets/4bdd9c55-28ed-4ac4-b63e-f7c5bb023654" />

Downloading and installing Ubuntu server image into VirtualBox

<img width="1030" height="493" alt="image" src="https://github.com/user-attachments/assets/9cac5a0e-7581-4d86-9099-36e2eaafcd7b" />

The installed Ubuntu server and Network configurations

<img width="924" height="828" alt="image" src="https://github.com/user-attachments/assets/5676ec23-1664-4cf4-bd28-d0a160f51e09" />

My first commands- Always Update, then reboot

<img width="550" height="906" alt="image" src="https://github.com/user-attachments/assets/5f1f32b1-e869-43b0-82f7-d6d20afaaa6b" />

My first issue, DNS translation

<img width="978" height="603" alt="image" src="https://github.com/user-attachments/assets/fcfb42e0-22f6-4aed-b954-19a36021fe13" />

Network connection issue, resolved

<img width="660" height="897" alt="image" src="https://github.com/user-attachments/assets/936091bd-ee32-42e5-88df-1d86cac0e0fa" />

Now to install Splunk into the VM 

<img width="1518" height="210" alt="image" src="https://github.com/user-attachments/assets/a2daa2f0-0f65-4e9a-bece-b8f7042f05be" />

The command to install the installation file into the VM

<img width="958" height="274" alt="image" src="https://github.com/user-attachments/assets/73712a28-84b0-4387-b887-750058359d77" />

now we go through some installation processes
- `wget -O splunk-10.0.1-c486717c322b-linux-amd64.deb "https://download.splunk.com/products/splunk/releases/10.0.1/linux/splunk-10.0.1-c486717c322b-linux-amd64.deb"'
    ##To download the installer
- 'sudo dpkg -i splunk-10.0.1-c486717c322b-linux-amd64.deb'
    ##Download the package onto Ubuntu VM
- 'sudo /opt/splunk/bin/splunk start --accept-license'
    ##Accepting the license
- 'sudo /opt/splunk/bin/splunk enable boot-start'
    ##This enables splunk to run on startup


