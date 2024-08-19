## SRXのFirewall機能における参考　　[元に戻る](./JunosSRX-Firewall-Basic.md) <br>
### アプリケーションにおけるポート番号設定
　SRXにおいては各アプリケーションにおける事前のポート番号が予め設定されています<br> 

 configモードで以下のコマンドにより確認します<br> 
root#show groups junos-defaults applications<br> 

### アプリケーションにおけるコネクション（セッション）タイムアウト値の設定
　SRXにおいては各アプリケーション毎にコネクションのタイムアウト値がそれぞれ設定させています
 
ＴＣＰアプリケーションのタイムアウト値を確認する場合は以下で確認します<br> 
root > request pfe execute target fpc0 command "show usp app-def tcp"<br> 
  

