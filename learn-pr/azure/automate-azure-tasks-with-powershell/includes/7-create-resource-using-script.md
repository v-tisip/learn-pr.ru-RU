<span data-ttu-id="982d6-101">Для выполнения сложных или повторяющихся задач часто требуется немало административного времени.</span><span class="sxs-lookup"><span data-stu-id="982d6-101">Complex or repetitive tasks often take a great deal of administrative time.</span></span> <span data-ttu-id="982d6-102">Организации предпочитают автоматизировать эти задачи, чтобы сократить затраты и избежать возникновения ошибок.</span><span class="sxs-lookup"><span data-stu-id="982d6-102">Organizations prefer to automate these tasks to reduce costs and avoid errors.</span></span>

<span data-ttu-id="982d6-103">Этот момент имеет важное значение в примере компании CRM.</span><span class="sxs-lookup"><span data-stu-id="982d6-103">This is important in the Customer Relationship Management (CRM) company example.</span></span> <span data-ttu-id="982d6-104">В нем вы тестируете программное обеспечение на нескольких виртуальных машинах Linux, которые необходимо постоянно удалять и создавать повторно.</span><span class="sxs-lookup"><span data-stu-id="982d6-104">There, you test your software on multiple Linux Virtual Machines (VMs) that you need to continuously delete and recreate.</span></span> <span data-ttu-id="982d6-105">Вы хотите использовать сценарий PowerShell, позволяющий автоматизировать создание виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="982d6-105">You want to use a PowerShell script to automate the creation of the VMs.</span></span>

<span data-ttu-id="982d6-106">Помимо базовой операции по созданию виртуальной машины, у вас есть несколько дополнительных требований к сценарию.</span><span class="sxs-lookup"><span data-stu-id="982d6-106">Beyond the core operation of creating a VM you have a few additional requirements for your script.</span></span> 
- <span data-ttu-id="982d6-107">Поскольку вы будете создавать несколько виртуальных машин, операцию создания необходимо поместить в цикл.</span><span class="sxs-lookup"><span data-stu-id="982d6-107">You will create multiple VMs, so you want to put the creation inside a loop</span></span>
- <span data-ttu-id="982d6-108">Вам необходимо создать виртуальные машины в трех разных группах ресурсов, поэтому имя группы ресурсов должно передаваться в сценарий в виде параметра.</span><span class="sxs-lookup"><span data-stu-id="982d6-108">You need to create VMs in three different resource groups, so the name of the resource group should be passed to the script as a parameter</span></span>

<span data-ttu-id="982d6-109">В этом разделе вы узнаете, как создавать и выполнять сценарий Azure PowerShell, который отвечает этим требованиям.</span><span class="sxs-lookup"><span data-stu-id="982d6-109">In this section, you will see how to write and execute an Azure PowerShell script that meets these requirements.</span></span>

## <a name="what-is-a-powershell-script"></a><span data-ttu-id="982d6-110">Что такое сценарий PowerShell?</span><span class="sxs-lookup"><span data-stu-id="982d6-110">What is a PowerShell script?</span></span>
<span data-ttu-id="982d6-111">Сценарий PowerShell — это текстовый файл, содержащий команды и управляющие конструкции.</span><span class="sxs-lookup"><span data-stu-id="982d6-111">A PowerShell script is a text file containing commands and control constructs.</span></span> <span data-ttu-id="982d6-112">Команды являются вызовами командлетов.</span><span class="sxs-lookup"><span data-stu-id="982d6-112">The commands are invocations of cmdlets.</span></span> <span data-ttu-id="982d6-113">Управляющие конструкции представляют собой компоненты программирования, такие как циклы, переменные, параметры, комментарии и т. д., предоставляемые PowerShell.</span><span class="sxs-lookup"><span data-stu-id="982d6-113">The control constructs are programming features like loops, variables, parameters, comments, etc. supplied by PowerShell.</span></span>

