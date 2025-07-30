# Octra Testnet Rehberi

**Octra testnet** sürecinde yapılması gereken tüm adımları en anlaşılır haliyle bulabilirsiniz. Rehber zamanla güncellenecektir

Takıldığınız yerleri [grubumuzda](https://t.me/GoldenZoneWeb3) sorabilirsiniz.

---

## Ön Hazırlık

Herhangi bir sunucu seçebilirsiniz ben [Hetzner](https://hetzner.cloud/?ref=5p4lj5PZKsew) kullanıyorum. Uzun zamandır hiçbir sıkıntı yaşamadım. İlk kayıtta KYC sonrası hesabınıza  20€ tanımlanacaktır.
---

## Sunucuyu güncelleyelim ve gerekli paketleri yükleyelim

```bash
sudo apt update -y && sudo apt upgrade -y
```
---

- Hepsini kopyalayıp yapıştırın

```bash
  sudo apt install -y \
    build-essential pkg-config make gcc clang \
    libssl-dev libffi-dev libreadline-dev zlib1g-dev \
    libncurses5-dev libgdbm-dev libnss3-dev libleveldb-dev \
    ca-certificates lsb-release \
    curl wget git jq \
    screen tmux iptables nvme-cli \
    unzip lz4 tar file nano btop htop ncdu bsdmainutils \
    python3 python3-venv python3-pip
```
---

## Testnet'e katılmak için bir **Octra cüzdanı** oluşturacağız.

```bash
curl -fsSL https://octra.org/wallet-generator.sh | bash
```
<img width="922" height="174" alt="resim" src="https://github.com/user-attachments/assets/6d991066-04d5-4d69-aa37-206adf7bc606" />

- Bu kısmı görünce kendi tarayıcınızdan http://xxx:8888 adresine gireceksiniz.
- ÖNEMLİ xxx yerine kendi sunucu IP adresinizi girin.
- Generate Wallet tıklayıp cüzdan oluşturun
- Verilen bilgileri bir yere kaydedin lazım olacak. Sonra sunucudan CTRL + C yapıp kapatabilirsiniz.

## Octra Klasörü Oluşturun

```bash
mkdir octra
cd octra
```
---

## Preclient Yükleme ve Çalıştırma

```bash
git clone https://github.com/octra-labs/octra_pre_client.git
cd octra_pre_client
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
cp wallet.json.example wallet.json
```
---

## Cüzdan Bilgilerini Düzenleme

```bash
nano wallet.json
```
- Aşağıdaki şekilde düzenledikten sonra kaydetmek için CTRL'ye basılı tutup X + Y ardından Enter basalım.

```bash
{
  "priv": "B64 priv key buraya",
  "addr": "adres buraya",
  "rpc": "https://octra.network"
}
```
---

## Preclient'i Çalıştırın

```bash
./run.sh
```
- Terminalde çıkan adımları sırasıyla uygulayın. Birbirinize token göndererek işlem yapabilirsiniz. Kurcalayın. Her şeyi yapınca devam edin.
- Çıkmak istiyorsanız exit dedikten sonra sanal ortamı "deactivate" yazarak kapatabilirsiniz.

---

## Rust Kuralım

```bash
cd
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
Enter deyip devam ediyoruz.

```bash
source $HOME/.cargo/env
```
---

## Diğer Kısıma Geçelim

```bash
git clone https://github.com/octra-labs/ocs01-test.git
cd ocs01-test
cargo build --release
cp EI/exec_interface.json .
```
---

## Tekrar Cüzdan Import Ediyoruz

```bash
nano wallet.json
```
- Aşağıdaki şekilde düzenledikten sonra kaydetmek için CTRL'ye basılı tutup X + Y ardından Enter basalım.

```bash
{
  "priv": "B64 priv key buraya",
  "addr": "adres buraya",
  "rpc": "https://octra.network"
}
```
---

## Testi Başlatıyoruz

```bash
./target/release/ocs01-test
```

- Terminalde çıkan görevleri sırayla tamamlamaya çalışın.
- Claim adımını yapamıyorsanız, daha önce bir TX yapmadığınız içindir. Başkalarına Oct göndererek bu sorunu çözebilirsiniz.
- Cüzdanınızı https://octrascan.io/ adresinden aratıp detaylara bakabilirsiniz
