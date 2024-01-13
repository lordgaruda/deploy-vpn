# deploy-vpn
VPN deploy guide in VPS server
```
sudo su
```
after giving sudo premission

```
wget https://git.io/wireguard -O wireguard-install.sh && bash wireguard-install.sh
```
don,t do other settings . use as it is default else not work.

Now Scan That QR in Wireguard App if Network Not Working then do step as below.

Launch Azure Shell.

in my case i use azure so  u need to open port of openvpn aswell wireguard .
so follow this steps.

Create NSG Rule and Open SSH port
```
az network nsg rule create \
    --resource-group <ResourceGroupName> \
    --nsg-name <NSG Name> \
    --name SSHRule \
    --protocol tcp \
    --priority 100 \
    --destination-port-range 22
```
Open port for use by WireGuard
```
az network nsg rule create \
    --resource-group <ResourceGroupName> \
    --nsg-name <NSG Name> \
    --name wireGuardNSGRule \
    --protocol udp \
    --priority 200 \
    --destination-port-range 51820
```
Apply the NSG to the VM
```
az network nic update \
    --resource-group <ResourceGroupName> \
    --name <nic-name> \
    --network-security-group <NSG Name>
```
