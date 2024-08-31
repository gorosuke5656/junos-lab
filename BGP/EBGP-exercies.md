[目次に戻る](./Junos-BGP-exercises.md) <br>

# EBGPによるネットワーク演習

## EBGP接続(Juniper間の設定）<br>
今回は以下の条件で設定します。<br>

１　通常EBGP接続に場合は対向ASの物理インターフェスアドレスをピアアドレスとして<br>
　　設定しますが、今回は対向ASルータのループバックアドレスをピアーアドレスとして<br>
　　設定します。<br>

２　AS間のStaticルートを冗長化するために以下の設定を実施します<br>
　（AS65000：CORE、AS65001：VR1/VR2）<br>
　　　BFDを用いたStaticルートを設定する<br>
   　　→　これによりAS65001向けの回線がDOWNした場合でも別の回線を<br>
   　　　　使用して迂回することが可能<br>


　（AS65001：VR1/VR2）<br>
　　　IGP(OSPF)においてお互いにデフォルトルートを通知する設定を実施<br>
   　　→　各ルータのAS65000向け回線がDOWNした場合でも別のルータの回線<br>
   　　　を使用して迂回することが可能<br>


**【EBGP間の接続(AS65000～AS65001）】**<br>
  ![Diagram](./images/ebgp-topology-1.jpg)<br>
  
  
  
  今回、AS間の接続についてはStaticルートを使用しますが、BFDを活用して
   回線障害時に切替ができるようにします<br>
   
   #### BFDとは？<br>
   BFD（Bidirectional Forwarding Detection）は<br>
   2台の隣接するルータ間の転送パスの生存状況を調べて高速に障害を検知してルーティングプロトコルに通知する機能です<br>
   BFD機能は、隣接するルータとの間にL2スイッチなどが存在し、リンクステータスが伝わらない障害が発生した場合に効果的な機能<br>
   
   **(参考：）BFD がネットワーク障害を検出する方法の理解 Juniper networks**<br>
   https://www.juniper.net/documentation/jp/ja/software/junos/high-availability/topics/topic-map/bfd.html<br>
   
   
 **【現状の課題】**<br>
  ![Diagram](./images/ebgp-bfd-1.jpg)<br>
  
  ![Diagram](./images/ebgp-bfd-2.jpg)<br>
  
 **【BFDを使用した構成】**<br>
 ![Diagram](./images/ebgp-bfd-3.jpg)<br>
 
 ### BFDの設定例<br>
 **【AS65000(CORE)での設定】**<br>

 AS65001配下のサブネット(50.5.1.1/32、50.6.1.1/32）に対するStatic経路をBFDで記述<br>

set routing-instances VR2 routing-options static route 1.1.1.1/32 next-hop 172.16.200.1<br>

set routing-instances VR2 routing-options static route 50.5.1.1/32 next-hop 172.16.5.254<br>
set routing-instances VR2 routing-options static route 50.5.1.1/32 qualified-next-hop 172.16.6.254 
preference 10<br>
set routing-instances VR2 routing-options static route 50.5.1.1/32 qualified-next-hop 172.16.6.254
bfd-liveness-detection minimum-interval 60<br>
set routing-instances VR2 routing-options static route 50.5.1.1/32 bfd-liveness-detection 
minimum-interval 60<br>

set routing-instances VR2 routing-options static route 50.6.1.1/32 next-hop 172.16.6.254<br>
set routing-instances VR2 routing-options static route 50.6.1.1/32 qualified-next-hop 172.16.5.254 
bfd-liveness-detection minimum-interval 60<br>
set routing-instances VR2 routing-options static route 50.6.1.1/32 bfd-liveness-detection 
minimum-interval 60<br>


 AS65001配下のサブネット(10.1.5.0/24、10.1.6.0/24）に対するStatic経路をBFDで記述<br>
set routing-instances VR2 routing-options static route 10.1.5.0/24 next-hop 172.16.5.254<br>
set routing-instances VR2 routing-options static route 10.1.5.0/24 qualified-next-hop 172.16.6.254 
preference 10<br>
set routing-instances VR2 routing-options static route 10.1.5.0/24 qualified-next-hop 172.16.6.254 
bfd-liveness-detection minimum-interval 60<br>
set routing-instances VR2 routing-options static route 10.1.5.0/24 bfd-liveness-detection 
minimum-interval 60<br>

set routing-instances VR2 routing-options static route 10.1.6.0/24 next-hop 172.16.6.254<br>
set routing-instances VR2 routing-options static route 10.1.6.0/24 qualified-next-hop 172.16.5.254 
preference 10<br>
set routing-instances VR2 routing-options static route 10.1.6.0/24 qualified-next-hop 172.16.5.254 
bfd-liveness-detection minimum-interval 60<br>
set routing-instances VR2 routing-options static route 10.1.6.0/24 bfd-liveness-detection 
minimum-interval 60<br>


**【AS65001(VR1/VR2)での設定】**<br>

AS65000向けのデフォルトルート並びにループバックアドレスに対するStatic経路をBFDで記述<br>
set routing-instances VR1 routing-options static route 0.0.0.0/0 next-hop 172.16.6.1<br>
set routing-instances VR1 routing-options static route 0.0.0.0/0 bfd-liveness-detection 
minimum-interval 60<br>
set routing-instances VR1 routing-options static route 2.2.2.2/32 next-hop 172.16.6.1<br>
set routing-instances VR1 routing-options static route 2.2.2.2/32 bfd-liveness-detection 
minimum-interval 60<br>

set routing-instances VR2 routing-options static route 0.0.0.0/0 next-hop 172.16.5.1<br>
set routing-instances VR2 routing-options static route 0.0.0.0/0 bfd-liveness-detection 
minimum-interval 60<br>
set routing-instances VR2 routing-options static route 2.2.2.2/32 next-hop 172.16.5.1<br>
set routing-instances VR2 routing-options static route 2.2.2.2/32 bfd-liveness-detection 
minimum-interval 60<br>


#### AS65001内のIGP(OSPF）でデフォルトルートを通知する設定を実施<br>

AS65001内のルータ間はお互いにOSPFで経路を交換していますが、お互いにデフォルトルートを通知しあうことにより<br>
AS65000向けの回線が断になった場合においても迂回してAS65000に接続できるようにします<br>
