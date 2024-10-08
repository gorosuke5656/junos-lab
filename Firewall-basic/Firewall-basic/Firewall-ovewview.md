# Firewallの概要
[元に戻る](./JunosSRX-Firewall-Basic.md) <br>

## Firewallとは
ファイアウォール（英: Firewall）は、コンピュータネットワークにおいて、ネットワークの結節、コンピュータセキュリティの保護、その他の目的のため、通過させてはいけない通信を阻止するシステムを指す。<br> 

https://ja.wikipedia.org/wiki/%E3%83%95%E3%82%A1%E3%82%A4%E3%82%A2%E3%82%A6%E3%82%A9%E3%83%BC%E3%83%AB<br>

　**【Firewallのイメージ】**<br>
  
  ![Diagram](./image/Firewall-overview.jpg)<br>

## Firewallによるフィルタリング方式
Firewallにおけるフィルタリング方式は以下の３つに分類されます<br> 
１　パケットフィルタリング型（ステートレス）<br> 
　　パケットのヘッタ情報に含まれるIPアドレス、ポート番号に基づいてフィルタリングを行う方式<br> 
  
２　ステートレスインスペクション型（ステートフル）<br>
　　セッション（通信の開始から終了まで管理する単位）の状態を管理して、常にその情報に基づいてフィルタリングを行う。<br>

３　アプリケーションレベルゲートウェイ型<br>
　　プロトコルごとにプロキシ（中継専用プログラム）を持ち、パケットのアプリケーション層も含めた情報に基づいてフィルタリングを行う方式<br>

## ステートフルインスペクション型Firewallの動作
フィルタリングルールとコネクションテーブル（セッションテーブル）双方が連携して動作<br>

フィルタリングルール（管理者が作成）<br> 
どんな通信を許可し、どんな通信を拒否するかを定義する<br> 
　設定項目：<br>
 　送信元IPアドレス、宛先IPアドレス、プロトコル、送信元ポート番号、通信制御（許可/拒否）　などがあります<br> 

 コネクションテーブル（セッションテーブル）（Firewallを通過する通信により動的に作成）<br> 
　Firewallを経由するセッション（コネクション）の情報を管理しているテーブル<br> 
　テーブルの内容：<br>
 　送信元IPアドレス、宛先IPアドレス、プロトコル、送信元ポート番号、宛先ポート番号、コネクションの状態（、アイドルタイムアウト　などがあります<br> 

  

  　**【ステートフルインスペクション形Firewallのイメージ】**<br>
  
  ![Diagram](./image/statefull.jpg)<br>

　**【ステートフルインスペクション形Firewallの動作(その１）】**<br>
　![Diagram](./image/statefull-motion-1.jpg)<br>

 **【ステートフルインスペクション形Firewallの動作(その２）】**<br>
　![Diagram](./image/statefull-motion-2.jpg)<br>

  **【ステートフルインスペクション形Firewallの動作(その３）】**<br>
　![Diagram](./image/statefull-motion-3.jpg)<br>
 

 Juniper SRXのステートフルインスペクション形Firewallの動作についてはこちらで紹介します<br>
[JuniperSRXにおけるFirewallの設定](./Junos-Firewall-config.md) <br>

 　　　　　　　　　　
