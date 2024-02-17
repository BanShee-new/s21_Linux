Part 1. Установка ОС

1.1. Узнайте версию Ubuntu, выполнив команду
cat /etc/issue.
Р1

Part 2. Создание пользователя

2.1. Создать пользователя 
sudo adduser username
Р2.1
2.2. Пользователь добавлен в группу adm
sudo usermod -a -G groupname username
cat /etc/passwd
Р2.2

Part 3. Настройка сети ОС

3.1.Задать имя машины вида user-1:
sudo hostname user-1
sudo hostname
P3.1

3.2.Установить временную зону, соответствующую текущему местоположению, и вывести информации о времени:
sudo timedatectl set-timezone Europe/Moscow
P3.2

3.3.Установить набор сетевых интерфейсов:
sudo apt install net-tools
P3.3

Вывести информацию о сетевых интерфейсах:
ifconfig
P3.4

lo (loopback device) - виртуальный интерфейс, присутствующий по умолчанию в любом Linux. Он используется для отладки сетевых программ и запуска серверных приложений на локальной машине. С этим интерфейсом всегда связан адрес 127.0.0.1. У него есть dns-имя – localhost.

3.5. Получить ip-адрес устройства от DHCP сервера
sudo dhclient -v
P3.5
ip адрес устройства указан после bound to

DHCP (Dynamic Host Configuration Protocol) — это сетевой протокол, позволяющий сетевым устройствам автоматически получать IP-адрес и другие параметры, необходимые для работы в сети TCP/IP.

3.6. Получить внешний ip-адрес
curl ifconfig.me/ip
P3.6

3.7. Получить внутренний IP-адрес шлюза, он же ip-адрес по умолчанию (gw)
ip rout
P3.7

3.8. Задать статичные настройки ip, gw, dns
sudo vim /etc/netplan/00-installer-config.yaml

Основные настройки:
addresses — ip адрес который будет назначен вашей сетевой карте.
gateway4 — ip адрес вашего роутера.
nameservers — DNS сервера. Первый - наш роутер.
search — домен в котором будет произведен поиск. Домен можно настроить при помощи DNS сервера

P3.8

3.9. Применить изменения в netplan и перезагрузиться
sudo netplan apply
reboot
P3.9

3.10. Проверить соответствия адресов адресам, указанным в предыдущем пункте
ifconfig
P3.10

3.11.Пропинговать удаленные хосты 1.1.1.1 и ya.ru
ping 1.1.1.1
ping ya.ry
P3.11

Part 4. Обновление ОС

4.1. Обновить системные пакеты до последней на момент выполнения задания версии
sudo apt-get upgrade
P4.1

Part 5. Использование команды sudo

5.1.sudo - позволяет временно поднимать привилегии и выполнять команды администрирования с максимальными правамии.

5.2. Разрешить пользователю, созданному в Part 2, выполнять команду sudo.
sudo usermod -aG sudo "пользователь 2"

5.3. Поменять hostname ОС от имени пользователя, созданного в пункте Part 2 (используя sudo).
su "пользователь 2"
hostname (проверяем hostname ОС)
sudo hostname "новое hostname"
hostname (проверяем, что hostname изменилось)
Р5.3

Part 6. Установка и настройка службы времени

6.1. Вывести время, часового пояса, в котором вы сейчас находитесь
date
P6.1

6.2. Вывод следующей команды должен содержать NTPSynchronized=yes
timedatectl show
P6.2

Part 7. Установка и использование текстовых редакторов
Используя каждый из трех выбранных редакторов, создайте файл test_X.txt, где X -- название редактора, в котором создан файл. Напишите в нём свой никнейм, закройте файл с сохранением изменений.

7.1. Текстовый редактор VIM - поставляется с ОС:
- vim - открыть редактор vim
- i - режим вставки
- Esc - выход из режима вставки
- :w "имя файла" - сохранить файл с заданным именем
- :q - выйти из редактора vim
P7.1

7.2. Текстовый редактор NANO - поставляется с ОС:
- nano - ткрыть редактор nano
- Ctrl + О - сохранить изменения, затем ввести имя файла
- Ctrl + Х - выйти из редактора NANO
P7.2

