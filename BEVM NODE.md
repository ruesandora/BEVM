سلام هستیم با شما همراه نود BEVM
مشخصات سرور مورد نیاز

OS : Ubuntu 20.4+ 
CPU : 2 Cores 
RAM : 2 GB 
SSD : 300 GB


بعد سرورو اجرا میکنید و کد هارو میزنید

sudo apt-get update
sudo apt-get upgrade
mkdir -p $HOME/.bevm
wget -O bevm https://github.com/btclayer2/BEVM/releases/download/testnet-v0.1.1/bevm-v0.1.1-ubuntu20.04 && chmod +x bevm
sudo cp bevm /usr/bin/
bevm --version

خب حالا تو دیسکورد عضو بشید 
https://discord.gg/fwsym3Je
و ادرس EVM خودتونو بدید تا فاست بگیرید از دیسکوردش با دستور /faucet

حالا دستور زیر دقت کنید که جایگزین کنید ادرستونو در نوشته های : replace_with_your_address_evm 


sudo tee /etc/systemd/system/bevm-node.service > /dev/null << EOF
[Unit]
Description=BEVM Node
After=network-online.target
StartLimitIntervalSec=0

[Service]
User=$USER
Restart=always
RestartSec=3
ExecStart=/usr/bin/bevm \
  --base-path $HOME/.bevm/data/validator/replace_with_your_address_evm \
  --name replace_with_your_address_evm \
  --chain testnet \
  --telemetry-url "wss://telemetry.bevm.io/submit 0"
[Install]
WantedBy=multi-user.target
EOF
Start Services


خب حالا استارت نود :

sudo systemctl daemon-reload

sudo systemctl enable bevm-node

sudo systemctl start bevm-node

چک کردن لاگ 
sudo journalctl -u bevm-node -f --no-hostname -o cat

با همچین تصویری باید روبرو بشید ، یکساعت طول میکشه تا سینک بشه
![image](https://github.com/ruesandora/BEVM/assets/106862644/3f830d50-e0ae-4427-a3a0-0a3142bbde55)


این نصب از طریق باینری بود 🫶🫶🫶 امیدوارم لذت برده باشید
