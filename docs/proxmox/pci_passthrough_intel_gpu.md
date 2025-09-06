
Integrated GPU Passthrough to a Virtual Machine in Proxmox (Step-by-Step Tutorial)

https://www.youtube.com/watch?v=UoL8YJAc-vE 

Step by Step tasks:

Step 1: Edit GRUB  
  Execute: nano /etc/default/grub 
     Change this line from 
   GRUB_CMDLINE_LINUX_DEFAULT="quiet"
     to 
   GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on i915.enable_gvt=1 iommu=pt pcie_acs_override=downstream,multifunction video=efifb:off video=vesa:off vfio_iommu_type1.allow_unsafe_interrupts=1 kvm.ignore_msrs=1 modprobe.blacklist=radeon,nouveau,nvidia,nvidiafb,nvidia-gpu"
  Save file and exit the text editor  
   
Step 2: Update GRUB  
  Execute the command: update-grub 
   
Step 3: Edit the module files   
  Execute: nano /etc/modules 
     Add these lines: 
 vfio
 vfio_iommu_type1
 vfio_pci
 vfio_virqfd
 kvmgt
  Save file and exit the text editor  
   
Step 4: IOMMU remapping  
 a) Execute: nano /etc/modprobe.d/iommu_unsafe_interrupts.conf 
     Add this line: 
    options vfio_iommu_type1 allow_unsafe_interrupts=1
     Save file and exit the text editor  
 b) Execute: nano /etc/modprobe.d/kvm.conf 
     Add this line: 
    options kvm ignore_msrs=1
     Save file and exit the text editor  
   
Step 5: Blacklist the GPU drivers  
  Execute: nano /etc/modprobe.d/blacklist.conf 
     Add these lines: 
    blacklist radeon
    blacklist nouveau
    blacklist nvidia
    blacklist nvidiafb
  Save file and exit the text editor  
   
Step 6: Adding GPU to VFIO  
 a) Execute: lspci -v 
     Look for your GPU and take note of the first set of numbers 
 b) Execute: lspci -n -s (PCI card address) 
   This command gives you the GPU vendors number.
 c) Execute: nano /etc/modprobe.d/vfio.conf 
     Add this line with your GPU number and Audio number: 
   options vfio-pci ids=(GPU number,Audio number) disable_vga=1
  Save file and exit the text editor  
   
Step 7: Command to update everything and Restart  
 a) Execute: update-initramfs -u 
 b) Then restart the your Proxmox Node