### документация Ансибл
https://docs.ansible.com/ansible/latest/

### модули Ансибл
https://docs.ansible.com/ansible/2.9/modules/modules_by_category.html

### ansible-galaxy collection install amazon.aws
пример установки коллекции
https://galaxy.ansible.com/amazon/aws?extIdCarryOver=true&sc_cid=701f2000001OH6uAAG


## Переменные Ансибл
###Return Values
### Common Return Values
https://docs.ansible.com/ansible/2.9/reference_appendices/common_return_values.html
###Переменные в коде
### Передача переменных из вне
`--extra-vars или просто -e`
`ansible-playbook -i hosts deploy-node.yaml -e "version=1.0.0 node_file_location=/home/tehuser/react-nodejs-example-master/my-app"`
### Внешний файл с переменными
````
version: 1.0.0
node_file_location: /home/tehuser/react-nodejs-example-master/my-app
user_home_dir: "{{node_file_location}}/{{version}}"
````



# Комманды Ansible

### ansible all -i hosts -m ping
all - всем хостам в списке
-i файл с хостами
-m модуль который будем использовать

### ansible droplet -i hosts -m ping
droplet - только тем хостам которые в этом списке

### ansible 10.10.10.10 -i hosts -m ping
10.10.10.10 - конкретной машине

### ssh-keyscan -H 64.227.70.122 >> ~/.ssh/known_hosts
с помощью этот команды мы добавляем хост в список известных хостов, что бы не задавал не нужных вопросов

### ssh-copy-id root@188.166.87.242
копирование ssh ключа на удаленную машину

### vim ~/.ansible.cfg
создание конфиг файла на маке
/etc/ansible/ansible.cfg на линуксе
### ansible.cfg можно создать в локальной папке

### настройка ansible.cfg
```
[defaults]
host_key_checking = False
```
не проверять что это первое соединение

# Playbooks

### ansible-playbook -i hosts my-playbook.yaml
запуск плайбука (первый плейбук в папке 2)