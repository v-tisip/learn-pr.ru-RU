<span data-ttu-id="cd2c8-101">Ниже представлен типичный рабочий процесс для приложений, использующих хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-101">The following is the typical workflow for apps that use Azure Blob storage:</span></span>

1. <span data-ttu-id="cd2c8-102">**Получение конфигурации**. При запуске загружается конфигурация, например строка подключения с ключом учетной записи.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-102">**Retrieve configuration**: At startup, load the configuration, such as the connection string with the account key.</span></span> <span data-ttu-id="cd2c8-103">Это необходимо для проверки подлинности вызовов API.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-103">This is needed to authenticate API calls.</span></span>
1. <span data-ttu-id="cd2c8-104">**Инициализация клиента**. Клиентская библиотека службы хранилища Azure инициализируется с помощью строки подключения.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-104">**Initialize client**: Use the connection string to initialize the Azure Storage client library.</span></span> <span data-ttu-id="cd2c8-105">При этом создаются объекты, которые приложение будет использовать для работы с API хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-105">This creates the objects the app will use to work with the Blob storage API.</span></span>
1. <span data-ttu-id="cd2c8-106">**Использование**. С помощью клиентской библиотеки выполняются вызовы API для работы с контейнерами и BLOB-объектами.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-106">**Use**: Make API calls with the client library to operate on containers and blobs.</span></span>

## <a name="configure-your-connection-string"></a><span data-ttu-id="cd2c8-107">Настройка строки подключения</span><span class="sxs-lookup"><span data-stu-id="cd2c8-107">Configure your connection string</span></span>

<span data-ttu-id="cd2c8-108">Перед написанием кода вам потребуется строка подключения для используемой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-108">Before writing any code, you'll need the connection string for the storage account you will use.</span></span> 

<span data-ttu-id="cd2c8-109">Она включает в себя ваш ключ учетной записи.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-109">The connection string includes your account key.</span></span> <span data-ttu-id="cd2c8-110">Ключ учетной записи считается секретным и должен храниться в надежном месте.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-110">The account key is considered a secret and should be stored securely.</span></span> <span data-ttu-id="cd2c8-111">Мы будем хранить строку подключения в параметре приложения службы приложений.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-111">We will store the connection string in an App Service application setting.</span></span> <span data-ttu-id="cd2c8-112">Параметр приложения — надежное место для секретов приложения, но он не поддерживает локальную разработку и не способен решить все задачи.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-112">An application setting is a secure place for application secrets, but it does not support local development and is not a robust, end-to-end solution on its own.</span></span>

> [!WARNING]
> <span data-ttu-id="cd2c8-113">**Не включайте ключи учетных записей хранения в код или в незащищенные файлы конфигурации.**</span><span class="sxs-lookup"><span data-stu-id="cd2c8-113">**Do not place storage account keys in code or in unprotected configuration files.**</span></span> <span data-ttu-id="cd2c8-114">Ключ учетной записи предоставляет полный доступ к учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-114">Storage account keys enable full access to your storage account.</span></span> <span data-ttu-id="cd2c8-115">Его утечка может привести к неустранимым повреждениям и финансовым потерям.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-115">Leaking a key can result in unrecoverable damage and large bills.</span></span> <span data-ttu-id="cd2c8-116">Рекомендации по хранению ключей и действиям в случае их утечки см. в разделе "Дополнительные ресурсы" в конце этого модуля.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-116">See the Additional Resources section at the end of this module for storage guidance and advice about how to recover from a leaked key.</span></span>

## <a name="initialize-the-blob-storage-object-model"></a><span data-ttu-id="cd2c8-117">Инициализация объектной модели хранилища BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="cd2c8-117">Initialize the Blob storage object model</span></span>

<span data-ttu-id="cd2c8-118">В SDK службы хранилища Azure для .NET Core стандартная схема использования хранилища BLOB-объектов состоит из перечисленных ниже шагов.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-118">In the Azure Storage SDK for .NET Core, the standard pattern for using Blob storage consists of the following steps:</span></span>

