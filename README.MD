# Установка DiFX с помощью Ansible


## Установка Ansible:

`pip install ansible`
##  Описание файлов и переменных:

В файле _inventory.txt_ указываются ip-адрес серверов и порт ssh для подключения

В файле _ansible.cfg_ указываются настройки по умолчанию для работы ansible:
1) **host_key_checking** - Проверка нового сервера на _finger prints_
2) **inventory** - Путь до _inventory_ файла на локальной машине
3) **vault_password_file** - Путь до файла где хранится в текстовом виде пароль от _vault шифрования ansible_
(Будьте осторожны! Не добавляйте этот файл в git!)


Файл _group_vars/ubuntu_servers.yml_ содержит переменные для всех серверов в группе _ubuntu_servers_, описанных в _inventory_:
1) **ansible_user** - Имя пользователя, под которым будет подключаться Ansible.
(Для удобства это может быть первый пользователь, который был создан при развертывании сервера)
2) **ansible_sudo_pass** - Пароль этого пользователя, для режима sudo.
Этот пароль зашифрован методом _ansible vault_.
Чтобы зашифровать строку с паролем, требуется ключ, который хранится в файле, путь к которому вы указали в файле _ansible.cfg_.
Для шифрования пароля выполните следующую команду:
`ansible-vault encrypt_string --vault-password-file /file/with/vault/key 'your_password' --name 'ansible_sudo_pass'`
Затем вставьте результат команды в файл "как есть".
3) **ansible_ssh_port** - Порт  ssh для подключения Ansible.

## Запуск плейбуков:

Чтобы запустить плейбук выполните следующую команду:
`ansible-playbook playbook_name.yml`


Плейбуки стоит выполнять в порядке их нумерации.

1) **playbook1_create_user.yml** - Создает пользователей с именами, указанными в файле _spisok.txt_, и добавляет им ssh ключ для авторизации, указанный там же.
Пароль от пользователей будет тот же, что и указан в файле _group_vars/ubuntu_servers.yml_ (Рекомендуется поменять его сразу после создания пользователя)
2) **playbook2_ssh_port_setting.yml** - Меняет порт ssh подключения по умолчанию на 8822. После исполнения плейбука поменяйте значение ssh порта в _inventory.txt_ или _group_vars/ubuntu_servers.yml_
3) **playbook3_install_base_apps.yml** - Устанавливает базовые пакеты для работы на сервере
4) **playbook4_install_intel_ipp.yml** - Устанавливает _Intel IPP_ компилятор
5) **playbook5_instal_Difx.yml** - Устанавливает _DiFX_ коррелятор
6) **playbook6_NFS_mount.yml** - Монтирует NFS диск на сервер
