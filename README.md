![image](https://github.com/molla202/Avail/assets/91562185/6b726a06-d16c-4455-89a5-321ead104e37)

### Update ve gereklilikleri yükleyelim

```
sudo apt update
sudo apt install make clang pkg-config libssl-dev build-essential
```

### Create Avail File
```
cd ..
```

### Create Avail File in home Directory
```
sudo mkdir /root/avail-node/
```

### Go To Avail File You Created
```
cd /root/avail-node/
```

### Download The Required Files
```
wget https://github.com/availproject/avail/releases/download/v1.6.3/data-avail-linux-amd64.tar.gz
```
```
wget https://kate.avail.tools/chainspec.raw.json
```
### Zipten dosyaları çı çı çıkraaa :D (çıkaralım)
```
tar xvzf data-avail-linux-amd64.tar.gz
```
### Servis oluşturalım.
NOT: molla202 yazan kısmı değiştiriniz explorerdeki görünen isminiz...
```
sudo tee /etc/systemd/system/availd.service > /dev/null <<'EOF'
[Unit]
Description=Avail Validator
After=network.target
StartLimitIntervalSec=0

[Service]
User=root
Type=simple
Restart=always
RestartSec=120
ExecStart=/root/avail-node/data-avail-linux-amd64 --base-path /root/avail-node/data --chain /root/avail-node/chainspec.raw.json --port 30333 --validator --name "molla202"

[Install]
WantedBy=multi-user.target
EOF
```

### Nodu başlatalım
```
sudo systemctl daemon-reload
sudo systemctl enable availd.service
sudo systemctl restart availd.service
```

### Durmuna bakalım
```
sudo systemctl status availd.service
```

### Log kontrol
```
journalctl -f -u availd.service
```

### Cüzdan olusturma

https://kate.avail.tools/


### Sezon keyi oluşturuyoruz sunucumuzda
```
curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "author_rotateKeys", "params":[]}' http://localhost:9933
```


