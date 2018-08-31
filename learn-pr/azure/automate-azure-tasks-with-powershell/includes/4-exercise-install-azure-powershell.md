<span data-ttu-id="a4ca7-101">В этом упражнении вы установите **Azure PowerShell** на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-101">In this exercise, you will install **Azure PowerShell** on your local machine.</span></span> <span data-ttu-id="a4ca7-102">Выберите подходящий раздел для вашей операционной системы.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-102">Choose the appropriate section for your operating system.</span></span>

## <a name="linux-and-mac"></a><span data-ttu-id="a4ca7-103">Linux и Mac</span><span class="sxs-lookup"><span data-stu-id="a4ca7-103">Linux and Mac</span></span>
<span data-ttu-id="a4ca7-104">В Linux и macOS первым шагом будет установка **PowerShell Core**.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-104">On Linux and macOS, the first step is to install **PowerShell Core**.</span></span>

### <a name="linux"></a><span data-ttu-id="a4ca7-105">Linux</span><span class="sxs-lookup"><span data-stu-id="a4ca7-105">Linux</span></span>
<span data-ttu-id="a4ca7-106">Как упоминалось в последнем разделе, установка PowerShell для Linux осуществляется с помощью диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-106">As mentioned in the last unit, installing PowerShell for Linux will involve using a package manager.</span></span> <span data-ttu-id="a4ca7-107">В нашем примере мы будем использовать **Ubuntu 18.04**, но у нас есть [подробные инструкции для других версий и дистрибутивов в нашей документации](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).</span><span class="sxs-lookup"><span data-stu-id="a4ca7-107">We will use **Ubuntu 18.04** for our example here, but we have [detailed instructions for other versions and distributions in our documentation](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).</span></span>

<span data-ttu-id="a4ca7-108">PowerShell Core устанавливается в Ubuntu Linux с помощью средства управления пакетами Advanced Packaging Tool (**apt**) и командной строки Bash.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-108">You will install PowerShell Core on Ubuntu Linux using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span> 

1. <span data-ttu-id="a4ca7-109">Импортируйте ключ шифрования для репозитория Microsoft Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-109">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="a4ca7-110">Таким образом диспетчер пакетов сможет убедиться, что устанавливаемый пакет PowerShell Core поступает от корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-110">This will allow the package manager to verify that the PowerShell Core package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. <span data-ttu-id="a4ca7-111">Зарегистрируйте **репозиторий Microsoft Ubuntu**, чтобы диспетчер пакетов мог найти пакет PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-111">Register the **Microsoft Ubuntu repository** so the package manager can locate the PowerShell Core package.</span></span>

    ```bash
    sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list
    ```

1. <span data-ttu-id="a4ca7-112">Обновите список пакетов.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-112">Update the list of packages.</span></span>

    ```bash
    sudo apt-get update
    ```

1. <span data-ttu-id="a4ca7-113">Установите PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-113">Install PowerShell Core.</span></span>

    ```bash
    sudo apt-get install -y powershell
    ```

1. <span data-ttu-id="a4ca7-114">Запустите PowerShell, чтобы убедитесь, что он успешно установлен.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-114">Start PowerShell to verify that it installed successfully.</span></span>

    ```bash
    pwsh
    ```

### <a name="macos"></a><span data-ttu-id="a4ca7-115">macOS</span><span class="sxs-lookup"><span data-stu-id="a4ca7-115">macOS</span></span>
<span data-ttu-id="a4ca7-116">Затем установите **PowerShell Core** в macOS с помощью диспетчера пакетов Homebrew.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-116">Next, install **PowerShell Core** on macOS using the Homebrew package manager.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4ca7-117">Если команда **brew** недоступна, может потребоваться установить диспетчер пакетов Homebrew.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-117">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="a4ca7-118">Дополнительные сведения см. на [веб-сайте Homebrew](https://brew.sh/).</span><span class="sxs-lookup"><span data-stu-id="a4ca7-118">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="a4ca7-119">Установите Homebrew-Cask, чтобы получить дополнительные пакеты, включая пакет PowerShell Core:</span><span class="sxs-lookup"><span data-stu-id="a4ca7-119">Install Homebrew-Cask to obtain more packages, including the PowerShell Core package:</span></span>

    ```bash
    brew tap caskroom/cask
    ```
1. <span data-ttu-id="a4ca7-120">Установите PowerShell Core:</span><span class="sxs-lookup"><span data-stu-id="a4ca7-120">Install PowerShell Core:</span></span>

    ```bash
    brew cask installs powershell
    ```

1. <span data-ttu-id="a4ca7-121">Запустите PowerShell Core, чтобы убедитесь, что он успешно установлен:</span><span class="sxs-lookup"><span data-stu-id="a4ca7-121">Start PowerShell Core to verify that it installed successfully:</span></span>

    ```bash
    pwsh
    ```

## <a name="install-azure-powershell"></a><span data-ttu-id="a4ca7-122">Установите Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4ca7-122">Install Azure PowerShell</span></span>
<span data-ttu-id="a4ca7-123">После установки базового продукта **PowerShell** установите **Azure PowerShell**, чтобы добавить команды, характерные для Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-123">After installing the base **PowerShell** product, install **Azure PowerShell** to add the Azure-specific commands.</span></span>

