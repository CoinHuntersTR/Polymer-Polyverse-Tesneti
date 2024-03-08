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

```
git clone https://github.com/sarox0987/polymerlab-ibc-app-solidity.git
```
```
cd polymerlab-ibc-app-solidity
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

**Metamask Private Key alma**

> Görseldeki adımları takip ederek, metamask cüzdanınızın private key'ini alıp bir yere not edin.

![metmask](https://user-images.githubusercontent.com/111747226/214062437-69e144d9-528f-4a17-b46a-a747c1d5284c.png)


**Repoyu indirelim**
```
git clone https://github.com/sarox0987/polymerlab-ibc-app-solidity.git
```
```
cd polymerlab-ibc-app-solidity
```
**Just Kuralım**

```
curl --proto '=https' --tlsv1.2 -sSf https://just.systems/install.sh | bash -s -- --to /usr/local/bin
```

**Forge Kuralım**

```
curl -L https://foundry.paradigm.xyz | bash
```
```
foundryup
```
```
forge build
```
```
forge test
```


**env dosyasını düzenleyelim**

```
nano .env
```

>  `PRIVATE_KEY_1` yazan yere tırnaklar içinde metamaskımızdan aldığımız private key ekliyoruz.

> `OP_ALCHEMY_API_KEY`yazan yere tırnaklar içinde Alchemy'den aldığımız Optimisim Sepolia API keyi yazıyoruz.

> `BASE_ALCHEMY_API_KEY`yazan yere tırnaklar içinde Alchemy'den aldığımız Base Sepolia API keyi yazıyoruz.

![Ekran görüntüsü 2024-03-09 015338](https://github.com/CoinHuntersTR/Polymer-Polyverse-Tesneti/assets/111747226/ddd16905-427d-4290-b128-a7c2daf56875)


**IBC Transferi ve Kontratları Çalıştırma**

```
just install
```
```
just do-it
```
> Aşağıdakine benzer sonuç elde edeceksiniz. Hem Optimism hemde Base için olan linkleri bir yere not edin.

![Ekran görüntüsü 2024-03-09 015615](https://github.com/CoinHuntersTR/Polymer-Polyverse-Tesneti/assets/111747226/8483d2d2-ced3-4fcf-b8bd-12b30c2e8e7b)


**Polyverse Devs Discord Rolü Alma**

> Bu rolü almak için önce discord kanallarına giriyoruz. Eğer hala girmediyseniz. [BURADAN](https://discord.gg/DEedJybQqG) katılıyoruz. Verify adımını yaptıktan sonra `technical questions` kanalına orada paylaşılanlara benzer şekilde, ekran resmi ve linkleri paylaştığınızda `Polyverse Devs` rolünü alabilirsiniz. Testnet süresince ne değeri olur bilemem.

> Ayrıca kafanıza takılan sorular ve geri dönüşler için [BURADAN](https://t.me/PolymerTurkiye) telegram grubumuza katılabilirsiniz.
