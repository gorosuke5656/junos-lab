# Juniper EX-L2/L3-basic-lab<br>
### LastUpdate:2026/09/06<br>


# １　実習構成<br>
## 構成はEX2200が3台になります。me0（管理インタフェース）経由で設定します<br>
### 構成図



# ２ 　#Juniper EX-L2/L3-basic-labで取り上げる内容<br>
 - [(1) 基本設定と確認](#system-basic-conf)<br>
 - [(2) LLDP設定と確認](#lldp-conf)<br>  
 - [(3) STP設定と確認](#stp-conf)<br>
 - [(4) LAG設定と確認](#lag-conf)<br>
 - [(5) RTG設定と確認](#rtg-conf)<br>
 - [(6) 経路制御設定と確認](#ospf-conf)<br>
 - [(7) Firewall-filter設定と確認](#firewall-filter-conf)<br>
 - [(8) Virtual-chassis設定と確認](#Virtual-chassis-conf)<br>

# system-basic-conf


# lldp-conf



# 【参考資料】<br>
- [EX2200におけるJunosアップグレード方法](#ex2000-junos-verup)<br>

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













