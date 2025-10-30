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

Now we go through some installation processes
- `wget -O splunk-10.0.1-c486717c322b-linux-amd64.deb "https://download.splunk.com/products/splunk/releases/10.0.1/linux/splunk-10.0.1-c486717c322b-linux-amd64.deb"'
    ##To download the installer
- 'sudo dpkg -i splunk-10.0.1-c486717c322b-linux-amd64.deb'
    ##Download the package onto Ubuntu VM
- 'sudo /opt/splunk/bin/splunk start --accept-license'
    ##Accepting the license
- 'sudo /opt/splunk/bin/splunk enable boot-start'
    ##This enables splunk to run on startup

Setting up Port Forwarding to connect to my Splunk Server

<img width="966" height="634" alt="image" src="https://github.com/user-attachments/assets/83f13763-3ccd-4500-a572-61eb130165c7" />

Finally have access to Splunk from my Windows Host

<img width="1430" height="720" alt="image" src="https://github.com/user-attachments/assets/5e6ed51e-8f3a-493a-9dd5-c1ebcfaba170" />

THIS MARKS THE FINISHED SETUP FOR THE UBUNTU VM WITH SPLUNK SERVER CONNECTED 
NOW WE MOVE ONTO THE INSTALLATION AND SET UP OF THE WINDOWS VM FOR ENDPOINT INTEGRATION

INSTALLING WINDOWS 11 ENTERPRISE

https://www.microsoft.com/en-us/evalcenter/download-windows-11-enterprise

VERYFYING THE HASH VALUE OF WINDOWS 11

<img width="1102" height="192" alt="image" src="https://github.com/user-attachments/assets/0f007d4d-4073-48e6-960d-1da91d709860" />

THE ISO has been successfully installed into my VIRTUALBOX environment

<img width="1031" height="889" alt="image" src="https://github.com/user-attachments/assets/8cffb50f-c0bf-4f7b-8a39-80890abf1229" />

##PHASE 2 - Configure endpoint to Splunk communication

Both VMs will have 'Adapter 1' as NAT and 'Adapter 2' as Internal Network. This allows VMs to communicate with eachother, and my host to communicate with each VM.
<img width="920" height="637" alt="image" src="https://github.com/user-attachments/assets/573138c4-5c75-4160-a6a4-60c46a57cc85" />
<img width="965" height="639" alt="image" src="https://github.com/user-attachments/assets/2c4997f8-e433-4926-92b7-df681da1ab5c" />

Setting Static IP address for my Ubuntu server

<img width="529" height="874" alt="image" src="https://github.com/user-attachments/assets/aa3be292-66eb-45c5-a881-d27107fc6780" />

Setting Static IP address for Windows endpoint

<img width="458" height="277" alt="image" src="https://github.com/user-attachments/assets/bfaf0eb7-45fa-4447-a4bf-cfc2784ee1b0" />

Right-click "Ethernet 2" → 'Properties'
Select "Internet Protocol Version 4 (TCP/IPv4)" → click 'Properties'
Select "Use the following IP address"


<img width="624" height="848" alt="image" src="https://github.com/user-attachments/assets/c1234ff7-4783-41c0-bb92-712225e7eeef" />

After configuring Windows default firewall settings, the machines can now connect to eachother through the internal connection

<img width="1781" height="903" alt="image" src="https://github.com/user-attachments/assets/dfbdd6ec-42f8-46e2-9d04-6787ade1a015" />

## Log generation, forwarding and ingestion setup

Installing winlogbeat directly onto Windows endpoint (Elastic stack)

<img width="943" height="606" alt="image" src="https://github.com/user-attachments/assets/eb40fdf4-9615-4207-bead-1b63afe5ff3a" />

Splunk will be accessed through my Windows endpoint

In Splunk we will go to 'Settings → Data Inputs → HTTP Event Collector' and create a 'New Token'

Configuration settings for HEC Token

<img width="1183" height="665" alt="image" src="https://github.com/user-attachments/assets/9a0ef1a7-77ec-4f89-98b9-2c49d519c487" />

Configuring the Winlogbeat.yml file to send logs to Splunk

<img width="934" height="552" alt="image" src="https://github.com/user-attachments/assets/47726f4a-590e-43f0-88f4-8803a9868257" />

Scroll down to the "Outputs section" and modify the "Log stash" outputs (YAML requires spaces, no tabs)

<img width="662" height="182" alt="image" src="https://github.com/user-attachments/assets/23bd7757-b8e8-4a60-a8c7-1ac9d32551ff" />

The configuration using TCP port 5044 to ingest logs from Windows endpoint

<img width="1166" height="70" alt="image" src="https://github.com/user-attachments/assets/d7943084-0cfb-4af5-910e-25e29a06b828" />

We now have logs being ingested into our Splunk server

<img width="1140" height="211" alt="image" src="https://github.com/user-attachments/assets/5d9c79d2-c513-4392-b1cb-51ac60dd8bd0" />

Adding new Log sources to the .yml file to have more coverage on the endpoint

<img width="826" height="705" alt="image" src="https://github.com/user-attachments/assets/c84b278f-93ae-4c4e-94f8-4072d540b694" />

Adding processors into the .yml file for metadata enrichment in the Winlogbeat

<img width="594" height="337" alt="image" src="https://github.com/user-attachments/assets/839819d0-3e98-4d1e-a48e-1e9ffdcf787d" />

Only the Application logs are populating in Splunk, going to have to troubleshoot

<img width="919" height="336" alt="image" src="https://github.com/user-attachments/assets/507433c2-4852-42e3-a072-64b50acee2db" />

Winlogbeat is reading the logs locally, so have to check permissions next

<img width="1000" height="313" alt="image" src="https://github.com/user-attachments/assets/298b89e3-d5b7-4c23-b611-988a2eae484e" />







