
<span data-ttu-id="e7b70-101">В этом упражнении вы установите Azure CLI на локальном компьютере и выполните простую команду для проверки установки.</span><span class="sxs-lookup"><span data-stu-id="e7b70-101">In this exercise, you will install the Azure CLI on your local machine, and then run a simple command to verify your installation.</span></span> 

## <a name="installing-the-azure-cli"></a><span data-ttu-id="e7b70-102">Установка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e7b70-102">Installing the Azure CLI</span></span>
<span data-ttu-id="e7b70-103">Метод, который вы используете для установки Azure CLI, зависит от операционной системы компьютера.</span><span class="sxs-lookup"><span data-stu-id="e7b70-103">The method you use for installing the Azure CLI depends on the operating system of your computer.</span></span> <span data-ttu-id="e7b70-104">Выберите действия для вашей операционной системы.</span><span class="sxs-lookup"><span data-stu-id="e7b70-104">Please choose the steps for your operating system.</span></span>

### <a name="linux"></a><span data-ttu-id="e7b70-105">Linux</span><span class="sxs-lookup"><span data-stu-id="e7b70-105">Linux</span></span>
<span data-ttu-id="e7b70-106">Здесь вы устанавливаете Azure CLI на Ubuntu Linux с помощью средства управления пакетами Advanced Packaging Tool (**apt**) и командной строки Bash.</span><span class="sxs-lookup"><span data-stu-id="e7b70-106">Here you will install the Azure CLI on Ubuntu Linux using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span>

