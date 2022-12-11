# Tunneling on WireGuard : تونل زدن در وایرگارد

###### Video : لینک ویدیو یوتیوب
```

```

###### خرید دامنه از نیم چیپ: 
```
https://namecheap.pxf.io/BX7m6W
```
###### خرید دامنه سایت ایرانی: 
```
https://www.hub.shatelhost.com/aff.php?aff=290
```
###### خرید سرور از دیجیتال اوشن : 
```
https://m.do.co/c/0fb522deafa4
```
###### خرید سرور از سایت ایرانی : 
```
https://dashboard.azaronline.com/order/?aff=790
```

**If you think this project is helpful to you, you may wish to give a** 🌟

**Feel Free To Donation :** ❤️

>TRC20: ```TGTyqv2MH7dZztMvaP5PKuS9Bma8RY5Pk8```

>ETH: ```0x5b5202a54e5ce4fb25f0d886254eeb07bb088614```

#### EU Server : سرور خارجی
#### Update & Upgrade Server : آپدیت و آپگرید سرور
```
apt-get update -y && apt-get upgrade -y
```

#### Enable IP Forwarding on the Server : فعالسازی آیپی فورواردینگ

```
sudo nano /etc/sysctl.conf
```

#### Apply Changes : اعمال تغییرات در سیستم سی تی ال
```
sudo sysctl -p
```

#### Install WireGuard on Ubuntu : نصب وایرگارد

```
sudo apt install wireguard
```

#### Configure WireGuard VPN Server on Ubuntu : کانفیگ وایرگارد
###### Generate Public/Private Keypair : ساخت کلید عمومی و خصوصی
#### The files will be saved under /etc/wireguard/ directory.

```
wg genkey | sudo tee /etc/wireguard/server_private.key | wg pubkey | sudo tee /etc/wireguard/server_public.key
```

#### Configure Tunnel Device : کانفیگ تونلینگ
```
sudo nano /etc/wireguard/wg0.conf
```
#### Add the Following line to the file: اسکریپت زیر رو پیست کنید توی فایل
```
[Interface]
## Private IP address for the wg0 interface ##
Address = 10.0.0.1/24

## VPN server listening port ##
ListenPort = 51820

## VPN server private key ##
PrivateKey = mPIoWfKQWZP8lie2ISEZ6ul7vyESH9MqpFvxk1cxIWQ=

## Firewall rules ##
PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o enp1s0 -j MASQUERADE
PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o enp1s0 -j MASQUERADE
```

#### you should replace your PrivateKey , find it in : از کلید خصوصی خودتون که ساختیداستفاده کنید.
```
sudo cat /etc/wireguard/server_private.key
```

#### Make sure to replace enp1s0 after -A POSTROUTING -o ... to match the name of your public network interface. You can find it easily with:
#### حتما از اسم اترنت سرور خودتون استفاده کنید. با اسکریپت زیر پیداش کنید.
```
ip -o -4 route show to default | awk '{print $5}'
```

#### Change the Wg0 Permission: تغییر دسترسی کانفیگ وایرگارد
```
sudo chmod -R 600 /etc/wireguard/
```
#### Enable and Start WireGuard VPN Service : فعالسازی وایرگارد

```
sudo systemctl enable wg-quick@wg0
sudo systemctl start wg-quick@wg0
```

#### Check the status of Wg: چک کردن وضعیت وایرگارد
```
sudo systemctl status wg-quick@wg0.service
```

#### IR Server : سرور ایرانی
#### Update & Upgrade Server : آپدیت و آپگرید سرور
```
apt-get update -y && apt-get upgrade -y
```
#### Install and Configure WireGuard : نصب و کانفیگ وایرگارد
```
sudo apt install wireguard
```

#### Generate Public/Private : ساخت کلید عمومی و خصوصی
```
wg genkey | sudo tee /etc/wireguard/client_private.key | wg pubkey | sudo tee /etc/wireguard/client_public.key
```

#### Open Wg0 : ویرایش کانفیگ وایرگارد
```
sudo nano /etc/wireguard/wg0.conf
```
#### Add The Following Lines : اسکریپت زیر رو بهش اضافه کنید
```
[Interface]
## VPN client private IP address ##
Address = 10.0.0.2/24

## VPN client private key ##
PrivateKey = 0COkq1GMM86CmlF5blPFDYhU84iTX8iJ7lWoC1gLfnk=

[Peer]
## VPN server public key ##
PublicKey = ZnD/WMx0kasJfGjFf0/uCtJoFbz0oNdq7EcieHXVaSc=

## VPN server public IP address and port ##
Endpoint = 192.168.01.01:51820

## Route all the traffic through the VPN tunnel ##
AllowedIPs = 0.0.0.0/0

## Key connection alive ##
PersistentKeepalive = 15
```
###### Replace the PrivateKey with the content of the one you generated, stored in the /etc/wireguard/client_private.key file.
###### از کلید خصوصی خودتون استفاده کنید که ساختید.
```
sudo cat /etc/wireguard/client_private.key
```
###### Replace the server’s public key, which can be found in the /etc/wireguard/server_public.key file on the server.
###### از کلید عمومی یخودتون استفاده کنید.
###### Replace the Endpoint value (192.168.01.01:51820) with your server’s public IP address and port.
###### آیپی (192.168.01.01:51820) رو به آیپی و پورت سرور تغییر بدید.

#### configure the server-side VPN ( on the Forgin Server ) : اعمال تونلینگ در سرور خارجی
```
sudo nano /etc/wireguard/wg0.conf
```
#### Add the Following code : اسکریپت زیر رو اضافه کنید.
```
[Peer]
## Client public key ##
PublicKey = 6FLtyfBQie9+EB3QYF55CR1FASca7vVYPReynlEccAo=

## Client IP address ##
AllowedIPs = 10.0.0.2/24
```
#### Replace the PublicKey with the file’s content stored in the /etc/wireguard/client_public.key file on the IR Server.
#### کلید عمومی سرور ایران رو وارد کنید.

#### Restart the VPN server : سرور وی پی ان رو ریست کنید.

```
sudo systemctl restart wg-quick@wg0.service
```
#### Connecting the WireGuard Client to the Server (On IR Server) : یوزر رو فعال کنید و حالشو ببرید.
```
sudo systemctl start wg-quick@wg0
```
