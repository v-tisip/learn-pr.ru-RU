<span data-ttu-id="7c033-101">Azure CLI содержит команду `vm` для работы с виртуальными машинами в Azure.</span><span class="sxs-lookup"><span data-stu-id="7c033-101">The Azure CLI includes the `vm` command to work with virtual machines in Azure.</span></span> <span data-ttu-id="7c033-102">Мы можем передать несколько подкоманд для выполнения определенных задач.</span><span class="sxs-lookup"><span data-stu-id="7c033-102">We can supply several subcommands to do specific tasks.</span></span> <span data-ttu-id="7c033-103">Наиболее распространенные подкоманды:</span><span class="sxs-lookup"><span data-stu-id="7c033-103">The most common include:</span></span>

| <span data-ttu-id="7c033-104">Подкоманда</span><span class="sxs-lookup"><span data-stu-id="7c033-104">Sub-command</span></span> | <span data-ttu-id="7c033-105">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="7c033-105">Description</span></span> |
|-------------|-------------|
| `create`    | <span data-ttu-id="7c033-106">Создание новой виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="7c033-106">Create a new virtual machine</span></span> |
| `deallocate` | <span data-ttu-id="7c033-107">Освобождение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="7c033-107">Deallocate a virtual machine</span></span> |
| `delete` | <span data-ttu-id="7c033-108">Удаление виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="7c033-108">Delete a virtual machine</span></span> |
| `list` | <span data-ttu-id="7c033-109">Вывод списка созданных виртуальных машин в подписке</span><span class="sxs-lookup"><span data-stu-id="7c033-109">List the created virtual machines in your subscription</span></span> |
| `open-port` | <span data-ttu-id="7c033-110">Открытие определенного сетевого порта для входящего трафика</span><span class="sxs-lookup"><span data-stu-id="7c033-110">Open a specific network port for inbound traffic</span></span> |
| `restart` | <span data-ttu-id="7c033-111">Перезапуск виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="7c033-111">Restart a virtual machine</span></span> |
| `show` | <span data-ttu-id="7c033-112">Получение сведений для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="7c033-112">Get the details for a virtual machine</span></span> |
| `start` | <span data-ttu-id="7c033-113">Запуск остановленной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="7c033-113">Start a stopped virtual machine</span></span> |
| `stop` | <span data-ttu-id="7c033-114">Остановка запущенной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="7c033-114">Stop a running virtual machine</span></span> |
| `update` | <span data-ttu-id="7c033-115">Обновление свойства виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="7c033-115">Update a property of a virtual machine</span></span> |

