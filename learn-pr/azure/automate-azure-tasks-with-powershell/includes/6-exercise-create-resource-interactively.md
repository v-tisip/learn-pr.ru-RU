<span data-ttu-id="5663f-101">Предположим, ваша компания производит наборы средств администрирования Linux.</span><span class="sxs-lookup"><span data-stu-id="5663f-101">Suppose you work at a company that makes a suite of Linux admin tools.</span></span> <span data-ttu-id="5663f-102">Ваша задача — помогать потенциальным клиентам оценивать работу вашего программного обеспечения до покупки.</span><span class="sxs-lookup"><span data-stu-id="5663f-102">Your job is to help potential customers try your software before they buy it.</span></span> <span data-ttu-id="5663f-103">Так как программное обеспечение вносит изменения в операционную систему на корневом уровне, вы решили создавать виртуальную машину Linux для каждого клиента с пробной версией.</span><span class="sxs-lookup"><span data-stu-id="5663f-103">Because the software makes root-level changes to the OS, you have decided to create a Linux VM for each trial customer.</span></span> <span data-ttu-id="5663f-104">Вы создаете виртуальные машины по мере необходимости и удаляете их по окончании пробной подписки.</span><span class="sxs-lookup"><span data-stu-id="5663f-104">You create the VMs as needed and delete them at the end of the trial subscription.</span></span> <span data-ttu-id="5663f-105">Таким образом, каждый клиент начинает с чистой версии операционной системы.</span><span class="sxs-lookup"><span data-stu-id="5663f-105">This way, each customer starts with a clean version of the OS.</span></span> 

<span data-ttu-id="5663f-106">Чтобы изолировать эти виртуальные машины от виртуальных машин, которые ваша компания использует для внутреннего тестирования, вы создадите выделенную группу ресурсов для их размещения.</span><span class="sxs-lookup"><span data-stu-id="5663f-106">To keep these VMs separate from the VMs your company uses for internal testing, you will create a dedicated resource group to house them.</span></span> <span data-ttu-id="5663f-107">Вам нужна только одна группа ресурсов, поэтому для этой задачи лучше использовать Azure PowerShell в интерактивном режиме.</span><span class="sxs-lookup"><span data-stu-id="5663f-107">You only need one resource group so using Azure PowerShell in interactive mode is a reasonable choice for this task.</span></span>

## <a name="steps-to-create-a-resource-group"></a><span data-ttu-id="5663f-108">Действия по созданию группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="5663f-108">Steps to create a resource group</span></span>

1. <span data-ttu-id="5663f-109">Запустите PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5663f-109">Launch PowerShell.</span></span>

1. <span data-ttu-id="5663f-110">Импортируйте модуль в текущий сеанс, чтобы иметь доступ к командлетам Azure.</span><span class="sxs-lookup"><span data-stu-id="5663f-110">Import the module into the current session so you have access to the Azure cmdlets.</span></span>

   ```powershell
   Import-Module AzureRM
   ```

1. <span data-ttu-id="5663f-111">Подключитесь к Azure с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="5663f-111">Connect to Azure using the command shown below.</span></span> <span data-ttu-id="5663f-112">После ввода команды пройдите проверку подлинности, указав свои учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="5663f-112">After entering the command, authenticate by providing your Azure credentials.</span></span>

   ```powershell
   Connect-AzureRmAccount
   ```

1. <span data-ttu-id="5663f-113">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5663f-113">Create a resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name "TrialsResourceGroup" -Location "East US"
    ```

1. <span data-ttu-id="5663f-114">Убедитесь, что группа ресурсов успешно создана.</span><span class="sxs-lookup"><span data-stu-id="5663f-114">Verify the resource group was created successfully.</span></span>

    ```powershell
    Get-AzureRmResource | Format-Table
    ```
<span data-ttu-id="5663f-115">Вы также можете проверить успешное создание группы ресурсов на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="5663f-115">Another way to check whether the resource group was created successfully is to use the Azure Portal.</span></span> <span data-ttu-id="5663f-116">Для этого войдите на портал и перейдите к разделу **Группы ресурсов** (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="5663f-116">To do this, login to the Portal and navigate to the **Resource Groups** section (see below).</span></span> <span data-ttu-id="5663f-117">Новая группа ресурсов должна отображаться в списке.</span><span class="sxs-lookup"><span data-stu-id="5663f-117">The new resource group should be displayed in the list.</span></span>

![Использование портала для получения списка групп ресурсов](../media-drafts/6-listing-resource-groups.png)

## <a name="summary"></a><span data-ttu-id="5663f-119">Сводка</span><span class="sxs-lookup"><span data-stu-id="5663f-119">Summary</span></span>
<span data-ttu-id="5663f-120">В этом упражнении показан обычный интерактивный сеанс PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5663f-120">This exercise shows a common pattern for an interactive PowerShell session.</span></span> <span data-ttu-id="5663f-121">Вы использовали стандартный командлет для импорта модуля AzureRM, а затем командлеты Azure PowerShell для выполнения определенных задач.</span><span class="sxs-lookup"><span data-stu-id="5663f-121">You used a standard cmdlet to import the AzureRM module and then the Azure PowerShell cmdlets to perform a specific task.</span></span> <span data-ttu-id="5663f-122">Теперь у вас в подписке есть группа ресурсов, и все готово к созданию виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5663f-122">You now have a resource group in your subscription and are ready to create VMs.</span></span>