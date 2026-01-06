## SRX100の基本操作について<br>
### １　SRX100とは？<br>
SRX100は1Uのコンパクト設計でありながら、最大で700Mbpsのファイアウォール、75MbpsのVPN、60MbpsのIPSをサポートします<br>
また、アンチスパム、アンチウイルス、WebフィルタリングなどのUTM機能も同時に提供可能（ライセンスが必要です！）<br>

<img width="976" height="454" alt="image" src="https://github.com/user-attachments/assets/b74300f6-1581-408a-bd9c-133f588273f6" />

### 2  SRX100基本操作<br>
 (1) SRX100へのログイン<br>

 (2) 起動方法及び停止方法
 停止時の動作<br>
 "request system power-off"コマンドにより電源停止を実施しましょう<br>
 <img width="1044" height="600" alt="image" src="https://github.com/user-attachments/assets/573a3e19-4555-4ee8-80d0-3c74163a5b9d" />

### 3 事前準備<br>
以下の４つについて説明します<br>
(1) passwordリカバリーを実施する<br> 
  SRXシリーズデバイスの root パスワードを忘れた場合は、パスワードリカバリを使用して root パスワードをリセットすることができます<br> 
  この手順では、ウォッチドッグを無効にして、システムがシングルユーザーモードで 適切に起動できるようにします<br>

  <img width="1016" height="588" alt="image" src="https://github.com/user-attachments/assets/9bf60b09-1ae4-4acb-ae21-da9ba83fceff" />

（設定例）<br>

<img width="1028" height="688" alt="image" src="https://github.com/user-attachments/assets/d80fa1f0-2a02-479b-b3b7-5b2ac96dec19" />
<img width="1042" height="689" alt="image" src="https://github.com/user-attachments/assets/86a0a4a5-484d-4dc8-966c-bf5621cf158b" />
<img width="1037" height="658" alt="image" src="https://github.com/user-attachments/assets/5d2d8f80-4e6d-4676-bd2e-e2ba93a15881" />
<img width="1028" height="683" alt="image" src="https://github.com/user-attachments/assets/b2bd5786-4883-4d28-aedb-a8ae9a822af7" />

(2) rootパスワード及び管理者パスワードを設定する<br>

<img width="946" height="595" alt="image" src="https://github.com/user-attachments/assets/fd7631d1-77e6-4dc3-9a27-991391a38e66" />

(3) deleteコマンドにより設定を初期化する<br>

<img width="798" height="472" alt="image" src="https://github.com/user-attachments/assets/7313fb78-11a2-4c1a-97a6-eed22971ba9b" /><br>
　　⇒　注意事項：このままcommitしてもエラーになるので注意しましょう！！<br> 
　　　（最低限rootパスワード設定を実施しないとcommitできません！）<br>


(4) commitにより設定を反映する<br>



### 4 各種設定紹介
 (1) バーチャルルータ（VR）の設定と確認<br>
  バーチャルルータとは、仮想的なルータのことです。これにより、1つの物理的な SRX上に複数の仮想的なルータを存在させることができるので、<br>
  バーチャルルータの数だけ独自のルーティングテーブルを保持することができます。SRXでは、機種ごとにバーチャルルータの最大数が異なります。<br>
   SRX100の場合 3 です ⇒　と言われていますが。。３以上バーチャルルーターを設定できそうです！<br>

#### バーチャルルータの設定例<br>
ここでは、SRX100１台に３つのバーチャルルータ(VR）を設定し、確認した例を紹介します！<br> 
〇　今回の構成図<br>
<img width="1054" height="784" alt="image" src="https://github.com/user-attachments/assets/f1abfacc-6f81-44f2-94cb-785a6f974c35" /><br>

上図の通り３つのバーチャルルータを設定します。　ルーティングプロトコルはIS-ISを使用します<br>

今回は、対向装置が接続されていないインタフェースを強制的にUPさせます！<br>
<img width="1040" height="779" alt="image" src="https://github.com/user-attachments/assets/fe6f43b7-da9a-4a42-a05e-6a6218f54adc" /><br>

【例：Fe-0/0/5を強制的にUP】
<img width="1043" height="705" alt="image" src="https://github.com/user-attachments/assets/71ee74f7-cc17-4270-a7e8-2b885db00ab3" /><br>

〇 今回の設定<br>
<img width="974" height="567" alt="image" src="https://github.com/user-attachments/assets/ea5016f8-6e9c-4434-9d1e-3142936cb327" />

今回の設定要領<br>
<img width="1043" height="681" alt="image" src="https://github.com/user-attachments/assets/28208255-5dc1-4ecb-afbb-eb684992da82" />

 Routingに専念するためにセキュリティ設定を無効化します<br>
 <img width="1032" height="174" alt="image" src="https://github.com/user-attachments/assets/7d2d515a-4bb0-47fb-8184-3cd5bef25b99" />

　SRX1台で3つのバーチャルルータ-（VR）に設定します<br>
 <img width="1033" height="286" alt="image" src="https://github.com/user-attachments/assets/e5bebc90-37ab-4fb5-bced-89787929655c" />

  ループバックアドレスを作成し、各VRに割りあてます<br>
<img width="1034" height="259" alt="image" src="https://github.com/user-attachments/assets/fcf965bf-72e8-40bd-933e-af00824116ec" />

　Policy-Optionsを設定し、各VRのポリシーを許可します<br>
 <img width="1028" height="658" alt="image" src="https://github.com/user-attachments/assets/f08b7f29-74b9-4a93-be55-241ada9661c2" />

 ３台のVRに対してIS-IS設定を実施します<br>
 <img width="1031" height="694" alt="image" src="https://github.com/user-attachments/assets/df873fa0-7d4b-4e32-b8f7-a91364ca9c9b" />

 設定後、IS-IS関連コマンドで確認します<br>
 (1)  show isis overview<br>
 <img width="1015" height="693" alt="image" src="https://github.com/user-attachments/assets/c60fc1ab-217a-4f6a-bc2b-01dba7b30543" />
 (2)  show isis adjacency<br>
 <img width="1033" height="667" alt="image" src="https://github.com/user-attachments/assets/47f54936-4b92-4713-ae82-e056e4076cab" />
 (3)  show isis database<br>
 <img width="1022" height="666" alt="image" src="https://github.com/user-attachments/assets/56176f0c-3d95-44b6-b8f7-787772f6996e" />

#### IS-ISのパケットを取得<br>
<img width="1037" height="751" alt="image" src="https://github.com/user-attachments/assets/94281363-0b8c-4d53-806a-4927b36c4f53" />
<img width="1051" height="741" alt="image" src="https://github.com/user-attachments/assets/5a83a7af-eae2-491b-813c-e2ad5fcc17e3" />
<img width="1044" height="738" alt="image" src="https://github.com/user-attachments/assets/75202268-59bf-4772-81fb-1e5feb974a5c" /><br>

バーチャルルーターを実施した今回の内容は以下のブログでも紹介しています！！<br> 

JuniperSRXのバーチャルルーターを使ってみる<br>
https://gorosuke5656.hatenablog.com/entry/2025/09/14/122216<br>



### ５　参考資料
　(1)　レスキューconfigについて<br> 
　(2)  インタフェースの強制UP方法<br> 
　(3)　内部INFを使用したバーチャルルータ（ＶＲ）設定<br> 
  (4)  SRXの初期化要領について<br> 
　(5)　Configファイルの保存及び読み出し<br> 
　(6)　リモートホストへのSSH接続時でwarningが出た場合の対処例<br> 