<span data-ttu-id="982d6-114">Файлы сценариев PowerShell имеют расширение **PST1**.</span><span class="sxs-lookup"><span data-stu-id="982d6-114">PowerShell script files have a **.ps1** file extension.</span></span> <span data-ttu-id="982d6-115">Эти файлы можно создавать и сохранять в любом текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="982d6-115">You can create and save these files with any text editor.</span></span> 

> [!TIP]
> <span data-ttu-id="982d6-116">Если вы пишете сценарии PowerShell в Windows, можно использовать интегрированную среду сценариев (ISE) Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="982d6-116">If you’re writing PowerShell scripts under Windows, you can use the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="982d6-117">Этот редактор предоставляет такие функции, как раскраска синтаксических конструкций и список доступных командлетов.</span><span class="sxs-lookup"><span data-stu-id="982d6-117">This editor provides features such as syntax coloring and a list of available cmdlets.</span></span>
>
>![Среда ISE Windows PowerShell](../media-drafts/7-windows-powershell-ise-screenshot.png)

<span data-ttu-id="982d6-119">После написания сценария выполните его из командной строки PowerShell, передав имя файла, в начале которого стоит точка и обратная косая черта:</span><span class="sxs-lookup"><span data-stu-id="982d6-119">Once you have written the script, execute it from the PowerShell command line by passing the name of the file preceded by a dot and a backslash:</span></span>

```powershell
.\myScript.ps1
```

## <a name="powershell-techniques"></a><span data-ttu-id="982d6-120">Методы PowerShell</span><span class="sxs-lookup"><span data-stu-id="982d6-120">PowerShell techniques</span></span>
<span data-ttu-id="982d6-121">PowerShell поддерживает множество функций, которые встречаются в стандартных языках программирования.</span><span class="sxs-lookup"><span data-stu-id="982d6-121">PowerShell has many features found in typical programming languages.</span></span> <span data-ttu-id="982d6-122">Вы можете определять переменные, использовать ветви и циклы, записывать параметры командной строки, создавать функции, добавлять комментарии и т. д.</span><span class="sxs-lookup"><span data-stu-id="982d6-122">You can define variables, use branches and loops, capture command-line parameters, write functions, add comments, and so on.</span></span> <span data-ttu-id="982d6-123">Для сценария нам потребуются три компонента: переменные, циклы и параметры.</span><span class="sxs-lookup"><span data-stu-id="982d6-123">We will need three features for our script: variables, loops, and parameters.</span></span>

### <a name="variables"></a><span data-ttu-id="982d6-124">Переменные</span><span class="sxs-lookup"><span data-stu-id="982d6-124">Variables</span></span>
<span data-ttu-id="982d6-125">PowerShell поддерживает переменные.</span><span class="sxs-lookup"><span data-stu-id="982d6-125">PowerShell supports variables.</span></span> <span data-ttu-id="982d6-126">Используйте **$** для объявления переменной и **=** для присвоения значения.</span><span class="sxs-lookup"><span data-stu-id="982d6-126">Use **$** to declare a variable and **=** to assign a value.</span></span> <span data-ttu-id="982d6-127">Например:</span><span class="sxs-lookup"><span data-stu-id="982d6-127">For example:</span></span>

```powershell
$loc = "East US"
$iterations = 3
```

<span data-ttu-id="982d6-128">Переменные могут содержать объекты.</span><span class="sxs-lookup"><span data-stu-id="982d6-128">Variables can hold objects.</span></span> <span data-ttu-id="982d6-129">Например, следующее определение задает переменную **adminCredential** для объекта, возвращаемого командлетом **Get-Credential**.</span><span class="sxs-lookup"><span data-stu-id="982d6-129">For example, the following definition sets the **adminCredential** variable to the object returned by the **Get-Credential** cmdlet.</span></span>

```powershell
$adminCredential = Get-Credential
```

<span data-ttu-id="982d6-130">Чтобы получить значение, сохраненное в переменной, используйте префикс **$** и его имя, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="982d6-130">To obtain the value stored in a variable, use the **$** prefix and its name as shown below:</span></span> 