7.3. Текстовый редактор JOE: 
- sudo apt update
- sudo apt install joe
P7.3.1
- Ctrl + K + X - сохранить изменения, ввести имя файла и выйти из редактора JOE
P7.3.2

7.4. Используя каждый из трех выбранных редакторов, откройте файл на редактирование, отредактируйте файл, заменив никнейм на строку "21 School 21", закройте файл без сохранения изменений.

7.4.1 VIM:
- vim test_vim.txt
- i - войти в режим вставки, заменить никнейм на "21 School 21"
- для закрытия файла без изменений войти в стандартный режим (ESC) и прописать :q!
P7.4.1

7.4.2 NANO
- nano test_nano.txt
- для закрытия файла без изменений Ctrl + X -> N
Р7.4.2

7.4.3 JOE
- joe test_joe.txt
- для закрытия файла без изменений Ctrl + C -> Y

7.5. Используя каждый из трех выбранных редакторов, отредактируйте файл ещё раз (по аналогии с предыдущим пунктом), а затем освойте функции поиска по содержимому файла (слово) и замены слова на любое другое.

7.5.1. Результат поиска слова в VIM:
- vim test_vim.txt
- i (режим вставки) отредактировать текст
- Esc + /"текст для поиска"
Р7.5.1.1
- Esc + :s/"текст для замены"/"текст замены"
Р7.5.1.2

7.5.2. Результат поиска слова в NANO:
- nano test_nano.txt
- отредактировать текст
- Ctrl + W -> "текст для поиска"
P7.5.2.1
- Ctrl + \ -> "текст для замены" -> "текст замены" -> Y
P7.5.2.2

7.5.3 Результат поиска слова в JOE:
- joe test_joe.txt
- отредактировать текст
- Ctrl + K + F -> "текст для поиска" -> I
P7.5.3.1
- Ctrl + K + F -> "текст для замены" -> R -> "текст замены" -> Y

Part 8. Установка и базовая настройка сервиса SSHD

8.1. Установить пакет OpenSSH server:
sudo apt install openssh-server

8.2. Добавить автостарт службы при загрузке системы:
sudo systemctl start ssh
Проверить работоспособность утилиты:
ssh localhost
8.3. Перенастроить службу SSHd на порт 2022
- Перед модификацией конфигурационного файла создать резеврную копию:
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.factory-defaults
- Открыть файл конфигурации:
sudo vim /etc/ssh/sshd_config 
- Изменить порт на 2022:
P8.2

8.4. Используя команду ps, показать наличие процесса sshd:
ps -ef | grep sshd
ps - выводит список текущих процессов
-e - выбрать все процессы
-f - показывает полную информацию
grep ssh - вывод процессов, которые содержат строку ssh
ps -ef | grep sshd - показывает полную информацию по процессам, содержащим строку sshd
P8.4

8.5. Перезагрузить систему.
sudo reboot

8.6. Вывод команды netstat -tan:
P8.6
-t - отображать TCP подключения
-a - показать состояние всех сокетов
-n - показывать сетевые адреса как числа
Proto - Содержит тип протокола
Recv-Q - Счётчик байтов не скопированных программой пользователя из этого сокета.
Send-Q - Счётчик байтов, не подтверждённых удалённым узлом.
Local Address - Адрес и номер порта локального конца сокета.
Foreign Address - Адрес и номер порта удалённого конца сокета.
State - Состояние сокета.
LISTEN Сокет ожидает входящих подключений.
SYN_SENT Сокет, находящийся в режиме активной попытки установки подключения.
0.0.0.0 - это немаршрутизируемый адрес IPv4, который используется в качестве адреса по умолчанию или адреса-заполнителя

Part 9. Установка и использование утилит top, htop

9.1. Установить и запустить утилиты top и htop.

9.1.1. Утилита top является предустановлнной, для её запуска необходимо ввести команду "top"
P9.1.1

9.1.2. По выводу команды top определить и написать в отчёте:
- uptime: 12 min
- количество авторизованных пользователей: 1
- общую загрузку системы: 0.00, 0.00, 0.00
- общее количество процессов: 119
- загрузку cpu:  0.0 us, 0.0 sy, 0.0 ni, 100.0 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st
- загрузку памяти: 5833.5 total, 5346.6 free, 165.0 used, 321.9 buff/cache
- pid процесса занимающего больше всего памяти: 1
- pid процесса, занимающего больше всего процессорного времени: 1

