# Установка и настройка ОС Ubuntu

## Часть 1. Установка ОС

1. Определение версии Ubuntu:
    ```bash
        cat /etc/issue
    ```
    ![img](images/1.png)

## Часть 2. Создание пользователя

1. Просмотр существующих пользователей:
    ```bash
        cat /etc/passwd
    ```
    ![img](images/2.png)

2. Добавление нового пользователя:
    ```bash
        sudo useradd <имя пользователя>
    ```
    ![img](images/3.png)

3. Добавление пользователя в группу `adm`:
    ```bash
        sudo usermod -aG adm <имя пользователя>
    ```
    ![img](images/4.png)

4. Проверка созданного пользователя:
    ```bash
        cat /etc/passwd
    ```
    ![img](images/5.png)

## Часть 3. Настройка сети ОС

1. Задание имени машины:
    ```bash
        sudo vim /etc/hostname
    ```
    ![img](images/6.png)

2. Просмотр сетевых интерфейсов:
    ```bash
        ls /sys/class/net
    ```
    ![img](images/9.png)

    *Примечание*: `lo` - это loopback интерфейс, используемый для отладки.

3. Установка часового пояса:
    ```bash
        sudo timedatectl set-timezone Europe/Moscow
    ```
    ![img](images/7.png)

4. Проверка времени:
    ```bash
        timedatectl
    ```
    ![img](images/8.png)

5. Определение IP-адреса устройства:
    ```bash
        ifconfig
    ```
    ![img](images/10.png)

    *Примечание*: DHCP - протокол для автоматической настройки IP-адресов и других параметров сети.

6. Определение внешнего и внутреннего IP-адресов:
    ```bash
        ip route | grep default
    ```
    ![img](images/11.png)

    ```bash
        route -n
    ```
    ![img](images/12.png)

7. Настройка статического IP, шлюза и DNS:
    Открываем файл конфигурации:

    ```bash
        sudo vim /etc/netplan/01-netcfg.yaml
    ```
    ![img](images/13.png)
    ![img](images/14.png)

    Применение настроек:
    ```bash
        sudo netplan apply
    ```
    ![img](images/15.png)

8. Перезагрузка виртуальной машины.

9. Проверка подключения к удалённым хостам:
    Команда для проверки:
    Вывод должен содержать фразу `0% packet loss`.
    ```bash
        ping <адрес хоста>
    ```

    ![img](images/16.png)
    ![img](images/17.png)

## Part 4. Обновление ОС
1. Обновить системные пакеты до последней на момент выполнения задания версии.
```bash
    sudo apt-get update
```
![img](images/18.png)

```bash
    sudo apt-get upgrade
```
![img](images/19.png)

## Part 5. Использование команды sudo
1. Разрешить пользователю, созданному в Part 2, выполнять команду sudo.
```bash
    sudo usermod -aG sudo username
```
![img](images/20.png)

2. Поменять hostname ОС от имени пользователя
```bash
    sudo hostnamectl set-hostname name
```
![img](images/21.png)
```bash
    sudo (англ. Substitute User and do, дословно «подменить пользователя и выполнить») — программа для системного администрирования UNIX-систем, позволяющая делегировать те или иные привилегированные ресурсы пользователям с ведением протокола работы.
```

## Part 6. Установка и настройка службы времени
1. Настроить службу автоматической синхронизации времени.

2. Время, часового пояса, в котором я сейчас нахожусь.
```bash
    timedatectl
```
![img](images/22.png)
```bash
    Вывод следующей команды должен содержать `NTPSynchronized=yes: timedatectl status`
```

```bash
    timedatectl show
```
![img](images/23.png)

## Part 7. Установка и использование текстовых редакторов
1. Установить текстовые редакторы VIM (+ любые два по желанию NANO, MCEDIT, JOE и т.д.)

```bash
    sudo apt install nano
```
![img](images/24.png)

```bash
    sudo apt install mcedit
```
![img](images/25.png)

2. Используя каждый из трех выбранных редакторов, создайте файл test_X.txt, где X -- название редактора, в котором создан файл. Написать в нём свой никнейм, закрыкть файл с сохранением изменений.
 
```bash
    vim test_vim.txt
```
```bash
    Вышел с сохранением таким образом: `:wq`
```
![img](images/26.png)

```bash
    nano /etc/test_nano.txt
```
```bash
    Вышел с сохранением таким образом: `ctrl+o+x`
```
![img](images/27.png)

```bash
    mcedit test_mcedit.txt
```
```bash
    Вышел с сохранением таким образом: `f2+f10`
```
![img](images/28.png)

3. Используя каждый из трех выбранных редакторов, открываю файл на редактирование, отредактировал файл, заменив никнейм на строку "21 School 21", закрываю файл без сохранения изменений.

```bash
    vim test_vim.txt
```
```bash
    Вышел без сохранения таким образом: `:q!`
```
![img](images/29.png)

```bash
    sudo nano /etc/test_nano.txt
```
```bash
    Вышел без сохранения таким образом: `ctrl+x`
```
![img](images/30.png)

```bash
    mcedit /etc/test_mcedit.txt
```
```bash
    Вышел без сохранения таким образом: `f10`
```
![img](images/31.png)

4. Используя каждый из трех выбранных редакторов, нужно отредактировать файл ещё раз (по аналогии с предыдущим пунктом), а затем освоить функции поиска по содержимому файла (слово) и замены слова на любое другое.

```bash
    vim test_vim.txt
```
```bash
    /поиск слова
```
![img](images/32.png)

```bash
    :s/слово/новое слово/g
```
![img](images/33.png)

