# SRXのFirewall機能における参考　　
[元に戻る](./JunosSRX-Firewall-Basic.md) <br>

## アプリケーションにおけるポート番号設定
　SRXにおいては各アプリケーションにおける事前のポート番号が予め設定されています<br> 

 configモードで以下のコマンドにより確認します<br> 
　#show groups junos-defaults applications <br> 


## アプリケーションにおけるコネクション（セッション）タイムアウト値の設定
　SRXにおいては各アプリケーション毎にコネクションのタイムアウト値がそれぞれ設定させています

 
TCPアプリケーションのタイムアウト値を確認する場合は以下で確認します<br> 
　>request pfe execute target fpc0 command "show usp app-def tcp"<br> 

（参考）<br> 
[Juniper]SRX アプリケーション別のタイムアウト設定<br>
 https://www.harumaki.net/2014/01/28/juniper-srx-atimeout-configure/



### Juniper SRX（Junos OS） 非対称ルーティング を許可する方法




　（参考）<br> 
【ネットワーク】Juniper SRX（Junos OS） 非対称ルーティング 疎通不可<br> 
 https://hack2notes.com/495/<br> 
 
[juniper] SRX(JunOS) ルーティング不具合修正(非対称ルートへの対応)<br> 
https://www.harumaki.net/2014/03/31/juniper-srx-junos-routing-troubleshoot/<br> 
  

