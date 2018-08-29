<span data-ttu-id="b421f-101">Последнее, что нам осталось попробовать сделать с виртуальной машиной, — это установить веб-сервер.</span><span class="sxs-lookup"><span data-stu-id="b421f-101">The last thing we want to try on our VM is to install a web server.</span></span> <span data-ttu-id="b421f-102">Один из самых простых для установки пакетов — `nginx`.</span><span class="sxs-lookup"><span data-stu-id="b421f-102">One of the easiest packages to install is `nginx`.</span></span>

1. <span data-ttu-id="b421f-103">Найдите общедоступный IP-адрес виртуальной машины Linux.</span><span class="sxs-lookup"><span data-stu-id="b421f-103">Locate the public IP address of your Linux virtual machine.</span></span> <span data-ttu-id="b421f-104">Помните, что для его определения можно использовать команду `vm list-ip-addresses`.</span><span class="sxs-lookup"><span data-stu-id="b421f-104">Remember you can use the `vm list-ip-addresses` command to look it up.</span></span>

2. <span data-ttu-id="b421f-105">Затем откройте подключение `ssh` к машине, как мы делали это при ее тестировании.</span><span class="sxs-lookup"><span data-stu-id="b421f-105">Next, open an `ssh` connection to the machine like you did when we tested it.</span></span> <span data-ttu-id="b421f-106">Помните, что необходимо передать имя администратора (**aldis**).</span><span class="sxs-lookup"><span data-stu-id="b421f-106">Remember you will need to pass in the admin name ("**aldis**").</span></span>

3. <span data-ttu-id="b421f-107">В открывшейся оболочке выполните приведенную ниже команду, чтобы установить веб-сервер `nginx`.</span><span class="sxs-lookup"><span data-stu-id="b421f-107">In the presented shell, execute the following command to install the `nginx` web server.</span></span>

```azurecli
sudo apt-get -y update && sudo apt-get -y install nginx
```

4. <span data-ttu-id="b421f-108">В Azure Cloud Shell используйте `curl`, чтобы получить страницу по умолчанию с веб-сервера Linux.</span><span class="sxs-lookup"><span data-stu-id="b421f-108">In Azure Cloud Shell, use `curl` to read the default page from your Linux web server.</span></span> <span data-ttu-id="b421f-109">Вы также можете открыть новую вкладку в браузере и перейти по общедоступному IP-адресу.</span><span class="sxs-lookup"><span data-stu-id="b421f-109">Alternatively, you can open a new browser tab and browse to the public IP address.</span></span>

```azurecli
curl 168.61.54.62
```

<span data-ttu-id="b421f-110">Страница не откроется, так как виртуальная машина Linux не предоставляет доступ к порту 80 (`http`) через встроенный брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="b421f-110">It will fail because the Linux virtual machine doesn't expose port 80 (`http`) through the built-in firewall.</span></span> <span data-ttu-id="b421f-111">К счастью, в Azure CLI для этого есть команда: `vm open-port`.</span><span class="sxs-lookup"><span data-stu-id="b421f-111">Luckily, the Azure CLI has a command for that: `vm open-port`.</span></span> 

5. <span data-ttu-id="b421f-112">Чтобы открыть порт 80, введите в Cloud Shell следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b421f-112">Type the following into Cloud Shell to open port 80:</span></span>

```
az vm open-port --port 80 --resource-group ExerciseResources --name SampleVM
```

<span data-ttu-id="b421f-113">Наконец, снова попробуйте выполнить команду `curl`.</span><span class="sxs-lookup"><span data-stu-id="b421f-113">Finally, try `curl` again.</span></span> <span data-ttu-id="b421f-114">На этот раз она должна вернуть данные.</span><span class="sxs-lookup"><span data-stu-id="b421f-114">This time it should return data.</span></span> <span data-ttu-id="b421f-115">Страница также должна отобразиться в браузере.</span><span class="sxs-lookup"><span data-stu-id="b421f-115">You can see the page in a browser as well.</span></span>



