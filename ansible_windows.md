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




#管控端（managed node) 設定 //中文翻譯自己發明的

##  windows powershell setup script

ansible/examples/scripts at devel   
https://github.com/ansible/ansible/tree/devel/examples/scripts




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
