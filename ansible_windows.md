#3.5 Ansible on windows 應用

【前言】  
1. 官方聲明不會支援控制端設在windows (cygwin 環境勉強算有）  
2. 控制端(control node)只有linux/bsd based，且必須
  - 安裝pywinrm 套件
  - 安裝kerberos套件  

3.管控端(managed node)如是windows 必須有以下條件
  - 支援powershell >3   
  - 設定環境給winrm 控制(ConfigureForWinrm.ps1)  
  - winrm 服務安裝  
  - winrm 服務執行  
  - 開啟防火牆5986(https), 5985(http) 給winrm連線（非ssh協議連線）

#控制端 (control node)設定
##安裝pywinrm
`pip install http://github.com/diyan/pywinrm/archive/master.zip#egg=pywinrm`

##安裝 kerberos
1. 執行`pip install kerberos`

- krb5-config
- libkrb5-dev
- libssl-dev
- libsasl2-dev
- libsasl2-modules-gssapi-mit

`sudo apt-get install -y krb5-config libkrb5-dev libssl-dev libsasl2-dev libsasl2-modules-gssapi-mit`

2. 如果出現「`krb5-config: not found`」錯誤訊息

  請先裝 
  
  credit: [kerberos installation error](http://stackoverflow.com/questions/30088355/kerberos-installation-error-error-setup-script-exited-with-error-command-i68)


#管控端（managed node) 設定 //自己的翻譯用詞

## 管理win 版本與環境設定

from [開始用 Ansible 管理 Windows](https://metavige.github.io/2016/01/19/ansible-windows-manage-start/)
from [Ansible For Windows （詳盡）](http://yumaojun03.gotoip55.com/?p=1232)

1. Windows 7/2008R2 版
 -  安裝 .net4.0 [下载地址](http://download.microsoft.com/download/B/A/4/BA4A7E71-2906-4B2D-A0E1-80CF16844F5F/dotNetFx45_Full_x86_x64.exe) 安装过后重启 windows ，进行下一步 更新到 power shell 3.0
 - patch bug http://support.microsoft.com/kb/2842230

2. Windows 8.1/2012  
已經安裝了 .Net 4.0，所以不需要特別作什麼事情


##  windows powershell setup script

ansible/examples/scripts at devel   
https://github.com/ansible/ansible/tree/devel/examples/scripts

1. 升級powershell3  
[upgradeps3.ps1](https://github.com/ansible/ansible/blob/devel/examples/scripts/upgrade_to_ps3.ps1)  

2. 設定winrm 環境  
[configwinrm.ps1](https://github.com/ansible/ansible/blob/devel/examples/scripts/ConfigureRemotingForAnsible.ps1)

3. 檢查winrm 服務狀態  
  開啟powershell (系統管理員權限) :`winrm quickconfig`

  應該會出現
```
WinRM 服務已在這台電腦上執行。
此電腦上的 WinRM 已設定為可接受遠端管理。
```

4. 設定 AllowUnencrytped = false（一定要加密連線） 

 `PS > winrm set winrm/config/service '@{AllowUnencrypted="false"}'`

5. 檢查連線驗證方式  
`PS > winrm get winrm/config/service/Auth`

  結果
```
Auth
    Basic = true
    Kerberos = true
    Negotiate = true
    Certificate = false
    CredSSP = false
    CbtHardeningLevel = Relaxed
```

#【應用】
## 1. 控制端 (via vagrant)
控制端：linux on virtualbox(win)
管控端：any ansible hosts

番外篇：在 Windows 上也能使用 Ansible
http://school.soft-arch.net/courses/ansible/lectures/659421

概念 用vagrant 新增控制端 Ansible 主機  
- vagrant box:  https://github.com/William-Yeh/ansible-vagrantbox  
- 工具: vag2inv (Vagrant to Inventory) 幫你爬出vb 虛擬主機的 hosts 資訊  
https://github.com/William-Yeh/vag2inv

## 2.Control 端 on windows (via cygwin)

Running Vagrant with Ansible Provisioning on Windows | Azavea Labs  
http://www.azavea.com/blogs/labs/2014/10/running-vagrant-with-ansible-provisioning-on-windows/

##ref
