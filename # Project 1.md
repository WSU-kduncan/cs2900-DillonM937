# Project 1
# Dillon McCormick

## Part 1 - Building VMs

- Guest VM used: Ubuntu 20.04.3 LTS
- VMM (virtual machine manager / software): VirtualBox

### Setting up a Ubuntu VM on a Windows 10 host

1. Downloaded ISO from [https://ubuntu.com/download/desktop]
2. Install VirtualBox for [Windows hosts](https://download.virtualbox.org/virtualbox/6.1.26/VirtualBox-6.1.26-145957-Win.exe)
3. Click "New" on the main menu of Virtual Box, select Linux for the type of OS, and Ubuntu 64 for the version, I followed most of the recommended settings not dealing with memory allocation.
    - I gave my Ubuntu 20 GBs of space, fixed. Personally, my hard drive is getting quite full so I did not want my memory to be flex and expand upon 20 GBs.
    - The recommended allocation of RAM is 2 GBs for Virtual Box, I allocated 4 GBs to ensure smooth operation. My computer has 16 GBs to spare.
    - I did not choose to enable 3D Acceleration because I do not need it for any of my current courses. I have an NVIDIA 1060 6GB, so I do have the real estate to enable it.
    ## If you choose to enable 3D Acceleration, on VirtualBox go to Settings > Display > Enable 3D Acceleration. 
    - I personally added drag and drop shared clipboard, and fullscreen guest additions. Guest additions add quality of life features that are very nice to have.
    # To add these Guest Additions, open your VM, click on Devices, and hover over Drag and Drop, enable it, then do the same for whichever Guest Addition you wish.
4. Install an OS to the Virtual Machine
    - For the Ubuntu Desktop install, you receive only one ISO file, this is your install ISO.
    - Once your VM is up and running, go back to the Virtual Box menu, click Settings > Storage, under the IDE controller you will see your ISO file, remove it. Your VM should now have all of the basic components set up.

## Part 2 - Exploring Virtualization

### Exploring Host Disk Usage
1. My Guest OS is currently in my VirtualBoxVMs folder within my users folder. Checking the properties tells me it is currently 8 GBs of memory, this will expand when data is added to it, up to 20 GBs.
2. As of right now, I cannot access the files on my guest as I have not added the shared files Guest Additions, nor did I add any files as of the making of this assignment.
3. Snapshots are essentially save files for your VM. Say you are pen testing or dealing with a malicious software. It is smart to make a snapshot prior to running the program so you can revert all damages done to the VM by going back to your snapshot. Snapshots are copies of the disk files of a VM. Clones are a entire copy of a virtual machine, the VM that has been copied will be considered a parent VM. Templates are master copies that can create a whole bunch of clones. The snapshot I created was near 800 MB, .save files, and .vdi files were found within the snapshot folder. Like stated earlier, snapshot are images of the DISK of the VM.

### Exploring Guest Networking

- Explain the network configuration for your Guest
    - The only device on my router than can connect with my VM is the Host, I tried on my laptop and couldn't ping it.
        - My guest is getting network access from the NAT Network provided by Virtual Box's NAT engine. An example photo that illustrates this point well is: https://www.nakivo.com/blog/wp-content/uploads/2019/07/VirtualBox-network-modes-%E2%80%93-how-the-NAT-mode-works.png . Right now my VM is on my 4th NAT adapter and it's IP is 10.0.2.6. The VM connects to the NAT made by VirtualBox, then connects to my computer. 

## Part 3 - Networking with Style

I chose to investigate how a bridged network operates. This network works if your host computer is wired into your router through an ethernet cable. VirtualBox uses a device driver on your host system to intercept data from your ethernet network and "inject data into it" according to Oracle's website. Enabling bridged networking is very simple, you just have to be wired in through an ethernet cable. Once you are, go to your VM's settings in virtual box, click Network, then change the network type to bridge network, and select which controller your ethernet is running through. You will be able to prove that this network is up and running by pinging your VM using a device on your router that isn't your host computer. My IP changed while under a bridged network, I could ping my VM from my laptop, and I could browse YouTube with my VM. 
