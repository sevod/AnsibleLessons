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