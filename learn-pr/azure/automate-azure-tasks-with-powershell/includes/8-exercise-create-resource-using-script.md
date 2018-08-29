<span data-ttu-id="ad8ad-101">В этом упражнении мы продолжим работу с примером, в котором компания разрабатывает средства администрирования Linux.</span><span class="sxs-lookup"><span data-stu-id="ad8ad-101">In this exercise, you will continue with the example of a company that makes Linux admin tools.</span></span> <span data-ttu-id="ad8ad-102">Если помните, вы планируете использовать виртуальные машины Linux, чтобы позволить потенциальным клиентам тестировать ваше программное обеспечение.</span><span class="sxs-lookup"><span data-stu-id="ad8ad-102">Recall that you plan to use Linux VMs to let potential customers test your software.</span></span> <span data-ttu-id="ad8ad-103">У вас есть готовая группа ресурсов, и теперь нужно создать виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="ad8ad-103">You have a resource group ready and now it is time to create the VMs.</span></span>

<span data-ttu-id="ad8ad-104">Ваша компания оплатила стенд на большой выставке-ярмарке по Linux.</span><span class="sxs-lookup"><span data-stu-id="ad8ad-104">Your company has paid for a booth at a big Linux trade show.</span></span> <span data-ttu-id="ad8ad-105">Вы планируете использовать демонстрационную область, содержащую три терминала, каждый из которых подключен к отдельной виртуальной машине Linux.</span><span class="sxs-lookup"><span data-stu-id="ad8ad-105">You plan a demo area containing three terminals each connected to a separate Linux VM.</span></span> <span data-ttu-id="ad8ad-106">В конце каждого дня требуется удалять эти виртуальные машины и создавать их заново, чтобы каждое утро они находились в исходном состоянии.</span><span class="sxs-lookup"><span data-stu-id="ad8ad-106">At the end of each day, you want to delete the VMs and recreate them, so they start fresh every morning.</span></span> <span data-ttu-id="ad8ad-107">Если заниматься созданием виртуальных машин вручную после работы, когда вы уже устали, это с высокой вероятностью приведет к ошибкам.</span><span class="sxs-lookup"><span data-stu-id="ad8ad-107">Creating the VMs manually after work when you are tired would be error prone.</span></span> <span data-ttu-id="ad8ad-108">Вы хотите написать сценарий PowerShell, позволяющий автоматизировать создание виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="ad8ad-108">You want to write a PowerShell script to automate the VM creation process.</span></span>

## <a name="write-a-script-that-creates-virtual-machines"></a><span data-ttu-id="ad8ad-109">Создание сценария, создающего виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="ad8ad-109">Write a script that creates Virtual Machines</span></span>

<span data-ttu-id="ad8ad-110">Чтобы создать сценарий, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="ad8ad-110">Follow these steps to write the script:</span></span>

1. <span data-ttu-id="ad8ad-111">Создайте текстовый файл с именем **ConferenceDailyReset.ps1**.</span><span class="sxs-lookup"><span data-stu-id="ad8ad-111">Create a new text file named **ConferenceDailyReset.ps1**.</span></span>

2. <span data-ttu-id="ad8ad-112">Запишите параметр в переменную:</span><span class="sxs-lookup"><span data-stu-id="ad8ad-112">Capture the parameter in a variable:</span></span>

    ```powershell
    param([string]$resourceGroup)
    ```

3. <span data-ttu-id="ad8ad-113">Выполните проверку подлинности в Azure, используя свои учетные данные:</span><span class="sxs-lookup"><span data-stu-id="ad8ad-113">Authenticate with Azure using your credentials:</span></span>

    ```powershell
    Connect-AzureRmAccount
    ```

4. <span data-ttu-id="ad8ad-114">Запросите имя пользователя и пароль для учетной записи администратора виртуальной машины и сохраните результат в переменной:</span><span class="sxs-lookup"><span data-stu-id="ad8ad-114">Prompt for a username and password for the VM's admin account and capture the result in a variable:</span></span>

    ```powershell
    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."
    ```