> [!NOTE]
> <span data-ttu-id="e7b70-107">Ниже перечислены команды для Ubuntu версии 18.04.</span><span class="sxs-lookup"><span data-stu-id="e7b70-107">The commands listed below are for Ubuntu version 18.04.</span></span> <span data-ttu-id="e7b70-108">Если вы используете другую версию Ubuntu, необходимо добавить другой репозиторий.</span><span class="sxs-lookup"><span data-stu-id="e7b70-108">If you are using a different version of Ubuntu, you must add a different repository.</span></span> <span data-ttu-id="e7b70-109">Дополнительные сведения см. в разделе [Установка Azure CLI 2.0 с помощью apt](https://docs.microsoft.com/cli/azure/install-azure-cli-apt).</span><span class="sxs-lookup"><span data-stu-id="e7b70-109">For details see [Install the Azure CLI 2.0 with apt](https://docs.microsoft.com/cli/azure/install-azure-cli-apt).</span></span>

1. <span data-ttu-id="e7b70-110">Измените список источников, чтобы зарегистрировать репозиторий Майкрософт, а диспетчер пакетов мог найти пакет Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e7b70-110">Modify your sources list so that the Microsoft repository is registered, and the package manager can locate the Azure CLI package.</span></span>

    ```bash
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```
1. <span data-ttu-id="e7b70-111">Импортируйте ключ шифрования для репозитория Microsoft Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e7b70-111">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="e7b70-112">Таким образом диспетчер пакетов сможет убедиться, что устанавливаемый пакет Azure CLI поступает от корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="e7b70-112">This will allow the package manager to verify that the Azure CLI package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. <span data-ttu-id="e7b70-113">Установите Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e7b70-113">Install the Azure CLI.</span></span>

    ```bash
    sudo apt-get install apt-transport-https
    sudo apt-get update && sudo apt-get install azure-cli
    ```

### <a name="macos"></a><span data-ttu-id="e7b70-114">macOS</span><span class="sxs-lookup"><span data-stu-id="e7b70-114">macOS</span></span>
<span data-ttu-id="e7b70-115">Здесь вы устанавливаете Azure CLI в macOS с помощью диспетчера пакетов Homebrew.</span><span class="sxs-lookup"><span data-stu-id="e7b70-115">Here you will install the Azure CLI on macOS using the Homebrew package manager.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7b70-116">Если команда **brew** недоступна, может потребоваться установить диспетчер пакетов Homebrew.</span><span class="sxs-lookup"><span data-stu-id="e7b70-116">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="e7b70-117">Дополнительные сведения см. на [веб-сайте Homebrew](https://brew.sh/).</span><span class="sxs-lookup"><span data-stu-id="e7b70-117">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="e7b70-118">Обновите репозиторий brew, чтобы убедиться, что вы получите последнюю версию пакета Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e7b70-118">Update your brew repository to make sure you get the latest Azure CLI package.</span></span>

    ```bash
    brew update
    ```
1. <span data-ttu-id="e7b70-119">Установите Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e7b70-119">Install the Azure CLI.</span></span>

    ```bash
    brew install azure-cli
    ```

### <a name="windows"></a><span data-ttu-id="e7b70-120">Windows</span><span class="sxs-lookup"><span data-stu-id="e7b70-120">Windows</span></span>
<span data-ttu-id="e7b70-121">Здесь вы устанавливаете Azure CLI в Windows с помощью установщика MSI.</span><span class="sxs-lookup"><span data-stu-id="e7b70-121">Here you will install the Azure CLI on Windows using the MSI installer.</span></span>

1. <span data-ttu-id="e7b70-122">Перейдите к [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows) и в диалоговом окне безопасности браузера щелкните **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="e7b70-122">Go to [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows), and in the browser security dialog box, click **Run**.</span></span>
1. <span data-ttu-id="e7b70-123">В установщике примите условия лицензионного соглашения и нажмите **Установить**.</span><span class="sxs-lookup"><span data-stu-id="e7b70-123">In the installer, accept the license terms, and then click **Install**.</span></span>
1. <span data-ttu-id="e7b70-124">В диалоговом окне **Контроль учетных записей пользователей** щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="e7b70-124">In the **User Account Control** dialog, select **Yes**.</span></span>

## <a name="running-the-azure-cli"></a><span data-ttu-id="e7b70-125">Запуск Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e7b70-125">Running the Azure CLI</span></span>
<span data-ttu-id="e7b70-126">Чтобы запустить Azure CLI, откройте командную оболочку bash (Linux и macOS) или используйте командную строку или PowerShell (Windows).</span><span class="sxs-lookup"><span data-stu-id="e7b70-126">You run the Azure CLI by opening a bash shell (Linux and macOS), or from the command prompt or PowerShell (Windows).</span></span>

1. <span data-ttu-id="e7b70-127">Запустите Azure CLI и проверьте правильность установки, выполнив проверку версии.</span><span class="sxs-lookup"><span data-stu-id="e7b70-127">Start the Azure CLI and verify your installation by running the version check.</span></span>

    ```bash
    az --version
    ```

> [!NOTE]
> <span data-ttu-id="e7b70-128">В Windows запуск Azure CLI с помощью PowerShell имеет некоторые преимущества по сравнению с запуском Azure CLI из командной строки. Например, PowerShell предоставляет дополнительные функции завершения с помощью Tab по сравнению с набором функций, доступных из командной строки.</span><span class="sxs-lookup"><span data-stu-id="e7b70-128">In Windows, running the Azure CLI from PowerShell has some advantages over running the Azure CLI from the command prompt; for example, PowerShell provides additional tab completion features over those available from the command prompt.</span></span> 

## <a name="summary"></a><span data-ttu-id="e7b70-129">Сводка</span><span class="sxs-lookup"><span data-stu-id="e7b70-129">Summary</span></span>
<span data-ttu-id="e7b70-130">Вы настроили локальные компьютеры для администрирования ресурсов Azure с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e7b70-130">You set up your local machines to administer Azure resources with the Azure CLI.</span></span> <span data-ttu-id="e7b70-131">Теперь вы можете использовать Azure CLI локально для ввода команд или выполнения скриптов.</span><span class="sxs-lookup"><span data-stu-id="e7b70-131">You can now use the Azure CLI locally to enter commands or execute scripts.</span></span> <span data-ttu-id="e7b70-132">Azure CLI будет пересылать команды в центры обработки данных Azure, где они будут выполняться в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="e7b70-132">The Azure CLI will forward your commands to the Azure datacenters where they will run inside your Azure subscription.</span></span>
