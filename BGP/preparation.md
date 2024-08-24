[目次に戻る](./Junos-BGP-exercises.md) <br>

**事前準備で以下を実施します**
*事前準備で以下を実施します*
□工場出荷時設定にして改めてホスト名、rootユーザ/adminユーザを設定<br>

admin@SRX100#load　factory-default<br>
#set system host-name SRX100<br>
#set system root-authentication plain-text-password<br>
 new password:         <br> 
 retype new password:  <br>
#set system login user admin class super-user<br>
#set system login user admin authentication plan-text-password<br>
  Net password:        <br>
  Retype new password:       <br>
commit cheak<br>
commit<br>


□ 純粋にルータ設定に専念したい！のでSecurity設定関係を無効化
#delete secuirty zone security-zone trust interface<br>
#delete secuirty zone security-zone untrust interface<br>
#set secuirty zone secuirty-zone trust interface all<br>
#set secuirty policies default-policy permit-all<br>


□バーチャルルータを２個作成（VR1、VR2）し、収容するインタフェースを設定します<br>。
#set routing-instances VR1 instance-type virtual-router<br>
#set routing-instances VR1　interface fe-0/0/1.0<br>
#set routing-instances VR1　interface fe-0/0/2.0<br>
#set routing-instances VR2 instance-type virtual-router<br>
#set routing-instances VR2　interface fe-0/0/5.0<br>
#set routing-instances VR2　interface fe-0/0/6.0<br>

〇ループバックアドレスを作成し、各VRに割りあて
#set interfaces lo0 unit 0 family inet address 50.5.1.1/32<br>
#set interfaces lo0 unit 1 family inet address 50.6.1.1/32<br>
#set routing-instances VR2 interface lo0.0<br>
#set routing-instances VR1 interface lo0.1<br>


□Policy-Optionsを設定し、各VRのポリシーを許可します（別スライドで説明）<br>
#set policy-options policy-statement from_VR1_to_VR2 term term1 from instance VR1;<br>
#set policy-options policy-statement from_VR1_to_VR2 term term1 then accept;<br>
#set policy-options policy-statement from_VR2_to_VR1 term term1 from instance VR2;<br>
#set policy-options policy-statement from_VR2_to_VR1 term term1 then accept;<br>


〇　その他、必要により設定の削除を実施します。<br>
#delete interface fe-0/0/1 family ethernet-switching　→　fe-0/0/7 まで削除<br>
　　　 　　　　　　（初期化した際にethernet-switchingに設定されているため）<br>



