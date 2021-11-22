
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