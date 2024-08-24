[目次に戻る](./Junos-BGP-exercises.md) <br>

# IBGPによるネットワーク演習

## 実習内容<br>
### １　AS内で動作するIGPとしてOSPFを設定します。
【VR1】
　#set routing-instances VR1 protocols ospf area 0 interface fe-0/0/5.0<br>
　#set routing-instances VR1 protocols ospf area 0 interface fe-0/0/6.0<br>
　#set routing-instances VR1 protocols ospf area 0 interface fe-0/0/7.0<br>
　#set routing-instances VR1 protocols ospf area 0 interface lo0.1<br>

　設定後、OSPFの確認を実施します<br>
　　>show ospf neighbor instance VR1<br>
　  > show ospf database instance VR1<br>
　  > show route protocol ospf<br>
