[始めに戻る](./Junos-JSEC-exercises.md) <br>

 ### Security-policy設定の構成<br>

![Diagram](./images/Security-policy-1.jpg)<br>

【事前準備】<br>
１　Linux（Ubuntu）において以下の設定及び確認を実施します
　(1) Python2を使用して簡易Webサーバーを起動します<br>
　(2) Syslogサーバーを設定及び起動します<br>
 　　〇 設定ファイル　”/etc/rsyslog.conf”に以下の内容を編集/追加<br>
　　　(ア)　ファイルの下記2行をコメントアウトし有効にする<br>
　　　　　module(load="imudp")<br>
　　　　　input(type="imudp" port="514")<br>
　　 （イ）　下記の設定を追加する<br>
　　　　　#SRX100-Flow-Log<br>　
　　　　　　if $msg contains 'RT_FLOW' then \ <br>		
　　　　　　　　		                                    /var/log/PolicyLog.log<br>
　　　　　　/' RT_FLOW 'が含まれているメッセージをログに記録する<br>
　　　
   　〇 rsyslogデーモンを再起動する<br>
　　　　　$sudo service rsyslog restart<br>
     〇rsyslogサーバーの起動状態の確認<br>
       ![Diagram](./images/Security-policy-5.jpg)<br>  
     
  (3) Loggerコマンドを使用して、Syslogサーバにログが残ることを確認します<br>
  　![Diagram](./images/Security-policy-4.jpg)<br>

２　SRXにおけるSyslog設定<br>
　(1)　SRX100H2(VR設定あり）での設定及び確認<br>
　　　Security Policyを設定し、SRXの内部ストレージにログを格納します<br>
　【関連設定】


　(2) SRX100(VR設定なし）での設定及び確認<br>
　　　Security Policyを設定し、Syslogサーバにログを転送します<br>

　【関連設定】<br>
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
    


    
   

 

