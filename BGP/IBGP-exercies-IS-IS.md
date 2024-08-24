
[目次に戻る](./Junos-BGP-exercises.md) <br>

#  AS内でのIBGP設定(IS-IS設定）

### IS-IS とは
IS-ISはOSPFと同様なリンクステートルーティングプロトコル<br>
 リンクステートデータベース（LSDB）により最小経路（SPF）を計算<br>
 もともとOSIにおいてCLNS（Connectionless Network　ServiceのIGPとして制定<br>
　　　　　　　　　　　　　　　　　　　　　　→　IS-ISの情報交換にはOSIパケットを使用<br>
**Intergrated IS-IS(統合IS-IS）とは**<br>
   IETFでTCP/IPに拡張したものでCLNS上でも IP上でも機能するように改良<br>

統合IS-ISでは以下のように使用される<br>
　IPアドレス：　MACアドレスと同様に端末の識別用アドレスとして使用<br>
　NSAP（Network Service Access Point)：<br>
　　　CLNS独自のアドレス。　IS-ISではNSAPを使用してルーティングを実施する<br>
   
（参考）<br>
IS-ISはじめの一歩<br>
     https://www.janog.gr.jp/meeting/janog44/program/isis/<br>
IS-IS　wikipedia<br>
　　　　https://ja.wikipedia.org/wiki/IS-IS<br>

**IS-ISにおけるNSAPアドレスフォーマットについて**

**IS-ISにおけるDISについて**
