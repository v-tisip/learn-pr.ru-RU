## <a name="motivation"></a><span data-ttu-id="c754a-101">Мотивация</span><span class="sxs-lookup"><span data-stu-id="c754a-101">Motivation</span></span>
<span data-ttu-id="c754a-102">Azure CLI позволяет писать команды и выполнять их немедленно.</span><span class="sxs-lookup"><span data-stu-id="c754a-102">The Azure CLI lets you write commands and execute them immediately.</span></span> <span data-ttu-id="c754a-103">Вспомним, что главная цель в примере разработки программного обеспечения — развернуть новые сборки веб-приложения для тестирования.</span><span class="sxs-lookup"><span data-stu-id="c754a-103">Recall that the overall goal in the software development example is to deploy new builds of a web app for testing.</span></span> <span data-ttu-id="c754a-104">Первый шаг — создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c754a-104">The first step is to create a resource group.</span></span> <span data-ttu-id="c754a-105">Помните, что целью является создать эти ресурсы с помощью локально установленного Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c754a-105">Remember that the goal here is to create these resources using a local installation of the Azure CLI.</span></span> 

<span data-ttu-id="c754a-106">В этом модуле вы узнаете, как использовать Azure CLI для входа в подписку Azure и создания нового ресурса.</span><span class="sxs-lookup"><span data-stu-id="c754a-106">This unit shows you how to use the Azure CLI to sign in to your Azure subscription and create a new resource.</span></span>

## <a name="what-azure-resources-can-be-managed-using-the-azure-cli"></a><span data-ttu-id="c754a-107">Какими ресурсами Azure можно управлять с помощью Azure CLI?</span><span class="sxs-lookup"><span data-stu-id="c754a-107">What Azure resources can be managed using the Azure CLI?</span></span>
<span data-ttu-id="c754a-108">Azure CLI позволяет управлять практически всеми аспектами каждого ресурса Azure.</span><span class="sxs-lookup"><span data-stu-id="c754a-108">The Azure CLI lets you control nearly every aspect of every Azure resource.</span></span> <span data-ttu-id="c754a-109">Вы можете работать с группами ресурсов, хранилищами, виртуальными машинами, Azure Active Directory (Azure AD), контейнерами, использовать машинное обучение и т. д.</span><span class="sxs-lookup"><span data-stu-id="c754a-109">You can work with resource groups, storage, virtual machines, Azure Active Directory (Azure AD), containers, machine learning, and so on.</span></span>

<span data-ttu-id="c754a-110">Команды в интерфейсе командной строки разделены на группы и подгруппы.</span><span class="sxs-lookup"><span data-stu-id="c754a-110">Commands in the CLI are structured in groups and subgroups.</span></span> <span data-ttu-id="c754a-111">Каждая группа представляет службу, предоставляемую Azure, а подгруппы позволяют распределить команды для этих служб в логические группы.</span><span class="sxs-lookup"><span data-stu-id="c754a-111">Each group represents a service provided by Azure, and the subgroups divide commands for these services into logical groupings.</span></span> <span data-ttu-id="c754a-112">Например, группа **хранения** содержит подгруппы **учетной записи**, **BLOB-объектов**, **хранения** и **очереди**.</span><span class="sxs-lookup"><span data-stu-id="c754a-112">For example, the **storage** group contains subgroups including **account**, **blob**, **storage**, and **queue**.</span></span>

<span data-ttu-id="c754a-113">Как найти конкретную необходимую команду?</span><span class="sxs-lookup"><span data-stu-id="c754a-113">So, how do you find the particular commands you need?</span></span> <span data-ttu-id="c754a-114">Один из способов — использование **az find**.</span><span class="sxs-lookup"><span data-stu-id="c754a-114">One way is to use **az find**.</span></span> <span data-ttu-id="c754a-115">Например, если вы хотите найти команды для управления хранилищем **BLOB-объектов**, используется следующая команда поиска:</span><span class="sxs-lookup"><span data-stu-id="c754a-115">For example, if you want to find commands that might help you manage a storage **blob**, you'd use the following find command:</span></span>

```bash
az find -q blob
```

<span data-ttu-id="c754a-116">Если вы уже знаете имя нужной команды, лучше использовать аргумент **--help** для этой команды.</span><span class="sxs-lookup"><span data-stu-id="c754a-116">If you already know the name of the command you want, the **--help** argument for that command may be more useful.</span></span> <span data-ttu-id="c754a-117">Вы получите подробные сведения о команде, а для группы команд — список доступных подкоманд.</span><span class="sxs-lookup"><span data-stu-id="c754a-117">You get detailed information on the command, and for a command group, a list of the available subcommands.</span></span> <span data-ttu-id="c754a-118">Таким образом, в нашем примере хранилища мы можем получить список подгрупп и команд для управления хранилищем BLOB-объектов следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c754a-118">So, with our storage example, here's how you can get a list of the subgroups and commands for managing blob storage:</span></span>

```bash
az storage blob --help
```

