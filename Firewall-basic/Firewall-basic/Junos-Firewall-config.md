
## Firewallルール設定について
### Firewallルールの概要
JuniperSRXにおいてはSecurity ZoneとSecurity Policyにより通過するトラヒックを制御します！<br> 
　【Security Zone】<br>
　　インタフェースに割り当てる仮想的なグループ（SRXではZoneを使用）<br> 
  【Security Policy】<br>
  　SRXを通過するトラヒックを制御するためのルール<br> 
### Firewallルール反映までの流れ
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
#### 1 　objectの作成
#### 2　ルールの作成、適用
#### 3　設定の反映
#### 4　ルール設定の例
　以下の状況におけるFirewallルール設定例について紹介します<br>
(1) 定義済みアプリケーションを指定してルールを適用する場合（その１、その２）<br>
　　＊Well-knonwポートを使用するアプリケーション（HTTPなど）に適用する場合<br>
(2) 新たなアプリケーションポート番号を指定し、ルールを適用する場合<br>
　　＊独自アプリケーションなど普段使用しないポート番号に適用する場合<br>
(3) 指定すべきアドレス範囲が点在している場合<br>
　　アドレスブックで指定したいアドレス範囲が点在している。。際に適用する場合<br>
##### (1) 定義済みアプリケーションを指定してルールを適用する場合(その１、その２）
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
   　
##### (2) 新たなアプリケーションポート番号を指定し、ルールを適用する場合
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
   #set security policies default-polices deny-a l<br>　　　　　　　　　　　　　　　　　　　　　　
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

##### (3) 指定すべきアドレス範囲が点在している場合
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
