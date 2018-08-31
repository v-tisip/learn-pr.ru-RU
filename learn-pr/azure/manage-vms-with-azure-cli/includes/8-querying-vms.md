<span data-ttu-id="4f063-101">После создания виртуальной машины мы можем получить интересующие нас сведения о ней с помощью других команд.</span><span class="sxs-lookup"><span data-stu-id="4f063-101">Now that a virtual machine has been created, we can get information about it through other commands.</span></span>

<span data-ttu-id="4f063-102">Начнем с `vm list`.</span><span class="sxs-lookup"><span data-stu-id="4f063-102">Let's start with `vm list`.</span></span>

```azurecli
az vm list
```

<span data-ttu-id="4f063-103">Эта команда возвращает _все_ виртуальные машины, определенные в этой подписке.</span><span class="sxs-lookup"><span data-stu-id="4f063-103">This command will return _all_ virtual machines defined in this subscription.</span></span> <span data-ttu-id="4f063-104">С помощью параметра `--resource-group` выполняется фильтрация выходных данных для определенной группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4f063-104">The output can be filtered to a specific resource group through the `--resource-group` parameter.</span></span> 

## <a name="output-types"></a><span data-ttu-id="4f063-105">Типы выходных данных</span><span class="sxs-lookup"><span data-stu-id="4f063-105">Output types</span></span>
<span data-ttu-id="4f063-106">Обратите внимание, что для всех команд, которые мы рассмотрели, типом ответа по умолчанию является JSON.</span><span class="sxs-lookup"><span data-stu-id="4f063-106">Notice that the default response type for all the commands we've done so far is JSON.</span></span> <span data-ttu-id="4f063-107">Он хорошо подходит для сценариев, но большинство пользователей считает его трудночитаемым.</span><span class="sxs-lookup"><span data-stu-id="4f063-107">This is great for scripting - but most people find it harder to read.</span></span> <span data-ttu-id="4f063-108">Флаг `--output` позволяет изменить стиль выходных данных для любого типа ответа.</span><span class="sxs-lookup"><span data-stu-id="4f063-108">You can change the output style for any response through the `--output` flag.</span></span> <span data-ttu-id="4f063-109">Например, попробуйте выполнить следующую команду в Azure Cloud Shell, чтобы применить другой стиль выходных данных.</span><span class="sxs-lookup"><span data-stu-id="4f063-109">For example, try the following command in Azure Cloud Shell to see the different output style.</span></span>

```azurecli
az vm list --output table
```

<span data-ttu-id="4f063-110">Вместе с `table` можно указать `json` (по умолчанию), `jsonc` (выделенный цветом JSON) или `tsv` (значения, разделенные табуляцией).</span><span class="sxs-lookup"><span data-stu-id="4f063-110">Along with `table`, you can specify `json` (the default), `jsonc` (colorized JSON), or `tsv` (Table-Separated Values).</span></span> <span data-ttu-id="4f063-111">Попробуйте несколько вариантов с приведенной выше командой, чтобы увидеть разницу.</span><span class="sxs-lookup"><span data-stu-id="4f063-111">Try a few variations with the above command to see the difference.</span></span>

## <a name="getting-the-ip-address"></a><span data-ttu-id="4f063-112">Получение IP-адреса</span><span class="sxs-lookup"><span data-stu-id="4f063-112">Getting the IP address</span></span>

<span data-ttu-id="4f063-113">Еще одной полезной командой является `vm list-ip-addresses`, которая выводит список общедоступных и частных IP-адресов для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4f063-113">Another useful command is `vm list-ip-addresses`, which will list the public and private IP addresses for a VM.</span></span> <span data-ttu-id="4f063-114">Если адреса изменились или вы не записали их во время создания, эту команду можно выполнить в любое время.</span><span class="sxs-lookup"><span data-stu-id="4f063-114">If they change, or you didn't capture them during creation, you can retrieve them at any time.</span></span>

```azurecli
az vm list-ip-addresses -n SampleVM -o table
```

<span data-ttu-id="4f063-115">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="4f063-115">This returns:</span></span>

```
VirtualMachine    PublicIPAddresses    PrivateIPAddresses
----------------  -------------------  --------------------
SampleVM          168.61.54.62         10.0.0.4
```

