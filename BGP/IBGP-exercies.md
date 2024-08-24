[目次に戻る](./Junos-BGP-exercises.md) <br>

# IBGPによるネットワーク演習

## 実習内容<br>
### １　ＡＳ内で動作するIGPとしてOSPFを設定します。
### ２　設定後、OSPFの確認を実施します
### ３　IBGPの設定を実施します
### ４　設定後、対向のルータ（VR2)とピアが張れていることを確認します
### ５　ピアが張れていますが、経路情報は送受信されていないことを確認します
### ６　広告したいNWを指定してBGPのエクスポートポリシーに適用します
### ７　再度ピアの確認と経路情報の送受信を確認します<br>



### １　ＡＳ内で動作するIGPとしてOSPFを設定します。
【VR1】
　#set routing-instances VR1 protocols ospf area 0 interface fe-0/0/5.0<br>
　#set routing-instances VR1 protocols ospf area 0 interface fe-0/0/6.0<br>
　#set routing-instances VR1 protocols ospf area 0 interface fe-0/0/7.0<br>
　#set routing-instances VR1 protocols ospf area 0 interface lo0.1<br>

　設定後、OSPFの確認を実施します<br>
　　>show ospf neighbor instance VR1<br>
　  > show ospf database instance VR1<br>
　  > show route protocol ospf<br>
