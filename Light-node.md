# <h1 align="center">Avail Light Node Kurulumu</h1>
![image](https://github.com/molla202/Avail/assets/91562185/a6461113-7737-40a0-9d2a-3049a7097663)


## Linkler:
 * [Avail Resmi Websitesi](https://www.availproject.org/)
 * [Avail Resmi Twitter](https://twitter.com/AvailProject)
 * [Avail Resmi Discord](https://discord.gg/kkHAXZCNZa)
 * [Avail Light Node Dökümantasyon](https://docs.availproject.org/operate/node/light-client/)
 * [Avail Light Node Form](https://docs.google.com/forms/d/e/1FAIpQLSeL6aXqz6vBbYEgD1cZKaQ4vwbN2o3Rxys-wKTuKySVR-oS8g/viewform)


### Sistem Gereksinimleri
| Bileşenler | Minimum Gereksinimler | 
| ------------ | ------------ |
| ✔️CPU |	2+ vcpu|
| ✔️RAM	| 4+ GB |
| ✔️Storage	| 40+ GB SSD |
| ✔️UBUNTU | 22 |
## Update
```
sudo apt update && sudo apt upgrade -y
sudo apt-get install make clang pkg-config libssl-dev build-essential
```
```
screen -S alight
```

### Avail Light Client'i yükleyin
```
cd
wget https://github.com/availproject/avail-light/releases/download/v1.7.2/avail-light-linux-amd64.tar.gz
tar -xvzf avail-light-linux-amd64.tar.gz
mv avail-light-linux-amd64 avail-light
rm -rf avail-light-linux-amd64.tar.gz
```



#### Servis dosyasını oluşturalım.
```
sudo tee /etc/systemd/system/availd.service > /dev/null <<EOF
[Unit]
Description=Avail Light Client
After=network.target
StartLimitIntervalSec=0
[Service]
User=root
ExecStart=/root/avail-light --network biryani
Restart=always
RestartSec=120
[Install]
WantedBy=multi-user.target
EOF
```

#### Başlatalım
```
sudo systemctl daemon-reload
systemctl enable availd
sudo systemctl restart availd
```

## Loglar
```
journalctl -u availd -fo cat
```

#### Son blok görüntüleme
```
curl "http://localhost:7000/v1/latest_block"
```
