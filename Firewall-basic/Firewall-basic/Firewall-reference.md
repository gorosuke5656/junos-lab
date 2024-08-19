## SRXのFirewall機能における参考
### アプリケーションにおけるポート番号設定
　SRXにおいては各アプリケーションにおける事前のポート番号が予め設定されています<br> 

 configモードで以下のコマンドにより確認します<br> 
root#show groups junos-defaults applications<br> 

### アプリケーションにおけるコネクション（セッション）タイムアウト値の設定
〇事前にZoneとInterfaceを設定した上で以下の流れで実施します<br> 
　１　Objectの作成<br> 
 　　対象となるアドレス、アプリケーション情報を作成します<br> 
   　　（address-book/addree-setで作成）　→　すべてを選択（any)する場合は必要ありません<br> 
　２　ルールの作成、適用<br> 
 　　通信許可/拒否に関するルール等の追加等を実施します<br> 
   　　（security-policy)<br> 
  ３　設定の反映<br>
  　作成したルールを保存します(commit)<br>
    *注意！： commitしないとSRXに設定情報が反映されません！！<br>
#### 1 　objectの作成
#### 2　ルールの作成、適用
#### 3　設定の反映
