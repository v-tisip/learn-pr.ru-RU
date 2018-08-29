Последнее, что нам осталось попробовать сделать с виртуальной машиной, — это установить веб-сервер. Один из самых простых для установки пакетов — `nginx`.

1. Найдите общедоступный IP-адрес виртуальной машины Linux. Помните, что для его определения можно использовать команду `vm list-ip-addresses`.

2. Затем откройте подключение `ssh` к машине, как мы делали это при ее тестировании. Помните, что необходимо передать имя администратора (**aldis**).

3. В открывшейся оболочке выполните приведенную ниже команду, чтобы установить веб-сервер `nginx`.

```azurecli
sudo apt-get -y update && sudo apt-get -y install nginx
```

4. В Azure Cloud Shell используйте `curl`, чтобы получить страницу по умолчанию с веб-сервера Linux. Вы также можете открыть новую вкладку в браузере и перейти по общедоступному IP-адресу.

```azurecli
curl 168.61.54.62
```

Страница не откроется, так как виртуальная машина Linux не предоставляет доступ к порту 80 (`http`) через встроенный брандмауэр. К счастью, в Azure CLI для этого есть команда: `vm open-port`. 

5. Чтобы открыть порт 80, введите в Cloud Shell следующую команду:

```
az vm open-port --port 80 --resource-group ExerciseResources --name SampleVM
```

Наконец, снова попробуйте выполнить команду `curl`. На этот раз она должна вернуть данные. Страница также должна отобразиться в браузере.