> [!NOTE]
> <span data-ttu-id="4f063-116">Обратите внимание, что мы используем сокращенный синтаксис для флага `--output` — `-o`.</span><span class="sxs-lookup"><span data-stu-id="4f063-116">Notice that we are using a shorthand syntax for the `--output` flag as `-o`.</span></span> <span data-ttu-id="4f063-117">Большинство параметров для команд Azure CLI можно сократить до одного дефиса и буквы.</span><span class="sxs-lookup"><span data-stu-id="4f063-117">Most parameters to Azure CLI commands can be shortened to a single dash and letter.</span></span> <span data-ttu-id="4f063-118">Например, `--name` сокращается до `-n`, а `--resource-group` — до `-g`.</span><span class="sxs-lookup"><span data-stu-id="4f063-118">For example, `--name` can be shortened to `-n` and `--resource-group` to `-g`.</span></span> <span data-ttu-id="4f063-119">Это удобно для ввода, но в сценариях для ясности рекомендуется использовать полное имя параметра.</span><span class="sxs-lookup"><span data-stu-id="4f063-119">This is handy for typing, but we recommend using the full option name in scripts for clarity.</span></span> <span data-ttu-id="4f063-120">Более подробные сведения о каждой команде см. в соответствующей документации.</span><span class="sxs-lookup"><span data-stu-id="4f063-120">Check the documentation for details on each command.</span></span>

## <a name="getting-vm-details"></a><span data-ttu-id="4f063-121">Получение сведений о виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="4f063-121">Getting VM details</span></span>

<span data-ttu-id="4f063-122">С помощью команды `vm show` можно получить более подробные сведения о конкретной виртуальной машине по ее имени или идентификатору.</span><span class="sxs-lookup"><span data-stu-id="4f063-122">We can get more detailed information about a specific virtual machine by name or ID using the `vm show` command.</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM
```

<span data-ttu-id="4f063-123">Эта команда возвращает довольно большой блок JSON с различными сведениями о виртуальной машине, в том числе подключенные устройства хранения, сетевые интерфейсы и все идентификаторы объектов для ресурсов, к которым подключена виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="4f063-123">This will return a fairly large JSON block with all sorts of information about the VM, including attached storage devices, network interfaces, and all of the object IDs for resources that the VM is connected to.</span></span> <span data-ttu-id="4f063-124">Опять же, можно изменить формат на табличный, но в этом случае будут пропущены все интересующие нас данные.</span><span class="sxs-lookup"><span data-stu-id="4f063-124">Again, we could change to a table format, but that omits almost all of the interesting data.</span></span> <span data-ttu-id="4f063-125">Поэтому перейдем к языку встроенных запросов для JSON, который называется [JMESPath](http://jmespath.org/).</span><span class="sxs-lookup"><span data-stu-id="4f063-125">Instead, we can turn to a built-in query language for JSON called [JMESPath](http://jmespath.org/).</span></span>

## <a name="adding-filters-to-queries-with-jmespath"></a><span data-ttu-id="4f063-126">Добавление фильтров в запросы с помощью JMESPath</span><span class="sxs-lookup"><span data-stu-id="4f063-126">Adding filters to queries with JMESPath</span></span>

<span data-ttu-id="4f063-127">JMESPath — это соответствующий отраслевым стандартам язык запросов, созданный на основе объектов JSON.</span><span class="sxs-lookup"><span data-stu-id="4f063-127">JMESPath is an industry-standard query language built around JSON objects.</span></span> <span data-ttu-id="4f063-128">Самым простым запросом является указание _идентификатора_, который выбирает ключ в объекте JSON.</span><span class="sxs-lookup"><span data-stu-id="4f063-128">The simplest query is to specify an _identifier_ that selects a key in the JSON object.</span></span>

<span data-ttu-id="4f063-129">Предположим, что есть объект:</span><span class="sxs-lookup"><span data-stu-id="4f063-129">For example, given the object:</span></span>

```json
{
  "people": [
    {
      "name": "Fred",
      "age": 28
    },
    {
      "name": "Barney",
      "age": 25
    },
    {
      "name": "Wilma",
      "age": 27
    }
  ]
}
```

<span data-ttu-id="4f063-130">С помощью запроса `people` можно вернуть массив значений для массива `people`.</span><span class="sxs-lookup"><span data-stu-id="4f063-130">We can use the query `people` to return the array of values for the `people` array.</span></span> <span data-ttu-id="4f063-131">Если нам нужен только _один_ человек, можно использовать индексатор.</span><span class="sxs-lookup"><span data-stu-id="4f063-131">If we just want _one_ of the people, we can use an indexer.</span></span> <span data-ttu-id="4f063-132">Например, `people[1]` возвращает:</span><span class="sxs-lookup"><span data-stu-id="4f063-132">For example, `people[1]` would return:</span></span>

```json
{
    "name": "Barney",
    "age": 25
}
```

<span data-ttu-id="4f063-133">Мы также можем добавить определенные квалификаторы, которые возвратят подмножество объектов на основе определенных критериев.</span><span class="sxs-lookup"><span data-stu-id="4f063-133">We can also add specific qualifiers that would return a subset of the objects based on some criteria.</span></span> <span data-ttu-id="4f063-134">Например, при добавлении квалификатора `people[?age > '25']` возвращается:</span><span class="sxs-lookup"><span data-stu-id="4f063-134">For example, adding the qualifier `people[?age > '25']` would return:</span></span>

```json
[
  {
    "name": "Fred",
    "age": 28
  },
  {
    "name": "Wilma",
    "age": 27
  }
]
```

<span data-ttu-id="4f063-135">Наконец, ограничим результаты, добавив select: `people[?age > '25'].[name]`, возвращающий только имена:</span><span class="sxs-lookup"><span data-stu-id="4f063-135">Finally, we can constrain the results by adding a select: `people[?age > '25'].[name]` that returns just the names:</span></span>

```json
[
  [
    "Fred"
  ],
  [
    "Wilma"
  ]
]
```

<span data-ttu-id="4f063-136">JMESQuery имеет ряд других интересных функций запросов.</span><span class="sxs-lookup"><span data-stu-id="4f063-136">JMESQuery has several other interesting query features.</span></span> <span data-ttu-id="4f063-137">Если у вас есть время, изучите [интерактивное руководство](http://jmespath.org/tutorial.html), доступное на сайте [JMESPath.org](http://jmespath.org/).</span><span class="sxs-lookup"><span data-stu-id="4f063-137">When you have time, check out the [online tutorial](http://jmespath.org/tutorial.html) available on the [JMESPath.org](http://jmespath.org/) site.</span></span>

## <a name="filtering-our-azure-cli-queries"></a><span data-ttu-id="4f063-138">Фильтрация запросов Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4f063-138">Filtering our Azure CLI queries</span></span>

<span data-ttu-id="4f063-139">Имея базовое представление о запросах JMES, добавим фильтры к данным, возвращаемым запросами, такими как команда `vm show`.</span><span class="sxs-lookup"><span data-stu-id="4f063-139">With a basic understanding of JMES queries, we can add filers to the data being returned by queries like the `vm show` command.</span></span> <span data-ttu-id="4f063-140">Например, можно получить имя администратора:</span><span class="sxs-lookup"><span data-stu-id="4f063-140">For example, we can retrieve the admin user name:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "osProfile.adminUsername"
```

