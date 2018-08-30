<span data-ttu-id="1d7a2-101">Для стека компонентов MEAN требуется сервер.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-101">The MEAN stack of components requires a server.</span></span> <span data-ttu-id="1d7a2-102">Это может быть компьютер под управлением Linux или виртуальная машина в вашем локальном серверном окружении или облачная виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-102">It could be a Linux machine or virtual machine running in your own server room, or it can be configured on a cloud-based virtual machine.</span></span> <span data-ttu-id="1d7a2-103">В этом модуле мы настроим работу стека на виртуальной машине Ubuntu Linux, работающей в Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-103">In this module, we will be setting up the stack to run on an Ubuntu Linux virtual machine running on Azure.</span></span>

<span data-ttu-id="1d7a2-104">В этом упражнении вы создадите в Azure виртуальную машину Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-104">In this exercise, you will be creating a new Ubuntu Linux virtual machine hosted on Azure.</span></span> <span data-ttu-id="1d7a2-105">Вместо этого вы можете установить компоненты стека MEAN на существующей виртуальной машины или физическом компьютере.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-105">You could also install your MEAN stack components on an existing virtual machine or physical host machine.</span></span> <span data-ttu-id="1d7a2-106">Создав виртуальную машину для этого упражнения, вы сможете собрать все компоненты в группу ресурсов Azure, чтобы упростить управление ресурсами и очистку после завершения работы.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-106">By creating a new one with this exercise, you can tie together all the components into an Azure resource group for easier management and clean-up after you complete the exercises.</span></span>

<span data-ttu-id="1d7a2-107">Для создания виртуальной Машины Linux мы будем использовать командную строку Cloud Shell, интегрированную в портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-107">We will use the Cloud Shell command-line integrated into the Azure portal to create the Linux VM.</span></span>

## <a name="provision-an-ubuntu-linux-vm"></a><span data-ttu-id="1d7a2-108">Подготовка виртуальной машины Ubuntu Linux</span><span class="sxs-lookup"><span data-stu-id="1d7a2-108">Provision an Ubuntu Linux VM</span></span>

