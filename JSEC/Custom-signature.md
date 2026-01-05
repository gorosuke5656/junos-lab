### Junosにおけるカスタムシグニチャ設定と確認<br>

１　カスタムシグニチャ作成/投入までの流れ<br>
　<img width="1027" height="682" alt="image" src="https://github.com/user-attachments/assets/b0552b8a-fbdb-4784-a47f-53da3704a69b" />

２　カスタムシグニチャ作成/適用例（その１）<br>
　今回確認した構成<br>
 <img width="1037" height="686" alt="image" src="https://github.com/user-attachments/assets/4399ac43-d689-4ed9-9a37-a61f59c321d6" />

【事前準備】<br>
<img width="1028" height="645" alt="image" src="https://github.com/user-attachments/assets/8a2b17d8-c52a-4d9d-ba33-1074fc77887b" />

今回は追加で以下の設定も実施<br> 
<img width="1041" height="695" alt="image" src="https://github.com/user-attachments/assets/10e7dc64-0476-462d-af2a-a24c2a9698a2" />


事前準備後の確認　⇒　Linux(Ubuntu）からのCurlコマンドによりWebアクセスが可能！！<br>
<img width="1034" height="683" alt="image" src="https://github.com/user-attachments/assets/b0250ed3-8de0-428f-a371-b68ed5fe3fb0" /><br>

【シグニチャ作成及び適用】<br>
<img width="1033" height="696" alt="image" src="https://github.com/user-attachments/assets/96d27029-d58d-48f3-81f8-4f30fe337f5b" />


<img width="1022" height="672" alt="image" src="https://github.com/user-attachments/assets/e084d122-daf6-42e7-bafa-938ff1c8d652" /><br>

【検知確認】<br>

<img width="1039" height="679" alt="image" src="https://github.com/user-attachments/assets/d2bb3bd5-9a4a-4419-b921-a46d6b44c205" /><br>

Junosコマンド "show security flow session”による確認<br>

<img width="1031" height="681" alt="image" src="https://github.com/user-attachments/assets/8c8ed8b5-813d-481b-b913-2a6103051178" />



 
　３　カスタムシグニチャ作成/適用例（その２）