<span data-ttu-id="4f063-141">Можно получить размер, назначенный виртуальной машине:</span><span class="sxs-lookup"><span data-stu-id="4f063-141">We can get the size assigned to our VM:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query hardwareProfile.vmSize
```

<span data-ttu-id="4f063-142">Чтобы получить все идентификаторы сетевых интерфейсов, используется запрос:</span><span class="sxs-lookup"><span data-stu-id="4f063-142">Or to retrieve all the IDs for your network interfaces, you can use the query:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id"
```

<span data-ttu-id="4f063-143">Этот метод запросов будет работать с любой командой Azure CLI и может использоваться для извлечения определенных фрагментов данных с помощью командной строки.</span><span class="sxs-lookup"><span data-stu-id="4f063-143">This query technique will work with any Azure CLI command and can be used to pull specific bits of data out on the command line.</span></span> <span data-ttu-id="4f063-144">Он полезен при написании сценариев: например, можно извлечь значение из учетной записи Azure и сохранить его в переменной среды или сценария.</span><span class="sxs-lookup"><span data-stu-id="4f063-144">It is useful for scripting as well - for example, you can pull a value out of your Azure account and store it in an environment or script variable.</span></span> <span data-ttu-id="4f063-145">Если вы решили применять его таким образом, рекомендуется добавить параметр `--output tsv` (сокращаемый до `-o tsv`).</span><span class="sxs-lookup"><span data-stu-id="4f063-145">If you decide to use it this way, a useful flag to add is the `--output tsv` parameter (which can be shortened to `-o tsv`).</span></span> <span data-ttu-id="4f063-146">В этом случае возвращаются значения, разделенные табуляцией, включающие только фактические значения данных с разделителями-табуляцией.</span><span class="sxs-lookup"><span data-stu-id="4f063-146">This will return the results in tab-separated values that only include the actual data values with tab separators.</span></span>

<span data-ttu-id="4f063-147">Например,</span><span class="sxs-lookup"><span data-stu-id="4f063-147">As an example,</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id" -o tsv
```

<span data-ttu-id="4f063-148">возвращает текст: `/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`</span><span class="sxs-lookup"><span data-stu-id="4f063-148">returns the text: `/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`</span></span>
