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

