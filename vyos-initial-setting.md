## Install
- Deploy OVF into ESXi
- Set VM Network : OVF NICs

## Set IP
set interfaces ethernet eht0 address '10.0.0.1/24'
set interfaces ethernet eht0 address '15.210.188.100/22'

set service ssh port '22'
set system ntp server '16/110.135.123'

set protocols static route 0.0.0.0/0 next-hop 15.210.188.1 distance '1'


## save
commit
save

