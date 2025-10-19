[始めに戻る](./Junos-JSEC-exercises.md) <br>

今回の演習で使用する演習環境は以下のようになっています！！<br>


![Diagram](./images/Exercise-environment.jpg)<br>



VM環境に構成されたUbuntuとVSRXと接続されたSRX100が2方向で対向のSRX100に接続されています<br>
対向のSRXはバーチャルルータ(VR）を使用して１台のSRX100上に２台のSRXを構成しています<br>
対向のSRX側はFast-etherオプション設定により端末が接続されていなくてもLinkUPしています<br>
必要によりAlpineLinuxを接続できるようにしています<br>


SRX100における事前設定（抜粋）<br>

【ゾーンの設定】<br>
〇 Zone：untrust<br>
set security zones security-zone untrust screen untrust-screen<br>
set security zones security-zone untrust host-inbound-traffic system-services all<br>
set security zones security-zone untrust host-inbound-traffic protocols all<br>
set security zones security-zone untrust interfaces fe-0/0/1.0<br>
set security zones security-zone untrust interfaces fe-0/0/3.0<br>

〇　Zone：Trust<br>
set security zones security-zone trust host-inbound-traffic system-services all<br>
set security zones security-zone trust host-inbound-traffic protocols all<br>
set security zones security-zone trust interfaces fe-0/0/0.0<br>



【セキュリティーポリシーの設定】<br>
set security policies from-zone trust to-zone untrust policy trust-to-untrust match source-address any<br>
set security policies from-zone trust to-zone untrust policy trust-to-untrust match destination-address any<br>
set security policies from-zone trust to-zone untrust policy trust-to-untrust match application any<br>
set security policies from-zone trust to-zone untrust policy trust-to-untrust then permit<br>
set security policies from-zone untrust to-zone trust policy untrust-to-trust match source-address any<br>
set security policies from-zone untrust to-zone trust policy untrust-to-trust match destination-address any<br>
set security policies from-zone untrust to-zone trust policy untrust-to-trust match application any<br>
set security policies from-zone untrust to-zone trust policy untrust-to-trust then permit<br>
set security policies default-policy deny-all<br>


【経路情報の設定】<br>
set routing-options static route 0.0.0.0/0 next-hop 172.16.100.1<br>
set routing-options static route 10.1.7.0/24 next-hop 172.16.7.254<br>
set routing-options static route 10.1.8.0/24 next-hop 172.16.8.254<br>


