## 1. Посмотрите журналы ssh
```bash
sudo journalctl -u ssh # логи юнита ssh.service (не демона)
sudo journalctl -u sshd # логи юнита ssh.service (демона)
```
![[Pasted image 20251228235129.png]]
## 2. Выведите журналы в реальном времени
```bash
sudo journalctl -f
```
![[Pasted image 20251228235423.png]]
## 3.Выведите лог в реальном времени для службы sshd
```bash
sudo journalctl -f -u sshd
```
![[Pasted image 20251228235513.png]]
## 4. Можно ли без команды journalctl прочитать логи systemd?
Да. Логи systemd также хранятся в бинарном виде в `/run/log/journal/` или `/var/log/journal/`
![[Pasted image 20251228235743.png]]
## 5. Сколько будет 2-2?
$f(x) = 2-2 = 67-67 = 420-420 = 69-69 = 52-52 = Cx - Cx$
$I = \int{f(x)dx}$
$\grave{I} = f(x)$
$I = \int{(Cx - Cx)dx} = \int{(Cx)dx} - \int{(Cx )dx} = C\frac{x^2}{2} - C\frac{x^2}{2}$
$\grave{I} = \grave{C\frac{x^2}{2}} - \grave{C\frac{x^2}{2}} = Cx -Cx$
$Cx - Cx = ln(Cx - Cx) = ln(2-2) \Rightarrow ln(Cx - Cx) - ln(2-2) = ln(\frac{Cx - Cx}{2 - 2}) = ln(1)$
$Вспоминаем, \ что \ log_e{b} = c \Rightarrow e^c=b$
$ln(1) = e^{ln(1)}=1$
Введем замену $x = ln(1)$
рассмотрим график $f(x) = e^x$, чтобы найти значение x, при значении функции равной 1
![[Pasted image 20251229001944.png]]
получается, что $e^0=1 \Rightarrow ln(1)=0$
Вывод: 2-2 = 0





