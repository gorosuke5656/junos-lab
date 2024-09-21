
[目次に戻る](./Junos-BGP-exercises.md) <br>

# BGPパケットをJuniperで取得してみよう
Junosにおいてパケットキャプチャを実施する方法はいくつかあります。<br>

ネットワーク管理と監視ガイド<br>
https://www.juniper.net/documentation/jp/ja/software/junos/network-mgmt/topics/topic-map/analyze-network-traffic-by-using-packet-capture.html<br>

今回はmonitor traffic コマンドを入力して、junosのインタフェース間で伝送されるパケットを取得してみます<br>

## 今回の取得イメージ<br>
![Diagram](./images/bgp-packet-capture-1.jpg)<br>

##取得要領<br>
![Diagram](./images/bgp-packet-capture-2.jpg)<br>

![Diagram](./images/bgp-packet-capture-3.jpg)<br>

![Diagram](./images/bgp-packet-capture-4.jpg)<br>

![Diagram](./images/bgp-packet-capture-5.jpg)<br>

##パケット取得の注意点<br>
パケットを取得する際はサイズ指定するようにしましょう！<br>

□取得できていない場合<br>
![Diagram](./images/bgp-packet-capture-6.jpg)<br>
□取得できた場合<br>
![Diagram](./images/bgp-packet-capture-7.jpg)<br>

