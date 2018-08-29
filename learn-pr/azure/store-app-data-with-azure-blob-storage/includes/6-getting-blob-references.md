Для работы с отдельными BLOB-объектами в пакете SDK хранилища Azure для .NET Core требуется *BLOB-ссылка* &mdash; экземпляр объекта `ICloudBlob`.

Получить `ICloudBlob` можно путем его запроса по имени BLOB-объекта или выбора его из списка BLOB-объектов в контейнере. В обоих случаях требуется `CloudBlobContainer`, получение которого мы рассмотрели в последнем блоке.

## <a name="getting-blobs-by-name"></a>Получение BLOB-объектов по имени

Вызовите один из методов `GetXXXReference` в `CloudBlobContainer`, чтобы получить `ICloudBlob` по имени. Если вы знаете тип BLOB-объекта, отдайте предпочтение одному из более конкретных методов (`GetBlockBlobReference`, `GetAppendBlobReference` или `GetPageBlobReference`).

Ни один из этих методов не выполняет сетевой вызов и не проверяет, действительно ли BLOB-объект существует. Отдельный метод, `GetBlobReferenceFromServerAsync`, вызывает API хранилища BLOB-объектов и выдает исключение, если BLOB-объект еще не существует.

## <a name="listing-blobs-in-a-container"></a>Перечисление BLOB-объектов в контейнере

Список BLOB-объектов в контейнере можно получить с помощью метода `CloudBlobContainer` `ListBlobsSegmentedAsync`. *Сегментированный* означает отдельные страницы возвращаемых результатов &mdash; один вызов `ListBlobsSegmentedAsync` не всегда возвращает все результаты на одной странице. Возможно, для просмотра всех страниц его придется вызвать несколько раз, используя `ContinuationToken`, который он возвращает. Это делает код для перечисления BLOB-объектов более сложным, чем код для их передачи или загрузки, однако для получения всех BLOB-объектов в контейнере можно использовать стандартную схему:

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

она будет вызывать `ListBlobsSegmentedAsync`, пока `continuationToken` не станет `null`, что будет означать окончание результатов.

### <a name="processing-list-results"></a>Обработка результатов перечисления

Объект, возвращенный из `ListBlobsSegmentedAsync`, содержит свойство `Results` типа `IEnumerable<IListBlobItem>`. `IListBlobItem` содержат несколько свойств контейнера BLOB-объектов и URL-адрес, но не включают методы передачи или загрузки. Это связано с тем, что в результаты могут входить объекты `CloudBlobDirectory`, которые представляют не отдельные BLOB-объекты, а виртуальные каталоги.

Если вас интересуют только отдельные BLOB-объекты, можно использовать для фильтрования результатов метод `OfType<>`. Вот несколько таких случаев.

```csharp
// Get all blobs
var allBlobs = resultSegment.Results.OfType<ICloudBlob>();

// Get only block blobs
var blockBlobs = resultSegment.Results.OfType<CloudBlockBlob();
```

Для использования `OfType<>` нужно добавить ссылку на пространство имен `System.Linq` (`using System.Linq;`).

## <a name="exercise"></a>Упражнение

Одна из функций нашего приложения требует получения списка BLOB-объектов из API. Для получения списка всех BLOB-объектов в контейнере мы будем использовать представленную выше схему. Обработав список, мы получим имя каждого BLOB-объекта.

Откройте файл `BlobStorage.cs` в редакторе и заполните `GetNames` следующим кодом:

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

Имена, возвращаемые этим методом, обрабатываются `FilesController` и превращаются в URL-адреса. После возвращения клиенту они отображаются как гиперссылки на странице.