### <a name="windows"></a><span data-ttu-id="a4ca7-124">Windows</span><span class="sxs-lookup"><span data-stu-id="a4ca7-124">Windows</span></span>
<span data-ttu-id="a4ca7-125">Установите Azure PowerShell в Windows с помощью команды PowerShell `Install-Module`.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-125">Install Azure PowerShell on Windows using the `Install-Module` PowerShell command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4ca7-126">Чтобы установить Azure PowerShell, требуется PowerShell начиная с версии 5.0.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-126">You must have PowerShell version 5.0 or higher to install Azure PowerShell.</span></span> <span data-ttu-id="a4ca7-127">Чтобы проверить версию PowerShell, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a4ca7-127">To check your version of PowerShell, use the following command:</span></span> 
>
> `$PSVersionTable.PSVersion` 
>
><span data-ttu-id="a4ca7-128">Если номер версии ниже, чем 5.0, следуйте инструкциям по [обновлению существующей версии Windows PowerShell](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).</span><span class="sxs-lookup"><span data-stu-id="a4ca7-128">If the version number is lower than 5.0, follow the instructions for [upgrading existing Windows PowerShell](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).</span></span>

1. <span data-ttu-id="a4ca7-129">Откройте меню **Пуск** и введите **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-129">Open the **Start** menu and type **Windows PowerShell**.</span></span>
2. <span data-ttu-id="a4ca7-130">Щелкните правой кнопкой мыши значок **Windows PowerShell** и выберите **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-130">Right-click the **Windows PowerShell** icon and select **Run as administrator**.</span></span>
3. <span data-ttu-id="a4ca7-131">В диалоговом окне **Контроль учетных записей пользователей** щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-131">In the **User Account Control** dialog, select **Yes**.</span></span>
4. <span data-ttu-id="a4ca7-132">Введите следующую команду и нажмите клавишу ВВОД:</span><span class="sxs-lookup"><span data-stu-id="a4ca7-132">Type the following command, and then press Enter:</span></span>

    ```powershell
    Install-Module -Name AzureRM
    ```
5. <span data-ttu-id="a4ca7-133">Если у вас спросят, доверяете ли вы модулям из PSGallery, ответьте **Да** или **Да для всех**.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-133">If you are asked whether you trust modules from PSGallery, answer **Yes** or **Yes to All**.</span></span>

> [!NOTE]
> <span data-ttu-id="a4ca7-134">Если появится сообщение об ошибке, указывающее, что версия модуля Azure PowerShell уже установлена, можно выполнить обновление до _последней_ версии с помощью команды:</span><span class="sxs-lookup"><span data-stu-id="a4ca7-134">If you get an error message indicating that a version of the Azure PowerShell module is already installed, you can update to the _latest_ version by issuing the command:</span></span>
> 
> `Update-Module -Name AzureRM`
> 
> <span data-ttu-id="a4ca7-135">Как и для команды `Install-Module`, ответьте **Да** или **Да для всех** при появлении запроса на доверие модулю.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-135">As with the `Install-Module` command, answer **Yes** or **Yes to All** when prompted to trust the module.</span></span>

### <a name="linux-or-macos"></a><span data-ttu-id="a4ca7-136">Linux и macOS</span><span class="sxs-lookup"><span data-stu-id="a4ca7-136">Linux or macOS</span></span>
<span data-ttu-id="a4ca7-137">Мы используем тот же базовый процесс для установки Azure PowerShell в macOS или Linux.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-137">We use the same basic process to install the Azure PowerShell on either Linux or macOS.</span></span> <span data-ttu-id="a4ca7-138">Процедура будет одинаковой для обеих операционных систем.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-138">The procedure is the same for both operating systems.</span></span> <span data-ttu-id="a4ca7-139">Различие заключается в создании сеанса с повышенными привилегиями PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-139">The difference is in getting an elevated PowerShell Core session.</span></span>

1. <span data-ttu-id="a4ca7-140">В окне терминала введите следующую команду, чтобы запустить PowerShell Core с повышенными привилегиями.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-140">In a terminal, type the following command to launch PowerShell Core with elevated privileges.</span></span>

    ```bash
    sudo pwsh
    ```

1. <span data-ttu-id="a4ca7-141">Выполните следующую команду в командной строке PowerShell Core, чтобы установить Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-141">Run the following command at the PowerShell Core prompt to install Azure PowerShell.</span></span>

    ```powershell
    Install-Module AzureRM.NetCore
    ```

1. <span data-ttu-id="a4ca7-142">Если у вас спросят, доверяете ли вы модулям из **PSGallery**, ответьте **Да** или **Да для всех**.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-142">If you are asked whether you trust modules from **PSGallery**, answer **Yes** or **Yes to All**.</span></span>

## <a name="summary"></a><span data-ttu-id="a4ca7-143">Сводка</span><span class="sxs-lookup"><span data-stu-id="a4ca7-143">Summary</span></span>
<span data-ttu-id="a4ca7-144">Вы настроили локальные компьютеры для администрирования ресурсов Azure с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-144">You have setup your local machine(s) to administer Azure resources with Azure PowerShell.</span></span> <span data-ttu-id="a4ca7-145">Теперь вы можете использовать Azure PowerShell локально для ввода команд или выполнения скриптов.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-145">You can now use Azure PowerShell locally to enter commands or execute scripts.</span></span> <span data-ttu-id="a4ca7-146">Azure PowerShell будет пересылать команды в центры обработки данных Azure, где они будут выполняться в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ca7-146">Azure PowerShell will forward your commands to the Azure datacenters where they will run inside your Azure subscription.</span></span>