```powershell
$loc = "East US"
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location $loc
```

### <a name="loops"></a><span data-ttu-id="982d6-131">Циклы</span><span class="sxs-lookup"><span data-stu-id="982d6-131">Loops</span></span>
<span data-ttu-id="982d6-132">PowerShell имеет несколько циклов: **For**, **Do...While**, **For...Each** и т. д.</span><span class="sxs-lookup"><span data-stu-id="982d6-132">PowerShell has several loops: **For**, **Do...While**, **For...Each**, and so on.</span></span> <span data-ttu-id="982d6-133">Цикл **For** подходит нам лучше всего, так как мы будем выполнять командлет фиксированное число раз.</span><span class="sxs-lookup"><span data-stu-id="982d6-133">The **For** loop is the best match for our needs because we will execute a cmdlet a fixed number of times.</span></span>

<span data-ttu-id="982d6-134">Основной синтаксис показан ниже. Пример выполняется два раза и каждый раз выводит значение **i**.</span><span class="sxs-lookup"><span data-stu-id="982d6-134">The core syntax is shown below; the example runs for two iterations and prints the value of **i** each time.</span></span> <span data-ttu-id="982d6-135">Операторы сравнения записываются следующим образом: **- lt** — меньше чем, **-le** — меньше или равно, **eq** — равно, **ne** — не равно.</span><span class="sxs-lookup"><span data-stu-id="982d6-135">The comparison operators are written **-lt** for "less than", **-le** for "less than or equal", **eq** for "equal", **ne** for "not equal", etc.</span></span>

```powershell
For ($i = 1; $i -lt 3; $i++)
{
    $i
}
```

### <a name="parameters"></a><span data-ttu-id="982d6-136">Параметры</span><span class="sxs-lookup"><span data-stu-id="982d6-136">Parameters</span></span>
<span data-ttu-id="982d6-137">При выполнении сценария можно передать аргументы в командной строке.</span><span class="sxs-lookup"><span data-stu-id="982d6-137">When you execute a script, you can pass arguments on the command line.</span></span> <span data-ttu-id="982d6-138">Чтобы упростить получение значений в сценарии, укажите имена для каждого параметра.</span><span class="sxs-lookup"><span data-stu-id="982d6-138">You can provide names for each parameter to help the script extract the values.</span></span> <span data-ttu-id="982d6-139">Например: </span><span class="sxs-lookup"><span data-stu-id="982d6-139">For example:</span></span>

```powershell
.\setupEnvironment.ps1 -size 5 -location "East US"
```

<span data-ttu-id="982d6-140">Внутри скрипта значения записываются в переменные.</span><span class="sxs-lookup"><span data-stu-id="982d6-140">Inside the script, you capture the values into variables.</span></span> <span data-ttu-id="982d6-141">В этом случае параметры сопоставляются по имени:</span><span class="sxs-lookup"><span data-stu-id="982d6-141">In this example, the parameters are matched by name:</span></span>

```powershell
param([string]$location, [int]$size)
```

<span data-ttu-id="982d6-142">Имена из командной строки можно опустить.</span><span class="sxs-lookup"><span data-stu-id="982d6-142">You can omit the names from the command line.</span></span> <span data-ttu-id="982d6-143">Например:</span><span class="sxs-lookup"><span data-stu-id="982d6-143">For example:</span></span>

```powershell
.\setupEnvironment.ps1 5 "East US"
```

<span data-ttu-id="982d6-144">Если в сценарии используются неименованные параметры, при сопоставлении во внимание принимается позиция:</span><span class="sxs-lookup"><span data-stu-id="982d6-144">Inside the script, you rely on position for matching when the parameters are unnamed:</span></span>

```powershell
param([int]$size, [string]$location)
```

