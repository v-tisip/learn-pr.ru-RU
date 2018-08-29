<span data-ttu-id="513ce-101">Пришло время запустить наше приложение в Azure.</span><span class="sxs-lookup"><span data-stu-id="513ce-101">Now it's time to run our app in Azure.</span></span> <span data-ttu-id="513ce-102">Нам нужно создать приложение Службы приложений Azure, настроить его с использованием MSI и нашей конфигурации хранилища, а также развернуть код.</span><span class="sxs-lookup"><span data-stu-id="513ce-102">We need to create an Azure App Service app, set it up with MSI and our vault configuration, and deploy our code.</span></span>

## <a name="exercise"></a><span data-ttu-id="513ce-103">Упражнение</span><span class="sxs-lookup"><span data-stu-id="513ce-103">Exercise</span></span>

### <a name="create-the-app-service-plan-and-app"></a><span data-ttu-id="513ce-104">Создание приложения и плана Службы приложений</span><span class="sxs-lookup"><span data-stu-id="513ce-104">Create the App Service plan and app</span></span>

<span data-ttu-id="513ce-105">Создание приложения Службы приложений состоит из двух этапов: сначала создается *план*, а затем — *приложение*.</span><span class="sxs-lookup"><span data-stu-id="513ce-105">Creating an App Service app is a two-step process: First create the *plan*, then the *app*.</span></span>

<span data-ttu-id="513ce-106">Имя *плана* должно быть уникальным только в рамках вашей подписки, поэтому вы можете использовать то же имя, что и мы: **keyvault-exercise-plan**.</span><span class="sxs-lookup"><span data-stu-id="513ce-106">The *plan* name only needs to be unique within your subscription, so you can use the same name we've used: **keyvault-exercise-plan**.</span></span> <span data-ttu-id="513ce-107">Имя приложения должно быть уникальным на глобальном уровне, поэтому вам нужно выбрать его самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="513ce-107">The app name needs to be globally unique, though, so you'll need to pick your own.</span></span>

<span data-ttu-id="513ce-108">В Azure Cloud Shell выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="513ce-108">In Azure Cloud Shell, run the following:</span></span>

```azurecli
az appservice plan create --name keyvault-exercise-plan --resource-group keyvault-exercise-group
az webapp create --name <your-unique-app-name> --plan keyvault-exercise-plan --resource-group keyvault-exercise-group
```

### <a name="add-configuration-to-the-app"></a><span data-ttu-id="513ce-109">Добавление конфигурации в приложение</span><span class="sxs-lookup"><span data-stu-id="513ce-109">Add configuration to the app</span></span>

<span data-ttu-id="513ce-110">При развертывании в Azure мы будем следовать рекомендациям для Службы приложений, заключающимся в помещении конфигурации в параметры приложения вместо файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="513ce-110">For deploying to Azure, we'll follow the App Service best practice of putting configuration in Application Settings instead of a configuration file.</span></span>

```azurecli
az webapp config appsettings set --name <your-unique-app-name> --resource-group keyvault-exercise-group --settings VaultName=<your-unique-vault-name>
```

### <a name="enable-msi"></a><span data-ttu-id="513ce-111">Включение MSI</span><span class="sxs-lookup"><span data-stu-id="513ce-111">Enable MSI</span></span>

<span data-ttu-id="513ce-112">Включение MSI для приложения выполняется одной строкой:</span><span class="sxs-lookup"><span data-stu-id="513ce-112">Enabling MSI on an app is a one-liner:</span></span>

```azurecli
az webapp identity assign --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

<span data-ttu-id="513ce-113">В полученных выходных данных JSON скопируйте значение **principalId**.</span><span class="sxs-lookup"><span data-stu-id="513ce-113">From the JSON output that results, copy the **principalId** value.</span></span> <span data-ttu-id="513ce-114">PrincipalId — это уникальный идентификатор нового удостоверения приложения в Azure Active Directory, который мы будем использовать в следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="513ce-114">PrincipalId is the unique ID of the app's new identity in Azure Active Directory, and we're going to use it in the next step.</span></span>

### <a name="grant-access-to-the-vault"></a><span data-ttu-id="513ce-115">Предоставление доступа к хранилищу</span><span class="sxs-lookup"><span data-stu-id="513ce-115">Grant access to the vault</span></span>

<span data-ttu-id="513ce-116">Теперь нужно предоставить удостоверению приложения разрешения для получения и перечисления секретов из хранилища рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="513ce-116">Now you need to give your app identity permissions to get and list secrets from your production-environment vault.</span></span> <span data-ttu-id="513ce-117">Используйте значение **principalId**, скопированное на предыдущем шаге, в качестве значения **object-id** в приведенной ниже команде.</span><span class="sxs-lookup"><span data-stu-id="513ce-117">Use the **principalId** value you copied from the previous step as the value for **object-id** in the command below.</span></span>

```azurecli
az keyvault set-policy --name <your-unique-vault-name> --object-id <your-msi-principleid> --secret-permissions get list
```

### <a name="deploy-the-app-and-try-it-out"></a><span data-ttu-id="513ce-118">Развертывание и оценка приложения</span><span class="sxs-lookup"><span data-stu-id="513ce-118">Deploy the app and try it out</span></span>

<span data-ttu-id="513ce-119">Конфигурация настроена, и вы можете приступать к развертыванию.</span><span class="sxs-lookup"><span data-stu-id="513ce-119">All your configuration is set and you're ready to deploy!</span></span> <span data-ttu-id="513ce-120">Приведенные ниже команды опубликуют сайт в папке `pub`, запакуют ее в `site.zip` и развернут этот ZIP-файл в Службе приложений.</span><span class="sxs-lookup"><span data-stu-id="513ce-120">The below commands will publish the site to the `pub` folder, zip it up into `site.zip`, and deploy the zip to App Service.</span></span>

> [!NOTE]
> <span data-ttu-id="513ce-121">Вам потребуется вернуться в каталог KeyVaultDemoApp с помощью команды `cd`, если вы еще это не сделали.</span><span class="sxs-lookup"><span data-stu-id="513ce-121">You'll need to `cd` back to the KeyVaultDemoApp directory if you haven't already.</span></span>

```console
dotnet publish -o pub
zip -j site.zip pub/*
az webapp deployment source config-zip --src site.zip --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

<span data-ttu-id="513ce-122">Получив результат, указывающий на развертывание сайта, откройте `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` в браузере.</span><span class="sxs-lookup"><span data-stu-id="513ce-122">Once you get a result that indicates the site has deployed, open `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` in a browser.</span></span> <span data-ttu-id="513ce-123">Вы должны увидеть значение секрета **reindeer_flotilla**.</span><span class="sxs-lookup"><span data-stu-id="513ce-123">You should see the secret value, **reindeer_flotilla**.</span></span>

<span data-ttu-id="513ce-124">Приложение завершено и развернуто.</span><span class="sxs-lookup"><span data-stu-id="513ce-124">Your app is finished and deployed!</span></span>