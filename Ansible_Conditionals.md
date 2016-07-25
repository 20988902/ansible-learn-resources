

## Conditionals 條件式 

目的：利用條件式協助task 過濾，滿足條件時才執行

使用時機[語法]
- when [when:]
- loops [with_items:]
- loops [with_dicts:]
- Custom Facts [ when: my_custom_facts == '1234']
- Conditional imports
- Select files and Templates based on variables


## 2. 常見ansible_os_family

- when: ansible_os_family == "CentOS"
- when: ansible_os_family == "Redhat"
- when: ansible_os_family == "Darwin"
- when: ansible_os_family == "Debian"
- when: ansible_os_family == "Windows"

## 3. 條件可以多選，並且可以用 And/OR 組合

`when: (條件一) and/or (條件二）...and/or (更多條件）`

不過要寫到那麼精準，會不會讓playbook 變得很難維護，就要看人嚕


## 4. 本文英文版
順手寫了 Stack Overflow Docs beta 的文件，很開心被接受了，整理的過程中也發現自己的不足，讓全世界的人都來補完，是個好點子！ 

Ansible: Conditionals - ansible - Stack Overflow
http://stackoverflow.com/documentation/ansible/3555/ansible-conditionals#t=201607251002236395826
