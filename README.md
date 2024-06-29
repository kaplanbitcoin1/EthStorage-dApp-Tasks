```shell


İlk olarak sunucumuzun root kısmına 'dist' ismiyle bir klasör oluşturalım.
(Ben Visual Studio Code kullandım, tercih sizin.)




```





```shell
Ardından bu 'dist' klasörü içine: (app.html ve degen.jpeg dosyalarını) ekleyelim.
```




<img width="375" alt="Ekran Resmi 2024-06-29 14 28 39" src="https://github.com/kaplanbitcoin1/EthStorage-dApp-Tasks/assets/98455323/ceabe228-0b2a-4a24-9e59-7ecdf968d367">




```shell
app.html içine bu kodu yapıştırıyoruz:
```





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
