# ubuntuSetUpInVM
ubuntuSetUpInVM

## preparation      
VM: Vmware      
linux distro iso: ubuntu18/ubuntu20     

## Notes:  
- The official ubuntu destop is fast enough, no need for lubuntu/xubuntu    
- Do not use server version + xfce, it cannot show chinese fonts correctly. You need to install a lot of apps         

## Steps:      
1. new virtual machine wizard     
2. select ios, easy install     
3. next, next, then finish      
4. if there is some random text poped up, just force it to restart    

## enable ssh   
ubuntu server/ubuntu destop installs ssh by default    
[https://linuxconfig.org/enable-ssh-on-ubuntu-20-04-focal-fossa-linux]    
```
Install SSH server and client metapackage using the apt command:
$ sudo apt install ssh
Enable and start SSH server daemon:
$ sudo systemctl enable --now ssh
Check SSH server status:
$ sudo systemctl status ssh
```

## Network:    
Use Nat for internet - ens33    
Nat can port forwarding, Host-Only cannot   
```
example: 

network:
    ethernets:
        #ens33:
            #dhcp4: true
            #addresses: [192.168.206.20/24]
        ens38:
            addresses: [192.168.240.10/24]
#            gateway4: 192.168.240.1
            routes:
            - to: 192.168.240.0/24
              via: 192.168.240.1
    version: 2

Normally two nic will show up together. If you have gateway for ens38, only one NIC will work.

We use the configuration script here:

network:
  version: 2
  renderer: networkd
  ethernets:
    ens33:
      dhcp4: no
      addresses: [192.168.206.21/24]
      gateway4: 192.168.206.2
      nameservers:
        addresses: [8.8.8.8,8.8.4.4]

network:
  version: 2
  renderer: networkd
  ethernets:
    ens33:
      dhcp4: no
      addresses: [192.168.206.21/24]
      gateway4: 192.168.206.2
      nameservers:
        addresses: [8.8.8.8,8.8.4.4]
    ens38:
      dhcp4: no
      addresses: [192.168.240.21/24]
      #gateway4: 192.168.206.2
      nameservers:
        addresses: [8.8.8.8,8.8.4.4]

sudo netplan apply

gateway starts with 2!
renderer doesn't matter
```

## change timezone      
[https://linuxize.com/post/how-to-set-or-change-timezone-on-ubuntu-18-04/]      
```
timedatectl list-timezones | grep Chicago
sudo timedatectl set-timezone America/Chicago
```

## Turn off screen lock and black screen     
[https://blog.csdn.net/G_66_hero/article/details/71598021]      
privacy -> Screen lock    
power -> power saving -> blank screen   

## update   
```
sudo apt update
sudo apt upgrade -y
sudo apt install net-tools
```

## VMware Nat port forwarding   
[https://windowsreport.com/open-firewall-ports/]    
Remember to open port on your firewall, especially Win10    

## Port Scanning    
[https://danielmiessler.com/study/tcpdump/]    
[https://phoenixnap.com/kb/nmap-scan-open-ports]    

```
tcpdump port 3389

netstat -ab

sudo nmap 192.168.0.1
```
 
## double nic configuration(not useful)     
```
ip a

route -4
check if there is two gateway

if yes
sudo route del -net 192.168.240.0 gw 0.0.0.0 netmask 255.255.255.0


```
