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
```
3. yum update
1. other packages
- wget
- 