5. nano
```bash
    ctrl+w поиск слова
```
```bash
    ctrl+w поиск слова
```
```bash
    ctrl+\замена
```
![img](images/34.png)
![img](images/35.png)

6. mcedit
```bash
    поиск f7
```

![img](images/36.png)
```bash
    замена f4
```
![img](images/37.png)

## Part 8. Установка и базовая настройка сервиса SSHD
1. Установить службу SSHd.
```bash
    sudo apt-get install ssh
    sudo apt install openssh-server
```
![img](images/38.png)
![img](images/40.png)

2. Добавить автостарт службы при загрузке системы
```bash
    systemctl status sshd
```
![img](images/39.png)


3. Перенастроить службу SSHd на порт 2022.
```bash
    sudo vim /etc/ssh/sshd_config
```
![img](images/41.png)

4. Перезагрузить систему.
```bash
    systemctl restart sshd
```
![img](images/42.png)

```bash
    ps aux | grep sshd
```
![img](images/43.png)

```bash
    netstat -tan
```
![img](images/44.png)

```bash
    Команда netstat -tan
    Команда ps aux | grep sshd
```
5. ps aux показывает все процессы, их состояние и дополнительную информацию.
grep sshd фильтрует вывод, чтобы показать только процессы, связанные с sshd.

-t — показывает только TCP соединения.
-a — показывает все активные соединения и порты, на которых прослушиваются подключения.
-n — отображает IP-адреса и порты в числовом формате.

Recv-Q -количество запросов в очередях на приём на данном узле/компьютере
Send-Q -количество запросов в очередях на отправку на данном узле/компьютере
Local Address - адрес и номер локального конца сокета
Foreign Address - адрес и номер порта удаленного порта сокета

## Part 9. Установка и использование утилит top, htop
1. Установить и запустить утилиты top и htop.
```bash
    sudo apt update
    sudo apt install procps htop
```
![img](images/45.png)

```bash
    top
```
![img](images/46.png)

```bash
    uptime & количество пользователей
```
![img](images/47.png)

```bash
   общая загрузка системы
```
![img](images/48.png)

```bash
    общее количество процессов
```
![img](images/49.png)


```bash
    загрузка cpu
```
![img](images/50.png)

```bash
    загрузку памяти
```
![img](images/51.png)

```bash
    pid процесса занимающего больше всего памяти
```
![img](images/52.png)

```bash
    pid процесса, занимающего больше всего процессорного времении
```
![img](images/53.png)

```bash
    htop
```
![img](images/54.png)

```bash
    отсортированны по PID
```
![img](images/55.png)

```bash
    отсортированны по PERCENT_CPU
```
![img](images/56.png)

```bash
    отсортированны по PERCENT_MEM
```
![img](images/57.png)

```bash
    отсортированны по TIME
```
![img](images/58.png)

```bash
    отфильтрованный для процесса sshd
```
![img](images/59.png)

```bash
    с процессом syslog, найденным, используя поиск
```
![img](images/60.png)

```bash
    с добавленным выводом hostname, clock и uptime
```
![img](images/61.png)

## Part 10. Использование утилиты fdisk
1. Запустить команду fdisk -l.
```bash
    sudo fdisk -l
```

```bash
    название жесткого диска
```
![img](images/62.png)

```bash
    размер и количество секторов
```
```bash
    free -h
```
![img](images/63.png)

## Part 11. Использование утилиты df
1. Запустить команду df.

```bash
    df /root
```
![img](images/64.png)
```bash
    размер раздела = 11758760
```
```bash
    размер занятого пространства = 3362600
```
```bash
    размер свободного пространства = 7777052
```
```bash
    процент использования = 31%
```
```bash
    вывод = килобайты
```
2. Запусти команду df -Th.

```bash
    df -Th /root
```
![img](images/65.png)

```bash
    размер раздела = 12G
```
```bash
    размер занятого пространства = 3.3G
```
```bash
    размер свободного пространства = 7.5G
```
```bash
    процент использования = 31%
```
```bash
    тип раздела = ext4
```

## Part 12. Использование утилиты du
1. Вывести размер папок /home, /var, /var/log (в байтах)

```bash
    sudo du -sb /home
```
![img](images/67.png)

```bash
    sudo du -sb /var
```
![img](images/68.png)

```bash
    sudo du -sb /var/log
```
![img](images/69.png)

## Part 13. Установка и использование утилиты ncdu
1. Установить утилиту ncdu
```bash
    sudo apt install ncdu
```
![img](images/66.png)

```bash
    sudo ncdu /var
```
![img](images/70.png)

```bash
    sudo ncdu /home
```
![img](images/71.png)

```bash
    sudo ncdu /var/log
```
![img](images/72.png)

## Part 14. Работа с системными журналами
```bash
    sudo less /var/log/dmesg
```
![img](images/73.png)

```bash
    sudo less /var/log/syslog
```
![img](images/74.png)

```bash
    sudo less /var/log/auth.log
```
![img](images/75.png)

```bash
    время последней успешной авторизации = Jul 31 16:06:00

    имя пользователя = timmi-serv

    метод входа в систему = sudo
```
Перезапустить службу SSHd.
```bash
    sudo systemctl restart ssh.service
```
![img](images/77.png)
```bash
    cat /var/log/syslog | grep ssh
```
![img](images/76.png)

## Part 15. Использование планировщика заданий CRON

```bash
    crontab -e
```
![img](images/78.png)

```bash
    grep 'uptime' /var/log/syslog
```
![img](images/79.png)

```bash
    crontab -l
    `Cписок текущих задач`
```
![img](images/80.png)
```bash
    crontab -r
    `Удаление всех заданий из планировщика задач`
```
