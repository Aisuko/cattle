# cattle
The Ansible script that init the infrastructure for Kubernetes.


### Contributor

* Thanks for your help [Youngman](https://github.com/spring-bu)


### This is a ansible script that can help you init infrastrucure.

Tips: The os we use is Centos7, you can change it for yourself.

* Install Ansible on Mac OSX 

  * Use `brew` Command:
    
    ```brew install ansible```

* Install Ansible on RHEL/CentOS 

  * Use  `yum`  Command:
    
    ```yum install ansible -y```

* How to use?
  
  * Please make sure that your ssh_key_pub_key was set by default path in your local

   ```ssh-copy-id root@<your-ip>```

  * Init your infrastructure
    
    * Add your ip into the `templ.host`
    * Add the extra task in `tasks.main.yml`

  ```ansible-playbook -i templ.host templ.yml```


**Notice**

If you are macOS ,When you use the ansible command to connect to a remote host via ssh and password, you will see below error:

```
to use the 'ssh' connection type with passwords, you must install the sshpass program
```

And you well want use brew install it:

```
brew install sshpass
```

Unfortunately, you will receive the following tips：

```
Error: No available formula with the name "sshpass"
We won't add sshpass because it makes it too easy for novice SSH users to
ruin SSH's security.
```

By default, brew official removed the package for security reasons, so we chose other installation methods.

```
brew install http://git.io/sshpass.rb
```

If you are RHEL/CentOS ,you can use yum command:

```
yum install sshpass -y
```

Finally, you can use ansible via ssh username with password to connect remote host, for example in you inventory:

```
[web]
10.16.18.194 ansible_ssh_user=USERNAME ansible_ssh_pass='MYPASSWORD' ansible_ssh_common_args='-o StrictHostKeyChecking=no'
```
---

```
 ~/Desktop/playbook   develop ● ? ⍟1  ansible-playbook -i templ.host templ.yml
[DEPRECATION WARNING]: Instead of sudo/sudo_user, use become/become_user and make sure become_method is 'sudo' (default). This feature will be removed in version 2.9. Deprecation warnings can be
disabled by setting deprecation_warnings=False in ansible.cfg.

PLAY [all] *********************************************************************************************************************************************************************************************

TASK [Gathering Facts] *********************************************************************************************************************************************************************************
ok: [10.16.18.180]

TASK [comm : Set rc.local can be execution] ************************************************************************************************************************************************************
ok: [10.16.18.180]

TASK [comm : Set timezone to Asia/Shanghai] ************************************************************************************************************************************************************
ok: [10.16.18.180]

TASK [comm : Disable SELinux] **************************************************************************************************************************************************************************
 [WARNING]: SELinux state change will take effect next reboot

ok: [10.16.18.180]

TASK [comm : Dsiable Firewalld] ************************************************************************************************************************************************************************
ok: [10.16.18.180]

TASK [comm : Add or modify nofile soft limit] **********************************************************************************************************************************************************
 [WARNING]: The value 655360 (type int) in a string field was converted to u'655360' (type string). If this does not look like what you expect, quote the entire value to ensure it does not change.

ok: [10.16.18.180]

TASK [comm : Set ipv4 forward] *************************************************************************************************************************************************************************
 [WARNING]: The value 1 (type int) in a string field was converted to u'1' (type string). If this does not look like what you expect, quote the entire value to ensure it does not change.

ok: [10.16.18.180]

TASK [comm : Add centos base yum repositories] *********************************************************************************************************************************************************
ok: [10.16.18.180]

TASK [comm : Add centos update yum repositories] *******************************************************************************************************************************************************
changed: [10.16.18.180]

TASK [comm : Add centos extra yum repositories] ********************************************************************************************************************************************************
changed: [10.16.18.180]

TASK [comm : Add epel repository] **********************************************************************************************************************************************************************
ok: [10.16.18.180]

TASK [comm : Add docker repositories] ******************************************************************************************************************************************************************
ok: [10.16.18.180]

TASK [comm : Add nginx repositories] *******************************************************************************************************************************************************************
ok: [10.16.18.180]

TASK [comm : Install comm software] ********************************************************************************************************************************************************************
[DEPRECATION WARNING]: Invoking "yum" only once while using a loop via squash_actions is deprecated. Instead of using a loop to supply multiple items and specifying `name: "{{ item }}"`, please use
`name: ['zip', 'unzip', 'vim', 'wget', 'curl', 'bash-completion', 'docker-ce']` and remove the loop. This feature will be removed in version 2.11. Deprecation warnings can be disabled by setting
deprecation_warnings=False in ansible.cfg.
changed: [10.16.18.180] => (item=['zip', 'unzip', 'vim', 'wget', 'curl', 'bash-completion', 'docker-ce'])

TASK [comm : Restart docker] ***************************************************************************************************************************************************************************
changed: [10.16.18.180]

TASK [comm : Add user rancher] *************************************************************************************************************************************************************************
changed: [10.16.18.180]

TASK [comm : Add passwd for rancher] *******************************************************************************************************************************************************************
changed: [10.16.18.180]

TASK [comm : ssh-copy] *********************************************************************************************************************************************************************************
changed: [10.16.18.180]

PLAY RECAP *********************************************************************************************************************************************************************************************
10.16.18.180               : ok=18   changed=7    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```




 # License

Copyright 2019 Aisuko.

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND.