## <a name="how-to-create-an-azure-resource"></a><span data-ttu-id="c754a-119">Как создать ресурс Azure</span><span class="sxs-lookup"><span data-stu-id="c754a-119">How to create an Azure resource</span></span>
<span data-ttu-id="c754a-120">Для создания нового ресурса Azure обычно необходимо выполнить три действия: подключиться к подписке Azure, создать ресурс и убедиться, что создание выполнено успешно (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="c754a-120">When creating a new Azure resource, there are typically three steps: connect to your Azure subscription, create the resource, and verify that creation was successful (see below).</span></span>

![Этапы создания ресурса с помощью Azure CLI](../media-drafts/4-create-resources-overview.png)

<span data-ttu-id="c754a-122">На каждом этапе используется своя команда Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c754a-122">Each step corresponds to a different Azure CLI command.</span></span>

### <a name="connect"></a><span data-ttu-id="c754a-123">Подключение</span><span class="sxs-lookup"><span data-stu-id="c754a-123">Connect</span></span>
<span data-ttu-id="c754a-124">Так как вы работаете с локальной установкой Azure CLI, перед выполнением команд Azure вам потребуется пройти проверку подлинности с помощью команды Azure CLI **login**.</span><span class="sxs-lookup"><span data-stu-id="c754a-124">Since you're working with a local install of the Azure CLI, you'll need to authenticate before you can execute Azure commands, by using the Azure CLI **login** command.</span></span> 

```bash
az login
```

<span data-ttu-id="c754a-125">Azure CLI обычно запускает браузер по умолчанию и открывает страницу входа в Azure.</span><span class="sxs-lookup"><span data-stu-id="c754a-125">The Azure CLI will typically launch your default browser to open the Azure sign-in page.</span></span> <span data-ttu-id="c754a-126">Если это не срабатывает, следуйте указаниям командной строки и введите код авторизации в [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span><span class="sxs-lookup"><span data-stu-id="c754a-126">If this doesn't work, follow the command-line instructions and enter an authorization code at [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span></span>

<span data-ttu-id="c754a-127">После успешного входа вы будете подключены к вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="c754a-127">After a successful sign in, you'll be connected to your Azure subscription.</span></span> 

### <a name="create"></a><span data-ttu-id="c754a-128">Создание</span><span class="sxs-lookup"><span data-stu-id="c754a-128">Create</span></span>
<span data-ttu-id="c754a-129">Часто необходимо создать новую группу ресурсов перед созданием новой службы Azure, поэтому мы будем использовать группы ресурсов в качестве примера, чтобы показать, как создать ресурсы Azure из интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="c754a-129">You'll often need to create a new resource group before you create a new Azure service, so we'll use resource groups as an example to show how to create Azure resources from the CLI.</span></span>

<span data-ttu-id="c754a-130">Чтобы создать группу ресурсов, используйте команду Azure CLI **group create**.</span><span class="sxs-lookup"><span data-stu-id="c754a-130">The Azure CLI **group create** command creates a resource group.</span></span> <span data-ttu-id="c754a-131">Необходимо указать имя и расположение.</span><span class="sxs-lookup"><span data-stu-id="c754a-131">You must specify a name and location.</span></span> <span data-ttu-id="c754a-132">Имя должно быть уникальным в пределах вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="c754a-132">The name must be unique within your subscription.</span></span> <span data-ttu-id="c754a-133">Расположение определяет место хранения метаданных для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c754a-133">The location determines where the metadata for your resource group will be stored.</span></span> <span data-ttu-id="c754a-134">Используйте такие строки, как "West US", "North Europe" или "West India", чтобы указать расположение. Кроме того, вы можете использовать эквиваленты в одно слово, например westus, northeurope или westindia.</span><span class="sxs-lookup"><span data-stu-id="c754a-134">You use strings like "West US", "North Europe", or "West India" to specify the location; alternatively, you can use single word equivalents, such as westus, northeurope, or westindia.</span></span> <span data-ttu-id="c754a-135">Основной синтаксис выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c754a-135">The core syntax is:</span></span>

```bash
az group create --name <name> --location <location>
```

### <a name="verify"></a><span data-ttu-id="c754a-136">Проверка</span><span class="sxs-lookup"><span data-stu-id="c754a-136">Verify</span></span>
<span data-ttu-id="c754a-137">Azure CLI предоставляет **список** подкоманд для просмотра сведений о ресурсе для многих ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="c754a-137">For many Azure resources, the Azure CLI provides a **list** subcommand to view resource details.</span></span> <span data-ttu-id="c754a-138">Например, команда Azure CLI **group list** выводит список групп ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="c754a-138">For example, the Azure CLI **group list** command lists your Azure resource groups.</span></span> <span data-ttu-id="c754a-139">Это полезно для проверки успешного создания группы ресурсов:</span><span class="sxs-lookup"><span data-stu-id="c754a-139">This is useful here to verify whether creation of the resource group was successful:</span></span>

```bash
az group list
```

<span data-ttu-id="c754a-140">Чтобы получить более краткое представление, отформатируйте выходные данные в виде простой таблицы:</span><span class="sxs-lookup"><span data-stu-id="c754a-140">To get a more concise view, you can format the output as a simple table:</span></span>

```bash
az group list --output table
```
