# Juniper EX-L2/L3-basic-lab<br>
### LastUpdate:2026/10/03<br>


# １　実習構成<br>
## 構成はEX2200が3台になります。me0（管理インタフェース）経由で設定します<br>
### 構成図
<img width="1380" height="679" alt="image" src="https://github.com/user-attachments/assets/87d506b2-1c44-4f91-ab11-adcf92025c94" />

### 今回使用するJunos Ver
<img width="1387" height="567" alt="image" src="https://github.com/user-attachments/assets/6a0f6e19-7fd7-4109-8c58-c42d8e15d917" />

# ２ 　#Juniper EX-L2/L3-basic-labで取り上げる内容<br>
 - [(1) 基本設定と確認](#system-basic-conf)<br>
 - [(2) LLDP設定と確認](#lldp-conf)<br>  
 - [(3) RSTP/STP設定と確認](#rstp-stp-conf)<br>
 - [(4) VLAN設定と確認](#vlan-conf)<br>
 - [(5) LAG設定と確認](#lag-conf)<br>
 - [(6) RTG設定と確認](#rtg-conf)<br>
 - [(7) 経路制御設定と確認](#ospf-conf)<br>
 - [(8) Firewall-filter設定と確認](#firewall-filter-conf)<br>
 - [(9) Virtual-chassis設定と確認](#Virtual-chassis-conf)<br>

 # 【参考資料】<br>
- [EX2200におけるJunosアップグレード方法](#ex2000-junos-verup)<br>

# system-basic-conf
<img width="1383" height="674" alt="image" src="https://github.com/user-attachments/assets/361067a9-90cb-479f-b609-227668cb8cf1" />


# lldp-conf
## 参考資料<br>
### lldpの概要<br>
 https://www.juniper.net/documentation/jp/ja/software/junos/multicast-l2/topics/concept/layer-2-services-lldp-overview.html<br>
### lldpの設定<br>
https://www.juniper.net/documentation/jp/ja/software/junos/multicast-l2/topics/task/layer-2-services-lldp-configuring.html<br>
 
<img width="1382" height="672" alt="image" src="https://github.com/user-attachments/assets/e0a92581-7efe-43f5-b265-8c1055160c82" />

<img width="1393" height="676" alt="image" src="https://github.com/user-attachments/assets/98036695-89b8-42ca-9d84-9d9d3a97a564" />

<img width="1388" height="662" alt="image" src="https://github.com/user-attachments/assets/c55ee808-bb84-4ef9-b01f-043c872d0754" />

<img width="1389" height="675" alt="image" src="https://github.com/user-attachments/assets/ce4095e6-5320-4e40-ad6a-50d20f7b8405" />

<img width="1386" height="679" alt="image" src="https://github.com/user-attachments/assets/a2f3698e-3aac-4401-b766-5da7dbb669ce" />

<img width="1389" height="686" alt="image" src="https://github.com/user-attachments/assets/88514362-b582-4a1a-9435-69f0a0a2e521" />

<img width="1385" height="604" alt="image" src="https://github.com/user-attachments/assets/29bbea15-5c5a-4eca-acbc-061b749b3f5d" />

<img width="1388" height="689" alt="image" src="https://github.com/user-attachments/assets/58c5a7cc-f510-4e29-8bcf-0fd25b4b28b4" />

<img width="1394" height="655" alt="image" src="https://github.com/user-attachments/assets/c6efff51-7633-4b91-899b-71a23da83a97" />

#### LLDP設定後の確認<br>
<img width="1390" height="628" alt="image" src="https://github.com/user-attachments/assets/3e6457c4-475e-4ec2-960d-6d70e7b46a47" />

<img width="1392" height="673" alt="image" src="https://github.com/user-attachments/assets/f90997db-d4e8-4c76-aba9-c6f53f4f608d" />

<img width="1392" height="674" alt="image" src="https://github.com/user-attachments/assets/1dd785f9-afaa-4c28-8d3f-d6f343a64d3d" />

#### LLDPでこんなこともわかりました！<br>
<img width="1394" height="629" alt="image" src="https://github.com/user-attachments/assets/e50c2881-07aa-42bc-a90e-965c7a5bc0d9" />

<img width="1393" height="646" alt="image" src="https://github.com/user-attachments/assets/dfbaba28-f518-4028-a007-014161bed459" />

#### LLDPのパケットを取得してみましょう！<br>
<img width="1387" height="671" alt="image" src="https://github.com/user-attachments/assets/c699a106-e78a-4ac9-a5cf-cfb3e5f7af69" />

#### 【monitor traffic コマンドについて】<br>

https://www.juniper.net/documentation/jp/ja/software/junos/network-mgmt/topics/topic-map/analyze-network-traffic-by-using-packet-capture.html<br>

> **注意**
>
> `monitor traffic interface` は、指定したインタフェースを通過する
> **すべてのパケットをキャプチャできる機能ではありません。**
>
> Junos の `monitor traffic` は、主に **Routing Engine（RE）に関連する
> トラフィック**を対象としています。
>
> そのため、通常の **Transit Traffic** のキャプチャには利用できません。
>
> #### 今回はLLDPパケットをキャプチャしてみます！

今回確認する **LLDP** は、スイッチ自身が送受信する制御系のフレームです。

そのため、`monitor traffic` を使用して **LLDPDU（LLDP Data Unit）を
キャプチャし、実際のパケットを確認することができます。**

> **ポイント**
>
> - LLDPなど、スイッチ自身が送受信する制御系トラフィック
>   → `monitor traffic` で確認可能
> - 通常のTransit Traffic
>   → `monitor traffic` では確認できない
> - Transit Trafficを確認したい場合
>   → **ポートミラーリング**を利用する

　　
　関連ドキュメント<br>

　https://www.juniper.net/documentation/us/en/software/junos/cli-reference/topics/ref/command/monitor-traffic.html?utm_source=chatgpt.com<br>


公式説明に、"Display packet headers or packets received and sent from the Routing Engine."とあります～<br>

<img width="1387" height="682" alt="image" src="https://github.com/user-attachments/assets/940f1720-f573-4abf-b0aa-411f2889f325" />

<img width="1384" height="639" alt="image" src="https://github.com/user-attachments/assets/a0ebfcad-1c1f-45ef-bbac-aac27dcd8acc" />

<img width="1392" height="639" alt="image" src="https://github.com/user-attachments/assets/a0569935-f144-403e-b31f-f333eff60573" />

##### monitor traffic コマンドでSizeオプションを使用<br>
<img width="1390" height="606" alt="image" src="https://github.com/user-attachments/assets/9f17d10d-935d-44ae-b2dd-59f004ca45bd" />

<img width="1391" height="639" alt="image" src="https://github.com/user-attachments/assets/ed0ec388-abf4-48bd-a90f-d0b2ddb7d05e" />


# rstp-stp-conf




# vlan-conf
#### 今回の構成 <br>
<img width="1392" height="736" alt="1" src="https://github.com/user-attachments/assets/f1db0a2e-d387-4e49-a119-5fd3782f61f8" />


#### おさらい(VLANについて） <br>
<img width="1393" height="736" alt="2" src="https://github.com/user-attachments/assets/aa7cf0c7-8f47-4151-b5f6-6a944fda5f71" />

<img width="1385" height="726" alt="3" src="https://github.com/user-attachments/assets/60e74e82-9c4b-456e-ba2d-086a00f36a92" />

<img width="1381" height="720" alt="4" src="https://github.com/user-attachments/assets/a7490b72-beff-41be-9c06-fe8b6d2c7cca" />

<img width="1390" height="729" alt="5" src="https://github.com/user-attachments/assets/8c29c9db-72cd-4d35-a44c-49e5b03287a6" />

<img width="1392" height="729" alt="6" src="https://github.com/user-attachments/assets/19c69bb5-cd02-428a-9fd3-dba94c408c67" />

<img width="1387" height="730" alt="7" src="https://github.com/user-attachments/assets/ca4d190b-a4d6-4c30-b8e2-a72057905a2d" />

#### VLANの設定と確認 <br>
<img width="1392" height="733" alt="8" src="https://github.com/user-attachments/assets/f088ad30-e806-4981-aa46-bdd7fffd9846" />

<img width="1391" height="728" alt="9" src="https://github.com/user-attachments/assets/c5be1543-3bb7-4d0c-b205-d3513979d3a2" />

<img width="1386" height="721" alt="10" src="https://github.com/user-attachments/assets/16b6d718-e320-4fc8-9727-99c711dccddc" />

<img width="1384" height="735" alt="11" src="https://github.com/user-attachments/assets/d47f1ec9-69cb-4a4f-a451-4e870ffa5a4f" />

<img width="1385" height="648" alt="12" src="https://github.com/user-attachments/assets/214b6eea-fe6f-49cd-9c97-090fffdc8a6f" />

<img width="1387" height="727" alt="13" src="https://github.com/user-attachments/assets/2d982afc-2f58-4855-bca9-77a6e8291db5" />

<img width="1391" height="747" alt="14" src="https://github.com/user-attachments/assets/7bd2e00a-1094-4116-8770-605089380950" />

<img width="1387" height="721" alt="15" src="https://github.com/user-attachments/assets/99466b9d-7ffd-434d-9451-ba420dcb07e7" />

<img width="1384" height="725" alt="16" src="https://github.com/user-attachments/assets/90037a80-1eb1-414c-b806-644f4c8f639e" />

<img width="1388" height="737" alt="17" src="https://github.com/user-attachments/assets/f5d8e181-c689-467e-910f-8f858d6fc6a8" />

<img width="1392" height="692" alt="18" src="https://github.com/user-attachments/assets/841493e1-9c7e-4767-b7fb-aa1e31b1b7cb" />

<img width="1387" height="718" alt="20" src="https://github.com/user-attachments/assets/f4a5b71c-471b-408d-840a-07ec113d6dab" />



# ex2000-junos-verup
### 全体構成(FTPクライアントはFFFTPを使用）<br>
<img width="1390" height="732" alt="image" src="https://github.com/user-attachments/assets/1dabf32c-b482-42a6-8cb9-e0fc5625d621" />

### FFFTPによるJunosイメージの転送<br>
<img width="1393" height="728" alt="image" src="https://github.com/user-attachments/assets/fd357abd-ab01-46d8-9f40-ede811044e6d" />

<img width="1387" height="727" alt="image" src="https://github.com/user-attachments/assets/cd2e65ac-5b3d-4626-aeef-122c49127b3f" />

<img width="1388" height="728" alt="image" src="https://github.com/user-attachments/assets/b5c92a3a-2493-4277-b552-9b27b1baaed2" />

<img width="1378" height="718" alt="image" src="https://github.com/user-attachments/assets/61600a42-1093-4c82-8fc3-c276f95b16c6" />

<img width="1388" height="730" alt="image" src="https://github.com/user-attachments/assets/a40f120e-9ddc-45a8-be59-298939490400" />

### 転送されたJunosイメージの確認<br>
<img width="1396" height="701" alt="image" src="https://github.com/user-attachments/assets/40480450-902e-4bf8-92a1-6b053c5275fe" />

### 転送されたJunosイメージでの起動<br>
<img width="1396" height="565" alt="image" src="https://github.com/user-attachments/assets/6a3a7a3e-fa39-45af-afd8-87545ed534a4" />

### 実際の実行結果ログ例<br>
https://github.com/gorosuke5656/junos-lab/blob/main/junos-config/EX/EX220-OS-VerUP-NEW.cfg<br>







### 参考<br>













