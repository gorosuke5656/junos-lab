[目次に戻る](./Junos-BGP-exercises.md) <br>

# IBGPによるネットワーク演習

**【IBGPを設定します】**<br>
  ![Diagram](./images/ibgp-topology.jpg)<br>

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

### 2 IBGPの設定を実施します(ASは65000）
#set routing-instances VR1 routing-options autonomous-system 65001<br>
#set routing-instances VR1 protocols bgp group INTERNAL peer-as 65001<br>
#set routing-instances VR1 protocols bgp group INTERNAL type internal<br>
#set routing-instances VR1 protocols bgp group INTERNAL neighbor 50.5.1.1<br>
#set routing-instances VR1 protocols bgp group INTERNAL local-address 50.6.1.1<br>


### 3 設定後、対向のルータ（VR2）とピアが張れていることを確認します
　> show bgp summary<br>
　　Groups: 2 Peers: 2 Down peers: 0<br>
　　Peer                     AS      InPkt     OutPkt    OutQ   Flaps Last Up/Dwn State|#Active/Received/Accepted/Damped...<br> 
　　　50.5.1.1              65001        657        657       0       0     4:53:23 Establ<br>
　　　　VR1.inet.0: 0/1/1/0<br>
　　　50.6.1.1              65001        656        657       0       0     4:53:23 Establ<br>
　　　　VR2.inet.0: 0/1/1/0<br>


### 4 ピアが張れていますが、経路情報は送受信されていないことを確認します
> show bgp neighbor instance VR1<br>
       .
        .
    Received prefixes:            0　　　　　　　　　　　→　経路受信もなし<br>
    
    Advertised prefixes:          0　　　　　　　　　　　→　経路送信もなし<br>


 
>show route receive-protocol bgp 50.6.1.1<br>

inet.0: 1 destinations, 1 routes (1 active, 0 holddown, 0 hidden)<br>

VR1.inet.0: 11 destinations, 11 routes (11 active, 0 holddown, 0 hidden)<br>

VR2.inet.0: 11 destinations, 11 routes (11 active, 0 holddown, 0 hidden)<br>

  

