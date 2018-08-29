<span data-ttu-id="43537-101">В этом упражнении вы создадите виртуальную машину Windows в Azure.</span><span class="sxs-lookup"><span data-stu-id="43537-101">In this exercise, you'll create a Windows virtual machine in Azure.</span></span>

## <a name="motivation"></a><span data-ttu-id="43537-102">Мотивация</span><span class="sxs-lookup"><span data-stu-id="43537-102">Motivation</span></span>

<span data-ttu-id="43537-103">Рассмотрим альтернативный сценарий для этого упражнения.</span><span class="sxs-lookup"><span data-stu-id="43537-103">Let's consider an alternate scenario for this exercise.</span></span> <span data-ttu-id="43537-104">В нем ваша организация является учебным заведением, которое использует виртуальные машины Windows для запуска тестовых сред, где учащиеся устанавливают веб-приложения, настраивают домены и изучают службы и компоненты Windows без нарушения работы компьютеров учебного заведения.</span><span class="sxs-lookup"><span data-stu-id="43537-104">Here, your organization is a school that uses Windows virtual machines to spin up test environments on which students install web apps, configure domains, and explore Windows services and features without affecting the school's computers.</span></span> <span data-ttu-id="43537-105">Преподаватели подключаются к этим виртуальным машинам по протоколу RDP и отслеживают успеваемость учащихся.</span><span class="sxs-lookup"><span data-stu-id="43537-105">Teachers connect to these VMs by using RDP and check on student progress.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="43537-106">Создание виртуальной машины Windows</span><span class="sxs-lookup"><span data-stu-id="43537-106">Create a Windows VM</span></span>

<span data-ttu-id="43537-107">Чтобы создать виртуальную машину Windows, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="43537-107">To create a Windows VM, complete the following steps:</span></span>

