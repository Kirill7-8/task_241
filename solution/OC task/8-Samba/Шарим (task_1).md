## 1. Установите пакет samba
```bash
sudo apt-get install samba samba-client
```
![[Pasted image 20251229233300.png]]
## 2. Что такое общая папка, зачем оно может быть нужно?    
Общая папка - это каталог на Linux-компьютере, к которому другие компьютеры могут подключаться по сети и работать с файлами. Нужна она для передачи файлов между компьютерами, общий доступ к документам, сетевое хранилище, работа нескольких пользователей с одними файлами
## 3. Создайте общую папку без пароля с правами только на чтение файлов
```bash
sudo mkdir -p /srv/samba/public_read # Создаём рекурсивно папку
sudo chmod 755 /srv/samba/public_read # Даём права на чтение всем
sudo nano /etc/samba/smb.conf # Редактируем конфиг Samba
```
Добавляем в конец файла:
```bash
[public_read]
path = /srv/samba/public_read
browseable = yes
guest ok = yes
read only = yes
```
Перезапускаем Samba:
```bash
sudo systemctl restart smb
```
![[Pasted image 20251230000539.png]]
![[Pasted image 20251230000522.png]]
## 4. Создайте общую папку с паролем с правами на чтение и запись
```bash
sudo mkdir -p /srv/samba/private_rw # также рекурсивно создаем папки
sudo chmod 770 /srv/samba/private_rw # выдаем права
sudo smbpasswd -a <Юзер> # Добавляем пользователя в Samba и задаем пароль
sudo nano /etc/samba/smb.conf # редактируем конфиг
```

Добавляем:
```bash
[private_rw]
path = /srv/samba/private_rw
browseable = yes
guest ok = no
read only = no
valid users = <юзер> # опционально
```
```bash
sudo systemctl restart smb # перезапуск
```
## 5. Создайте общую папку с доступом для какой-то группы с полными правами
```bash
sudo groupadd test_group # создаем группу
sudo useradd user3 # создаем юзера
sudo useradd user4 # и еще одного
sudo usermod -aG test_group user3 # добавляем пользователя 1
sudo usermod -aG test_group user4 # добавляем пользователя 2
sudo mkdir -p /srv/samba/group_full # создаем папку
sudo chown :test_group /srv/samba/group_full # Назначаем группу
sudo chmod 770 /srv/samba/group_full # выдаем права
```
Добавляем в конфиг
```bash
[group_full]
path = /srv/samba/group_full
browseable = yes
guest ok = no
read only = no
valid users = @test_group
```
![[Pasted image 20251230010449.png]]
## 6. Создайте общую папку в которой у одной группы будет полный доступ, а у другой только доступ на чтение. Третья группа не должна иметь к ней доступа
```bash
# создаем группы
sudo groupadd fullgroup
sudo groupadd readgroup
sudo groupadd nogroup

# создаем папку
sudo mkdir -p /srv/samba/mixed_access

# назначаем владельца и права
sudo chown :fullgroup /srv/samba/mixed_access
sudo chmod 770 /srv/samba/mixed_access

# настраиваем доп права
sudo setfacl -m g:readgroup:rx /srv/samba/mixed_access
sudo setfacl -m g:nogroup:0 /srv/samba/mixed_access

# ну и конфиг
[mixed_access]
path = /srv/samba/mixed_access
browseable = yes
guest ok = no
read only = no
valid users = @fullgroup, @readgroup
write list = @fullgroup
```
![[Pasted image 20251230011742.png]]