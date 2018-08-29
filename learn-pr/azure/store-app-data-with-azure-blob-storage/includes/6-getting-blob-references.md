<span data-ttu-id="e84c4-101">Для работы с отдельными BLOB-объектами в пакете SDK хранилища Azure для .NET Core требуется *BLOB-ссылка* &mdash; экземпляр объекта `ICloudBlob`.</span><span class="sxs-lookup"><span data-stu-id="e84c4-101">Working with an individual blob in the Azure Storage SDK for .NET Core requires a *blob reference* &mdash; an instance of an `ICloudBlob` object.</span></span>

<span data-ttu-id="e84c4-102">Получить `ICloudBlob` можно путем его запроса по имени BLOB-объекта или выбора его из списка BLOB-объектов в контейнере.</span><span class="sxs-lookup"><span data-stu-id="e84c4-102">You can get an `ICloudBlob` by requesting it with the blob's name or selecting it from a list of blobs in the container.</span></span> <span data-ttu-id="e84c4-103">В обоих случаях требуется `CloudBlobContainer`, получение которого мы рассмотрели в последнем блоке.</span><span class="sxs-lookup"><span data-stu-id="e84c4-103">Both require a `CloudBlobContainer`, which we saw how to get in the last unit.</span></span>

## <a name="getting-blobs-by-name"></a><span data-ttu-id="e84c4-104">Получение BLOB-объектов по имени</span><span class="sxs-lookup"><span data-stu-id="e84c4-104">Getting blobs by name</span></span>

<span data-ttu-id="e84c4-105">Вызовите один из методов `GetXXXReference` в `CloudBlobContainer`, чтобы получить `ICloudBlob` по имени.</span><span class="sxs-lookup"><span data-stu-id="e84c4-105">Call one of the `GetXXXReference` methods on a `CloudBlobContainer` to get an `ICloudBlob` by name.</span></span> <span data-ttu-id="e84c4-106">Если вы знаете тип BLOB-объекта, отдайте предпочтение одному из более конкретных методов (`GetBlockBlobReference`, `GetAppendBlobReference` или `GetPageBlobReference`).</span><span class="sxs-lookup"><span data-stu-id="e84c4-106">If you know the type of the blob you are retrieving, prefer using one of the more specific methods (`GetBlockBlobReference`, `GetAppendBlobReference`, or `GetPageBlobReference`).</span></span>

<span data-ttu-id="e84c4-107">Ни один из этих методов не выполняет сетевой вызов и не проверяет, действительно ли BLOB-объект существует.</span><span class="sxs-lookup"><span data-stu-id="e84c4-107">None of these methods make a network call, nor do they confirm whether or not the blob actually exists.</span></span> <span data-ttu-id="e84c4-108">Отдельный метод, `GetBlobReferenceFromServerAsync`, вызывает API хранилища BLOB-объектов и выдает исключение, если BLOB-объект еще не существует.</span><span class="sxs-lookup"><span data-stu-id="e84c4-108">A separate method, `GetBlobReferenceFromServerAsync`, does call the Blob storage API and will throw an exception if the blob doesn't already exist.</span></span>

## <a name="listing-blobs-in-a-container"></a><span data-ttu-id="e84c4-109">Перечисление BLOB-объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="e84c4-109">Listing blobs in a container</span></span>

<span data-ttu-id="e84c4-110">Список BLOB-объектов в контейнере можно получить с помощью метода `CloudBlobContainer` `ListBlobsSegmentedAsync`.</span><span class="sxs-lookup"><span data-stu-id="e84c4-110">You can get a list of the blobs in a container using `CloudBlobContainer`'s `ListBlobsSegmentedAsync` method.</span></span> <span data-ttu-id="e84c4-111">*Сегментированный* означает отдельные страницы возвращаемых результатов &mdash; один вызов `ListBlobsSegmentedAsync` не всегда возвращает все результаты на одной странице.</span><span class="sxs-lookup"><span data-stu-id="e84c4-111">*Segmented* refers to the separate pages of results returned &mdash; a single call to `ListBlobsSegmentedAsync` is never guaranteed to return all the results in a single page.</span></span> <span data-ttu-id="e84c4-112">Возможно, для просмотра всех страниц его придется вызвать несколько раз, используя `ContinuationToken`, который он возвращает.</span><span class="sxs-lookup"><span data-stu-id="e84c4-112">We may need to call it repeatedly using the `ContinuationToken` it returns to work our way through the pages.</span></span> <span data-ttu-id="e84c4-113">Это делает код для перечисления BLOB-объектов более сложным, чем код для их передачи или загрузки, однако для получения всех BLOB-объектов в контейнере можно использовать стандартную схему:</span><span class="sxs-lookup"><span data-stu-id="e84c4-113">This makes the code for listing blobs a little more complex than the code for uploading or downloading, but there's a standard pattern you can use to get every blob in a container:</span></span>

