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

###　3 事前準備<br>
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

<img width="798" height="472" alt="image" src="https://github.com/user-attachments/assets/7313fb78-11a2-4c1a-97a6-eed22971ba9b" />
　　⇒　注意事項：このままcommitしてもエラーになるので注意しましょう！！<br> 
　　　（最低限rootパスワード設定を実施しないとcommitできません！）<br>


(4) commitにより設定を反映する<br>



### 4 各種設定紹介
 (1) バーチャルルータ（VR）の設定と確認<br>
 (2) セキュリティ設定の解除<br> 

### ５　参考資料
　(1)　レスキューconfigについて<br> 
　(2)  インタフェースの強制UP方法<br> 
　(3)　内部INFを使用したバーチャルルータ（ＶＲ）設定<br> 
  (4)  SRXの初期化要領について<br> 
　(5)　Configファイルの保存及び読み出し<br> 
　(6)　リモートホストへのSSH接続時でwarningが出た場合の対処例<br> 

