# Установка и настройка VirtualBox под управлением CentOS 7x.

Подготовка операционной системы после установки, установка производилась из образа: http://isoredirect.centos.org/centos/7/isos/x86_64/CentOS-7-x86_64-Minimal-1708.iso
Выполните в терминале:

```
yum -y update && yum -y install mc nano net-tools bash-completion wget
```

После установки необходимых пакетов, перезагрузите систему, т.к., после обновления возможно установка новых ядер системы. 
После перезагрузки проверьте количество установленных ядер:

```
rpm -q kernel
```

Удалите неиспользуемые ядра, по желанию. Перейдите в каталог хранения конфигурации репозиториев. 

```
cd /etc/yum.repos.d/
```

Скачайте  последний доступный репозиторий, на сайте https://www.virtualbox.org, на данный момент актуальный репозиторий: 

```
wget http://download.virtualbox.org/virtualbox/rpm/rhel/virtualbox.repo
```

Обновите дерево пакетов и установите последнюю версию VirtualBox:

```
yum -y update && yum -y install VirtualBox-5.2.x86_64
```

Для корректной работы всех модулей, установите следующие пакеты:

```
yum -y install gcc make perl kernel-devel kernel-devel-3.10.0-693.11.1.el7.x86_6
```

Выполните конфигурирование модулей VirtualBox:

```
/usr/lib/virtualbox/vboxdrv.sh setup
```

После конфигурирования, запустите сервис и проверьте его статус:

```
systemctl start vboxdrv.service && systemctl status vboxdrv.service
```

Для удаленного мониторинга гипервизора установите следующие пакеты:

```
yum -y install xauth libxkbcommon.x86_64 xorg-x11-xkb-utils.x86_64 dejavu-lgc-sans-fonts
```

В домашней директории создайте файл: 

```
touch .Xauthority
```

На этом настройка закончена, можно подключаться и использовать гипервизор.
