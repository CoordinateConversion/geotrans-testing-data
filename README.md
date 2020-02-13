This is not ready for use in production yet

# geotrans-testing-data
Work In Progress: This repository describes how to pull out testing data from GEOTRANS

# setup
```bash
sudo apt install -y virtualbox

VBoxManage createvm --name GEOTRANS --ostype RedHat_64  --register
VBoxManage modifyvm GEOTRANS --memory 1024
VBoxManage createhd --filename ~/VirtualBox\ VMs/GEOTRANS/GEOTRANS.vdi --size 18000 --format VDI

VBoxManage storagectl GEOTRANS --name "IDE Controller" --add ide --controller PIIX4
VBoxManage storageattach GEOTRANS --storagectl "IDE Controller" --port 1 --device 0 --type dvddrive --medium /tmp/rhel-server-7.7-x86_64-dvd.iso

# optionally output progress
VBoxManage showvminfo GEOTRANS

# start it
VBoxManage modifyvm GEOTRANS --vrde on
VBoxManage modifyvm GEOTRANS --vrdemulticon on --vrdeport 3390

# security risk!  if you want to make it accessible from outside
VBoxManage modifyvm GEOTRANS --vrdeaddress 0.0.0.0

# switch
#VBoxManage setproperty vrdeextpack VNC
sudo VBoxManage extpack uninstall VNC

# install Extension Pack
sudo apt install virtualbox-ext-pack
VBoxManage setproperty vrdeextpack "Oracle VM VirtualBox Extension Pack"

VBoxHeadless --startvm GEOTRANS

# install prereqs for next steps
sudo apt install -y dkms build-essential

# create a kickstart file
#https://access.redhat.com/labs/kickstartconfig/

```

# To-Dos
Figure out how to boot with kickstart file through VirtualBox.
Maybe this will help
https://gist.github.com/jtyr/816e46c2c5d9345bd6c9
