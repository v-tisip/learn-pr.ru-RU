
<span data-ttu-id="38716-101">В этом упражнении вы будете использовать Azure CLI на локальном компьютере, чтобы сначала создать группу ресурсов, а затем развернуть в ней веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="38716-101">In this exercise, you will use the Azure CLI on your local machine to create a resource group, and then to deploy a web app into this resource group.</span></span> 

### <a name="steps-to-create-a-resource-group"></a><span data-ttu-id="38716-102">Действия по созданию группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="38716-102">Steps to create a resource group</span></span>
1. <span data-ttu-id="38716-103">Откройте оболочку Bash в Linux или macOS либо откройте окно командной строки или PowerShell, если вы работаете в Windows.</span><span class="sxs-lookup"><span data-stu-id="38716-103">Open a bash shell on Linux or macOS, or open the Command Prompt window or PowerShell if working from Windows.</span></span>

1. <span data-ttu-id="38716-104">Запустите Azure CLI и выполните команду для входа.</span><span class="sxs-lookup"><span data-stu-id="38716-104">Start the Azure CLI and run the login command.</span></span>

    ```bash
    az login
    ```
    <span data-ttu-id="38716-105">Если страница входа в Azure не открывается в веб-браузере, следуйте указаниям в командной строке и введите код авторизации в [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span><span class="sxs-lookup"><span data-stu-id="38716-105">If you do not get an Azure sign-in page in your web browser, follow the command-line instructions and enter an authorization code at [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span></span>

1. <span data-ttu-id="38716-106">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="38716-106">Create a resource group.</span></span>

    ```bash
    az group create --location westeurope --name popupResGroup
    ```

1. <span data-ttu-id="38716-107">Убедитесь, что группа ресурсов успешно создана, просмотрев все группы ресурсов в таблице.</span><span class="sxs-lookup"><span data-stu-id="38716-107">Verify that the resource group was created successfully by listing all your resource groups in a table.</span></span>

    ```bash
    az group list --output table
    ```
1. <span data-ttu-id="38716-108">Или проверьте создание ресурса на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="38716-108">Optionally, confirm the resource was created in the Azure portal.</span></span> <span data-ttu-id="38716-109">Откройте веб-браузер, войдите на портал и перейдите к разделу **Группы ресурсов** (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="38716-109">Open a web browser, sign in to the portal and navigate to the **Resource Groups** section (see below).</span></span> <span data-ttu-id="38716-110">Новая группа ресурсов должна отображаться в списке.</span><span class="sxs-lookup"><span data-stu-id="38716-110">The new resource group should be displayed in the list.</span></span>

![Использование портала для получения списка групп ресурсов](../media-drafts/5-listing-resource-groups.png)

### <a name="steps-to-create-a-service-plan"></a><span data-ttu-id="38716-112">Действия по созданию плана обслуживания</span><span class="sxs-lookup"><span data-stu-id="38716-112">Steps to create a service plan</span></span>
<span data-ttu-id="38716-113">При запуске веб-приложений с помощью службы приложений Azure, вы платите за вычислительные ресурсы Azure, используемые приложением, а это зависит от плана службы приложений, связанного с веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="38716-113">When you run Web Apps, using the Azure App Service, you pay for the Azure compute resources used by the app, and this depends on the App Service plan associated with your Web Apps.</span></span> <span data-ttu-id="38716-114">Планы обслуживания определяют регион, используемый для центра обработки данных приложения, количество виртуальных машин и ценовую категорию.</span><span class="sxs-lookup"><span data-stu-id="38716-114">Service plans determine the region used for the app datacenter, number of VMs used, and pricing tier.</span></span>

1. <span data-ttu-id="38716-115">Создайте план службы приложений для работы своего приложения.</span><span class="sxs-lookup"><span data-stu-id="38716-115">Create an App Service plan to run your app.</span></span> <span data-ttu-id="38716-116">Имена приложения и плана должны быть уникальными, поэтому замените строку "12345" на произвольное число.</span><span class="sxs-lookup"><span data-stu-id="38716-116">The name of the app and plan must be unique, so change the string "12345" to a random number.</span></span> <span data-ttu-id="38716-117">Следующая команда не указывает ценовую категорию или сведения об экземпляре виртуальной машины, поэтому по умолчанию вы получите **Базовый** план с одним **небольшим** экземпляром виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="38716-117">The following command does not specify a pricing tier or VM instance details, so by default, you'll get a **Basic** plan with 1 **Small** VM instance.</span></span>

    ```bash
    az appservice plan create --name popupapp12345 --resource-group popupResGroup --location westeurope
    ```

1. <span data-ttu-id="38716-118">Убедитесь, что план обслуживания успешно создан, просмотрев все планы в таблице.</span><span class="sxs-lookup"><span data-stu-id="38716-118">Verify that the service plan was created successfully by listing all your plans in a table.</span></span>

    ```bash
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a><span data-ttu-id="38716-119">Действия по созданию веб-приложения</span><span class="sxs-lookup"><span data-stu-id="38716-119">Steps to create a web app</span></span>
<span data-ttu-id="38716-120">Далее вы создадите веб-приложение в плане обслуживания.</span><span class="sxs-lookup"><span data-stu-id="38716-120">Next, you'll create the web app in your service plan.</span></span> <span data-ttu-id="38716-121">Одновременно с этим вы можете развернуть код, но в нашем примере мы сделаем это отдельно.</span><span class="sxs-lookup"><span data-stu-id="38716-121">You can deploy the code at the same time, but for our example, we'll do this as separate steps.</span></span>

1. <span data-ttu-id="38716-122">Создайте веб-приложение. Не забудьте заменить строку "12345" на то же произвольное число, которое использовалось ранее.</span><span class="sxs-lookup"><span data-stu-id="38716-122">Create the web app, remembering to change the string "12345" to the same random number you used earlier.</span></span>
    ```bash
    az webapp create --name popupapp12345 --resource-group popupResGroup --plan popupapp12345
    ```

1. <span data-ttu-id="38716-123">Убедитесь, что приложение успешно создано, просмотрев все приложения в таблице.</span><span class="sxs-lookup"><span data-stu-id="38716-123">Verify that the app was created successfully by listing all your apps in a table.</span></span>

    ```bash
    az webapp list --output table
    ```

1. <span data-ttu-id="38716-124">Запомните значение **DefaultHostName** — оно потребуется позже.</span><span class="sxs-lookup"><span data-stu-id="38716-124">Make a note of the **DefaultHostName**; you will need this later.</span></span>

### <a name="steps-to-deploy-code-from-github"></a><span data-ttu-id="38716-125">Действия по развертыванию кода с сайта GitHub</span><span class="sxs-lookup"><span data-stu-id="38716-125">Steps to deploy code from GitHub</span></span>
1. <span data-ttu-id="38716-126">Последним шагом является развертывание кода из репозитория GitHub в веб-приложении. Не забудьте заменить строку "12345" на то же произвольное число, которое использовалось ранее.</span><span class="sxs-lookup"><span data-stu-id="38716-126">The final step is to deploy code from a GitHub repository to the web app, again remembering to change the string "12345" to the same random number you used earlier.</span></span>
    ```bash
    az webapp deployment source config --name popupapp12345 --resource-group popupResGroup --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. <span data-ttu-id="38716-127">Чтобы просмотреть веб-приложение, скопируйте следующий URL-адрес в адресную строку браузера.</span><span class="sxs-lookup"><span data-stu-id="38716-127">Copy the following url into a browser to see the web app.</span></span>
<span data-ttu-id="38716-128">http://popupapp12345.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="38716-128">http://popupapp12345.azurewebsites.net</span></span>

1. <span data-ttu-id="38716-129">На странице отображается "HelloWorld!"</span><span class="sxs-lookup"><span data-stu-id="38716-129">The page displays "HelloWorld!"</span></span>

1. <span data-ttu-id="38716-130">Закройте окно браузера.</span><span class="sxs-lookup"><span data-stu-id="38716-130">Close the browser window.</span></span>

## <a name="summary"></a><span data-ttu-id="38716-131">Сводка</span><span class="sxs-lookup"><span data-stu-id="38716-131">Summary</span></span>
<span data-ttu-id="38716-132">В этом упражнении приводилась стандартная схема для интерактивного сеанса Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="38716-132">This exercise demonstrated a typical pattern for an interactive Azure CLI session.</span></span> <span data-ttu-id="38716-133">Сначала вы использовали стандартную команду для создания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="38716-133">You first used a standard command to create a new resource group.</span></span> <span data-ttu-id="38716-134">Затем с помощью набора команд вы развернули в ней ресурс (в этом примере — веб-приложение).</span><span class="sxs-lookup"><span data-stu-id="38716-134">You then used a set of commands to deploy a resource (in this example, a web app) into this resource group.</span></span> <span data-ttu-id="38716-135">Этот набор команд можно легко объединить в сценарий оболочки и выполнять каждый раз, когда требуется создать тот же самый ресурс.</span><span class="sxs-lookup"><span data-stu-id="38716-135">This set of commands could easily be combined into a shell script, and executed every time you need to create the same resource.</span></span>
