## 1. Удалите iptables и установите firewalld
```bash
# Останавливаем и отключаем iptables 
sudo systemctl stop iptables
sudo systemctl disable iptables

sudo apt-get install firewalld -y # Устанавливаем firewalld

# Запускаем и включаем автозагрузку firewalld
sudo systemctl start firewalld
sudo systemctl enable firewalld

sudo systemctl status firewalld # Проверяем 
```
![[Pasted image 20251230104250.png]]
![[Pasted image 20251230104314.png]]
## 2. Попробуйте так-же проверить возможность подключения по ssh
сработало
![[Pasted image 20251230104445.png]]

## 3. Если её нет то откройте порт
ну пусть будет
```bash
sudo firewall-cmd --add-port=232/tcp 
```
![[Pasted image 20251230104558.png]]
## 4. Выведите список открытых портов с помощью firewall-cmd
```bash
sudo firewall-cmd --list-ports
```
![[Pasted image 20251230104659.png]]
## 5. Можно ли там добавить порты по названию сервиса?
Да, например так
```bash
sudo firewall-cmd --permanent --add-service=ssh
sudo firewall-cmd --reload
```

## 6. На вашей Локальной виртуальной машине попробуйте подключиться к серверу samba из предыдущих заданий
не получилось
![[Pasted image 20251230114611.png]]
## 7. Если не получилось то откройте нужные порты
```bash
sudo firewall-cmd --permanent --add-service=samba
```
и еще конфиг самбы меняем (по другому не работало)
![[Pasted image 20251230115450.png]]
результат
![[Pasted image 20251230114643.png]]
(я тестировал уже прост)
## 8. Сделайте так чтобы изменения были постоянными
```bash
firewall-cmd --runtime-to-permanent
```
![[Pasted image 20251230115029.png]]