5. <span data-ttu-id="ad8ad-115">Создайте цикл, который выполняет три раза:</span><span class="sxs-lookup"><span data-stu-id="ad8ad-115">Create a loop that executes three times:</span></span>

    ```powershell
    For ($i = 1; $i -le 3; $i++) 
    {

    }
    ```

6. <span data-ttu-id="ad8ad-116">В теле цикла создайте имя для каждой виртуальной машины и сохраните его в переменной:</span><span class="sxs-lookup"><span data-stu-id="ad8ad-116">In the loop body, create a name for each VM and store it in a variable:</span></span>

    ```powershell
    $vmName = "ConferenceDemo" + $i
    ```

7. <span data-ttu-id="ad8ad-117">Создайте виртуальную машину с помощью переменной `$vmName`:</span><span class="sxs-lookup"><span data-stu-id="ad8ad-117">Next, create a VM using the `$vmName` variable:</span></span>

   ```powershell
   New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" 
   ```

8. <span data-ttu-id="ad8ad-118">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="ad8ad-118">Save the file.</span></span>

<span data-ttu-id="ad8ad-119">Готовый сценарий будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="ad8ad-119">The completed script should look like this:</span></span>

```powershell
param([string]$resourceGroup)

$adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."

Connect-AzureRmAccount

For ($i = 1; $i -le 3; $i++)
{
    $vmName = "ConferenceDemo" + $i

    New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" -Image UbuntuLTS
}
```

## <a name="execute-the-script"></a><span data-ttu-id="ad8ad-120">Выполнение скрипта</span><span class="sxs-lookup"><span data-stu-id="ad8ad-120">Execute the script</span></span>

<span data-ttu-id="ad8ad-121">Запустите PowerShell и перейдите в каталог, где был сохранен файл сценария.</span><span class="sxs-lookup"><span data-stu-id="ad8ad-121">Launch PowerShell and change to the directory where you saved the script file.</span></span> <span data-ttu-id="ad8ad-122">Чтобы запустить сценарий, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ad8ad-122">To run the script, execute the following command:</span></span>

```powershell
.\ConferenceDailyReset.ps1 TrialsResourceGroup
```

<span data-ttu-id="ad8ad-123">Выполнение сценария может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="ad8ad-123">The script may take a few minutes to complete.</span></span> <span data-ttu-id="ad8ad-124">После завершения убедитесь, что он выполнен успешно:</span><span class="sxs-lookup"><span data-stu-id="ad8ad-124">When it is finished, verify that it ran successfully:</span></span>

1. <span data-ttu-id="ad8ad-125">В браузере войдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ad8ad-125">In a browser, sign into the Azure portal.</span></span>
2. <span data-ttu-id="ad8ad-126">В области навигации слева щелкните **Группы ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="ad8ad-126">In the navigation on the left, click **Resource Groups**.</span></span>
3. <span data-ttu-id="ad8ad-127">В списке групп ресурсов выберите **TrialsResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="ad8ad-127">In the list of resource groups, click **TrialsResourceGroup**.</span></span> <span data-ttu-id="ad8ad-128">В списке ресурсов должны отображаться только что созданные виртуальные машины и связанные с ними ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ad8ad-128">In the list of resources, you should see the newly created VMs and their associated resources.</span></span>

## <a name="summary"></a><span data-ttu-id="ad8ad-129">Сводка</span><span class="sxs-lookup"><span data-stu-id="ad8ad-129">Summary</span></span>
<span data-ttu-id="ad8ad-130">Вы написали сценарий, автоматизирующий создание трех виртуальных машин в группе ресурсов, указанной параметром сценария.</span><span class="sxs-lookup"><span data-stu-id="ad8ad-130">You wrote a script that automated the creation of three VMs in the resource group indicated by a script parameter.</span></span> <span data-ttu-id="ad8ad-131">Это короткий и простой сценарий, но он автоматизирует процесс, который может занять много времени при работе вручную на портале.</span><span class="sxs-lookup"><span data-stu-id="ad8ad-131">The script is short and simple but automates a process that would take a long time to complete manually with the portal.</span></span>