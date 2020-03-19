## Install KVM
1. First, verify your CPU supports virtualization:
```
grep -E '(vmx|svm)' /proc/cpuinfo
```
We should get either the word vmx or svm in the output, otherwise CPU doesn’t support virtualization.

2. Install KVM and associated packages:
```
yum install qemu-kvm qemu-img virt-manager libvirt libvirt-python libvirt-client virt-install virt-viewer bridge-utils
```
3. Enable and start libvirtd:
```
systemctl enable --now libvirtd
```
4. Verify that the KVM kernel module is loaded:
```
$ lsmod | grep kvm
kvm_intel             162153  0
kvm                   525409  1 kvm_intel
```
5. If you're running CentOS/RHEL 7 minimal, virt-manager may not start unless the x-window-system package is installed:
```
yum install "@X Window System" xorg-x11-xauth xorg-x11-fonts-* xorg-x11-utils -y
```
6. If not running as root (which you shouldn't be), add your $USER to the libvirt and KVM groups:
```
usermod -aG libvirt $USER
usermod -aG kvm $USER
```
7. Start the virt-manager GUI:
```
sudo virt-manager
```

## Network
All KVM guests to be used as OpenShift nodes will need to be connected to the same network, which can be achieved by creating a Bridge in KVM.

Start up virt-manager
Go into Menu --> Connection details --> Virtual networks
Click + to add a network
Give a name shadowman
Set IP range
Enable DHCPv4
Click Next
Skip IPv6 details
Select Forward to physical network
For destination, select your network (eth0, eno1, wlps0, etc)
Set Mode to NAT
Optional: Set domain name (or leave as shadowman)
