[目次に戻る](./Junos-BGP-exercises.md) <br>

# Local-Preferrence属性変更による確認
## Local-Preferrence属性とは？？
LOCAL_PREFアトリビュートは、内部ASのIBGPネイバールータに対し、<br>
外部ASに存在するネットワーク宛のトラフィックへの発信元を示すアトリビュート<br>
です。<br>
このアトリビュートはLOCAL_PREFENCEとも呼ばれておりAS内でのローカル優先度を示します<br>

またLOCAL_PREF値はIBGPピアにのみ伝達されて、EBGPピアには伝達されません<br>
（LOCAL_PREF値は自分自身のBGPルータに対し適用される値）<br>
文字通り、宛先ネットワークへのネクストホップのIPアドレスを示すアトリビュートです<br>

### Local-Preferrence属性設定イメージ
　
　次のスライドで動作を説明します
  ![Diagram](./images/Local-preference-1.jpg)<br>
  
  自身のAS(AS3）からAS50に存在するネットワーク(50.0.0.0/16）に通信する状況です<br>
  AS3はAS50向けの経路として異なる２つのAS(AS1/AS2）と接続されています<br>
  今回AS3からAS50向けの経路としてAS1を指定したい場合、上記のようにIBGP設定においてLocal-Preferrenceを設定します<br>
  図のように<br>
  　AS1向けルータにはLocal-Preferrence：200<br>
  　AS2向けルータにはLocal-Preferrence：150<br>
  
  Local-Preferrenceは値の大きい方を優先しますので<br>
  次のスライドのように実際の通信はAS1経由でトラヒックが転送されます<br>
  
  ![Diagram](./images/Local-preference-2.jpg)<br>
  
  
### Local-Preferrence属性変更の設定と確認
  （実施手順）<br>
  【事前確認】<br>
   ①　AS65100のCiscoルータが保有するサブネットをBGPで学習するように設定追加を実施します<br>

   ②　各PODにおいてAS65100のアドレス（200.200.200.0/24)の経路情報を確認します<br>
　　　【先に設定したNEXT-HOP属性の変更はしたままで大丈夫です】<br>

　【設定変更】<br>
　 ①　POD６において200.200.200.0/24の経路にLocal-Preferrenceを200に設定します<br>
　 ②　POD６において200.200.200.0/24に対する経路情報を確認します<br>
　　　　→　どのようになっているでしょうか？？<br>
    ![Diagram](./images/Local-preference-3.jpg)<br>
    ![Diagram](./images/Local-preference-4.jpg)<br>
    ![Diagram](./images/Local-preference-5.jpg)<br>
    ![Diagram](./images/Local-preference-6.jpg)<br>
  
  
 
