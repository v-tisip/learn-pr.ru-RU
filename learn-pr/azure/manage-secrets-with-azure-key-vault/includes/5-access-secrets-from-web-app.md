<span data-ttu-id="661ae-101">Теперь, когда вы знаете, как включение MSI создает для вашего приложения удостоверение для проверки подлинности, создадим приложение, которое будет использовать это удостоверение для доступа к секретам в хранилище.</span><span class="sxs-lookup"><span data-stu-id="661ae-101">Now that you know how enabling MSI creates an identity for our app to use for authentication, we'll create an app that uses that identity to access secrets in the vault.</span></span>

## <a name="reading-secrets-in-an-aspnet-core-app"></a><span data-ttu-id="661ae-102">Чтение секретов в приложении ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="661ae-102">Reading secrets in an ASP.NET Core app</span></span>

<span data-ttu-id="661ae-103">API хранилища ключей Azure — это API REST, который обрабатывает все операции управления и использования ключей и хранилищ.</span><span class="sxs-lookup"><span data-stu-id="661ae-103">The Azure Key Vault API is a REST API that handles all management and usage of keys and vaults.</span></span> <span data-ttu-id="661ae-104">Каждый секрет в хранилище имеет уникальный URL-адрес, а значения секретов извлекаются с помощью HTTP-запросов GET.</span><span class="sxs-lookup"><span data-stu-id="661ae-104">Each secret in a vault has a unique URL, and secret values are retrieved with HTTP GET requests.</span></span>

<span data-ttu-id="661ae-105">Официальной клиентской библиотекой хранилища ключей служит класс `KeyVaultClient` в пакете NuGet Microsoft.Azure.KeyVault.</span><span class="sxs-lookup"><span data-stu-id="661ae-105">The official Key Vault client library for .NET Core is the `KeyVaultClient` class in the Microsoft.Azure.KeyVault NuGet package.</span></span> <span data-ttu-id="661ae-106">Использовать его напрямую, через &mdash; с помощью метода ASP.NET Core `AddAzureKeyVault`, необязательно; все секреты из хранилища можно загрузить в API конфигурации при запуске.</span><span class="sxs-lookup"><span data-stu-id="661ae-106">You don't need to use it directly, though &mdash; with ASP.NET Core's `AddAzureKeyVault` method, you can load all the secrets from a vault into the Configuration API at startup.</span></span> <span data-ttu-id="661ae-107">Этот способ позволит вам получить доступ ко всем своим секретам по имени, используя тот же интерфейс `IConfiguration`, что и в остальной части конфигурации.</span><span class="sxs-lookup"><span data-stu-id="661ae-107">This technique enables you to access all of your secrets by name using the same `IConfiguration` interface you use for the rest of your configuration.</span></span> <span data-ttu-id="661ae-108">Приложения, использующие `AddAzureKeyVault`, должны иметь разрешения **Get** и **List** в отношении хранилища.</span><span class="sxs-lookup"><span data-stu-id="661ae-108">Apps that use `AddAzureKeyVault` require both **Get** and **List** permissions to the vault.</span></span>

> [!TIP]
> <span data-ttu-id="661ae-109">В отсутствие конкретной причины не прибегать к этому способу секреты можно загружать в память независимо от того, какую платформу или язык вы используете для создания своего приложения.</span><span class="sxs-lookup"><span data-stu-id="661ae-109">Regardless of the framework or language you use to build your app, load secrets into memory once at app startup unless you have a specific reason not to.</span></span> <span data-ttu-id="661ae-110">Считывание секретов из хранилища каждый раз, когда в них возникнет необходимость, отнимает слишком много времени и ресурсов.</span><span class="sxs-lookup"><span data-stu-id="661ae-110">Reading them directly from the vault every time you need them is unnecessarily slow and expensive.</span></span>

<span data-ttu-id="661ae-111">`AddAzureKeyVault` требует указать только имя хранилища, которое можно получить из локальной конфигурации приложения.</span><span class="sxs-lookup"><span data-stu-id="661ae-111">`AddAzureKeyVault` only requires the vault name as an input, which we'll get from our local app configuration.</span></span> <span data-ttu-id="661ae-112">Кроме того, он автоматически осуществляет проверку подлинности MSI &mdash; при использовании в приложении, развернутом в службе приложений Azure с включенным MSI, определяет службу токенов MSI и использует ее для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="661ae-112">It also automatically handles MSI authentication &mdash; when used in an app deployed to Azure App Service with MSI enabled, it will detect the MSI token service and use it to authenticate.</span></span> <span data-ttu-id="661ae-113">Этот способ подходит для большинства сценариев и включает все передовые методы — именно им мы воспользуемся в упражнении этого модуля.</span><span class="sxs-lookup"><span data-stu-id="661ae-113">It's a good fit for most scenarios and implements all best practices, and we'll use it in this unit's exercise.</span></span>

