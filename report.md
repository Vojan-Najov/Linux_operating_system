# UNIX/Linux operating systems (Basic).

## Contents

1. [Installation of the OS](#part-1-installation-of-the-os)
2. [Creating a user](#part-2-creating-a-user)
3. [Setting up of the OS network](#part-3-setting-up-of-the-os-network)
4. [OS Update](#part-4-os-update)
5. [Using the sudo command](#part-5-using-the-sudo-command)
6. [Installing and configuring the time service](#part-6-installing-and-configuring-the-time-service)
7. [Installing and using text editors](#part-7-installing-and-using-text-editors)
8. [Installing and basic setup of the SSHD service](#part-8-installing-and-basic-setup-of-the-sshd-service)
9. [Installing and using the top, htop utilities](#part-9-installing-and-using-the-top-htop-utilities)
10. [Using the fdisk utility](#part-10-using-the-fdisk-utility)
11. [Using the df utility](#part-11-using-the-df-utility)
12. [Using the du utility](#part-12-using-the-du-utility)
13. [Installing and using the ncdu utility](#part-13-installing-and-using-the-ncdu-utility)
14. [Working with system logs](#part-14-working-with-system-logs)
15. [Using the CRON job scheduler](#part-15-using-the-cron-job-scheduler)

## Part 1. Installation of the OS

#### Установить Ubuntu 20.04 Server LTS без графического интерфейса. (Используем программу для виртуализации - VirtualBox)

- Загрузка образа операционной системы ubuntu-20.04 LTS и проверка чек-суммы. \
  <img src="./misc/images/check_shasum.png" alt="check_shasum" width="700"/>
- Конфигурация новой виртуальной машины в Oracle VM VirtualBox:
  - Создание новой виртуальной машины в Oracle VM VirtualBox \
    <img src="./misc/images/vm_configure_1.png" alt="vm_configure_1" width="500"/>
  - Настройка аппаратного обеспечения виртуальной машины \
    <img src="./misc/images/vm_configure_2.png" alt="vm_configure_2" width="500"/>
  - Создание виртуального жесткого диска \
    <img src="./misc/images/vm_configure_3.png" alt="vm_configure_3" width="500"/>
  - Итоговые настройки виртуальной машины \
    <img src="./misc/images/vm_configure_4.png" alt="vm_configure_4" width="500"/>
- Установка операционной системы на виртуальную машину:
  - Выбор языка \
    <img src="./misc/images/install_01.png" alt="install_01" width="500"/>
  - Выбор расскладки клавиатуры \
    <img src="./misc/images/install_02.png" alt="install_02" width="500"/>
  - Настройка сетевого интерфейса (по умолчанию) \
    <img src="./misc/images/install_03.png" alt="install_03" width="500"/>
  - Настройка прокси (по умолчанию) \
    <img src="./misc/images/install_04.png" alt="install_04" width="500"/>
  - Выбор зеркала архива Ubuntu (по умолчанию) \
    <img src="./misc/images/install_05.png" alt="install_05" width="500"/>
  - Разбиение жесткого диска (по умолчанию) \
    <img src="./misc/images/install_06.png" alt="install_06" width="500"/>
  - Результат разиения жесткого диска \
    <img src="./misc/images/install_07.png" alt="install_07" width="500"/>
  - Настройки профиля (имя пользователя, название машины, задание пароля) \
    <img src="./misc/images/install_08.png" alt="install_08" width="500"/>
  - Установка ssh (по умолчнию нет) \
    <img src="./misc/images/install_09.png" alt="install_09" width="500"/>
  - Установка дополнительных snap пакетов (по умолчанию нет) \
    <img src="./misc/images/install_10.png" alt="install_10" width="500"/>
  - Установка завершена \
    <img src="./misc/images/install_11.png" alt="install_11" width="500"/>
- Версия установенной операционной системы \
  <img src="./misc/images/os_version.png" alt="os_version" width="700"/> \
  `/etc/issue` это текстовый файл, в котором содержится сообщение о индитификаторе системы.

[VirtualBox User Manual](https://www.virtualbox.org/manual/UserManual.html) \
[Basic installation tutorial](https://ubuntu.com/server/docs/installation) \
[/etc/issue man-page](https://manpages.ubuntu.com/manpages/focal/en/man5/issue.5.html)

## Part 2. Creating a user

#### Cоздать нового пользователя и добавить его в группу adm.

- Cоздать нового пользователя: \
  <img src="./misc/images/create_user_01.png" alt="create_user_01" width="700"/>
  - Утилита `useradd` позволяет создать нового пользователя. \
    Опция `-G` позволяет добавить пользователя в определенные группы. \
    Oпция `-s` - назначить командную оболочку по умолчанию.\
    Опция `-с` - добавить информацию о пользователе. \
    Опция `-d` - назначить домашнюю директорию.
  - С помощью утилиты `passwd` назначаем пароль для нового пользователя.
  - C помощью утилиты `mkdir` создаем домашнюю директорию для нового пользователя.
  - C помощью утилиты `chown` меняем владельца домашней директории на нового пользователя.
  - C помощью утилиты `su` меняем пользователя. Переходим в домашний каталог. \
    Используя утилиту `groups`, отображаем группы, в которых состоит новый пользователь. \
    Члены группы adm имеют права для чтения журналов. Пробуем прочитать файл `/var/log/syslog`.
- Файл `/etc/passwd` содержит информацию о всех пользовательских аккаунтах.
  <img src="./misc/images/create_user_02.png" alt="create_user_02" width="700"/>
- Строка, содержащая информацию о новом пользователе. \
  <img src="./misc/images/create_user_03.png" alt="create_user_03" width="700"/>

[Ubuntu user management](https://ubuntu.com/server/docs/security-users) \
[useradd man-page](https://manpages.ubuntu.com/manpages/focal/en/man8/useradd.8.html) \
[passwd man-page](https://manpages.ubuntu.com/manpages/focal/en/man1/passwd.1.html) \
[mkdir man-page](https://manpages.ubuntu.com/manpages/focal/en/man1/mkdir.1.html) \
[chown man-page](https://manpages.ubuntu.com/manpages/focal/en/man1/chown.1.html) \
[su man-page](https://manpages.ubuntu.com/manpages/focal/en/man1/su.1.html) \
[groups man-page](https://manpages.ubuntu.com/manpages/focal/en/man1/groups.1.html) \
[/etc/passwd man-page](https://manpages.ubuntu.com/manpages/focal/en/man5/passwd.5.html)
