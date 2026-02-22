[始めに戻る](./Junos-JSEC-exercises.md) <br>

 ### Security-policy設定の構成<br>
<img width="1044" height="732" alt="image" src="https://github.com/user-attachments/assets/7e2ec66a-d21a-46c4-9663-0f01a7231915" />


今回はSRX100(VR設定なし）とSRX100(VR設定あり：VR2）のみSecuirty-policy及びSyslog設定を実施します<br>

#### 【事前準備】<br>
１　Linux（Ubuntu）において以下の設定及び確認を実施します<br>
　(1) Python2を使用して簡易Webサーバーを起動します<br>
　　　<img width="1041" height="690" alt="image" src="https://github.com/user-attachments/assets/d3033a24-77fe-4103-b7ce-56bfff7a10dc" />

　(2) Syslogサーバーを設定及び起動します<br>
 　　〇 設定ファイル　”/etc/rsyslog.conf”に以下の内容を編集/追加<br>
　　　<img width="1023" height="637" alt="image" src="https://github.com/user-attachments/assets/752a57ca-f066-44b9-bde1-f6b11b6aafb9" />
   
  　〇rsyslogサーバーの状態確認<br>
   <img width="1038" height="647" alt="image" src="https://github.com/user-attachments/assets/d79a73c2-929b-4afd-932d-2de8ddf1a75d" />
     
  (3) Loggerコマンドを使用して、Syslogサーバにログが残ることを確認します<br>
  　<img width="1038" height="633" alt="image" src="https://github.com/user-attachments/assets/79b1f881-309a-4893-a1d0-a37d6f803b8c" />


２　SRXにおけるSecuirty-policy設定及びSyslog設定<br>
　(1)　SRX100H2(VR設定あり）での設定及び確認<br>
　　　Security Policyを設定し、SRXの内部ストレージにログを格納します<br>

#### 【設定手順】<br>
   <img width="1039" height="690" alt="image" src="https://github.com/user-attachments/assets/dcd878c2-00aa-449a-8bfe-1fb37e6409ed" />

#### 【設定内容】<br>
<img width="1040" height="687" alt="image" src="https://github.com/user-attachments/assets/fc3cce7f-a330-4d35-a22a-335c11528ccb" />

<img width="1030" height="676" alt="image" src="https://github.com/user-attachments/assets/7e95ba91-07e5-4de3-95af-d75aa529be1b" />

<img width="1035" height="684" alt="image" src="https://github.com/user-attachments/assets/16ad05ad-fdfb-40c0-8e40-91793ccda4b2" />

#### 【設定後の確認】<br>

<img width="1047" height="785" alt="image" src="https://github.com/user-attachments/assets/ff14f7e3-a8aa-4c14-b6a1-10b55f907dfd" />

<img width="1040" height="784" alt="image" src="https://github.com/user-attachments/assets/532b4cf2-9732-4d8e-bf98-9504c2212c0c" />

<img width="1041" height="785" alt="image" src="https://github.com/user-attachments/assets/a942e827-f6df-4d04-b841-843fe76daff3" />

##### Secuirty　Policies設定およびSyslog設定<br>
１　SRX100BにおいてUntrust⇔Trust間の全ての通信を許可及びセッションログを残す設定を実施します<br>
２　SRX100Bにおいてsyslog設定（内部及びsyslogサーバ）を実施します<br>
３　UbuntuからSRX100BH（VR2）に対してpingを送信します<br>
４　SRX100Bにおいて内部ログがあるかを確認します<br>
　　 Syslogサーバ（Ubunｔu）においてもログがあるかを確認します<br>

<img width="1054" height="789" alt="image" src="https://github.com/user-attachments/assets/3e6af81c-dae1-49f8-8f80-8c1f78656085" />

<img width="1037" height="790" alt="image" src="https://github.com/user-attachments/assets/cd173abc-44c1-4e8a-9cd1-0716222aadd2" />

<img width="1050" height="785" alt="image" src="https://github.com/user-attachments/assets/bf459208-c7fd-4ec1-99e0-5eb0bfe8720d" />

<img width="1054" height="795" alt="image" src="https://github.com/user-attachments/assets/6eeeefd0-0855-4beb-b8c2-fe9d5dfb8c0d" />

<img width="1040" height="780" alt="image" src="https://github.com/user-attachments/assets/2af95eb3-0422-4f97-8644-dd9b74ce1b66" />

<img width="1040" height="789" alt="image" src="https://github.com/user-attachments/assets/d91949e0-fe49-4c49-a6d4-2c176e7fdd6d" />

<img width="1045" height="782" alt="image" src="https://github.com/user-attachments/assets/5ae9ad91-fcf3-4a9e-a45f-77349e81e88c" />

<img width="1043" height="782" alt="image" src="https://github.com/user-attachments/assets/43ad9a66-78e4-41e0-9bc2-6344ca3125ad" />

<img width="1035" height="693" alt="image" src="https://github.com/user-attachments/assets/8d77e776-88c1-44e8-9520-34d670be17a4" />











   
