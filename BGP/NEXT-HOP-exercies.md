[目次に戻る](./Junos-BGP-exercises.md) <br>

# NEXT-HOP属性変更による確認
## NEXT-HOP属性とは？？
文字通り、宛先ネットワークへのネクストホップのIPアドレスを示すアトリビュートです<br>

### IGPとの考え方の違い<br>
 ASに到達するためのIPアドレス　→　ネクストホップ<br>
### EBGPピアとIBGPピアにそれぞれアドバタイズする際の動作の違い。
　EBGPピアに対して経路を広告する場合<br>
  　　→　NEXT_HOPアトリビュートを自分のIPアドレスにして送信<br>
　IBGPピアに対して経路を広告する場合<br>
　　　→　NEXT_HOPアトリビュートを変更せずにルートを送信<br>
　
　次のスライドで動作を説明します
  ![Diagram](./images/NEXT-HOP-1.jpg)<br>
  
  図に示す通り、AS1とAS2がEBGPで接続されています<br>
  　AS１からEBGPで経路情報を受け取ったAS2のR2はAS2のR3に対してIBGPで経路を広告しますが<br>
  　R2の動作は以下になります<br>
  　 →　R1から受け取った経路情報をR3（IBGP接続）への広報する際ははBGPのNEXT-HOP属性を変更せずに通知<br>
  　
 　　R3はR2経由で受け取った50.0.0.0/16を学習しますが、R3から50.0.0.0/16へ到達するためには<br>
 　　1.0.0.0/24の経路を知っておく必要があります。。<br>

   以下の方法で解決が可能ですが、
    ![Diagram](./images/NEXT-HOP-2.jpg)<br>
   
   (3)のNEXT-HOP属性を変更することにより疎通が可能です！<br>
  　 
　　(3)のNEXT-HOP属性を変更した場合のイメージを下記に示します。<br>
  　 ![Diagram](./images/NEXT-HOP-3.jpg)<br>

   ### NEXT-HOP属性変更の設定と確認
  （実施手順）<br>
  【事前準備】<br>
　　AS65001への経路確認を確認します<br>
　　　ア　各ルータからAS65001向けの経路情報<br>
　　　イ　AS65001（2.2.2.2）からの受信経路<br>
  【Next-Hop属性機能確認】<br>
     〇 回線断を模擬します<br>
　　 　　　VR2においてCORE向けインタフェースのDownを実施<br>
     〇 回線断におけるAS65001(VR2)のBGP経路情報の確認します<br>
     〇 Next-Hop属性変更によるPolicy設定の実施します<br>
     〇 Next-Hop属性変更後におけるAS65001(VR2)のBGP路情報の確認します<br>
  【現状復帰】
     回線断を復旧させます<br>

  【事前準備】<br>
　 　AS65001への経路確認を確認します<br>
   ![Diagram](./images/NEXT-HOP-4.jpg)<br>
   ![Diagram](./images/NEXT-HOP-5.jpg)<br>
   ![Diagram](./images/NEXT-HOP-6.jpg)<br>
   ![Diagram](./images/NEXT-HOP-7.jpg)<br>
    【Next-Hop属性機能確認】<br>
     〇 回線断を模擬します<br>
　　 　　　VR2においてCORE向けインタフェースのDownを実施<br>
    ![Diagram](./images/NEXT-HOP-7.jpg)<br>
　（障害による回線断を想定）<br>
[edit]<br>
admin@SRX100H2# set interfaces fe-0/0/0 disable<br>
[edit]<br>
admin@SRX100H2# commit<br>
commit complete<br>
[edit]<br>
admin@SRX100H2#<br>

![Diagram](./images/NEXT-HOP-8.jpg)<br>
![Diagram](./images/NEXT-HOP-9.jpg)<br>
![Diagram](./images/NEXT-HOP-10.jpg)<br>
![Diagram](./images/NEXT-HOP-11.jpg)<br>
![Diagram](./images/NEXT-HOP-12.jpg)<br>
![Diagram](./images/NEXT-HOP-13.jpg)<br>
![Diagram](./images/NEXT-HOP-14.jpg)<br>
![Diagram](./images/NEXT-HOP-15.jpg)<br>


     


    
  

  
  
 

