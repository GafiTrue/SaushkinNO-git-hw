# Домашнее задание к занятию "`Система мониторинга Zabbix`" - `Саушкин Николай Олегович`
---

### Задание 1
Установите Zabbix Server с веб-интерфейсом.
Прикрепите в файл README.md скриншот авторизации в админке.
<img width="1280" height="577" alt="image" src="https://github.com/user-attachments/assets/37b229b4-07dd-4e1b-a1a6-1a04564dd813" />

Приложите в файл README.md текст использованных команд в GitHub.
#### 1. Скачивание и установка репозитория Zabbix
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_6.0+ubuntu24.04_all.deb
sudo dpkg -i zabbix-release_latest_6.0+ubuntu24.04_all.deb
sudo apt update

#### 2. Установка компонентов Zabbix
sudo apt install zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-nginx-conf zabbix-sql-scripts zabbix-agent

#### 3. Установка PostgreSQL
sudo apt install postgresql

#### 4. Создание пользователя и базы данных
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix

#### 5. Импорт схемы базы данных
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

#### 6. Настройка пароля в конфиге Zabbix Server
sudo nano /etc/zabbix/zabbix_server.conf

#### 7. Настройка Nginx
sudo nano /etc/zabbix/nginx.conf


#### 8. Запуск и автозагрузка сервисов
sudo systemctl restart zabbix-server zabbix-agent nginx php8.3-fpm
sudo systemctl enable zabbix-server zabbix-agent nginx php8.3-fpm

---

### Задание 2

Установите Zabbix Agent на два хоста.

<img width="1280" height="138" alt="image" src="https://github.com/user-attachments/assets/0b343085-1733-4f39-af7b-3d2032dbc38f" />
<img width="919" height="165" alt="image" src="https://github.com/user-attachments/assets/a8520cff-0d1e-489c-8354-e0c9f6712b17" />
<img width="1280" height="463" alt="image" src="https://github.com/user-attachments/assets/25c4f2db-ecb0-4c1e-a93a-894e9f31a2a4" />
<img width="1280" height="493" alt="image" src="https://github.com/user-attachments/assets/d80e5216-6b15-436b-9316-a1ca5336a483" />

---

#### 1. Скачивание и установка репозитория Zabbix
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_6.0+ubuntu24.04_all.deb
sudo dpkg -i zabbix-release_latest_6.0+ubuntu24.04_all.deb
sudo apt update

#### 2. Установка Zabbix Agent
sudo apt install zabbix-agent

#### 3. Настройка агента
sudo nano /etc/zabbix/zabbix_agentd.conf

Найти и изменить следующие параметры:
Server=IP_ZABBIX_СЕРВЕРА
ServerActive=IP_ZABBIX_СЕРВЕРА
Hostname=Yandex Cloude

#### 4. Перезапуск и автозагрузка агента
sudo systemctl restart zabbix-agent
sudo systemctl enable zabbix-agent
