<!--TODO: explain Etag in knowledge needed-->
<!--TODO: Update to weave in the online retailer story-->


Данные хранятся в виде документов JSON в Azure Cosmos DB. [Документы](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) можно создавать, получать, заменять или удалять на портале, как показано в предыдущем модуле, или программными средствами, как описано в этом модуле. Azure Cosmos DB предоставляет клиентские пакеты SDK для .NET, .NET Core, Java, Node.js и Python, каждый из которых поддерживает эти операции. В этом модуле мы будем использовать пакет SDK для .NET Core для выполнения операций CRUD (создание, получение, обновление и удаление). 

Основные операции для документов Azure Cosmos DB являются частью класса [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet):
* [CreateDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentasync?view=azure-dotnet)
* [ReadDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentasync?view=azure-dotnet)
* [ReplaceDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.replacedocumentasync?view=azure-dotnet)
* [UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet). Upsert выполняет операцию создания или замены в зависимости от того, существует ли документ.
* [DeleteDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.deletedocumentasync?view=azure-dotnet)

Для выполнения любой из этих операций необходимо создать класс, представляющий объект, который хранится в базе данных. Так как мы работаем с базой данных пользователей, вам необходимо создать класс **User** для хранения основных данных, например имя и идентификатор пользователя (который является обязательным элементом, поскольку существует ключ раздела для горизонтального масштабирования), и подклассы для параметров доставки и истории заказов.

Когда вы создадите эти классы для представления пользователей, вы создадите новые документы пользователя для каждого экземпляра, а затем мы выполним некоторые простые операции CRUD с этими документами.

## <a name="create-documents"></a>Создание документов

1. Сначала создайте класс **User**, который представляет объекты для хранения в Azure Cosmos DB. Мы также создадим подклассы **OrderHistory** (история заказов) и **ShippingPreference** (параметры доставки), которые используются в классе **User**. Обратите внимание, документы должны иметь свойство **Id**, сериализуемое как **id** в файле JSON. 

    Чтобы создать эти классы, скопируйте и вставьте следующие классы **User**, **OrderHistory** и **ShippingPreference** под методом **BasicOperations**.

    <!--TODO: specify JSON for all of these? -->
    ```csharp
    public class User
    {
            [JsonProperty("id")]
            public string Id { get; set; }
            [JsonProperty("userId")]
            public string UserId { get; set; }
            [JsonProperty("lastName")]
            public string LastName { get; set; }
            [JsonProperty("firstName")]
            public string FirstName { get; set; }
            [JsonProperty("email")]
            public string Email { get; set; }
            [JsonProperty("dividend")]
            public string Dividend { get; set; }
            public OrderHistory[] OrderHistory { get; set; }
            public ShippingPreference[] ShippingPreference { get; set; }
            public CouponsUsed[] Coupons { get; set; }
            public override string ToString()
            {
            return JsonConvert.SerializeObject(this);
            }
    }
    
    public class OrderHistory
    {
            public string OrderId { get; set; }
            public string DateShipped { get; set; }
            public string Total { get; set; }
    }
    
    public class ShippingPreference
    {
            public int Priority { get; set; }
            public string AddressLine1 { get; set; }
            public string AddressLine2 { get; set; }
            public string City { get; set; }
            public string State { get; set; }
            public string ZipCode { get; set; }
            public string Country { get; set; }
    }
    
    public class CouponsUsed
    {
            public string CouponCode { get; set; }
    
    }
    
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }
    ```

2. В окне интегрированного терминала введите следующую команду, чтобы запустить программу и убедиться, что она работает.

    ```csharp
    dotnet run
    ```

3. Теперь скопируйте и вставьте задачу **CreateUserDocumentIfNotExists** в классе **ShippingPreference**.

    ```csharp
    private async Task CreateUserDocumentIfNotExists(string databaseName, string collectionName, User user)
    {
            try
            {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey("user.userId") });
            this.WriteToConsoleAndPromptToContinue("Found {0}", user.Id);
            }
            catch (DocumentClientException de)
            {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                    await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), user);
                    this.WriteToConsoleAndPromptToContinue("Created User {0}", user.Id);
            }
            else
            {
                    throw;
            }
            }
    }
    ```