```csharp
BlobContinuationToken continuationToken = null;
BlobResultSegment resultSegment = null; 

do
{
    resultSegment = await container.ListBlobsSegmentedAsync(continuationToken);

    // Do work here on resultSegment.Results

    continuationToken = resultSegment.ContinuationToken;
} while (continuationToken != null);
```

<span data-ttu-id="e84c4-114">она будет вызывать `ListBlobsSegmentedAsync`, пока `continuationToken` не станет `null`, что будет означать окончание результатов.</span><span class="sxs-lookup"><span data-stu-id="e84c4-114">This will call `ListBlobsSegmentedAsync` repeatedly until `continuationToken` is `null`, which signals the end of the results.</span></span>

### <a name="processing-list-results"></a><span data-ttu-id="e84c4-115">Обработка результатов перечисления</span><span class="sxs-lookup"><span data-stu-id="e84c4-115">Processing list results</span></span>

<span data-ttu-id="e84c4-116">Объект, возвращенный из `ListBlobsSegmentedAsync`, содержит свойство `Results` типа `IEnumerable<IListBlobItem>`.</span><span class="sxs-lookup"><span data-stu-id="e84c4-116">The object you'll get back from `ListBlobsSegmentedAsync` contains a `Results` property of type `IEnumerable<IListBlobItem>`.</span></span> <span data-ttu-id="e84c4-117">`IListBlobItem` содержат несколько свойств контейнера BLOB-объектов и URL-адрес, но не включают методы передачи или загрузки.</span><span class="sxs-lookup"><span data-stu-id="e84c4-117">`IListBlobItem`s contain a handful of properties about the blob's container and URL, but no upload or download methods.</span></span> <span data-ttu-id="e84c4-118">Это связано с тем, что в результаты могут входить объекты `CloudBlobDirectory`, которые представляют не отдельные BLOB-объекты, а виртуальные каталоги.</span><span class="sxs-lookup"><span data-stu-id="e84c4-118">This is because some of the result objects may be `CloudBlobDirectory` objects that represent virtual directories rather than individual blobs.</span></span>

<span data-ttu-id="e84c4-119">Если вас интересуют только отдельные BLOB-объекты, можно использовать для фильтрования результатов метод `OfType<>`.</span><span class="sxs-lookup"><span data-stu-id="e84c4-119">If you are only interested in individual blobs, you can use the `OfType<>` method to filter the results.</span></span> <span data-ttu-id="e84c4-120">Вот несколько таких случаев.</span><span class="sxs-lookup"><span data-stu-id="e84c4-120">Here are a few examples:</span></span>

```csharp
// Get all blobs
var allBlobs = resultSegment.Results.OfType<ICloudBlob>();

// Get only block blobs
var blockBlobs = resultSegment.Results.OfType<CloudBlockBlob();
```

<span data-ttu-id="e84c4-121">Для использования `OfType<>` нужно добавить ссылку на пространство имен `System.Linq` (`using System.Linq;`).</span><span class="sxs-lookup"><span data-stu-id="e84c4-121">Using `OfType<>` will require a reference to the `System.Linq` namespace (`using System.Linq;`).</span></span>

## <a name="exercise"></a><span data-ttu-id="e84c4-122">Упражнение</span><span class="sxs-lookup"><span data-stu-id="e84c4-122">Exercise</span></span>

<span data-ttu-id="e84c4-123">Одна из функций нашего приложения требует получения списка BLOB-объектов из API.</span><span class="sxs-lookup"><span data-stu-id="e84c4-123">One of the features in our app requires getting a list of blobs from the API.</span></span> <span data-ttu-id="e84c4-124">Для получения списка всех BLOB-объектов в контейнере мы будем использовать представленную выше схему.</span><span class="sxs-lookup"><span data-stu-id="e84c4-124">We'll use the pattern shown above to list all the blobs in our container.</span></span> <span data-ttu-id="e84c4-125">Обработав список, мы получим имя каждого BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="e84c4-125">As we process the list, we get the name of each blob.</span></span>

<span data-ttu-id="e84c4-126">Откройте файл `BlobStorage.cs` в редакторе и заполните `GetNames` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="e84c4-126">Open `BlobStorage.cs` in the editor and fill in `GetNames` with the following code:</span></span>

```csharp
public async Task<IEnumerable<string>> GetNames()
{
    List<string> names = new List<string>();

    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);

    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    do
    {
        resultSegment = await container.ListBlobsSegmentedAsync(continuationToken);

        // Get the name of each blob.
        names.AddRange(resultSegment.Results.OfType<ICloudBlob>().Select(b => b.Name));

        continuationToken = resultSegment.ContinuationToken;
    } while (continuationToken != null);

    return names;
}
```

<span data-ttu-id="e84c4-127">Имена, возвращаемые этим методом, обрабатываются `FilesController` и превращаются в URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="e84c4-127">The names returned by this method are processed by `FilesController` to turn them into URLs.</span></span> <span data-ttu-id="e84c4-128">После возвращения клиенту они отображаются как гиперссылки на странице.</span><span class="sxs-lookup"><span data-stu-id="e84c4-128">When they are returned to the client, they are rendered as hyperlinks on the page.</span></span>