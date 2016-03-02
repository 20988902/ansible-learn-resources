#基本概念

//待補



## **1. Ansible 環境**

* controller 端  python > 2.7
* _managed 端（自己稱為受控端） _python > 2.5
* _ansible_ (pip/yum/apt) 最新2.0

安裝ansible步驟 [點我](https://github.com/marxwang/ansible-learn-resources/blob/master/install_ansible.md) 

## 2.學習 Ansible 專注focus 幾件事

* Inventory (hosts) file
* playbook(s)
* role(s)
* variables

## 3. 基本名詞
from [Ansible状态管理](http://xdays.me/ansible%E7%8A%B6%E6%80%81%E7%AE%A1%E7%90%86.html)

### hosts/inventory 
重點：管理對象、用什麼帳號管理，連線方式ssh/winrm
- host，应用play的主机范围
- user，在这些主机上以什么用户运行playbook

### task/play/playbooks/roles 
重點：執行單一任務task、一組任務play、一系列任務roles
- task，由模块来完成的一个单位任务，如修改文件或者启动服务
- play，一组task的集合，ansible会自上而下执行
- handler，task可以触发一定的事件，而处理该事件的task即为handler
- role，角色，一组playbook以及和其配合的元素（vars, files等）的集合


## roles 目錄結構
//待補


