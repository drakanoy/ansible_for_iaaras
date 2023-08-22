Установка DiFX с помощью Ansible


Установка Ansible:
pip install ansible

В файле inventory.txt указываются ip-адрес серверов и порт ssh для подключения

В файле ansible.cfg указываются настройки по умолчанию для работы ansible:
1) host_key_checking - проверка нового сервера на finger prints
2) inventory - путь до inventory файла на локальной машине
3) vault_password_file - путь до файла где хранится в текстовом виде пароль от vault шифрования ansible (Будьте осторожны! Не добавляйте этот файл в git!)
