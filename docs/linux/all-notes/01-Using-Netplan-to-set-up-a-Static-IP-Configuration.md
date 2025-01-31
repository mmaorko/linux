## Using Netplan to set up a Static IP Configuration
#### Netplan
 Netplan is a utility for easily configuring networking on a linux system. You simply create a YAML description of the required network interfaces and what each should be configured to do. From this description, Netplan will generate all the necessary configurations for your chosen renderer tool.
#### How to Configure Static IP Address on Ubuntu 24.04.1
Netplan configuration files are stored in the /etc/netplan/ directory and here static ip configuration step:
`sudo nano /etc/netplan/50-cloud-init.yaml`

![Screenshot from 13-12-2024 2 10-1-24](https://i.ibb.co.com/ZWBTZJc/command-for-into-netplan.png)
```shell
network:
  version: 2
  renderer: networkd
  ethernets:
    ens33:
      dhcp4: no
      addresses:
        - 192.168.0.200/24
      routes:
        - to: default
          via: 192.168.0.1
      nameservers:
          addresses: [8.8.8.8, 8.8.4.4]
```

then `sudo netplan apply`
