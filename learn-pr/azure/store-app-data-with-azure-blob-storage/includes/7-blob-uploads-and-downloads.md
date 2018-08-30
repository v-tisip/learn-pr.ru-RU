<span data-ttu-id="5c8c1-101">Получив ссылку на BLOB-объект, можно отправлять и скачивать данные.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-101">Once we have a reference to a blob, we can upload and download data.</span></span> <span data-ttu-id="5c8c1-102">Объекты `ICloudBlob` имеют методы `Upload` и `Download`, которые поддерживают массивы байтов, потоки и файлы в качестве источников и целевых объектов.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-102">`ICloudBlob` objects have `Upload` and `Download` methods that support byte arrays, streams, and files as sources and targets.</span></span> <span data-ttu-id="5c8c1-103">Определенные типы имеют дополнительные методы, повышающие удобство работы. Например, `CloudBlockBlob` поддерживает отправку и скачивание строк с помощью методов `UploadTextAsync` и `DownloadTextAsync`.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-103">Specific types have additional methods for convenience &mdash; for example, `CloudBlockBlob` supports uploading and downloading strings with `UploadTextAsync` and `DownloadTextAsync`.</span></span>

## <a name="creating-new-blobs"></a><span data-ttu-id="5c8c1-104">Создание BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="5c8c1-104">Creating new blobs</span></span>

<span data-ttu-id="5c8c1-105">Чтобы создать BLOB-объект, нужно вызвать один из методов `Upload` для несуществующего BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-105">To create a new blob, you call one of the `Upload` methods on a blob that doesn't exist.</span></span> <span data-ttu-id="5c8c1-106">При этом выполняются два действия: создается BLOB-объект и отправляются данные.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-106">This does two things: creates the blob and uploads the data.</span></span> 

## <a name="moving-data-to-and-from-blobs"></a><span data-ttu-id="5c8c1-107">Перемещение данных в BLOB-объекты и из них</span><span class="sxs-lookup"><span data-stu-id="5c8c1-107">Moving data to and from blobs</span></span>

<span data-ttu-id="5c8c1-108">Перемещение данных в BLOB-объект или из него является сетевой операцией и требует времени.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-108">Moving data to and from a blob is a network operation that takes time.</span></span> <span data-ttu-id="5c8c1-109">В SDK службы хранилища Azure для .NET Core все методы, требующие сетевой активности, возвращают объекты `Task`, поэтому методы контроллера должны быть `async`, а для вызовов методов необходимо выполнять `await`, а не `Wait`.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-109">In the Azure Storage SDK for .NET Core, all methods that require network activity return `Task`s, so make sure your controller methods are `async` as appropriate and that you are `await`ing method calls and not `Wait`ing on them.</span></span>

<span data-ttu-id="5c8c1-110">При работе с большими объектами данных, как правило, рекомендуется использовать потоки вместо структур в памяти, таких как массивы байтов или строки.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-110">A common recommendation when working with large data objects is to use streams instead of in-memory structures like byte arrays or strings.</span></span> <span data-ttu-id="5c8c1-111">Это позволяет избежать буферизации всего содержимого в памяти перед его отправкой целевому объекту.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-111">This avoids buffering the full content in memory before sending it to the target.</span></span> <span data-ttu-id="5c8c1-112">ASP.NET Core поддерживает считывание потоков из запросов и ответов и запись потоков в них.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-112">ASP.NET Core supports reading and writing streams from requests and responses.</span></span>

## <a name="concurrent-access"></a><span data-ttu-id="5c8c1-113">Одновременный доступ</span><span class="sxs-lookup"><span data-stu-id="5c8c1-113">Concurrent access</span></span>

<span data-ttu-id="5c8c1-114">В процессе использования BLOB-объектов приложением другие процессы могут добавлять, изменять или удалять их.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-114">It is possible that other processes may be adding, changing, or deleting blobs as your app is using them.</span></span> <span data-ttu-id="5c8c1-115">При написании кода будьте внимательны и учитывайте проблемы, вызываемые параллелизмом, например возможность того, что BLOB-объект, из которого вы пытаетесь скачать данные, был удален или что содержимое BLOB-объектов может непредвиденно меняться.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-115">Always code defensively and think about problems caused by concurrency, such as blobs that are deleted right as you try to download from them, or blobs whose contents change when you don't expect them to.</span></span> <span data-ttu-id="5c8c1-116">Сведения об использовании AccessConditions и аренды BLOB-объектов для управления одновременным доступом к BLOB-объектам см. в разделе "Дополнительные ресурсы" в конце этого модуля.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-116">See the Additional Resources section at the end of this module for information about using AccessConditions and blob leases to manage concurrent blob access.</span></span>

## <a name="exercise"></a><span data-ttu-id="5c8c1-117">Упражнение</span><span class="sxs-lookup"><span data-stu-id="5c8c1-117">Exercise</span></span>

<span data-ttu-id="5c8c1-118">Давайте завершим приложение, добавив код для отправки и скачивания данных, а затем развернем его в Службе приложений Azure для тестирования.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-118">Let's finish our app by adding upload and download code, then deploy it to Azure App Service for testing.</span></span>

