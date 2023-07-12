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
## 3. Добавить автозапуск контейнеру, перезагрузить ОС и убедиться, что контейнер действительно запустился самостоятельно
## 4. При создании указать файл, куда записывать логи
## 5. После перезагрузки проанализировать логи


