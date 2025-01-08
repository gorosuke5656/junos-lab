[目次に戻る](./Junos-BGP-exercises.md) <br>

# NEXT-HOP属性変更による確認

##NEXT-HOP属性とは？？
文字通り、宛先ネットワークへのネクストホップのIPアドレスを示すアトリビュートです<br>

###IGPとの考え方の違い<br>

ASに到達するためのIPアドレス　→　ネクストホップ<br>


###EBGPピアとIBGPピアにそれぞれアドバタイズする際の動作の違い。

　EBGPピアにアドバタイズ<br>
  →　NEXT_HOPアトリビュートを自分のIPアドレスにして送信<br>
　
　IBGPピアにアドバタイズ<br>
　→　NEXT_HOPアトリビュートを変更せずにルートを送信<br>
　
　次のスライドで説明します
  ![Diagram](./images/NEXT-HOP-1.jpg)<br>
  
  図に示す通り、AS1とAS2がEBGPで接続されています。
  　AS１からEBGPで経路情報を受け取ったAS2のR2はAS2のR3に対してIBGPで経路を広告しますが
  　R2の動作は以下になります<br>
  　 →　R1から受け取った経路情報をR3（IBGP接続）への広報する際ははBGPのNEXT-HOP属性を変更せずに通知
  　
 　　R3はR2経由で受け取った50.0.0.0/16を学習しますが、R3から50.0.0.0/16へ到達するためには
 　　1.0.0.0/24の経路を知っておく必要があります。。
 　　
 　　 
  
  
  
  
  
  
 
![Diagram](./images/bfd-1.jpg)<br>
  
  ![Diagram](./images/bfd-2.jpg)<br>
  
  ![Diagram](./images/bfd-3.jpg)<br>
  
  ![Diagram](./images/bfd-4.jpg)<br>
  
  ![Diagram](./images/bfd-5.jpg)<br>
  
  ![Diagram](./images/bfd-6.jpg)<br>

