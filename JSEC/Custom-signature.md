[始めに戻る](./Junos-JSEC-exercises.md) <br>

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
<img width="1031" height="681" alt="image" src="https://github.com/user-attachments/assets/8c8ed8b5-813d-481b-b913-2a6103051178" /><br>


Junosコマンド "show security idp attack table”による確認<br>
<img width="1035" height="691" alt="image" src="https://github.com/user-attachments/assets/cba83292-938c-40c4-af03-5485c1280f90" />

<img width="1033" height="676" alt="image" src="https://github.com/user-attachments/assets/47117caf-2a7d-47a1-b18a-c753242d7e82" />

<img width="1030" height="691" alt="image" src="https://github.com/user-attachments/assets/d3aeb167-f285-4e78-b3e1-3cafc6384842" />


【SRXでの検知情報をSyslogサーバに転送】<br>

<img width="1041" height="644" alt="image" src="https://github.com/user-attachments/assets/b512461f-0be5-4cc3-a18a-4339d2260895" />

<img width="1034" height="634" alt="image" src="https://github.com/user-attachments/assets/86e8a064-9b78-4eb0-8837-aeec304d7872" />

<img width="1024" height="632" alt="image" src="https://github.com/user-attachments/assets/d0c9a09b-b31c-418d-a000-1696702ab552" />

<img width="1024" height="623" alt="image" src="https://github.com/user-attachments/assets/32fd4881-92c4-4de9-a04e-af7bb2d6101d" />
 
　３　カスタムシグニチャ作成/適用例（その２）<br> 
 今回の構成<br>
 <img width="1386" height="684" alt="image" src="https://github.com/user-attachments/assets/3672950f-257e-4b65-8d7f-8604be6928d2" />

 <img width="1382" height="669" alt="image" src="https://github.com/user-attachments/assets/60d7ba58-e299-4154-b1f9-4376ed9a9712" />

<img width="1390" height="684" alt="image" src="https://github.com/user-attachments/assets/8b45b9cb-7411-4ea8-93ea-04874d870629" />

<img width="1388" height="675" alt="image" src="https://github.com/user-attachments/assets/fa95aca5-3524-4e12-83f0-e1771d019d58" />

<img width="1396" height="680" alt="image" src="https://github.com/user-attachments/assets/eead6969-a8e1-42c5-b776-86fba6e2546c" />

<img width="1395" height="695" alt="image" src="https://github.com/user-attachments/assets/6368b304-6e39-4f2c-9068-97e65c6061a9" />

<img width="1387" height="674" alt="image" src="https://github.com/user-attachments/assets/bf5b0617-4e65-4871-8205-8e14a5d7d37a" />








