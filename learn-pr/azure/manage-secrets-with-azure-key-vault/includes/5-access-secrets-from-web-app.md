Теперь, когда вы знаете, как включение MSI создает для вашего приложения удостоверение для проверки подлинности, создадим приложение, которое будет использовать это удостоверение для доступа к секретам в хранилище.

## <a name="reading-secrets-in-an-aspnet-core-app"></a>Чтение секретов в приложении ASP.NET Core

API хранилища ключей Azure — это API REST, который обрабатывает все операции управления и использования ключей и хранилищ. Каждый секрет в хранилище имеет уникальный URL-адрес, а значения секретов извлекаются с помощью HTTP-запросов GET.

Официальной клиентской библиотекой хранилища ключей служит класс `KeyVaultClient` в пакете NuGet Microsoft.Azure.KeyVault. Использовать его напрямую, через &mdash; с помощью метода ASP.NET Core `AddAzureKeyVault`, необязательно; все секреты из хранилища можно загрузить в API конфигурации при запуске. Этот способ позволит вам получить доступ ко всем своим секретам по имени, используя тот же интерфейс `IConfiguration`, что и в остальной части конфигурации. Приложения, использующие `AddAzureKeyVault`, должны иметь разрешения **Get** и **List** в отношении хранилища.

> [!TIP]
> В отсутствие конкретной причины не прибегать к этому способу секреты можно загружать в память независимо от того, какую платформу или язык вы используете для создания своего приложения. Считывание секретов из хранилища каждый раз, когда в них возникнет необходимость, отнимает слишком много времени и ресурсов.

`AddAzureKeyVault` требует указать только имя хранилища, которое можно получить из локальной конфигурации приложения. Кроме того, он автоматически осуществляет проверку подлинности MSI &mdash; при использовании в приложении, развернутом в службе приложений Azure с включенным MSI, определяет службу токенов MSI и использует ее для проверки подлинности. Этот способ подходит для большинства сценариев и включает все передовые методы — именно им мы воспользуемся в упражнении этого модуля.

## <a name="handling-secrets-in-an-app"></a>Обработка секретов в приложении

После того как секрет будет загружен в приложение, именно от него будет зависеть безопасность его использования. В приложении, которое мы создадим в этом модуле, мы выведем значение секрета в ответ клиента и откроем его в веб-браузере, чтобы убедиться в том, что он успешно загружен. **На практике значение секрета в клиент *не* передается!** Как правило, секреты используются для выполнения таких задач, как инициализация клиентских библиотек для баз данных или удаленных API.

> [!IMPORTANT]
> Всегда тщательно проверяйте свой код и следите за тем, чтобы ваше приложение не записывало секреты ни в какие выходные данные, включая журналы, хранилища и ответы.

## <a name="exercise"></a>Упражнение

Создадим новый веб-API ASP.NET Core и используем `AddAzureKeyVault`, чтобы загрузить секрет из хранилища.

### <a name="create-the-app"></a>Создание приложения

В терминале Azure Cloud Shell выполните указанную ниже команду, чтобы создать новый веб-API ASP.NET Core и открыть его в редакторе.

```console
dotnet new webapi -o KeyVaultDemoApp
cd KeyVaultDemoApp
code .
```

После того, как загрузится редактор, выполните в оболочке указанные ниже команды, чтобы добавить пакет NuGet, содержащий `AddAzureKeyVault`, и восстановить все зависимости приложения.

```console
dotnet add package Microsoft.Extensions.Configuration.AzureKeyVault
dotnet restore
```

### <a name="add-code-to-load-and-use-secrets"></a>Добавление кода для загрузки и использования секретов

Чтобы продемонстрировать надлежащее использование хранилища ключей, изменим наше приложение таким образом, чтобы секреты загружались из хранилища при запуске. Также добавим новый контроллер с конечной точкой, которая получает из хранилища секрет **SecretPassword**.

Для начала запустим приложение: откройте `Program.cs`, удалите содержимое и замените его на следующий код:

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
> Закончив редактирование, обязательно сохраните файлы с `Ctrl+S`.

Единственное изменение по сравнению с начальным кодом — это добавление `ConfigureAppConfiguration`. В него загружается имя хранилища из конфигурации и с его помощью вызывается `AddAzureKeyVault`.

Далее контроллер: создайте новый файл в папке `Controllers` с именем `SecretTestController.cs` и вставьте в него представленный ниже код.

> [!NOTE]
> Чтобы создать новый файл, выполните в оболочке команду `touch`. В этом случае используйте `touch Controllers/SecretTestController.cs`. Чтобы увидеть его в редакторе, нажмите кнопку обновления на панели "Файлы".

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

Выполните в оболочке команду `dotnet build`, чтобы убедиться в том, что компиляция прошла успешно. Приложение готово для запуска &mdash; теперь перенесем его в Azure!