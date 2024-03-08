# Polymer Polyverse Testnet Rehberi

![polymer](https://pbs.twimg.com/media/GHrV-BVaUAA5qFd?format=jpg&name=medium)



## Sistem gereksinimleri:

**Ubuntu 22.04+**

NODE TİPİ | CPU     | RAM      | SSD     |
| ------------- | ------------- | ------------- | -------- |
| Polyverse | 2          | 2         | 40  |
  
  

**Gerekli Güncellemeler ve Kurulum**

```
sudo apt update && sudo apt upgrade -y
```
```
sudo apt-get install -y ca-certificates curl gnupg
```
```
sudo mkdir -p /etc/apt/keyrings
```
```
curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
```
```
echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_${NODE_MAJOR}.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
```
```
sudo apt-get update
```
```
sudo apt-get install -y nodejs
```


**Git Yüklüyoruz.**

```
sudo apt-get install git
```

**Foundry İndiriyoruz.**
```
curl -L https://foundry.paradigm.xyz | bash
```
```
source /root/.bashrc
```
```
foundryup
```

**Optimism ve Base Sepolia Faucet**

> Optimism Sepolia için [BURADAN](https://www.alchemy.com/faucets/optimism-sepolia) fauceti kullanabilirsiniz.

> Base Sepolia için [BURADAN](https://www.alchemy.com/faucets/base-sepolia) fauceti kullanabilirsiniz.

> Bu iki fauceti kullanarak, işlem yapacağınız test cüzdanında yeterli ETH olmasına dikkat edin.

**Alchemy RPC alma**

> [BURADAN](https://alchemy.com/?r=b9d675bdc6edda35) Alchemy sitesine gidiyoruz. Gmail ile oturum açıyoruz.

> Burada Optimism ve Base Sepolia için Public RPC alıyoruz.

![Ekran görüntüsü 2024-03-09 012918](https://github.com/CoinHuntersTR/Polymer-Polyverse-Tesneti/assets/111747226/701c5d2a-74dd-498c-a85e-a2ce941cdf81)

> App bölümüne geliyoruz. Create App diyoruz;

![Ekran görüntüsü 2024-03-09 013116](https://github.com/CoinHuntersTR/Polymer-Polyverse-Tesneti/assets/111747226/0bf9bb01-853f-4587-b751-621fc9a41803)

> Burada Optimism seçiyoruz. Network olarak Optimism Sepolia seçiyoruz. App bir isim ve açıklama ekleyip Create App diyoruz.

![Ekran görüntüsü 2024-03-09 013259](https://github.com/CoinHuntersTR/Polymer-Polyverse-Tesneti/assets/111747226/c4377cc0-1c69-4c92-9340-e295ecb940ad) 


> Aynı adımları Base Sepolia ağı içinde yapıyoruz. Kısaca elimizde iki farklı RPC olması gerekiyor.

![Ekran görüntüsü 2024-03-09 013542](https://github.com/CoinHuntersTR/Polymer-Polyverse-Tesneti/assets/111747226/e52f2d86-1fc0-432f-b311-cfe4c7c99c37)

> API Key butonuna basıyoruz.

![Ekran görüntüsü 2024-03-09 013714](https://github.com/CoinHuntersTR/Polymer-Polyverse-Tesneti/assets/111747226/612db66f-a03f-47c6-a93d-5d9fdd171a68)

> Burada ilk satırda olan API key bir yere not ediyoruz. Aynı şekilde Base Sepolia içinde Apı Key alıp bir yere not ediyoruz.
















```
curl -Ls https://ss-t.selfchain.nodestake.org/addrbook.json > $HOME/.selfchain/config/addrbook.json
```

**Servis Dosyasını Oluşturuyoruz.**
```
sudo tee /etc/systemd/system/selfchaind.service > /dev/null <<EOF
[Unit]
Description=selfchaind Daemon
After=network-online.target
[Service]
User=$USER
ExecStart=$(which selfchaind) start
Restart=always
RestartSec=3
LimitNOFILE=65535
[Install]
WantedBy=multi-user.target
EOF
```
```
sudo systemctl daemon-reload
```
```
sudo systemctl enable selfchaind
```

**Snapshot**
```
SNAP_NAME=$(curl -s https://ss-t.selfchain.nodestake.org/ | egrep -o ">20.*\.tar.lz4" | tr -d ">")
curl -o - -L https://ss-t.selfchain.nodestake.org/${SNAP_NAME}  | lz4 -c -d - | tar -x -C $HOME/.selfchain
```
**Node Tekrar Başlatıyoruz**
```
sudo systemctl restart selfchaind
```
```
journalctl -u selfchaind -f
```


**Node Sync Kontrolü**
> Senkronize olup olmadığımızı kontrol etmek için aşağıdaki kodu kullanıyoruz. `false` çıktısı aldığımızda işlem tamamdır.

![Ekran görüntüsü 2024-02-27 163227](https://github.com/CoinHuntersTR/Self-Chain/assets/111747226/bfc7630a-09bf-45e4-9d5d-aaf0c8d39f7b)


```
selfchaind status 2>&1 | jq .SyncInfo
```

**Cüzdan Oluşturma**
> `Cüzdanismi` yazan yeri silip kendinize bir cüzdan oluşturabilirsiniz.

> Sizden bir şifre belirlemenizi isteyecek (2 kere aynı şifreyi gireceğiz.) unutmayacağınız bir şifre girin!

> Size verilen gizli kelimeleri bir yere not etmeyi unutmayın! 

```
selfchaind keys add Cüzdanismi
```

> Eğer kullandığınız bir cüzdanı eklemek istiyorsanız. `Cüzdanismi` yazan yeri değiştirmeyi unutmayın!

> Sizden şifre isteyecek (2 kere aynı şifreyi giriyoruz.)
```
selfchaind keys add Cüzdanismi --recvoer
```

**Cüzdanda Token Değerini Görme**
> `Cüzdanismi` yazan yeri, verdiğiniz cüzdan ismi ile değiştirin. Cüzdanınıza token gelip gelmediğini kontrol etmiş olursunuz.
```
selfchaind q bank balances $(selfchaind keys show Cüzdanismi -a)
```
## Bu adımdan sonrasında Discord'a Gidiyoruz.

> İlk olarak [BURADAN](https://discord.gg/selfchainxyz) discord kanalına gidip verify adımını yapıyoruz.

> #verify-role-request kanalına gidiyoruz.

![Ekran görüntüsü 2024-02-27 164048](https://github.com/CoinHuntersTR/Self-Chain/assets/111747226/cea07184-83bb-4c88-8de0-18d99b87c7c5)

> Buradaki botu çalıştırdığınızda size DM atacak.

> Sizden iki bilgi istiyor. Birincisi Node ID yukarıda Node kurarken almış olmanız gerekiyor. İkincisi ise IP adresiniz. Bunları girdikten sonra rol gelmesini bekliyorsunuz. Rol geldikten sonra fauceti kullanabiliyoruz.


**Validator Oluşturuyoruz..**

> `Cüzdanismi` yazan yere kendi cüzdan adınızı giriyoruz.

> `MonikerName` yerine kendi verdiğiniz Moniker adınızı giriyoruz.

> `website` "" içine kendi twitter veya websitesinizi ekleyebilirsiniz.

>  `details` "" içine istediğiniz bir şey yazabilirsiniz. 
```
selfchaind tx staking create-validator \
--amount=1000000000uself \
--pubkey=$(selfchaind tendermint show-validator) \
--moniker=MonikerName \
--identity="" \
--details="Coin Hunters Community" \
--website="" \
--chain-id=self-dev-1 \
--commission-rate=0.10 \
--commission-max-rate=0.15 \
--commission-max-change-rate=0.01 \
--min-self-delegation=1 \
--from=Cüzdanismi \
--gas-prices=0.5uself \
--gas-adjustment=1.5 \
--gas=auto \
-y
```


**SelfChain Explorer**
> Tüm adımları tamamladıktan sonra [BURADAN](https://explorer-devnet.selfchain.xyz/self) kendi validatorünüzü kontrol edebilirsiniz.