4. Затем добавьте следующий код в метод **BasicOperations**.

    ```csharp
     User yanhe = new User
                {
                    Id = "1",
                    UserId = "yanhe",
                    LastName = "He",
                    FirstName = "Yan",
                    Email = "yanhe@todo.com",
                    OrderHistory = new OrderHistory[]
            {
                new OrderHistory {
                    OrderId = "1000",
                    DateShipped = "08/17/2018",
                    Total = "52.49"
                }
            },
                    ShippingPreference = new ShippingPreference[]
            {
                    new ShippingPreference {
                            Priority = 1,
                            AddressLine1 = "90 W 8th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    }
            },
                };
    
                await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", yanhe);
    
                User nelapin = new User
                {
                    Id = "2",
                    UserId = "nelapin",
                    LastName = "Pindakova",
                    FirstName = "Nela",
                    Email = "nelapin@todo.com",
                    Dividend = "8.50",
                    OrderHistory = new OrderHistory[]
            {
                new OrderHistory {
                    OrderId = "1001",
                    DateShipped = "08/17/2018",
                    Total = "105.89"
                }
            },
                    ShippingPreference = new ShippingPreference[]
            {
                    new ShippingPreference {
                            Priority = 1,
                            AddressLine1 = "505 NW 5th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    },
                    new ShippingPreference {
                            Priority = 2,
                            AddressLine1 = "505 NW 5th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    }
            },
                    Coupons = new CouponsUsed[]
             {
                 new CouponsUsed{
                     CouponCode = "Fall2018"
                 }
             }
                };
    
                await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);
    ```

5. В окне интегрированного терминала снова введите следующую команду, чтобы запустить программу и убедиться, что она работает.

    ```csharp
    dotnet run
    ```

    Терминал отображает следующие выходные данные, указывающее на то, что обе записи пользователя успешно созданы. 

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="read-documents"></a>Чтение документов

1. Для чтения документов из базы данных скопируйте следующий код и поместите его в конце файла Program.cs.

    ```csharp
    private async Task ReadUserDocument(string databaseName, string collectionName, User user)
    {
            try
            {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey("user.userId") });
            this.WriteToConsoleAndPromptToContinue("Found user {0}", user.Id);
            }
            catch (DocumentClientException de)
            {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not found", user.Id);
            }
            else
            {
                throw;
            }
            }
    }
    ```

2.  Скопируйте следующий код и вставьте его в конец метода **BasicOperations**, после строки `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`.

    ```csharp
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

4. Сохраните файл Program.cs и в окне интегрированного терминала выполните следующую команду.

    ```
    dotnet run
    ```
    Терминал отображает следующие выходные данные, где "Found user 1" означает, что документ найден.

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    Found user 1
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="replace-documents"></a>Замена документов
Azure Cosmos DB поддерживает замену документов JSON. В этом случае мы обновим запись пользователя, чтобы указать изменение фамилии.

1. Скопируйте и вставьте метод **ReplaceFamilyDocument** под кодом метода **CreateUserDocumentIfNotExists**.

    ```csharp
    private async Task ReplaceUserDocument(string databaseName, string collectionName, string LastName, User updatedUser)
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, LastName), updatedUser);
        this.WriteToConsoleAndPromptToContinue("Replaced last name for {0}", LastName);
    }
    ```

2. Скопируйте следующий код и вставьте его в конец метода **BasicOperations**, после строки `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`.

    ```csharp
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe.LastName, yanhe);
    ```
    <!--TODO: need to fix this as it's giving an error-->

4. Сохраните файл Program.cs и в окне интегрированного терминала выполните следующую команду.

    ```
    dotnet run
    ```
    Терминал отображает следующие выходные данные, где "Replaced last name for Suh" означает, что документ заменен.

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    Found user 1
    Press any key to continue ...
    Replaced last name for Suh 
    End of demo, press any key to exit.
    ```

## <a name="delete-documents"></a>Удаление документов

1. Скопируйте и вставьте метод **DeleteUserDocument** под кодом метода **ReplaceUserDocument**.
    
    ```csharp
    private async Task DeleteUserDocument(string databaseName, string collectionName, string documentName)
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName), new RequestOptions { PartitionKey = new PartitionKey("User.UserId") });
        Console.WriteLine("Deleted User {0}", documentName);
    }
    ```

2. Скопируйте и вставьте приведенный код в метод **BasicOperations** под кодом выполнения второго запроса.

    ```csharp
    await this.DeleteUserDocument("Users", "WebCustomers", "1");
    ```

3. Сохраните файл Program.cs и в окне интегрированного терминала выполните следующую команду.

    ```
    dotnet run
    ```

    Поздравляем! Вы успешно удалили документ Azure Cosmos DB.

## <a name="summary"></a>Сводка

В этом блоке вы создали, заменили и удалили документы в базе данных Azure Cosmos DB.