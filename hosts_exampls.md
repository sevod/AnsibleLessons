
###Использование переменных
````
[droplet]
167.99.133.30
206.189.58.240

[droplet:vars]
ansible_ssh_private_key_file=~/.ssh/id_rsa
ansible_user=root
ansible_python_interpreter=/usr/bin/python3
````

###ansible_python_interpreter=/usr/bin/python3
указать в явном виде инерпретатор пайтона