## 1. Создайте скрипт который создаёт папку заполняет её файлами ( имена 1-4 ) и записывает в них информацию о текущей дате, версии ядра, имени компьютера и списке всех файлов в домашнем каталоге пользователя от которого выполняется скрипт (не забудьте сделать проверку на существование файлов и папок)
![[Pasted image 20251230211206.png]]
Запустим и проверим
![[Pasted image 20251230211301.png]]
содержимое каждого файла:
![[Pasted image 20251230211348.png]]
## 2. Создайте юнит который будет вызывать этот скрипт при запуске. Проверьте
создаем юнит
```bash
sudo nano /etc/systemd/system/lab_script.service`
```
![[Pasted image 20251230211459.png]]
Включаем юнит
```bash
sudo systemctl enable lab_script.service
```
## 3. Создайте таймер который будет вызывать выполнение одноимённого systemd юнита каждые 5 минут.
```bash 
sudo nano /etc/systemd/system/lab_script.timer
```
![[Pasted image 20251230211737.png]]
Запускаем
```bash
sudo systemctl daemon-reexec
sudo systemctl enable lab_script.timer
sudo systemctl start lab_script.timer
```
![[Pasted image 20251230211952.png]]
## 4. От какого пользователя вызываются юниты по умолчанию?
По умолчанию systemd system-юниты запускаются от пользователя root, если в юните явно не указан параметр User.
## 5. Создайте пользователя от имени которого будет выполняться ваш скрипт.
```bash
sudo useradd -m -s /bin/bash labuser
sudo passwd labuser
```
![[Pasted image 20251230212011.png]]
## 6. Дополните юнит информацией о пользователе от которого должен выполняться скрипт.
обновляем содержимое: `/etc/systemd/system/lab_script.service`
![[Pasted image 20251230212103.png]]
применяем изменения
```bash
sudo systemctl daemon-reexec
sudo systemctl restart lab_script.service
```
## 7. Дополните ваш скрипт так, что бы он независимо от местоположения всегда выполнялся в домашней папке того кто его вызывает.
добавляем эту строчку в начало скрипта
```bash
cd ~
```
![[Pasted image 20251230212412.png]]