
# JuniperSRXにおけるFirewallルール設定について　　

[元に戻る](./JunosSRX-Firewall-Basic.md) <br>

## Firewallルールの概要
JuniperSRXにおいてはSecurity ZoneとSecurity Policyにより通過するトラヒックを制御します！<br> 
【Security Zone】<br>
　インタフェースに割り当てる仮想的なグループ（SRXではZoneを使用）<br> 
【Security Policy】<br>
　SRXを通過するトラヒックを制御するためのルール<br>

 **JunosにおけるZoneとSecurity Policyのイメージ**<br>
 ![Diagram](./image/zone,policy.jpg)<br>
   
## Firewallルール反映までの流れ
〇事前にZoneとInterfaceを設定した上で以下の流れで実施します<br> 
　１　Objectの作成<br> 
 　　対象となるアドレス、アプリケーション情報を作成します<br> 
   　　（address-book/addree-setで作成）　→　すべてを選択（any)する場合は必要ありません<br> 
　２　ルールの作成、適用<br> 
 　　通信許可/拒否に関するルール等の追加等を実施します<br> 
   　　（security-policy)<br>　
  ３　設定の反映<br>
  　作成したルールを保存します(commit)<br>
    *注意！： commitしないとSRXに設定情報が反映されません！！<br>

   **JunosにおけるFirewallルール反映までの流れ**<br>
 ![Diagram](./image/Firewall-rule-flow.jpg)<br>
  