1. <span data-ttu-id="cd2c8-119">Вызовите `CloudStorageAccount.Parse` (или `TryParse`) со строкой подключения, чтобы получить `CloudStorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-119">Call `CloudStorageAccount.Parse` (or `TryParse`) with your connection string to get a `CloudStorageAccount`.</span></span>
1. <span data-ttu-id="cd2c8-120">Вызовите метод `CreateCloudBlobClient` класса `CloudStorageAccount`, чтобы получить `CloudBlobClient`.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-120">Call `CreateCloudBlobClient` on the `CloudStorageAccount` to get a `CloudBlobClient`.</span></span>
1. <span data-ttu-id="cd2c8-121">Вызовите метод `GetContainerReference` класса `CloudBlobClient`, чтобы получить `CloudBlobContainer`.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-121">Call `GetContainerReference` on the `CloudBlobClient` to get a `CloudBlobContainer`.</span></span>
1. <span data-ttu-id="cd2c8-122">Используйте методы контейнера, чтобы получить список BLOB-объектов или ссылки на отдельные BLOB-объекты для отправки и скачивания данных.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-122">Use methods on the container to get a list of blobs and/or get references to individual blobs to upload and download data.</span></span>

<span data-ttu-id="cd2c8-123">В коде шаги 1&ndash;3 выглядят так:</span><span class="sxs-lookup"><span data-stu-id="cd2c8-123">In code, steps 1&ndash;3 look like this:</span></span>

```csharp
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); // or TryParse()
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference(containerName);
```

<span data-ttu-id="cd2c8-124">В этом коде инициализации вызовы по сети не совершаются.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-124">None of this initialization code makes calls over the network.</span></span> <span data-ttu-id="cd2c8-125">Это означает, что исключения из-за неправильных данных на этом этапе создаваться не будут. Например, вызов `GetContainerReference` будет выполнен успешно вне зависимости от того, существует ли контейнер в учетной записи.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-125">This means exceptions that occur from incorrect information won't be thrown until later; for example, the call to `GetContainerReference` will succeed whether or not the container actually exists in the account.</span></span>

## <a name="create-containers-at-startup"></a><span data-ttu-id="cd2c8-126">Создание контейнеров при запуске</span><span class="sxs-lookup"><span data-stu-id="cd2c8-126">Create containers at startup</span></span>

<span data-ttu-id="cd2c8-127">Как правило, контейнеры создаются приложениями в коде, даже если мы заранее знаем, какие контейнеры требуются.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-127">Common practice is for applications to create needed containers in code, even when we know what those containers will be up-front.</span></span> <span data-ttu-id="cd2c8-128">Лучше всего это делать с помощью вызова метода `CreateIfNotExistsAsync` класса `CloudBlobContainer`. С помощью этого метода следует создать каждый требуемый контейнер, прежде чем использовать его.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-128">Calling `CreateIfNotExistsAsync` on a `CloudBlobContainer` is the best way to do this, and we should use it to create each container we know we'll need before we use them.</span></span>

<span data-ttu-id="cd2c8-129">Метод `CreateIfNotExistsAsync` *выполняет* вызов службы хранилища Azure по сети.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-129">`CreateIfNotExistsAsync` *does* make a network call to Azure Storage.</span></span> <span data-ttu-id="cd2c8-130">Рекомендуется совершать этот вызов один раз при запуске, а не каждый раз при обращении к контейнеру.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-130">Best practice is to call it once at startup and not every time we access a container.</span></span>

## <a name="exercise"></a><span data-ttu-id="cd2c8-131">Упражнение</span><span class="sxs-lookup"><span data-stu-id="cd2c8-131">Exercise</span></span>

### <a name="clone-and-explore-the-unfinished-app"></a><span data-ttu-id="cd2c8-132">Клонирование и изучение незавершенного приложения</span><span class="sxs-lookup"><span data-stu-id="cd2c8-132">Clone and explore the unfinished app</span></span>

<span data-ttu-id="cd2c8-133">Сначала клонируем простейшее приложение из GitHub.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-133">First, let's clone the starter app from GitHub.</span></span> <span data-ttu-id="cd2c8-134">В терминале Cloud Shell выполните следующую команду, чтобы получить копию исходного кода и открыть ее в редакторе:</span><span class="sxs-lookup"><span data-stu-id="cd2c8-134">In the Cloud Shell terminal, run the following command to get a copy of the source code and open it in the editor:</span></span>

```console
git clone TODO
cd TODO
code .
```

<span data-ttu-id="cd2c8-135">Откройте файл `Controllers/FilesController.cs`.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-135">Open the file `Controllers/FilesController.cs`.</span></span>

<span data-ttu-id="cd2c8-136">Этот контроллер реализует интерфейс API с тремя действиями:</span><span class="sxs-lookup"><span data-stu-id="cd2c8-136">This controller implements an API with three actions:</span></span>

* <span data-ttu-id="cd2c8-137">**Index** (GET /api/Files) возвращает список URL-адресов, по одному для каждого отправленного файла.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-137">**Index** (GET /api/Files) returns a list of URLs, one for each file that's been uploaded.</span></span> <span data-ttu-id="cd2c8-138">Интерфейсная часть приложения вызывает этот метод для формирования списка гиперссылок на отправленные файлы.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-138">The app front end calls this method to build a list of hyperlinks to the uploaded files.</span></span>
* <span data-ttu-id="cd2c8-139">**Upload** (POST /api/Files) получает отправленный файл и сохраняет его.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-139">**Upload** (POST /api/Files) receives an uploaded file and saves it.</span></span>
* <span data-ttu-id="cd2c8-140">**Download** (GET /api/Files/{имя-файла}) скачивает отдельный файл по его имени.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-140">**Download** (GET /api/Files/{file-name}) downloads an individual file by its name.</span></span>

<span data-ttu-id="cd2c8-141">Для выполнения работы каждый метод вызывает экземпляр `IStorage` с именем `storage`.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-141">Each method uses an `IStorage` instance called `storage` to do its work.</span></span> <span data-ttu-id="cd2c8-142">В файле `Models/BlobStorage.cs` имеется неполная реализация `IStorage`.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-142">There is an incomplete implementation of `IStorage` in  `Models/BlobStorage.cs`.</span></span>

### <a name="add-the-nuget-package"></a><span data-ttu-id="cd2c8-143">Добавление пакета NuGet</span><span class="sxs-lookup"><span data-stu-id="cd2c8-143">Add the NuGet package</span></span>

<span data-ttu-id="cd2c8-144">Сначала добавьте ссылку на SDK службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-144">First, add a reference to the Azure Storage SDK.</span></span> <span data-ttu-id="cd2c8-145">В терминале выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="cd2c8-145">In the terminal, run the following:</span></span>

```console
dotnet add package WindowsAzure.Storage
dotnet restore
```

<span data-ttu-id="cd2c8-146">Таким образом гарантируется использование последней версии клиентской библиотеки хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-146">This will make sure we're using the newest version of the Blob storage client library.</span></span>

### <a name="configure"></a><span data-ttu-id="cd2c8-147">Настройка</span><span class="sxs-lookup"><span data-stu-id="cd2c8-147">Configure</span></span>

<span data-ttu-id="cd2c8-148">Наше простейшее приложение уже включает в себя необходимые конфигурационные данные.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-148">Our starter app already includes the configuration plumbing we need.</span></span> <span data-ttu-id="cd2c8-149">Параметр конструктора `IOptions<AzureStorageConfig>` в `BlobStorage` имеет два свойства: строку подключения к учетной записи хранения и имя контейнера, в котором приложение будет хранить BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-149">The `IOptions<AzureStorageConfig>` constructor parameter in `BlobStorage` has two properties: the storage account connection string and the name of the container our app will store blobs in.</span></span> <span data-ttu-id="cd2c8-150">В методе `ConfigureServices` в файле `Startup.cs` есть код, загружающий значения из конфигурации при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-150">There is code in the `ConfigureServices` method of `Startup.cs` that loads the values from configuration when the app starts.</span></span>

<span data-ttu-id="cd2c8-151">В этом упражнении мы запустим приложение в Службе приложений Azure, поэтому позднее мы добавим значения конфигурации в параметры приложения службы приложений.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-151">In this exercise, we will run the app in Azure App Service, so we will add the configuration values to the App Service application settings later.</span></span> <span data-ttu-id="cd2c8-152">Пока же не требуется выполнять никаких действий, связанных с конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-152">For now, we don't need to do any work related to configuration.</span></span>

### <a name="initialize"></a><span data-ttu-id="cd2c8-153">Инициализация</span><span class="sxs-lookup"><span data-stu-id="cd2c8-153">Initialize</span></span>

<span data-ttu-id="cd2c8-154">Откройте `BlobStorage.cs`.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-154">Open `BlobStorage.cs`.</span></span>

<span data-ttu-id="cd2c8-155">Найдите метод `Initialize`.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-155">Location the `Initialize` method.</span></span> <span data-ttu-id="cd2c8-156">Наше приложение вызовет его при первом использовании.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-156">Our app will call this method when it's first used.</span></span> <span data-ttu-id="cd2c8-157">Если вам интересно, вы можете изучить `ConfigureServices` в файле `Startup.cs`, чтобы понять, как это делается.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-157">If you're curious, you can look at `ConfigureServices` in `Startup.cs` to see how this is done.</span></span> 

<span data-ttu-id="cd2c8-158">Именно в методе `Initialize` создается контейнер, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="cd2c8-158">`Initialize` is where we want to create our container if it doesn't already exist.</span></span> <span data-ttu-id="cd2c8-159">Заполните метод `Initialize` следующим кодом и сохраните результаты работы:</span><span class="sxs-lookup"><span data-stu-id="cd2c8-159">Fill in `Initialize` with the following code and save your work:</span></span>

```csharp
public Task Initialize()
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.CreateIfNotExistsAsync();
}
```