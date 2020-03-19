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
