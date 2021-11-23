
````
#три дефиса разделяют разные задачи
---
# name может быть произвольным
- name: Configure nginx web server
# беретсф из файла hosts
hosts: webserver
# задачи которые мы будем выполнять, используем для этого список
tasks:
- name: install nginix server
# это уже модуль, устанавливаем nginx последнюю (latest) версию
    apt:
# можно определить конкретную версию пакета, или использовать регулярные выражения
# взять можно например сдесь https://launchpad.net/, так же меняем state
#      name: nginx
      name: nginx=1.18.0-0ubuntu1.2
#      name: nginx=1.18.*
#      state: latest
      state: present
# это уже следующая задача, используем модуль service, и запускаем nginx
- name: start nginx server
  service:
  name: nginx
  state: started
````

````
# name может быть произвольным
- name: Configure nginx web server
# беретсф из файла hosts
  hosts: webserver
# задачи которые мы будем выполнять, используем для этого список
  tasks:
  - name: uninstall nginix server
# это уже модуль, УДАЛЯЕМ nginx
    apt:
      name: nginx
      state: absent
# это уже следующая задача, используем модуль service, и запускаем nginx
  - name: STOP nginx server
    service:
      name: nginx
      state: stopped
````

````
- name: Deploy nodejs app
  hosts: all
  tasks:
    - name: Unpack the nodejs file
      unarchive:
        src: ./../distr/node-example.tgz
        dest: /root/

    - name: Copy nodejs foder to a server
      copy:
        src: ./../distr/node-example.tgz
        dest: /root/app-1.0.0.tgz
    - name: Unpack the nodejs file
      unarchive:
        src: /root/app-1.0.0.tgz
        dest: /root/
#       указыаем, что все это проделывается на удаленной машине, иначе он будет пытаться распаковать с локальной
        remote_src: yes
````

### Создание и использование нового пользователя

````
- name: Create new linux user for node app
  hosts: all
  tasks:
    - name: Create linux user
      user:
        name: tehuser
        comment: Tehuser Admin
        group: admin
        
- name: Deploy nodejs app
  hosts: all
# эти две строки для настройки пользователя, без них будет рут
  become: True
  become_user: tehuser        
````

###Переменные  Return Values (то что возвращают модули)
```
- name: Create new linux user for node app
  hosts: all
  tasks:
    - name: Create linux user
      user:
        name: tehuser
        comment: Tehuser Admin
        group: admin
      #это Registering variables, сюда попадает Return Values модуля
      register: user_creation_result1
    - debug: msg={{user_creation_result1}}
```
### Переменные в коде и в файле
````
- name: Deploy nodejs app
  hosts: all
  #обьявление переменных как файл и в коде
  vars_files:
    - project-vars
#  vars:
#    - node_file_location: /home/tehuser/react-nodejs-example-master/my-app
#    - version: 1.0.0
  tasks:
    - name: Install dependencies
      npm:
        path: "{{node_file_location}}"
````

### Передача переменных из вне
`--extra-vars или просто -e`

`ansible-playbook -i hosts deploy-node.yaml -e "version=1.0.0 node_file_location=/home/tehuser/react-nodejs-example-master/my-app"`