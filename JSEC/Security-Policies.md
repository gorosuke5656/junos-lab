[始めに戻る](./Junos-JSEC-exercises.md) <br>

 ### Security-policy設定の構成<br>

![Diagram](./images/Security-policy-1.jpg)<br>

今回はSRX100(VR設定なし）とSRX100(VR設定あり：VR2）のみSecuirty-policy及びSyslog設定を実施します<br>

【事前準備】<br>
１　Linux（Ubuntu）において以下の設定及び確認を実施します
　(1) Python2を使用して簡易Webサーバーを起動します<br>
　　　<img width="1041" height="690" alt="image" src="https://github.com/user-attachments/assets/d3033a24-77fe-4103-b7ce-56bfff7a10dc" />

　(2) Syslogサーバーを設定及び起動します<br>
 　　〇 設定ファイル　”/etc/rsyslog.conf”に以下の内容を編集/追加<br>
　　　<img width="1023" height="637" alt="image" src="https://github.com/user-attachments/assets/752a57ca-f066-44b9-bde1-f6b11b6aafb9" />
   
     〇 rsyslogサーバーの起動状態の確認<br>
   <img width="1038" height="647" alt="image" src="https://github.com/user-attachments/assets/d79a73c2-929b-4afd-932d-2de8ddf1a75d" />
     
  (3) Loggerコマンドを使用して、Syslogサーバにログが残ることを確認します<br>
  　![Diagram](./images/Security-policy-4.jpg)<br>

２　SRXにおけるSecuirty-policy設定及びSyslog設定<br>
　(1)　SRX100H2(VR設定あり）での設定及び確認<br>
　　　Security Policyを設定し、SRXの内部ストレージにログを格納します<br>
　【設定手順】<br>
    <img width="1039" height="690" alt="image" src="https://github.com/user-attachments/assets/dcd878c2-00aa-449a-8bfe-1fb37e6409ed" />
　　　（細部は別スライド）<br>　
　　　
　〇　通信を発生させSRX100（VR2）の内部ログに残るかを確認します<br>
【設定結果】<br>
　　ア）Policyで使用するAddressbookを作成します<br>
  　　set security zones security-zone untrust-VR2 address-book address Server-net 130.230.0.0/24<br>
　　　set security zones security-zone trust-VR2 address-book address Client-Net 10.1.7.0/24<br>

    イ）
 
 　　(2) SRX100(VR設定なし）での設定及び確認<br>
　　　Security Policyを設定し、Syslogサーバにログを転送します<br>
　【設定】
　【設定結果】<br>
  　 （Security-Policy設定)<br>
     admin@SRX100> show configuration security policies | display set<br>
     set security policies from-zone trust to-zone untrust policy trust-to-untrust match source-address any<br>
     set security policies from-zone trust to-zone untrust policy trust-to-untrust match destination-address any<br>
     set security policies from-zone trust to-zone untrust policy trust-to-untrust match application any<br>
     set security policies from-zone trust to-zone untrust policy trust-to-untrust then permit<br>
     set security policies from-zone untrust to-zone trust policy untrust-to-trust match source-address any<br>
     set security policies from-zone untrust to-zone trust policy untrust-to-trust match destination-address any<br>
     set security policies from-zone untrust to-zone trust policy untrust-to-trust match application any<br>
     set security policies from-zone untrust to-zone trust policy untrust-to-trust then permit<br>
     set security policies default-policy deny-all<br>
    
　　（Syslog設定）<br>
       admin@SRX100> show configuration system syslog | display set<br>
                     set system syslog host 130.230.0.1 user info<br>
                     set system syslog host 130.230.0.1 source-address 172.16.100.254<br>
                     set system syslog file Policylog user info<br>
                     set system syslog file Policylog explicit-priority<br>
    


    
   

 

