> İlk olarak sunucumuzun root kısmına 'dist' ismiyle bir klasör oluşturalım. (Ben Visual Studio Code kullandım, tercih sizin.)



> Ardından bu 'dist' klasörü içine: (app.html ve degen.jpeg dosyalarını) ekleyelim. (Sonuç, görseldeki gibi)



<img width="375" alt="Ekran Resmi 2024-06-29 14 28 39" src="https://github.com/kaplanbitcoin1/EthStorage-dApp-Tasks/assets/98455323/ceabe228-0b2a-4a24-9e59-7ecdf968d367">



> app.html içine bu kodu yapıştırıyoruz:



```shell

<html>
    <head>
        <script>
            async function fetchData() {
                const url = 'web3://0xf14e64285Db115D3711cC5320B37264708A47f89:11155111/greeting';
                const response = await fetch(url);
                const data = await response.text();
                document.getElementById('content').textContent = data;
            }
            window.onload = fetchData;
        </script>
    </head>
    <body>
        <div id="content"> Loading greeting... </div>
        <br>
        <img src="./degen.jpeg" alt="">
    </body>
</html>

```


> 'Dikkat edelim fotoğrafın uzantısı jpeg olmalı yoksa ileride hata alırsınız' (Denendi) :)


> Eğer hazırsanız kemerlerinizi bağlayın, dApp oluşturmaya başlıyoruz.

  
### NOT: "Bu işlemleri onaylanan cüzdan adresimizle yapıyoruz, unutmayın, boşa kürek çekmeyelim."


> İlk olarak ufak bir contract deploy işlemimiz olacak. Bunu Remix üzerinden rahatlıkla yapabilirsiniz. [Deploy Sepolia](https://remix.ethereum.org/)

  
```shell
  pragma solidity >=0.8.2 <0.9.0;

contract App {
    function greeting() public pure returns (string memory) {
        return "LFG, Degen!";
    }
}
```

### Ethfs-cli'yi yükleyelim.

```shell
npm i -g ethfs-cli
```


###  🐅  FlatDirectory Contract Oluşturalım.


###  🐅  Önemli: "Seçilen cüzdan adresimizin Private Key'ini giriyoruz." (Tabii tırnakları silmeden olmaz.)

###  🐅  (Bu kod bize ileride kullanacağımız FlatDirectory adresimizi ve ip adresini verecek. Kaydetmeyi unutmayın.) 


```console
ethfs-cli create -p "Private Key" -c 11155111
```


### Uygulamamızı Deploy edelim. Bunun için hesabımızda 2 civarı SepoliaETH bulunduralım. (Parantezler 😁)

```console
ethfs-cli upload -f dist -a (flat-adresimiz) -c 11155111 -p (private-keyimiz) -t 1
```


<img width="1069" alt="Ekran Resmi 2024-06-29 15 36 33" src="https://github.com/kaplanbitcoin1/EthStorage-dApp-Tasks/assets/98455323/7b1cdd8c-eb19-4c12-9922-690792d4b17e">

### Bu şekilde tx çıktısı atmamız gerekiyor. Birkaç defa bu işlemi yapsak güzel olur. En azından ben öyle yaptım.


### Bu kısımda dApp'imize web3 üzerinden erişelim. 

```console
web3://flat-adresimiz:11155111/app.html
```

# Normalde link üzerinden bağlanması gerekiyor ama Chrome gibi tarayıcılarda sorun çıkıyor. Şöyle deneyelim 😁

```console
flat-adresimiz.sep.w3link.io/app.html
```


### LFG, Degen! yazısı ile birlikte en başta oluşturduğunuz degen.jpeg dosyasındaki fotoğrafın görünüyor olması gerekiyor. 🐅

<img width="1042" alt="Ekran Resmi 2024-06-29 15 58 56" src="https://github.com/kaplanbitcoin1/EthStorage-dApp-Tasks/assets/98455323/513580d0-a27a-4ecd-a5e6-33564f9527eb">


```console
Sonlara yaklaşıyoruz 🐈
```


* Maaliyetleri azaltmak için EIP-4844 BLOB kullanalım.

* Bunun için Eth-Blob-Uploader'i yüklememiz gerekiyor.


```console
npm i -g eth-blob-uploader
```

### Blop aracını kullanarak dosyalarımızı yükleyelim.

```console
eth-blob-uploader -r (Sepolia RPC) -p (Private-Key) -f dist/app.html -t (FlatDirectoryAdres)
```
```console
eth-blob-uploader -r (Sepolia RPC) -p (Private-Key) -f dist/degen.jpeg -t (FlatDirectoryAdres)
```


### Hem app.html hem de degen.jpeg komutundan sonra bu şekilde tx almanız lazım.

<img width="601" alt="Ekran Resmi 2024-06-29 16 14 47" src="https://github.com/kaplanbitcoin1/EthStorage-dApp-Tasks/assets/98455323/0e60beeb-4bd7-42c4-8031-37ea2f918fe8">


### Son olarak dApp'imizi ETH+EthStorage ile dağıtalım. (Bu opsiyonel) 
### Sunucudan app.html ve degen.jpeg dosyasını: 'app1.html ve degen1.jpeg' olarak değiştirin.

```console
ethfs-cli create -p (Private-Key) -c 11155111
```
### Bu kod bize yeni bir Flat adres verecek, kaydedelim.


```console
ethfs-cli upload -f dist -a (yeni-flat-directory-adres) -c 11155111 -p (Private-Key) -t 2
```

### İşlemlerden sonra böyle bir çıktı almanız gerekiyor. 

<img width="997" alt="Ekran Resmi 2024-06-29 16 30 00" src="https://github.com/kaplanbitcoin1/EthStorage-dApp-Tasks/assets/98455323/c236adba-b446-4b1f-bf55-dfe814718104">


### İsteyen dosya isimlerini değiştirip birkaç farklı işlem yapabilir.

### Şimdi gelelim başvuru kısmına. İlk olarak:


```console
İLKFLATADRESİMİZ.3333.w3link.io/app.html
```
### Daha Sonra: Twitter'da bir tweet paylaşmamız gerekiyor. W3link ve işlemleri yaptığımız (twitterdan seçilen) adresimizi bu tweete ekleyelim ve EthStorage'yi etiketleyelim.


### Son olarak [Bu forma](https://dawme4mo.forms.app/ethstorage-2nd-campaign-submission?ref=blog.ethstorage.io/) gelip paylaştığımız tweet'in Url'sini ekleyip mail bırakalım.

### Onayladıklarında 5000 puan kazanmış olacağız. [Buradan](https://ethstorage.knack.com/campaigns/) kontrol edebilirsiniz. 

* 🐅 Sanırım başardın 🐅
* 🐅 Benim için bayağı uğraştıran bir içerik oldu. Bir yıldız bırakırsan sevinirim 🐅







