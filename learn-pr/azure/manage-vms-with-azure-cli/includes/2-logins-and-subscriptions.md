<span data-ttu-id="c84a3-101">Прежде чем мы начнем, давайте рассмотрим синтаксис средства интерфейса командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="c84a3-101">Before we start, let's review the syntax for the Azure CLI tool.</span></span> <span data-ttu-id="c84a3-102">Если вы изучили модуль **Управления службами Azure с помощью Azure CLI**, то знаете, что команды Azure CLI имеют следующий формат.</span><span class="sxs-lookup"><span data-stu-id="c84a3-102">If you've taken the **Control Azure services with the Azure CLI** module, then you know that Azure CLI commands take the form of:</span></span>

```azurecli
az [command] [subcommand] [--parameter --parameter]
```

<span data-ttu-id="c84a3-103">`[command]` указывает на определенную область Azure, которой вы хотите управлять.</span><span class="sxs-lookup"><span data-stu-id="c84a3-103">The `[command]` identifies the specific area of Azure you want to control.</span></span> <span data-ttu-id="c84a3-104">Например, вы можете управлять сведениями о подписке с помощь команды `account` или базами данных SQL с помощью команды `sql`.</span><span class="sxs-lookup"><span data-stu-id="c84a3-104">For example, you can manage subscription information with the `account` command, or SQL databases with the `sql` command.</span></span> <span data-ttu-id="c84a3-105">`[subcommand]` и `[--parameters]` зависят от команды, с которой вы работаете.</span><span class="sxs-lookup"><span data-stu-id="c84a3-105">The `[subcommand]` and `[--parameters]` are then dependent upon the command you're working with.</span></span> 

<span data-ttu-id="c84a3-106">Чтобы просмотреть список команд, подкоманд и параметров, введите часть команды.</span><span class="sxs-lookup"><span data-stu-id="c84a3-106">You can view a list of commands, subcommands, and parameters by typing in a partial command.</span></span> <span data-ttu-id="c84a3-107">Например, при вводе `az` в командной строке появится экран справки верхнего уровня, а при вводе `az vm` отобразятся все подкоманды для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c84a3-107">For example, typing `az` at the command line will give you the top-level help screen, and typing `az vm` will give you all the subcommands for virtual machines.</span></span> <span data-ttu-id="c84a3-108">Это очень удобный способ изучить средство Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c84a3-108">This approach can be a great way to explore the Azure CLI tool.</span></span>

> [!NOTE]
> <span data-ttu-id="c84a3-109">Мы будем использовать Azure Cloud Shell в браузере для работы с Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c84a3-109">We will be using browser-hosted Azure Cloud Shell to work with the Azure CLI.</span></span> <span data-ttu-id="c84a3-110">Если вы предпочитаете работать на локальном компьютере, все эти команды также можно выполнить из командной строки после [установки Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="c84a3-110">If you prefer to work from your local machine, all of the commands we cover can also be executed from the command line by [installing the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="c84a3-111">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="c84a3-111">Log in to Azure</span></span>

<span data-ttu-id="c84a3-112">Первое, что вы должны сделать при работе с Azure CLI, — войти в свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="c84a3-112">The first thing you'll do when working with the Azure CLI is to log in to your Azure account.</span></span> <span data-ttu-id="c84a3-113">Для этого используйте команду `login`.</span><span class="sxs-lookup"><span data-stu-id="c84a3-113">This is done with the `login` command.</span></span> <span data-ttu-id="c84a3-114">Если вы используете Cloud Shell, у вас будет кнопка для входа в Azure.</span><span class="sxs-lookup"><span data-stu-id="c84a3-114">If you're using Cloud Shell, there will be a button to sign in to Azure.</span></span>

```azurecli
az login
```

<span data-ttu-id="c84a3-115">Эта команда запустит окно браузера, где вы сможете выбрать учетную запись Майкрософт, которую хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="c84a3-115">This command will launch a browser window and allow you to select the Microsoft account you want to use.</span></span>

## <a name="working-with-subscriptions"></a><span data-ttu-id="c84a3-116">Использование подписок</span><span class="sxs-lookup"><span data-stu-id="c84a3-116">Working with subscriptions</span></span>

<span data-ttu-id="c84a3-117">В этом модуле мы будем работать во временной подписке, созданной для изучения, но обычно вы будете использовать подписку из вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="c84a3-117">In this module, we will work in a temporary subscription created as a playground, but you will normally use a subscription from your own account.</span></span> <span data-ttu-id="c84a3-118">Если у вас несколько подписок, вы можете вывести четко отформатированный список подписок с помощью инструкции `az account list --output table`.</span><span class="sxs-lookup"><span data-stu-id="c84a3-118">If you have more than one subscription, you can get a clearly formatted list of subscriptions using the `az account list --output table` statement.</span></span>

```
Name                                  CloudName    SubscriptionId                        State    IsDefault
------------------------------------  -----------  ------------------------------------  -------  -----------
Contoso Legacy Resources              AzureCloud   abc13b0c-d2c4-64b2-9ac5-2f4cb819b752  Enabled  True
Visual Studio Enterprise              AzureCloud   233aebce-23c2-4572-c056-c029449e93ed  Enabled  False
```

<span data-ttu-id="c84a3-119">Обратите внимание, что эта команда также задает подписку _по умолчанию_, где применяются все команды.</span><span class="sxs-lookup"><span data-stu-id="c84a3-119">Notice that the command also identifies the _default_ subscription where all your commands will apply.</span></span> <span data-ttu-id="c84a3-120">Если вы предпочитаете работать в другой подписке, используйте команду `az account set --subscription "[name]"`.</span><span class="sxs-lookup"><span data-stu-id="c84a3-120">If you would prefer to work in a different subscription, you can use the `az account set --subscription "[name]"` command.</span></span> <span data-ttu-id="c84a3-121">Например, мы можем установить текущую подписку `Visual Studio Enterprise` из приведенного выше списка с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="c84a3-121">For example, we could set our current subscription to be `Visual Studio Enterprise` from the above list through the following command:</span></span>

```azurecli
az account set --subscription "Visual Studio Enterprise"
```