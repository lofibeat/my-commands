```bash

⚙️ Система, процессы и сервисы

## Информация о системе

uname -a                        # полная информация о ядре и системе
uname -s                        # имя ядра (Linux)
uname -r                        # версия ядра
uname -m                        # архитектура процессора (x86_64, arm64)
hostnamectl                     # информация о хосте и ОС
hostnamectl set-hostname new-name  # изменить имя хоста
cat /etc/os-release             # информация о дистрибутиве
lsb_release -a                  # информация о релизе (Ubuntu/Debian)
cat /proc/cpuinfo               # информация о процессорах
cat /proc/meminfo               # информация о памяти
cat /proc/version               # версия ядра
cat /proc/uptime                # время работы системы
uptime                          # время работы и нагрузка на систему
w                               # кто залогинен и что делает
whoami                          # текущий пользователь
id                              # UID, GID, группы текущего пользователя
groups                          # группы текущего пользователя

## Процессы и управление ими

ps                              # показать процессы текущего пользователя
ps aux                          # все процессы с полной информацией
ps auxf                         # дерево процессов с полной информацией
ps -eo pid,ppid,cmd,%cpu,%mem --sort=-%cpu  # процессы отсортированные по CPU
ps -eo pid,ppid,cmd,%cpu,%mem --sort=-%mem  # процессы отсортированные по памяти
ps aux | grep process-name      # найти процесс по имени
pgrep process-name              # найти PID процесса по имени
pgrep -l process-name           # найти PID и имя процесса
pgrep -u username               # найти процессы конкретного пользователя
pidof process-name              # получить PID(s) процесса

top                             # интерактивный монитор процессов
top -u username                 # показать процессы конкретного пользователя
top -p PID                      # мониторить конкретный процесс
top -o %CPU                     # отсортировать по CPU
top -o %MEM                     # отсортировать по памяти
htop                            # улучшенный top (если установлен)
atop                            # детальный мониторинг (если установлен)

kill PID                        # отправить SIGTERM процессу (корректное завершение)
kill -9 PID                     # отправить SIGKILL (принудительное завершение)
kill -STOP PID                  # приостановить процесс
kill -CONT PID                  # возобновить процесс
kill -HUP PID                   # перезагрузить процесс (перечитать конфиг)
killall process-name            # завершить все процессы с данным именем
pkill process-name              # завершить процесс по имени (как killall)
pkill -9 process-name           # принудительно завершить по имени

nice -n 10 command              # запустить команду с приоритетом (10 = низкий)
renice -n 15 -p PID             # изменить приоритет уже запущенного процесса
renice -n -5 -u username        # изменить приоритет всех процессов пользователя

## Systemd и сервисы

systemctl status                # статус systemd системы
systemctl status service-name   # статус конкретного сервиса
systemctl start service-name    # запустить сервис
systemctl stop service-name     # остановить сервис
systemctl restart service-name  # перезапустить сервис
systemctl reload service-name   # перезагрузить конфиг (без перезапуска)
systemctl enable service-name   # включить запуск при загрузке
systemctl disable service-name  # отключить запуск при загрузке
systemctl is-enabled service-name  # проверить включён ли сервис при загрузке
systemctl is-active service-name   # проверить запущен ли сервис
systemctl list-units --type=service  # список всех сервисов
systemctl list-units --type=service --state=running  # список запущенных сервисов
systemctl list-units --type=service --state=failed   # список сервисов с ошибками
systemctl list-dependencies service-name  # зависимости сервиса
systemctl show service-name     # показать все свойства сервиса

systemctl isolate multi-user.target  # переключиться на multi-user режим (без GUI)
systemctl isolate graphical.target   # переключиться на GUI режим
systemctl get-default           # показать целевой режим по умолчанию
systemctl set-default graphical.target  # установить GUI режим по умолчанию

systemctl daemon-reload         # перезагрузить конфиги systemd
systemctl reset-failed          # сбросить статус неудачных сервисов

## Systemd таймеры и планировщики

systemctl list-timers           # список всех systemd таймеров
systemctl list-timers --all     # список всех таймеров (включая неактивные)
systemctl start timer-name      # запустить таймер
systemctl enable timer-name     # включить таймер при загрузке
systemctl status timer-name     # статус таймера

## Логи и journalctl

journalctl                      # показать все логи
journalctl -b                   # логи с текущей загрузки
journalctl -b -n 50             # последние 50 строк логов с текущей загрузки
journalctl -b -1                # логи с предыдущей загрузки
journalctl -u service-name      # логи конкретного сервиса
journalctl -u service-name -n 100  # последние 100 строк логов сервиса
journalctl -u service-name -f   # логи сервиса в реальном времени (follow)
journalctl -p err               # логи с приоритетом ERROR и выше
journalctl -p warning           # логи с приоритетом WARNING и выше
journalctl --since "2024-01-15" # логи с определённой даты
journalctl --since "1 hour ago" # логи за последний час
journalctl --until "2024-01-15" # логи до определённой даты
journalctl -o verbose           # подробный формат логов
journalctl -o json              # логи в JSON формате
journalctl -o json-pretty       # красиво отформатированные JSON логи
journalctl --vacuum=2G          # ограничить размер журнала 2GB
journalctl --vacuum=7d          # удалить логи старше 7 дней

tail -f /var/log/syslog         # последние строки логов в реальном времени
tail -n 50 /var/log/syslog      # показать последние 50 строк лога
grep pattern /var/log/syslog    # поиск в логах
grep -i pattern /var/log/syslog # поиск без учёта регистра

## Время и синхронизация

date                            # текущая дата и время
date +"%Y-%m-%d %H:%M:%S"       # показать время в определённом формате
timedatectl                     # информация о времени и часовых поясах
timedatectl list-timezones      # список доступных часовых поясов
timedatectl set-timezone Continent/City  # установить часовой пояс
timedatectl set-time "2024-01-15 14:30:00"  # установить дату/время (требует root)
timedatectl set-ntp true        # включить синхронизацию времени (NTP)
timedatectl set-ntp false       # отключить синхронизацию времени

ntpq -p                         # показать NTP пиры и синхронизацию
ntpstat                         # статус NTP синхронизации
chronyc tracking                # статус Chrony (альтернатива NTP)
chronyc sources                 # источники синхронизации времени

hwclock --show                  # показать время аппаратных часов
hwclock --set --date="2024-01-15 14:30:00"  # установить время на часах (требует root)
hwclock --systohc               # синхронизировать часы с системным временем

## Загрузка и инициализация

systemctl reboot                # перезагрузить систему
systemctl poweroff              # выключить систему
systemctl suspend               # перейти в режим сна
systemctl hibernate             # перейти в режим гибернации

systemd-analyze                 # анализ времени загрузки
systemd-analyze blame           # показать какие сервисы медленнее всего загружаются
systemd-analyze critical-chain  # критическая цепь загрузки

grub-mkconfig -o /boot/grub/grub.cfg  # переписать конфиг GRUB

## Переменные окружения и параметры

env                             # показать все переменные окружения
env | grep PATH                 # показать переменную PATH
echo $PATH                      # показать значение переменной
export VAR_NAME=value           # установить переменную окружения
unset VAR_NAME                  # удалить переменную окружения
printenv                        # показать переменные окружения (альтернатива env)

ulimit -a                       # показать лимиты ресурсов
ulimit -n 4096                  # установить максимальное кол-во открытых файлов

## Мониторинг ресурсов

free -h                         # использование памяти (human-readable)
free -m                         # использование памяти в MB
free -g                         # использование памяти в GB

vmstat 1 5                      # статистика памяти и CPU каждую секунду (5 итераций)
vmstat -s                       # краткая статистика памяти
iostat                          # статистика ввода-вывода
iostat -x                       # расширенная статистика I/O
iostat 1 5                      # статистика каждую секунду (5 итераций)

iotop                           # мониторинг I/O по процессам (требует root)
nethogs                         # мониторинг сети по процессам (требует root)

## Статистика и профилирование

dmesg                           # логи ядра (kernel messages)
dmesg | tail -20                # последние 20 строк логов ядра
dmesg -w                        # логи ядра в реальном времени
dmesg | grep error              # ошибки в логах ядра

strace -p PID                   # трассировка системных вызовов процесса
strace -e trace=open,read,write command  # трассировать конкретные системные вызовы
ltrace command                  # трассировка библиотечных вызовов

perf top                        # профилирование CPU в реальном времени (требует root)
perf record command             # записать профайл команды
perf report                     # показать результаты профайла