1. <span data-ttu-id="43537-108">Войдите в Azure с помощью [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="43537-108">Log onto Azure through the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="43537-109">В верхнем левом углу окна портала Azure щелкните **Создать ресурс**.</span><span class="sxs-lookup"><span data-stu-id="43537-109">Click **Create a resource** in the upper left corner of the Azure portal.</span></span>

1. <span data-ttu-id="43537-110">В **строке поиска** введите **Windows Server 2016 Datacenter**, а затем щелкните ссылку с таким же названием.</span><span class="sxs-lookup"><span data-stu-id="43537-110">In the **search bar**, enter  **Windows Server 2016 Datacenter**  and then click on the link with the same title.</span></span>

### <a name="configure-the-vm-settings"></a><span data-ttu-id="43537-111">Настройка параметров виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="43537-111">Configure the VM settings</span></span>

1. <span data-ttu-id="43537-112">В разделе **Основы** в поле **Имя** введите имя виртуальной машины, например "StudentVM".</span><span class="sxs-lookup"><span data-stu-id="43537-112">Under **Basics**, in the **Name** field, enter a name for your VM, such as "StudentVM."</span></span>

1. <span data-ttu-id="43537-113">В поле **Тип диска виртуальной машины** щелкните раскрывающееся меню, чтобы просмотреть параметры.</span><span class="sxs-lookup"><span data-stu-id="43537-113">In the **VM Disk Type** field, click the drop-down menu to see the options.</span></span> <span data-ttu-id="43537-114">Выберите **SSD**.</span><span class="sxs-lookup"><span data-stu-id="43537-114">Ensure that **SSD** is selected.</span></span>

1. <span data-ttu-id="43537-115">В поле **Имя пользователя** введите имя пользователя, подходящее для входа в виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="43537-115">In the **Username** field, enter a suitable user name to use to sign in to the VM.</span></span>

1. <span data-ttu-id="43537-116">В поле **Пароль** введите пароль длиной не менее 12 символов.</span><span class="sxs-lookup"><span data-stu-id="43537-116">In the **Password** field, enter a password that's at least 12 characters long.</span></span> <span data-ttu-id="43537-117">Пароль должен содержать прописные и строчные буквы, цифры и специальные символы.</span><span class="sxs-lookup"><span data-stu-id="43537-117">It must also have upper and lowercase characters, numbers, and special characters.</span></span>

1. <span data-ttu-id="43537-118">В разделе **Группа ресурсов** щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="43537-118">Under **Resource group**, click **Create new**.</span></span> <span data-ttu-id="43537-119">Укажите имя группы ресурсов, например "myTestRG".</span><span class="sxs-lookup"><span data-stu-id="43537-119">Give the resource group a name, such as "myTestRG."</span></span>

1. <span data-ttu-id="43537-120">Выберите подходящее расположение для создания виртуальной машины, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="43537-120">Select a suitable location for the VM to be created, and then click **OK**.</span></span>

### <a name="select-the-vm-image-size-and-options"></a><span data-ttu-id="43537-121">Выбор параметров и размера образа виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="43537-121">Select the VM image size and options</span></span>

1. <span data-ttu-id="43537-122">На странице **Выбор размера** выберите образ **B1s**, а затем щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="43537-122">In the **Choose a size** page, click the **B1s** image, and then click **Select**.</span></span>

   > [!Note] 
   > <span data-ttu-id="43537-123">Образ B1 имеет только 1 ГБ ОЗУ, что приведет к ошибкам памяти при первом входе.</span><span class="sxs-lookup"><span data-stu-id="43537-123">The B1 image has only 1 GB of RAM and will result in memory errors when you first sign in.</span></span> <span data-ttu-id="43537-124">Однако вы можете изменить размер образа позже при выполнении следующей лабораторной работы.</span><span class="sxs-lookup"><span data-stu-id="43537-124">However, you can resize the image later as part of a later lab.</span></span>

1. <span data-ttu-id="43537-125">На странице **Параметры** в разделе **Выберите общедоступные входящие порты** выберите **Нет открытых входящих портов**.</span><span class="sxs-lookup"><span data-stu-id="43537-125">In the **Settings** page, under **Select Public Inbound Ports**, select **No public inbound ports**.</span></span> <span data-ttu-id="43537-126">Доступ по протоколу RDP будет настроен позже.</span><span class="sxs-lookup"><span data-stu-id="43537-126">We'll configure RDP access later.</span></span>

### <a name="finish-configuring-the-vm-and-create-the-image"></a><span data-ttu-id="43537-127">Завершение настройки виртуальной машины и создания образа</span><span class="sxs-lookup"><span data-stu-id="43537-127">Finish configuring the VM and create the image</span></span>

1. <span data-ttu-id="43537-128">Прокрутите до нижней части страницы и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="43537-128">Scroll to the bottom and click **OK**.</span></span>

1. <span data-ttu-id="43537-129">В разделе **Создание** проверьте настроенные параметры.</span><span class="sxs-lookup"><span data-stu-id="43537-129">Under **Create**, check the settings that you configured.</span></span> <span data-ttu-id="43537-130">В нижней части нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="43537-130">At the bottom, click **Create**.</span></span> <span data-ttu-id="43537-131">Развертываемая виртуальная машина будет отображена на панели мониторинга Azure.</span><span class="sxs-lookup"><span data-stu-id="43537-131">The Azure dashboard will show the VM that's being deployed.</span></span> <span data-ttu-id="43537-132">Это может занять несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="43537-132">This may take several minutes.</span></span>

## <a name="summary"></a><span data-ttu-id="43537-133">Сводка</span><span class="sxs-lookup"><span data-stu-id="43537-133">Summary</span></span>

<span data-ttu-id="43537-134">Вы создали виртуальную машину Windows Server, соответствующую требованиям учащихся и доступную из сети учебного заведения.</span><span class="sxs-lookup"><span data-stu-id="43537-134">You've now created a Windows Server virtual machine that's suitable for student requirements and accessible from the school network.</span></span> <span data-ttu-id="43537-135">В следующем блоке вы узнаете, как подключиться к этой виртуальной машине и управлять ею с помощью протокола RDP.</span><span class="sxs-lookup"><span data-stu-id="43537-135">In the next unit, you will look at how you connect to and manage that VM by using RDP.</span></span>
