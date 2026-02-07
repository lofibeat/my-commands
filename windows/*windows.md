```powershell

🪟 Windows команды (CMD и PowerShell)

## Информация о системе

### CMD

systeminfo                      # полная информация о системе
wmic os get caption,version     # версия Windows
wmic os get buildnumber         # номер сборки
hostname                        # имя компьютера
echo %USERDOMAIN%               # показать домен
echo %USERNAME%                 # текущий пользователь
whoami                          # текущий пользователь (формат domain\user)
wmic logicaldisk get name       # список дисков
wmic cpu get name,numberofcores # информация о CPU
wmic memorychip get capacity    # объём оперативной памяти
ipconfig                        # конфигурация сетевых интерфейсов
ipconfig /all                   # подробная информация об интерфейсах
date /t                         # текущая дата
time /t                         # текущее время

### PowerShell

Get-ComputerInfo                # полная информация о системе
[System.Environment]::OSVersion # версия ОС
$env:COMPUTERNAME               # имя компьютера
$env:USERNAME                   # текущий пользователь
whoami                          # текущий пользователь
Get-PSDrive                     # список дисков и путей
Get-CimInstance Win32_Processor # информация о процессоре
Get-CimInstance Win32_PhysicalMemory | Measure-Object -Property Capacity -Sum  # объём памяти
Get-NetAdapter                  # информация об интерфейсах
Get-NetIPConfiguration          # IP конфигурация
Get-Date                        # текущая дата и время
Get-Date -Format "yyyy-MM-dd HH:mm:ss"  # форматированная дата и время

## Управление файлами и папками

### CMD

dir                             # список файлов в текущей папке
dir /A                          # показать все файлы (включая скрытые)
dir /S                          # рекурсивный список (со всеми подпапками)
dir /O:S                        # отсортировать по размеру
dir C:\Users                    # список конкретной папки
cd folder                       # перейти в папку
cd ..                           # перейти в родительскую папку
cd \                            # перейти в корень диска
pwd (или echo %cd%)             # показать текущий путь
mkdir folder                    # создать папку
mkdir C:\path\to\folder         # создать с полным путём
rmdir folder                    # удалить пустую папку
rmdir /s folder                 # удалить папку рекурсивно (с содержимым)
del file.txt                    # удалить файл
del *.txt                       # удалить все .txt файлы
copy file.txt newfile.txt       # копировать файл
copy file.txt C:\path\          # копировать в другую папку
xcopy source dest /E /I /Y      # копировать папку рекурсивно
move file.txt newfile.txt       # переместить/переименовать
ren oldname.txt newname.txt     # переименовать файл
type file.txt                   # показать содержимое файла
more file.txt                   # показать по страницам
findstr "text" file.txt         # поиск в файле
findstr /R "pattern" file.txt   # регулярное выражение

### PowerShell

Get-Item file.txt               # информация о файле
Get-ChildItem                   # список файлов текущей папки
Get-ChildItem -Force            # список со скрытыми файлами
Get-ChildItem -Recurse          # рекурсивный список
Get-ChildItem | Sort-Object Length -Descending  # отсортировать по размеру
Get-Location                    # текущий путь
Set-Location folder             # перейти в папку
New-Item -ItemType Directory -Path C:\folder  # создать папку
New-Item -ItemType File -Path C:\file.txt     # создать пустой файл
Remove-Item file.txt            # удалить файл
Remove-Item folder -Recurse     # удалить папку рекурсивно
Copy-Item file.txt newfile.txt  # копировать файл
Copy-Item folder newfolderr -Recurse  # копировать папку
Move-Item file.txt C:\path\     # переместить файл
Rename-Item oldname newname     # переименовать
Get-Content file.txt            # показать содержимое файла
Get-Content file.txt -Head 20   # первые 20 строк
Get-Content file.txt -Tail 10   # последние 10 строк
Select-String -Path file.txt -Pattern "text"  # поиск текста

## Процессы и управление ими

### CMD

tasklist                        # список всех процессов
tasklist /V                     # подробный список процессов
tasklist | findstr process-name # найти процесс
wmic process list brief         # список процессов через WMI
wmic process where name="process.exe" get processid  # найти PID процесса
taskkill /IM process.exe        # завершить процесс по имени
taskkill /PID 1234              # завершить процесс по PID
taskkill /F /IM process.exe     # принудительное завершение (/F = force)

### PowerShell

Get-Process                     # список всех процессов
Get-Process | Sort-Object CPU -Descending  # отсортировать по CPU
Get-Process | Sort-Object Memory -Descending  # отсортировать по памяти
Get-Process -Name process-name  # найти конкретный процесс
Get-Process | Where-Object {$_.ProcessName -eq "process.exe"}
Stop-Process -Name process.exe  # завершить процесс
Stop-Process -Id 1234           # завершить по PID
Stop-Process -Name process.exe -Force  # принудительное завершение
Start-Process notepad.exe       # запустить приложение
Start-Process -FilePath "C:\path\app.exe" -ArgumentList "-arg1 value1"

## Сетевые команды

### CMD

ipconfig                        # IP конфигурация
ipconfig /all                   # подробная информация
ipconfig /release               # освободить IP
ipconfig /renew                 # получить новый IP
ping host                       # проверить доступность
ping -n 4 host                  # отправить 4 пинга
ping -t host                    # непрерывный пинг (Ctrl+C для выхода)
tracert host                    # трассировка маршрута
nslookup domain                 # DNS запрос
nslookup domain 8.8.8.8         # запрос к конкретному DNS
netstat -an                     # показать соединения и порты
netstat -ano                    # с информацией о процессах
netstat -an | findstr :80       # соединения на порту 80
netstat -s                      # статистика по протоколам
arp -a                          # ARP таблица
route print                     # таблица маршрутизации
route add 192.168.0.0 mask 255.255.255.0 192.168.1.1  # добавить маршрут

### PowerShell

Get-NetIPConfiguration          # IP конфигурация
Get-NetAdapter                  # информация об интерфейсах
Get-NetIPAddress                # список IP адресов
Test-NetConnection host -Port 80  # проверить доступность порта
Test-NetConnection -ComputerName host -Port 443 -InformationLevel Detailed
Resolve-DnsName domain          # DNS запрос
Resolve-DnsName domain -Server 8.8.8.8  # запрос к конкретному DNS
Get-NetTCPConnection            # TCP соединения
Get-NetTCPConnection | Where-Object {$_.LocalPort -eq 80}
Get-NetTCPConnection | Select-Object -Property LocalAddress,LocalPort,RemoteAddress,State
Get-NetRoute                    # таблица маршрутизации
Test-Connection host -Count 4   # пинг (отправить 4 пакета)
Test-Connection host -Continuous  # непрерывный пинг
Trace-NetRoute -HostName host   # трассировка (PowerShell 6.0+)

## Управление сервисами

### CMD

sc query                        # список всех сервисов
sc query type= service          # список сервисов (не драйверов)
sc query state= running         # список запущенных сервисов
sc query service-name           # статус конкретного сервиса
sc start service-name           # запустить сервис
sc stop service-name            # остановить сервис
sc pause service-name           # приостановить сервис
sc continue service-name        # возобновить сервис
sc config service-name start= auto  # установить автозапуск
sc config service-name start= disabled  # отключить запуск
net start service-name          # запустить сервис (альтернатива)
net stop service-name           # остановить сервис

### PowerShell

Get-Service                     # список всех сервисов
Get-Service | Where-Object {$_.Status -eq "Running"}  # только запущенные
Get-Service -Name service-name  # статус конкретного сервиса
Start-Service -Name service-name  # запустить сервис
Stop-Service -Name service-name  # остановить сервис
Restart-Service -Name service-name  # перезапустить сервис
Set-Service -Name service-name -StartupType Automatic  # автозапуск
Set-Service -Name service-name -StartupType Disabled   # отключить запуск

## Управление пользователями (требует Admin)

### CMD

net user                        # список пользователей
net user username               # информация о пользователе
net user username password /add # создать пользователя
net user username /delete       # удалить пользователя
net user username /active:no    # отключить пользователя
net localgroup administrators   # список администраторов
net localgroup administrators username /add  # добавить в админ группу
wmic useraccount list brief     # список через WMI

### PowerShell

Get-LocalUser                   # список локальных пользователей
Get-LocalUser -Name username    # информация о пользователе
New-LocalUser -Name username -Password (ConvertTo-SecureString "password" -AsPlainText -Force)  # создать пользователя
Remove-LocalUser -Name username  # удалить пользователя
Get-LocalGroup                  # список групп
Get-LocalGroupMember -Group administrators  # члены группы админ
Add-LocalGroupMember -Group administrators -Member username  # добавить в админ

## Логи и события

### CMD

wmic logicalevent list          # список логических событий
wmic qfe list                   # список установленных обновлений
tasklist /v /fo csv > processes.csv  # экспортировать в CSV

### PowerShell

Get-EventLog -List              # список логов событий
Get-EventLog -LogName Application -Newest 10  # последние 10 событий
Get-EventLog -LogName System -EntryType Error  # ошибки в системном логе
Get-EventLog -LogName Application | Where-Object {$_.EventID -eq 1000}
Get-HotFix                      # список установленных обновлений
Get-HotFix | Sort-Object InstalledOn -Descending  # отсортировать по дате

## Управление дисками

### CMD

diskpart                        # интерактивное управление дисками
wmic logicaldisk get name,size,freespace  # информация о дисках
chkdsk C:                       # проверить диск
chkdsk C: /F                    # проверить и исправить ошибки
defrag C: /U /V                 # дефрагментация

### PowerShell

Get-Volume                      # информация о томах
Get-Disk                        # информация о дисках
Get-Partition                   # информация о разделах
Get-Volume | Select-Object DriveLetter, FileSystemLabel, Size, SizeRemaining
Repair-Volume -DriveLetter C -OfflineScandisk  # проверить диск

## Установка пакетов и приложений

### CMD

choco install package-name      # установить через Chocolatey (если установлен)
choco list                      # список установленных пакетов
winget install package-name