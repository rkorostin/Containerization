# Механизмы контрольных групп

## **Выполняется все под root**
## 1. Запустить контейнер с ubuntu, используя механизм LXC
а) Устанавливаем необходимые пакеты
```
apt-get update
apt-get install lxc
```
b) Создаём новый контейнер с именем "gbcontainer":
```
lxc-create -t download -n gbcontainer -- -d ubuntu -r focal -a amd64
```
c) Запускаем контейнер:
```
lxc-start -n gbcontainer
```
d) Смотрим
```
lxc-ls -f
```
![tasks_1](https://github.com/rkorostin/Images/blob/main/container/task1.gif)
## 2. Ограничить контейнер 256 Мб ОЗУ и проверить, что ограничение работает
a) Стопим контейнер:
```
lxc-stop -n gbcontainer
```
b) Редактируем конфигурационный файл контейнера:
```
vi /var/lib/lxc/gbcontainer/config
```
c) Добавляем следующую строку в конфигурацию, чтобы ограничить ОЗУ до 256 МБ:
```
lxc.cgroup2.memory.max = 256M
```
d) Запускаем контейнер
```
lxc-start -n gbcontainer
```
e) Проверяем, что ограничение работает, выполнив команду в контейнере:
```
free -m
```
![tasks_2](https://github.com/rkorostin/Images/blob/main/container/task2.gif)
## 3. Добавить автозапуск контейнеру, перезагрузить ОС и убедиться, что контейнер действительно запустился самостоятельно
a) Стопим контейнер:
```
lxc-stop -n gbcontainer
```
b) Редактируем конфигурационный файл для автозапуска контейнера:
```
vi /var/lib/lxc/gbcontainer/config
```
c) Добавляем следующую строку в конфигурацию, чтобы контейнер запускался автоматически при загрузке ОС:
```
lxc.start.auto = 1
```
d) Пезагружаем ОС:
```
reboot
```

e) После перезагрузки проверяем, что контейнер запустился самостоятельно:
```
lxc-ls -f
```
![tasks_3](https://github.com/rkorostin/Images/blob/main/container/task3.gif)
## 4. При создании указать файл, куда записывать логи
a) Стопим контейнер:
```
lxc-stop -n gbcontainer
```
b) Редактируем конфигурационный файл контейнера:
```
vi /var/lib/lxc/gbcontainer/config
```
c) Добавляем следующую строку в конфигурацию, чтобы указать файл для записи логов:
```
lxc.console.logfile = /var/log/lxc/gbcontainer.log
```
d) Создаём директорию и файл для хранения логов (если их нет):
```
mkdir /var/log/lxc
touch /var/log/lxc/gbcontainer.log
```
e) Запусткаем/стопим контейнер:
```
lxc-start -n gbcontainer
lxc-stop -n gbcontaine
lxc-start -n gbcontainer
```
## 5. После перезагрузки проанализировать логи
```
cat /var/log/lxc/gbcontainer.log
```
![tasks_4-5](https://github.com/rkorostin/Images/blob/main/container/task4_5.gif)