## <a name="handling-secrets-in-an-app"></a><span data-ttu-id="661ae-114">Обработка секретов в приложении</span><span class="sxs-lookup"><span data-stu-id="661ae-114">Handling secrets in an app</span></span>

<span data-ttu-id="661ae-115">После того как секрет будет загружен в приложение, именно от него будет зависеть безопасность его использования.</span><span class="sxs-lookup"><span data-stu-id="661ae-115">Once a secret is loaded into your app, it's up to your app to handle it securely.</span></span> <span data-ttu-id="661ae-116">В приложении, которое мы создадим в этом модуле, мы выведем значение секрета в ответ клиента и откроем его в веб-браузере, чтобы убедиться в том, что он успешно загружен.</span><span class="sxs-lookup"><span data-stu-id="661ae-116">In the app we build in this module, we write our secret value out to the client response and view it in a web browser to demonstrate that it has been loaded successfully.</span></span> <span data-ttu-id="661ae-117">**На практике значение секрета в клиент *не* передается!**</span><span class="sxs-lookup"><span data-stu-id="661ae-117">**Returning a secret value to the client is *not* something you'd normally do!**</span></span> <span data-ttu-id="661ae-118">Как правило, секреты используются для выполнения таких задач, как инициализация клиентских библиотек для баз данных или удаленных API.</span><span class="sxs-lookup"><span data-stu-id="661ae-118">Usually, you'll use secrets to do things like initialize client libraries for databases or remote APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="661ae-119">Всегда тщательно проверяйте свой код и следите за тем, чтобы ваше приложение не записывало секреты ни в какие выходные данные, включая журналы, хранилища и ответы.</span><span class="sxs-lookup"><span data-stu-id="661ae-119">Always carefully review your code to ensure that your app never writes secrets to any kind of output, including logs, storage, and responses.</span></span>

## <a name="exercise"></a><span data-ttu-id="661ae-120">Упражнение</span><span class="sxs-lookup"><span data-stu-id="661ae-120">Exercise</span></span>

<span data-ttu-id="661ae-121">Создадим новый веб-API ASP.NET Core и используем `AddAzureKeyVault`, чтобы загрузить секрет из хранилища.</span><span class="sxs-lookup"><span data-stu-id="661ae-121">We'll create a new ASP.NET Core web API and use `AddAzureKeyVault` to load the secret from our vault.</span></span>

### <a name="create-the-app"></a><span data-ttu-id="661ae-122">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="661ae-122">Create the app</span></span>

<span data-ttu-id="661ae-123">В терминале Azure Cloud Shell выполните указанную ниже команду, чтобы создать новый веб-API ASP.NET Core и открыть его в редакторе.</span><span class="sxs-lookup"><span data-stu-id="661ae-123">In the Azure Cloud Shell terminal, run the following to create a new ASP.NET Core web API application and open it in the editor.</span></span>

```console
dotnet new webapi -o KeyVaultDemoApp
cd KeyVaultDemoApp
code .
```

<span data-ttu-id="661ae-124">После того, как загрузится редактор, выполните в оболочке указанные ниже команды, чтобы добавить пакет NuGet, содержащий `AddAzureKeyVault`, и восстановить все зависимости приложения.</span><span class="sxs-lookup"><span data-stu-id="661ae-124">After the editor loads, run the following commands in the shell to add the NuGet package containing `AddAzureKeyVault` and restore all of the app's dependencies.</span></span>

```console
dotnet add package Microsoft.Extensions.Configuration.AzureKeyVault
dotnet restore
```

### <a name="add-code-to-load-and-use-secrets"></a><span data-ttu-id="661ae-125">Добавление кода для загрузки и использования секретов</span><span class="sxs-lookup"><span data-stu-id="661ae-125">Add code to load and use secrets</span></span>

<span data-ttu-id="661ae-126">Чтобы продемонстрировать надлежащее использование хранилища ключей, изменим наше приложение таким образом, чтобы секреты загружались из хранилища при запуске.</span><span class="sxs-lookup"><span data-stu-id="661ae-126">To demonstrate good usage of Key Vault, we will modify our app to load secrets from the vault at startup.</span></span> <span data-ttu-id="661ae-127">Также добавим новый контроллер с конечной точкой, которая получает из хранилища секрет **SecretPassword**.</span><span class="sxs-lookup"><span data-stu-id="661ae-127">We'll also add a new controller with an endpoint that gets our **SecretPassword** secret from the vault.</span></span>

