1. passwordless login
sshd config
```
sudo vi /etc/ssh/sshd_config
-- PublickeyAuthentication yes
sudo systemctl restart sshd
```
  ssh key config
```
mkdir ~/.ssh
vi ~/.ssh/authorized_keys
<write public key information from client>
```
2. redhat subscription / Repo
```
sudo subscription-manager register
sudo subscription-manager attach --pool <pool-id>
sudo subscription-manager repos --enable=rhel-7-server-rpms
sudo subscription-manager repos --enable=rhel-7-extra-rpms
sudo subscription-manager repos --enable=rhel-7-optional-rpms
```
1. (Optional) epel repo
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm  
sudo rpm -vh epel-release-latest-7.noarch.rpm  
sudo yum install epel-release  

3. yum update
1. sudo no password
```
usermod -aG wheel sampleuser　
sudo visudo
---add line
hoge ALL=NOPASSWD: ALL
---
```
1. set vi as a default keymap  
`set -o vi`  
1. other packages

```
yum install -y wget tmux vim tree bind-utils net-tools lsof ncdu htop tldr jq fd
```

1. modify sudoers file for password less login
```
/etc/sudoers
tom ALL=(ALL) NOPASSWD:ALL
```