9.2.1. Установка и использование утилиты htop:
sudo apt install htop
sudo apt-get install -y htop
Для запуска утилиты необходимо ввести команду "htop"
В отчёт вставить скрин с выводом команды htop:
- отсортированному по PID (F6 -> PID)
Р9.2.1
- отсортированному по PERCENT_CPU (F6 -> PERCENT_CPU)
Р9.2.2
- отсортированному по PERCENT_MEM (F6 -> PERCENT_MEM)
Р9.2.3
- отсортированному по TIME (F6 -> TIME)
Р9.2.4
- отфильтрованному для процесса sshd (F4 -> sshd)
Р9.2.5
- с процессом syslog, найденным, используя поиск (F3 -> syslog)
P9.2.6
- с добавленным выводом hostname, clock и uptime (F2 -> добавить hostname, clock и uptime в одну из колонок)
P9.2.7

Part 10. Использование утилиты fdisk

10.1.Запустить команду fdisk -l
P10.1

В отчёте написать название жесткого диска, его размер и количество секторов, а также размер swap:
- Disk /dev/sda: 20 Gib
- 2147836480 bytes
- 41943040 sectors

Part 11. Использование утилиты df
11.1. Запустить команду df (для запуска утилиты необходимо ввести команду "df"):
Р11.1

В отчёте написать для корневого раздела (/):
- размер раздела 10218772 байт
- размер занятого пространства 3246048 байт
- размер свободного пространства 6432052 байт
- процент использования 34%
Определить и написать в отчёт единицу измерения в выводе. Команда "df -h" указывает утилите выводить размеры в килобайтах, мегабайтах, гигабайтах и других кратных величинах.

11.2. Запустить команду df -Th.
Р11.2

В отчёте написать для корневого раздела (/):
- размер раздела 9,8G
- размер занятого пространства 3.1G
- размер свободного пространства 6.2G
- процент использования 34%
- тип файловой системы для раздела ext4

Part 12. Использование утилиты du
 
12.1. Запустить команду du.
P12.1

12.2. Вывести размер папок /home, /var, /var/log (в байтах, в человекочитаемом виде)
- du -b /home
Р12.2.1
- du -b /var
Р12.2.2
- du -b /var/log
Р12.2.3

12.3. Вывести размер всего содержимого в /var/log (не общее, а каждого вложенного элемента, используя *): 
- du -b var/log/*
Р12.3

Part 13. Установка и использование утилиты ncdu

13.1. Установить утилиту ncdu. (sudo apt install ncdu)
P13.1

13.2. Вывести размер папок /home, /var, /var/log:
- ncdu /home
P13.2.1
- ncdu /var
P13.2.2
- ncdu /var/log
P13.2.3

Part 14. Работа с системными журналами

14.1. Открыть для просмотра (cat /var/log/...):
1. /var/log/dmesg 
Р14.1.1
2. /var/log/syslog
Р14.1.2.
3. /var/log/auth.log
Р14.1.3

14.2. Написать в отчёте время последней успешной авторизации, имя пользователя и метод входа в систему.
P14.2

14.3. Перезапустить службу SSHd.
Вставить в отчёт скрин с сообщением о рестарте службы (искать в логах).
P14.3

Part 15. Использование планировщика заданий CRON

15.1. Используя планировщик заданий, запустите команду uptime через каждые 2 минуты.

nano crontab -e -> */2 * * * * uptime

* — оператор звездочки означает все допустимые значения. Если у есть символ звездочки в поле Минуты, это означает, что задача будет выполняться каждую минуту.
/ — оператор косой черты позволяет указать значения шага, которые можно использовать вместе с диапазонами. Вместо диапазона значений вы также можно использовать оператор звездочки.

Р15.1

15.2. Найти в системных журналах строчки (минимум две в заданном временном диапазоне) о выполнении (в журнале /var/log/syslog)
Р15.2

15.3. Вывести на экран список текущих заданий для CRON (crontab -l)
Р15.3

15.4. Удалите все задания из планировщика заданий команда "crontab -r" удаляет файл crontab целиком
В отчёт вставьте скрин со списком текущих заданий для CRON (crontab -l):
Р15.4