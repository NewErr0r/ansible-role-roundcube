<h1 align='center'>Автоматизация развёртывания приложения "Roundcube" для организации работы с электронной почтой посредством веб-интерфейса</h1>

<p>
    <strong>Шаг 1. </strong> Создание playbook для запуска роли
</p>
<p><i>Пример:</i></p>

<pre>
---
- name: Installing and configuring Roundcube Webmail
  hosts: dovecot 
  become: true 

  roles: 
    - ansible-role-roundcube
</pre>

<p>
    <strong>Шаг 2. </strong> Склонировать роль в дирректорию с playbook:
</p>

  <pre>https://github.com/NewErr0r/ansible-role-roundcube.git</pre>

<p>

<p>
    <strong>Список переопределяемых переменных для playbook. </strong>
</p>
<pre>
# Download Roundcube
url_download: 'https://github.com/roundcube/roundcubemail/releases/download/1.5.3/roundcubemail-1.5.3-complete.tar.gz'
path_download: /root<br>
# MariaDB
mariadb_root_password: "P@ssw0rd"
mariadb_database_roundcube: 'roundcubemail'
mariadb_username_roundcube: 'roundcube'
mariadb_username_password_roundcube: 'roundcube123'
</pre>

<p>
    <strong>Шаг 3. </strong> Запуск playbook:
</p>
<pre>
ansible-playbook -i inventory/hosts playbook.yml
</pre>

<p>
    <strong>Шаг 4. </strong> Запускаем браузер и вводим адрес http://'IP-адрес сервера'/webmail/installer/:
</p>
<p>
В самом низу нажимаем по кнопке Next. Если кнопка будет неактивна, проверяем, что нет ошибок (NOT OK).
</p>

<p>
    <strong>Шаг 5. </strong> На следующей странице проверяем, что все пункты находятся в состоянии OK. Установка выполнена:
</p>
<p>
Подключаемы по SSH к серверу, открываем конфигурационный файл 
</p>
<pre>
vi /usr/share/nginx/html/webmail/config/config.inc.php
</pre>
<p>
Запрещаем установку портала:
</p>
<pre>
...
$config['enable_installer'] = false;
</pre>
<p>
После удаляем папку с установочными скриптами:
</p>
<pre>
\rm -R /usr/share/nginx/html/webmail/installer
</pre>

<p>
    <strong>Шаг 6. </strong> http://'IP-адрес сервера'/webmail/
</p>