## <a name="how-to-create-a-linux-virtual-machine"></a><span data-ttu-id="982d6-145">Создание виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="982d6-145">How to create a Linux Virtual Machine</span></span>
<span data-ttu-id="982d6-146">Для создания виртуальной машины Azure PowerShell предоставляет командлет **New-AzureRmVm**.</span><span class="sxs-lookup"><span data-stu-id="982d6-146">Azure PowerShell provides the **New-AzureRmVm** cmdlet to create a Virtual Machine.</span></span> <span data-ttu-id="982d6-147">У командлета много параметров, позволяющих обрабатывать множество параметров конфигурации виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="982d6-147">The cmdlet has many parameters to let it handle the large number of VM configuration settings.</span></span> <span data-ttu-id="982d6-148">Большая часть параметров имеет разумные значения по умолчанию, поэтому нам нужно указать только пять.</span><span class="sxs-lookup"><span data-stu-id="982d6-148">Most of the parameters have reasonable default values so we only need to specify five things:</span></span>
- <span data-ttu-id="982d6-149">**ResourceGroupName**: группа ресурсов, в которой будет размещена новая виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="982d6-149">**ResourceGroupName**: The resource group into which the new VM will be placed.</span></span>
- <span data-ttu-id="982d6-150">**Имя**: имя виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="982d6-150">**Name**: The name of the VM in Azure.</span></span>
- <span data-ttu-id="982d6-151">**Расположение**: географическое расположение, где будет подготовлена виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="982d6-151">**Location**: Geographic location where the VM will be provisioned.</span></span>
- <span data-ttu-id="982d6-152">**Учетные данные**: объект, содержащий имя пользователя и пароль для учетной записи администратора виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="982d6-152">**Credential**: An object containing the username and password for the VM admin account.</span></span> <span data-ttu-id="982d6-153">Для запроса имени пользователя и пароля мы будем использовать командлет **Get-Credential**.</span><span class="sxs-lookup"><span data-stu-id="982d6-153">We will use the **Get-Credential** The cmdlet to prompt for a username and password.</span></span> <span data-ttu-id="982d6-154">Командлет **Get-Credential** упаковывает имя пользователя и пароль в объект учетных данных, который он возвращает в результате выполнения.</span><span class="sxs-lookup"><span data-stu-id="982d6-154">**Get-Credential** packages the username and password into a credential object, which it returns as its result.</span></span>
- <span data-ttu-id="982d6-155">**Образ**: удостоверение операционной системы для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="982d6-155">**Image**: Identity of the operating system to use for the VM.</span></span> <span data-ttu-id="982d6-156">Мы будем использовать "UbuntuLTS".</span><span class="sxs-lookup"><span data-stu-id="982d6-156">We will use "UbuntuLTS".</span></span>

<span data-ttu-id="982d6-157">Синтаксис командлета приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="982d6-157">The syntax for the cmdlet is shown below:</span></span>

```powershell
   New-AzureRmVm 
       -ResourceGroupName <resource group name> 
       -Name <machine name> 
       -Credential <credentials object> 
       -Location <location> 
       -Image <image name>
```

## <a name="summary"></a><span data-ttu-id="982d6-158">Сводка</span><span class="sxs-lookup"><span data-stu-id="982d6-158">Summary</span></span>
<span data-ttu-id="982d6-159">Благодаря сочетанию PowerShell и Azure PowerShell вы получаете все средства, необходимые для автоматизации задач в Azure.</span><span class="sxs-lookup"><span data-stu-id="982d6-159">The combination of PowerShell and Azure PowerShell gives you all the tools you need to automate Azure.</span></span> <span data-ttu-id="982d6-160">В примере CRM мы сможем создать несколько виртуальных машин Linux, используя параметр, чтобы сохранить универсальность сценария, и цикл, чтобы избежать повторяющегося кода.</span><span class="sxs-lookup"><span data-stu-id="982d6-160">In our CRM example, we will be able to create multiple Linux VMs using a parameter to keep the script generic and a loop to avoid repeated code.</span></span> <span data-ttu-id="982d6-161">Это означает, что прежняя сложная операция теперь может выполняться за один шаг.</span><span class="sxs-lookup"><span data-stu-id="982d6-161">This means that a formerly complex operation can now be executed in a single step.</span></span>