1. <span data-ttu-id="1d7a2-109">Перейдите на [портал Azure](https://portal.azure.com?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="1d7a2-109">Go to the [Azure Portal](https://portal.azure.com?azure-portal=true).</span></span>
1. <span data-ttu-id="1d7a2-110">Откройте Cloud Shell с помощью значка `>_` на панели инструментов портала Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-110">Open the Cloud Shell from the `>_` icon in the Azure portal toolbar.</span></span>
1. <span data-ttu-id="1d7a2-111">Выполните в Cloud Shell команду создания группы ресурсов Azure, куда будет входить новая виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-111">Within the Cloud Shell, execute the command to create an Azure resource group, which will include our VM.</span></span> <span data-ttu-id="1d7a2-112">Введите произвольное имя группы ресурсов вместо `<resource-group-name>` и нужное расположение Azure вместо `<resource-group-location>` (например, `westus`).</span><span class="sxs-lookup"><span data-stu-id="1d7a2-112">Substitute your own resource group name for `<resource-group-name>` and your desired Azure location for `<resource-group-location>` (`westus`, for example).</span></span>

    ```bash
    az group create --name <resource-group-name> --location <resource-group-location>
    ```

    <span data-ttu-id="1d7a2-113">Запомните это имя группы ресурсов — оно будет использоваться в других командах.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-113">Remember your resource group name as we will use it in other commands.</span></span>

1. <span data-ttu-id="1d7a2-114">Введите в Cloud Shell следующие команды, чтобы создать виртуальную машину Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-114">In the Cloud Shell, run the following command to create a new Ubuntu Linux VM.</span></span> <span data-ttu-id="1d7a2-115">Введите произвольное имя группы ресурсов вместо `<resource-group-name>`, а также имя пользователя и пароль администратора вместо `<vm-admin-username>` и `<vm-admin-password>`.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-115">Substitute your own resource group name for `<resource-group-name>` and your preferred admin username and password for `<vm-admin-username>` and `<vm-admin-password>`.</span></span>

    ```bash
    az vm create \
        --resource-group <resource-group-name> \
        --name MeanDemo \
        --image UbuntuLTS \
        --admin-username <vm-admin-username> \
        --admin-password <vm-admin-password> \
        --generate-ssh-keys
    ```

    <span data-ttu-id="1d7a2-116">Запишите имя пользователя и пароль администратора, чтобы позднее подключиться к этой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-116">Take note of your admin username and password to allow you to connect to this VM later.</span></span>

    <span data-ttu-id="1d7a2-117">Выполнение этой команды занимает около 2 минут.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-117">This command takes about 2 minutes to complete.</span></span> <span data-ttu-id="1d7a2-118">Затем эта команда возвращает примерно такой результат:</span><span class="sxs-lookup"><span data-stu-id="1d7a2-118">When the command finishes, the resulting output will look similar to this.</span></span>

    ```json
    {
        "fqdns": "",
        "id": "...",
        "location": "<location you chose for the resource group>",
        "macAddress": "00-0D-3A-3A-54-EC",
        "powerState": "VM running",
        "privateIpAddress": "10.0.0.4",
        "publicIpAddress": "<the public IP address of the newly created machine>",
        "resourceGroup": "<name you chose for thr resource group>",
        "zones": ""
    }
    ```

    <span data-ttu-id="1d7a2-119">Теперь сохраните общедоступный IP-адрес новой виртуальной машины, который потребуется для подключения к ней.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-119">You will also want to save the public IP address of the newly created VM in order to connect to the VM.</span></span>

1. <span data-ttu-id="1d7a2-120">Попробуйте подключиться к созданной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-120">Try connecting to your new VM.</span></span>

    <span data-ttu-id="1d7a2-121">Откройте окно командной строки или терминала и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1d7a2-121">Open a command prompt/terminal window and run the following command.</span></span> <span data-ttu-id="1d7a2-122">Замените заполнители `<vm-admin-username>` и `<vm-public-ip>` именем пользователя администратора и общедоступным IP-адресом виртуальной машину, которые вы настроили выше.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-122">Substitute your admin username and your VM's public IP address from above for the `<vm-admin-username>` and `<vm-public-ip>` placeholders.</span></span>

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

    <span data-ttu-id="1d7a2-123">При первом подключении к компьютеру вам будет предложено подтвердить, что вы доверяете удаленному компьютеру.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-123">The first time you connect to the machine, you'll be asked if you trust the remote machine.</span></span> <span data-ttu-id="1d7a2-124">Если вы ответите `yes`, отпечаток ключа ECDSA удаленного компьютера будет сохранен локально, чтобы все последующие подключения считались доверенными.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-124">By answering `yes`, the machine's ECDSA key fingerprint will be saved locally so subsequent connections will be trusted.</span></span>

    <span data-ttu-id="1d7a2-125">Если все работает правильно, введите `exit` и закройте сеанс SSH.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-125">If everything looks fine, type `exit` to close the SSH session.</span></span>

1. <span data-ttu-id="1d7a2-126">Откройте порт 80, чтобы разрешить входящий трафик по протоколу HTTP к новому веб-приложению.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-126">Open port 80 to allow incoming HTTP traffic to your new web application you will create.</span></span>

    <span data-ttu-id="1d7a2-127">Вернитесь к приглашению Cloud Shell на портале Azure и выполните следующую команду, указав свое имя группы ресурсов вместо `<resource-group-name>`.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-127">Go back to the Cloud Shell on the Azure portal and issue the following command, using your original resource group name for `<resource-group-name>`.</span></span>

    ``` bash
    az vm open-port --port 80 --resource-group <resource-group-name> --name MeanDemo
    ```

    <span data-ttu-id="1d7a2-128">Это действие открывает HTTP-порт на виртуальной машине с именем MeanDemo.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-128">This will open up the HTTP port on your VM that was named "MeanDemo" when it was created.</span></span>

## <a name="summary"></a><span data-ttu-id="1d7a2-129">Сводка</span><span class="sxs-lookup"><span data-stu-id="1d7a2-129">Summary</span></span>

<span data-ttu-id="1d7a2-130">Теперь новая виртуальная машина Ubuntu Linux готова к работе, и вы можете подключиться к ней и установить разные компоненты стека MEAN.</span><span class="sxs-lookup"><span data-stu-id="1d7a2-130">With your new Ubuntu Linux VM ready to go, we can now connect to it to start installing the various components of the MEAN stack.</span></span>