> [!NOTE]
> <span data-ttu-id="7c033-116">Полный список команд см. в [справочной документации по Azure CLI](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="7c033-116">For a complete list of commands, you can check the [Azure CLI reference documentation](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest).</span></span>

<span data-ttu-id="7c033-117">Давайте начнем с первой: `az vm create`.</span><span class="sxs-lookup"><span data-stu-id="7c033-117">Let's start with the first one: `az vm create`.</span></span> <span data-ttu-id="7c033-118">Эта команда используется для создания виртуальной машины в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7c033-118">This command is used to create a virtual machine in a resource group.</span></span> <span data-ttu-id="7c033-119">Вы можете передать несколько параметров, чтобы настроить все аспекты новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7c033-119">There are several parameters you can pass to configure all the aspects of the new VM.</span></span> <span data-ttu-id="7c033-120">Три обязательных параметра:</span><span class="sxs-lookup"><span data-stu-id="7c033-120">The three parameters that must be supplied are:</span></span>

| <span data-ttu-id="7c033-121">Параметр</span><span class="sxs-lookup"><span data-stu-id="7c033-121">Parameter</span></span> | <span data-ttu-id="7c033-122">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="7c033-122">Description</span></span> |
|-----------|-------------|
| `resource-group` | <span data-ttu-id="7c033-123">Группа ресурсов, которой будет принадлежать виртуальная машина</span><span class="sxs-lookup"><span data-stu-id="7c033-123">The resource group that will own the virtual machine</span></span> |
| `name` | <span data-ttu-id="7c033-124">Имя виртуальной машины — должно быть уникальным в пределах группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="7c033-124">The name of the virtual machine - must be unique within the resource group</span></span> |
| `image` | <span data-ttu-id="7c033-125">Образ операционной системы для создания виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="7c033-125">The operating system image to use to create the VM</span></span> |

<span data-ttu-id="7c033-126">Кроме того, полезно добавить флаг `--verbose`, чтобы смотреть ход выполнения при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7c033-126">In addition, it's helpful to add the `--verbose` flag to see progress while the VM is being created.</span></span> 

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="7c033-127">Создание виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="7c033-127">Create a Linux virtual machine</span></span>

<span data-ttu-id="7c033-128">Давайте создадим новую виртуальную машину Linux.</span><span class="sxs-lookup"><span data-stu-id="7c033-128">Let's create a new Linux virtual machine.</span></span> <span data-ttu-id="7c033-129">В Azure Cloud Shell введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7c033-129">Execute the following command in Azure Cloud Shell:</span></span>

```azurecli
az vm create --resource-group ExerciseResources --name SampleVM --image Debian --admin-username aldis --generate-ssh-keys --verbose 
```

<span data-ttu-id="7c033-130">Эта команда создаст новую виртуальную машину Linux **Debian** с именем `SampleVM`.</span><span class="sxs-lookup"><span data-stu-id="7c033-130">This command will create a new **Debian** Linux virtual machine with the name `SampleVM`.</span></span> <span data-ttu-id="7c033-131">Обратите внимание на то, что средство интерфейса командной строки Azure блокируется при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7c033-131">Notice that the Azure CLI tool is blocked while the VM is being created.</span></span> <span data-ttu-id="7c033-132">Если вы не хотите ждать, можно использовать параметр `--no-wait`, чтобы средство интерфейса командной строки Azure выполнило возврат немедленно, например, если вы выполняете команду в скрипте.</span><span class="sxs-lookup"><span data-stu-id="7c033-132">If you would prefer not to wait, you can use the `--no-wait` option to tell the Azure CLI tool to return immediately, for example if you're executing the command in a script.</span></span> <span data-ttu-id="7c033-133">Далее в скрипте используйте команду `azure vm wait --name [vm-name]`, чтобы дождаться завершения создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7c033-133">Later in the script, use the `azure vm wait --name [vm-name]` command to wait for the VM to finish being created.</span></span>

<span data-ttu-id="7c033-134">Если взглянуть на подробные ответы, вы также увидите, что имя `SampleVM` используется для именования различных зависимостей для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7c033-134">If you look at the verbose responses, you will also see that the `SampleVM` name is used to name various dependencies for the VM.</span></span>

```
Succeeded: SampleVMNSG (Microsoft.Network/networkSecurityGroups)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMPublicIP (Microsoft.Network/publicIPAddresses)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMVNET (Microsoft.Network/virtualNetworks)
Accepted: vm_deploy_vzKnQDyyq48yPUO4VrSDfFIi81vHKZ9g (Microsoft.Resources/deployments)
```

<span data-ttu-id="7c033-135">Вы можете переопределить эти автоматически созданные имена ресурсов, используя дополнительные параметры для `vm create`, такие как `--vnet-name` и `--public-ip-address-dns-name`.</span><span class="sxs-lookup"><span data-stu-id="7c033-135">You can override these auto-generated resource names using optional parameters to `vm create`, such as `--vnet-name` and `--public-ip-address-dns-name`.</span></span>

<span data-ttu-id="7c033-136">Обратите внимание на то, что мы указываем имя учетной записи администратора через флаг `admin-username`, чтобы получить "aldis".</span><span class="sxs-lookup"><span data-stu-id="7c033-136">Notice that we are specifying the admin account name through the `admin-username` flag to be "aldis".</span></span> <span data-ttu-id="7c033-137">Если опустить это, команда `vm create` будет использовать ваше _действующие имя пользователя_.</span><span class="sxs-lookup"><span data-stu-id="7c033-137">If you omit this, the `vm create` command will use your _current user name_.</span></span> <span data-ttu-id="7c033-138">Поскольку правила для имен учетных записей отличаются для каждой ОС, лучше указать определенное имя.</span><span class="sxs-lookup"><span data-stu-id="7c033-138">Since the rules for account names are different for each OS, it's safer to specify a specific name.</span></span> <span data-ttu-id="7c033-139">Общие имена, например "root" и "admin", запрещены для большинства образов.</span><span class="sxs-lookup"><span data-stu-id="7c033-139">Common names such as "root" and "admin" are not allowed for most images.</span></span>

<span data-ttu-id="7c033-140">Мы также используем флаг `generate-ssh-keys`.</span><span class="sxs-lookup"><span data-stu-id="7c033-140">We are also using the `generate-ssh-keys` flag.</span></span> <span data-ttu-id="7c033-141">Этот параметр используется для дистрибутивов Linux и создает пару ключей безопасности, чтобы мы могли использовать средство `ssh` для удаленного доступа к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="7c033-141">This parameter is used for Linux distributions and creates a pair of security keys so we can use the `ssh` tool to access the virtual machine remotely.</span></span> <span data-ttu-id="7c033-142">Два файла помещаются в папку `.ssh` на вашем компьютере и на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="7c033-142">The two files are placed into the `.ssh` folder on your machine and in the VM.</span></span> <span data-ttu-id="7c033-143">Если у вас уже есть ключ SSH с именем `id_rsa` в целевой папке, то он будет использоваться вместо создания нового ключа.</span><span class="sxs-lookup"><span data-stu-id="7c033-143">If you already have an SSH key named `id_rsa` in the target folder, then it will be used rather than having a new key generated.</span></span>

<span data-ttu-id="7c033-144">По завершении создания виртуальной машины вы получите ответ JSON, который включает в себя текущее состояние виртуальной машины и ее общедоступные и частные IP-адреса, назначенные Azure:</span><span class="sxs-lookup"><span data-stu-id="7c033-144">Once it finishes creating the VM, you will get a JSON response which includes the current state of the virtual machine and its public and private IP addresses assigned by Azure:</span></span>

```json
{
  "fqdns": "",
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Compute/virtualMachines/SampleVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-1A-D9-74",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "168.61.54.62",
  "resourceGroup": "ExerciseResources",
  "zones": ""
}
```

> [!NOTE]
> <span data-ttu-id="7c033-145">Обратите внимание, что виртуальная машина была создана в расположении **eastus**.</span><span class="sxs-lookup"><span data-stu-id="7c033-145">Notice that the VM was created in the **eastus** location.</span></span> <span data-ttu-id="7c033-146">По умолчанию виртуальная машина создается в расположении, определенном регионом владения.</span><span class="sxs-lookup"><span data-stu-id="7c033-146">By default, the virtual machine is created in the location identified by the owning region.</span></span> <span data-ttu-id="7c033-147">Но иногда может потребоваться привязать виртуальную машину к существующему региону, но запустить ее в другом месте.</span><span class="sxs-lookup"><span data-stu-id="7c033-147">However, sometimes you might want to associate the VM with an existing region, but actually have it spin up somewhere else in the world.</span></span> <span data-ttu-id="7c033-148">Это можно сделать, указав параметр `--location` в рамках команды `az vm create`.</span><span class="sxs-lookup"><span data-stu-id="7c033-148">You can do this by specifying the option `--location` parameter as part of the `az vm create` command.</span></span>