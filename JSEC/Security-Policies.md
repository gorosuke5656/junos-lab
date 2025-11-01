![Diagram](./images/security-policy-1.jpg)<br>

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
     
  (3) Loggerコマンドを使用して、Syslogサーバにログが残ることを確認します<br>

２　SRXにおけるSyslog設定<br>
　(1)　SRX100H2での設定及び確認<br>
　　　Security Policyを設定し、SRXの内部ストレージにログを格納します<br>

　(2) SRX100Bでの設定及び確認<br>
　　　Security Policyを設定し、Syslogサーバにログを転送します<br>

 

