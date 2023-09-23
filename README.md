
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
sudo mkdir /root/avail/avail-node/
```

### Go To Avail File You Created
```
cd /root/avail/avail-node/
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
User=avail
Type=simple
Restart=always
RestartSec=120
ExecStart=/root/avail/avail-node/data-avail --base-path /root/avail/avail-node/data --chain /root/avail/avail-node/chainspec.raw.json --port 30333 --validator --name "molla202"

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

### Stake Tokens
 https://kate.avail.tools/
Contact Avail Team for funds
Keep most of your funds in the stash account since it is meant to be the custodian of your staking funds, and have just enough funds in the controller account to pay for fees.
Make sure not to bond all your AVL balance since you will be unable to pay transaction fees from your bonded balance.
## Go To Staking Tab
Click on stash as shown in picture
![staking-bond-1](https://github.com/blacknodes/AvailProject/assets/85839823/3268afc3-5f89-441a-8070-2dd0954534f8)

Sign and Submit after entering the details
![staking-bond-2](https://github.com/blacknodes/AvailProject/assets/85839823/177e3640-3bd8-432c-8ce6-45beb839ac6b)

wait for the node to sync

# Set Session Key
Once your node is synced

## Generate Session key
```curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "author_rotateKeys", "params":[]}' http://localhost:9933```

## Submit Session Key
Go to Network → Staking again, Ensure you are on Account actions, and enter session key
![staking-bond-3](https://github.com/blacknodes/AvailProject/assets/85839823/17d53746-9b5e-4118-ae6c-f85a62154b2d)


# Validate
Click on Validate button and Validate
![start-validating](https://github.com/blacknodes/AvailProject/assets/85839823/059e5e28-2033-4be5-99a3-b448f5ad986a)

# Selection 
To verify that your node is ready for possible selection at the end of the next era , navigate to Network → Staking and select Waiting. Your account should be shown there. A new validator set is selected every era, based on the staking amount.

### Congratulations! you have done all the possible steps to become a validator.