<span data-ttu-id="661ae-128">Для начала запустим приложение: откройте `Program.cs`, удалите содержимое и замените его на следующий код:</span><span class="sxs-lookup"><span data-stu-id="661ae-128">First, the app startup: Open `Program.cs`, delete the contents and replace them with the following code:</span></span>

```csharp
using Microsoft.AspNetCore;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;

namespace KeyVaultDemoApp
{
    public class Program
    {
        public static void Main(string[] args)
        {
            CreateWebHostBuilder(args).Build().Run();
        }

        public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
            WebHost.CreateDefaultBuilder(args)
                .ConfigureAppConfiguration((context, config) =>
                {
                    // Build the current set of configuration to load values from
                    // JSON files and environment variables, including VaultName.
                    var builtConfig = config.Build();

                    // Use VaultName from the configuration to create the full vault URL.
                    var vaultUrl = $"https://{builtConfig["VaultName"]}.vault.azure.net/";

                    // Load all secrets from the vault into configuration. This will automatically
                    // authenticate to the vault using MSI. If MSI is not available, it will
                    // check if Visual Studio and/or the Azure CLI are installed locally and
                    // see if they are configured with credentials that can access the vault.
                    config.AddAzureKeyVault(vaultUrl);
                })
                .UseStartup<Startup>();
    }
}
```

> [!NOTE]
> <span data-ttu-id="661ae-129">Закончив редактирование, обязательно сохраните файлы с `Ctrl+S`.</span><span class="sxs-lookup"><span data-stu-id="661ae-129">Make sure to save files with `Ctrl+S` when you're done editing them.</span></span>

<span data-ttu-id="661ae-130">Единственное изменение по сравнению с начальным кодом — это добавление `ConfigureAppConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="661ae-130">The only change from the starter code is the addition of `ConfigureAppConfiguration`.</span></span> <span data-ttu-id="661ae-131">В него загружается имя хранилища из конфигурации и с его помощью вызывается `AddAzureKeyVault`.</span><span class="sxs-lookup"><span data-stu-id="661ae-131">This is where we load the vault name from configuration and call `AddAzureKeyVault` with it.</span></span>

<span data-ttu-id="661ae-132">Далее контроллер: создайте новый файл в папке `Controllers` с именем `SecretTestController.cs` и вставьте в него представленный ниже код.</span><span class="sxs-lookup"><span data-stu-id="661ae-132">Next, the controller: Create a new file in the `Controllers` folder called `SecretTestController.cs` and paste the following code into it.</span></span>

> [!NOTE]
> <span data-ttu-id="661ae-133">Чтобы создать новый файл, выполните в оболочке команду `touch`.</span><span class="sxs-lookup"><span data-stu-id="661ae-133">To create a new file, use the `touch` command in the shell.</span></span> <span data-ttu-id="661ae-134">В этом случае используйте `touch Controllers/SecretTestController.cs`.</span><span class="sxs-lookup"><span data-stu-id="661ae-134">In this case, use `touch Controllers/SecretTestController.cs`.</span></span> <span data-ttu-id="661ae-135">Чтобы увидеть его в редакторе, нажмите кнопку обновления на панели "Файлы".</span><span class="sxs-lookup"><span data-stu-id="661ae-135">You'll need to click the refresh button in the Files pane of the editor to see it there.</span></span>

```csharp
using System;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Configuration;

namespace KeyVaultDemoApp.Controllers
{
    [Route("api/[controller]")]
    public class SecretTestController : ControllerBase
    {
        private readonly IConfiguration _configuration;

        public SecretTestController(IConfiguration configuration)
        {
            _configuration = configuration;
        }

        [HttpGet]
        public IActionResult Get()
        {
            // Get the secret value from configuration. This can be done anywhere
            // we have access to IConfiguration. This does not call the Key Vault
            // API, because the secrets were loaded at startup.
            var secretName = "SecretPassword";
            var secretValue = _configuration[secretName];

            if (secretValue == null)
            {
                return StatusCode(
                    StatusCodes.Status500InternalServerError,
                    $"Error: No secret named {secretName} was found...");
            }
            else {
                return Content($"Secret value: {secretValue}" +
                    Environment.NewLine + Environment.NewLine +
                    "This is for testing only! Never output a secret " +
                    "to a response or anywhere else in a real app!");
            }
        }
    }
}
```

<span data-ttu-id="661ae-136">Выполните в оболочке команду `dotnet build`, чтобы убедиться в том, что компиляция прошла успешно.</span><span class="sxs-lookup"><span data-stu-id="661ae-136">Run `dotnet build` in the shell to make sure everything compiles.</span></span> <span data-ttu-id="661ae-137">Приложение готово для запуска &mdash; теперь перенесем его в Azure!</span><span class="sxs-lookup"><span data-stu-id="661ae-137">The app is ready to run &mdash; now let's get it into Azure!</span></span>