### <a name="upload"></a><span data-ttu-id="5c8c1-119">Передать</span><span class="sxs-lookup"><span data-stu-id="5c8c1-119">Upload</span></span>

<span data-ttu-id="5c8c1-120">Для отправки BLOB-объекта мы реализуем метод `BlobStorage.Save` с помощью `GetBlockBlobReference` для получения объекта `CloudBlockBlob` из контейнера.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-120">To upload a blob, we'll implement the `BlobStorage.Save` method using `GetBlockBlobReference` to get a `CloudBlockBlob` from the container.</span></span> <span data-ttu-id="5c8c1-121">`FilesController.Upload` передает файловый поток в метод `Save`, поэтому мы можем использовать `UploadFromStreamAsync` для выполнения отправки с максимальной эффективностью.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-121">`FilesController.Upload` passes the file stream to `Save`, so we can use `UploadFromStreamAsync` to perform the upload for maximum efficiency.</span></span>

<span data-ttu-id="5c8c1-122">Откройте файл `BlobStorage.cs` в редакторе и заполните реализацию метода `Save` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="5c8c1-122">Open `BlobStorage.cs` in the editor and fill in the `Save` implementation with the following code:</span></span>

```csharp
public Task Save(Stream fileStream, string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    CloudBlockBlob blockBlob = container.GetBlockBlobReference(name);
    return blockBlob.UploadFromStreamAsync(fileStream);
}
```

> [!NOTE]
> <span data-ttu-id="5c8c1-123">Приведенный здесь код отправки на основе потока работает эффективнее, чем считывание файла в массив байтов перед отправкой в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-123">The stream-based upload code shown here is more efficient than reading the file into a byte array before sending it to Azure Blob storage.</span></span> <span data-ttu-id="5c8c1-124">Однако использование `IFormFile` для получения файла от клиента не является потоковой реализацией в полном смысле этого слова и подходит для отправки только небольших файлов.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-124">However, the `IFormFile` technique we use to get the file from the client is not a true end-to-end streaming implementation and is only appropriate for handling uploads of small files.</span></span> <span data-ttu-id="5c8c1-125">Сведения об отправке файлов в полностью потоковом режиме см. в разделе "Дополнительные ресурсы" в конце этого модуля.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-125">See the Additional Resources section at the end of this module for information about fully streamed file uploads.</span></span>

### <a name="download"></a><span data-ttu-id="5c8c1-126">Загрузка</span><span class="sxs-lookup"><span data-stu-id="5c8c1-126">Download</span></span>

<span data-ttu-id="5c8c1-127">Метод `BlobStorage.Load` возвращает объект `Stream`. Это означает, что в коде не нужно физически перемещать байты из хранилища BLOB-объектов. Необходимо всего лишь вернуть ссылку на поток BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-127">`BlobStorage.Load` returns a `Stream`, meaning that our code doesn't need to physically move the bytes from Blob storage at all &mdash; we just need to return a reference to the blob stream.</span></span> <span data-ttu-id="5c8c1-128">Это можно сделать с помощью `OpenReadAsync`.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-128">We can do that with `OpenReadAsync`.</span></span> <span data-ttu-id="5c8c1-129">ASP.NET Core будет обрабатывать чтение и закрытие потока при создании ответа клиента.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-129">ASP.NET Core will handle reading and closing the stream when it builds the client response.</span></span>

<span data-ttu-id="5c8c1-130">Заполните метод `Load` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="5c8c1-130">Fill in `Load` with this code:</span></span>

```csharp
public Task<Stream> Load(string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.GetBlobReference(name).OpenReadAsync();
}
```

### <a name="deploy-and-run-in-azure"></a><span data-ttu-id="5c8c1-131">Развертывание и запуск в Azure</span><span class="sxs-lookup"><span data-stu-id="5c8c1-131">Deploy and run in Azure</span></span>

<span data-ttu-id="5c8c1-132">Наше приложение готово. Давайте развернем его и посмотрим, как оно работает.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-132">Our app is finished &mdash; let's deploy it and see it work.</span></span> <span data-ttu-id="5c8c1-133">В терминале Azure Cloud Shell выполните приведенный ниже код, чтобы выполнить сборку кода и развернуть его в новом экземпляре службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-133">Run the following code in the Azure Cloud Shell terminal to build our code and deploy it to a new App Service instance.</span></span> <span data-ttu-id="5c8c1-134">Кроме того, мы добавим в конфигурацию строку подключения к учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5c8c1-134">We also add our storage account connection string to configuration.</span></span>

```console

```

<span data-ttu-id="5c8c1-135">...</span><span class="sxs-lookup"><span data-stu-id="5c8c1-135">...</span></span>

<span data-ttu-id="5c8c1-136">Отправьте и скачайте файлы, чтобы протестировать приложение, а затем выполните в оболочке следующую команду, чтобы просмотреть отправленные BLOB-объекты:</span><span class="sxs-lookup"><span data-stu-id="5c8c1-136">Upload and download some files to test the app, then run the following in the shell to see the blobs that have been uploaded:</span></span>

```console

```

<span data-ttu-id="5c8c1-137">**Изображение списка задач с портала**</span><span class="sxs-lookup"><span data-stu-id="5c8c1-137">**TODO pic from portal**</span></span>