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
2. redhat subscription
```
sudo subscription-manager register
sudo subscription-manager attach --pool <pool-id>
sudo subscription-manager repos --enable=rhel-7-servers-rpms
sudo subscription-manager repos --enable=rhel-7-extras-rpms
sudo subscription-manager repos --enable=rhel-7-optional-rpms
```
3. yum update
1. sudo no password
```
sudo visudo
---add line
hoge ALL=NOPASSWD: ALL
---
```
1. set vi as a default keymap  
`set -o vi`  
1. other packages
- wget
- tmux
- vim