### 1 　objectの作成
　ルール適用時の対象サブネット（ホスト）等を指定する際に使用 <br>
(address-bookを複数組み合わせて使用する場合にはaddress-setを使用）<br>

《設定条件の例》<br>
　異なるIPサブネットを複数指定してFirewalポリシーに適用したい。<br>
 ADDRESS BOOKの定義<br>　
 　1.1.1.1/32　　  ⇒　address-book:AAA　として設定<br>　
 　172.16.0.0/16　 ⇒　address-book:BBB  として設定<br>　　
 　192.168.1.0/24　⇒　address-book:CCC　として設定<br>
 ADDRESS SETの定義<br>　　
 　　Address-set:BCSET　⇒　address-book:BBB及びCCCを組み合わせ<br>
   
《設定例》<br>
address-bookを定義<br>
  #set security address-book global address AAA 1.1.1.1/32<br>
  #set security address-book global address BBB 172.16.0.0/16 <br>
  #set security address-book global address CCC 192.168.1.0/24<br>
  #set security address-book global address-set BCSET address BBB <br>
  #set security address-book global address-set BCSET address CCC<br>

address-bookに対して以下のようにaddress-setを適用<br>
  #set security policies from-zone A to-zone B policy policy1 match source-address AAA <br>
  #set security policies from-zone A to-zone B policy policy1 match destination-address BCSET<br>

(参考）<br>
address-book、address-setの適用については以下の２つの方法があります。<br>

1　装置全体で適用する場合<br>
　#set security address-book global address AAA 1.1.1.1/32<br>
　#set security address-book global address BBB 172.16.0.0/16<br> 
　#set security address-book global address CCC 192.168.1.0/24<br>

2 個別のSecurity zoneで適用する場合<br>
　#set security  zones security-zones untrust  address-book address AAA 1.1.1.1/32<br>
　#set security  zones security-zones untrust  address-book address BBB  172.16.0.0/16<br>
　#set security  zones security-zones untrust  address-book address CCC 192.168.1.0/24<br>

 
### 2　ルールの作成、適用
**JunosにおけるFirewallルール（SecurityPolicy）の記述方法**<br>
 ![Diagram](./image/Firewall-rule.jpg)
#### Firewallルールにおけるinsertコマンドについて
一般的にFirewallにおけるルールは先頭に記述したFirewallルールが優先されます。<br>
Juniper SRXも例外ではありません。。<br>

SRXにおいてFirewallルールを入れ替える場合は　"insert”コマンドを使用します！<br>

（設定例）<br>
新規に作成したFirewallルール（ポリシー）”TRUST_UNTRUST_POLICY-0001”を"ALL_DENY"の前に入れ替えます<br>

【新規に適用したいルールを設定します】<br>
 #set security address-book global address UNTRUST_ADD-0001 XXX.XXX.XXX.XXX/XX<br>
 #set security address-book global address-set UNTRUST_ADD_SET-0001 address UNTRUST_ADD-0001<br>
 #set security policies from-zone TRUST to-zone UNTRUST policy TRUST_UNTRUST_POLICY-0001 match 
source-address any<br>
 #set security policies from-zone TRUST to-zone UNTRUST policy TRUST_UNTRUST_POLICY-0001<br> 
match destination-address UNTRUST_ADD_SET-0001<br>
 #set security policies from-zone TRUST to-zone UNTRUST policy TRUST_UNTRUST_POLICY-0001
match application any<br>
 #set security policies from-zone TRUST to-zone UNTRUST policy TRUST_UNTRUST_POLICY-0001 then permit<br>
 
【現行のルールの前に設定したルールを追加します】<br>
#insert security policies from-zone TRUST to-zone UNTRUST policy TRUST_UNTRUST_POLICY-0001 before 
policy ALL_DENY<br>

### 3　設定の反映
commitコマンドにより設定を反映させます<br>
commit checkコマンドによりcommitエラーがないか確認するのもよいでしょう<br>


### 3　JuniperSRXでステートフルインスペクション形Firewallの動作を確認してみましょう！
**JunosにおけるZoneとSecurity Policyのイメージ**<br>
 ![Diagram](./image/Firewall-rule-example1.jpg)<br>


### 4　JuniperSRXにおけるFirewallルール設定の例
　ここでは以下のシーンにおけるFirewallルール設定例について紹介します<br>

(1) 定義済みアプリケーションを指定してルールを適用する場合（その１、その２）<br>
　　＊Well-knonwポートを使用するアプリケーション（HTTPなど）に適用する場合<br>

(2) 新たなアプリケーションポート番号を指定し、ルールを適用する場合<br>
　　＊独自アプリケーションなど普段使用しないポート番号に適用する場合<br>

(3) 指定すべきアドレス範囲が点在している場合<br>
　　アドレスブックで指定したいアドレス範囲が点在している。。際に適用する場合<br>

#### (1) 定義済みアプリケーションを指定してルールを適用する場合(その１、その２）
　【例：HTTP通信のみを許可するルールを作成したい！】<br>
 　　（設定例）<br>
   #set security policies from-zone trust to-zone untrust policy HTTP-permit match source-address any<br>
   #set security policies from-zone trust to-zone untrust policy HTTP-permit match destination-address any<br>
   #set security policies from-zone trust to-zone untrust policy HTTP-permit match application junos-http<br>
   #set security policies from-zone trust to-zone untrust policy HTTP-permit then permit<br>
   #set security policies from-zone untrust to-zone trust policy a l-permit match source-address any<br>
   #set security policies from-zone untrust to-zone trust policy a l-permit match destination-address any<br>
   #set security policies from-zone untrust to-zone trust policy a l-permit match application any<br>
   #set security policies from-zone trust to-zone untrust policy a l-permit then permit<br>
   #Set security policies default-polices deny-all<br>　　　　　　　　　　　　　　　　　　　　　　
                                     /　デフォルトポリシー（廃棄）<br>　　
   　
#### (2) 新たなアプリケーションポート番号を指定し、ルールを適用する場合
 【例１：複数のアプリケーションをまとめて指定したい！】<br>　
    （設定例）<br>
application-setを使用して複数のサーバ（サービス）を選択する<br>
   #set applications application-set MANAGE-SET application junos-ssh<br>
   #set applications application-set MANAGE-SET application junos-telnet<br>
   #set applications application-set MANAGE-SET application junos-telnet<br>
設定したapplication-setを使用してFirewallルールを作成する<br>
   #set security policies from-zone trust to-zone untrust policy Server-permit match source-address any<br>
   #set security policies from-zone trust to-zone untrust policy Server-permit match destination-address any<br>
   #set security policies from-zone trust to-zone untrust policy Server-permit match application MANAGE-SET<br>
   #set security policies from-zone trust to-zone untrust policy Server-permit then permit<br>
   #set security policies from-zone untrust to-zone trust policy a l-permit match source-address any<br>
   #set security policies from-zone untrust to-zone trust policy a l-permit match destination-address any<br>
   #set security policies from-zone untrust to-zone trust policy a l-permit match application any<br>
   #set security policies from-zone trust to-zone untrust policy a l-rejecｔ then permit<br>
   #set security policies default-polices deny-all<br>　　　　　　　　　　　　　　　　　　　　　　
                               /　デフォルトポリシー（廃棄）<br>
                               
【例2：通常使用しないポート番号（Wel-Knownポート以外）を指定したい！】<br>
（設定例）<br>
　　宛先ポートTCP/23000を新たなアプリケーションとして定義（定義名：untrust-server)<br>
  #set applications application untrust-Server protocols tcp source-port 1-65535 destination-port 23000<br>
　　新たなアプリケーションを使用してFirewallルールを作成<br>
  #set security policies from-zone trust to-zone untrust policy Server-permit match source-address any<br>
  #set security policies from-zone trust to-zone untrust policy Server-permit match destination-address any<br>
  #set security policies from-zone trust to-zone untrust policy Server-permit match application untrust-Server<br>
  #Set security policies from-zone trust to-zone untrust policy Server-permit then permit<br>
  #set security policies from-zone untrust to-zone trust policy a l-permit match source-address any<br>
  #set security policies from-zone untrust to-zone trust policy a l-permit match destination-address any<br>
  #set security policies from-zone untrust to-zone trust policy a l-permit match application any<br>
  #Set security policies from-zone trust to-zone untrust policy a l-permit then permit<br>
  #Set security policies default-polices deny-all<br>
                             /　デフォルトポリシー（廃棄）<br>

#### (3) 指定すべきアドレス範囲が点在している場合
（設定例）<br>
点在しているアドレスをrange-addressでそれぞれ定義し、address-setにまとめる<br>
  #set security address-book global address Attaker-1 range-address 130.135.110.101 to 130.135.110.110<br>
  #set security address-book global address Attaker-2 range-address 130.190.100.100 to 130.190.100.103<br>
  #set security address-book global address-set Attaker-segment address Attaker-1<br>
  #set security address-book global address-set Attaker-segment address Attaker-2<br>
address-setにまとめたものを使用してFirewallルールを作成<br>
  #set security policies from-zone untrust to-zone trust policy Attaker-deny match source-address Attaker-segment<br>
  #set security policies from-zone untrust to-zone trust policy Attaker-deny match destination-address any<br>
  #set security policies from-zone untrust to-zone trust policy Attaker-deny match application any<br>
  #set security policies from-zone untrust to-zone trust policy Attaker-deny then deny<br>
  #set security policies default-polices permit-all　<br>　　　　　　　　　　　　　　　　　　　　　
 　　　　　　　　　　　　　　　/　デフォルトポリシー（通過）<br>
### 4　通信中のコネクション（セッション）に対する新規新規Firewallルールを適用
通信中のコネクション（セッション）に対して新たにルールを適用して切断したい！<br>
　　　　　　　　　　　　　　　→　　　　ルールを適用するには各種条件があります！！<br>
#### JunosSRXにおけるPolicy-rematchフラグの設定について
Policy-rematchフラグが有効の場合におけるJunos OSが実行するアクションは以下の通りです<br>
　　　　-ポリシーを挿入する：　影響なし<br>
　　　　-ポリシーのActionフィールドをpermitからdenyまたはrejectのいずれかに変更する<br>
　　　　　　　　　　　　　　　　　　：　既存のセッションがすべてドロップする<br>
　　　　　　　　　　　　　　　　　　　　（すべてのセッションがドロップするためお勧めしません）<br>
　　　　-送信元アドレス、宛先アドレス、アプリケーションフィールドの一部の組み合わせを変更する<br>
　　　　　　　　　　　　　　　　　　：  Junos OSがポリシールックアップを再評価する・・<br>
　　　　　　　　　　　　　　　　　　　　（こちらの方がベスト！）<br>
〇参考資料<br>
  SRXシリーズ スタディガイド　－パート１　第３章　セキュリティポリシー　を参照<br>
                    https://www.juniper.net/assets/jp/jp/local/pdf/others/JNCIS-SEC-1_.pdf<br>
