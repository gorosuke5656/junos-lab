１　SRX100H2の各VRに対して以下の条件でZoneを設定します<br>
　【VR1】<br>
　　　Zone名： Untrust-VR1　対象INF：fe-0/0/3<br>　　　
      Zone名: Trust-VR1　　対象INF :fe-0/0/2<br>
　【VR2】<br>
      Zone名: Untrust-VR2　対象INF:fe-0/0/7<br>　　　
      Zone名: Trust-VR2　　対象INF:fe-0/0/6<br>

２　Zone：Untrustに対してHost-Inbound-Trafficを設定を以下のように設定します<br>
　(1) 設定前　UbuntuからのPING及びSSHは失敗<br>
　(2) 以下のようにHost-inbound-trafficを設定します<br>
 　　　#set security zone security-zone Untrust host-inbound-traffic system service all<br>
  　　 #set security zone security-zone Untrust host-inbound-traffic protocols all<br>
   
   上記を設定後　UbuntuからのPING及びSSHは成功することを確認します<br>
　

３　Zone：Untrustに対してpingを除くアクセスを許可するように変更します<br>
　　【設定内容】<br>
 　　#set security zone security-zone Untrust host-inbound-traffic system-services ping except<br>
   
　　上記設定後、Ubuntu又はVSRXからUntrustに対してsshは成功するがpingが失敗することを確認します<br>　　　

