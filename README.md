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
lxc-start -n mycontainer
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
vi /var/lib/lxc/mycontainer/config
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
## 4. При создании указать файл, куда записывать логи
## 5. После перезагрузки проанализировать логи


