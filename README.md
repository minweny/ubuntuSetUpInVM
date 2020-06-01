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

## Network:    
Use Nat/bridged for internet    
Use Host-only for SSH access    

## change timezone      
[https://linuxize.com/post/how-to-set-or-change-timezone-on-ubuntu-18-04/]      
```
timedatectl list-timezones | grep Chicago
sudo timedatectl set-timezone America/Chicago
```

## Turn off screen lock     
[https://blog.csdn.net/G_66_hero/article/details/71598021]      
privacy -> Screen lock      

## update   
```
sudo apt update
sudo apt upgrade -y
```

