<!--TODO: explain Etag in knowledge needed-->
<!--TODO: Update to weave in the online retailer story-->


<span data-ttu-id="c8cf0-101">Данные хранятся в виде документов JSON в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-101">Data is stored in JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="c8cf0-102">[Документы](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) можно создавать, получать, заменять или удалять на портале, как показано в предыдущем модуле, или программными средствами, как описано в этом модуле.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-102">[Documents](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) can be created, retrieved, replaced, or deleted in the portal, as shown in the previous module, or programmatically, as described in this module.</span></span> <span data-ttu-id="c8cf0-103">Azure Cosmos DB предоставляет клиентские пакеты SDK для .NET, .NET Core, Java, Node.js и Python, каждый из которых поддерживает эти операции.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-103">Azure Cosmos DB provides client-side SDKs for .NET, .NET Core, Java, Node.js, and Python, each of which supports these operations.</span></span> <span data-ttu-id="c8cf0-104">В этом модуле мы будем использовать пакет SDK для .NET Core для выполнения операций CRUD (создание, получение, обновление и удаление).</span><span class="sxs-lookup"><span data-stu-id="c8cf0-104">In this module we'll be using the .NET Core SDK to perform CRUD (create, retrieve, update, and delete) operations.</span></span> 

<span data-ttu-id="c8cf0-105">Основные операции для документов Azure Cosmos DB являются частью класса [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet):</span><span class="sxs-lookup"><span data-stu-id="c8cf0-105">The main operations for Azure Cosmos DB documents are part of the [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) class:</span></span>
* [<span data-ttu-id="c8cf0-106">CreateDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="c8cf0-106">CreateDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="c8cf0-107">ReadDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="c8cf0-107">ReadDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="c8cf0-108">ReplaceDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="c8cf0-108">ReplaceDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.replacedocumentasync?view=azure-dotnet)
* <span data-ttu-id="c8cf0-109">[UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="c8cf0-109">[UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet).</span></span> <span data-ttu-id="c8cf0-110">Upsert выполняет операцию создания или замены в зависимости от того, существует ли документ.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-110">Upsert performs a create or replace operation depending on whether the document already exists.</span></span>
* [<span data-ttu-id="c8cf0-111">DeleteDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="c8cf0-111">DeleteDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.deletedocumentasync?view=azure-dotnet)

<span data-ttu-id="c8cf0-112">Для выполнения любой из этих операций необходимо создать класс, представляющий объект, который хранится в базе данных.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-112">To perform any of these operations, you need to create a class that represents the object stored in the database.</span></span> <span data-ttu-id="c8cf0-113">Так как мы работаем с базой данных пользователей, вам необходимо создать класс **User** для хранения основных данных, например имя и идентификатор пользователя (который является обязательным элементом, поскольку существует ключ раздела для горизонтального масштабирования), и подклассы для параметров доставки и истории заказов.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-113">Because we're working with a database of users, you'll want to create a **User** class to store primary data such as their name and UserId (which is required, as that's the partition key to enable horizontal scaling) and subclasses for shipping preferences and order history.</span></span>

<span data-ttu-id="c8cf0-114">Когда вы создадите эти классы для представления пользователей, вы создадите новые документы пользователя для каждого экземпляра, а затем мы выполним некоторые простые операции CRUD с этими документами.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-114">Once you have those classes created to represent your users, you'll create new user documents for each instance, and then we'll perform some simple CRUD operations on the documents.</span></span>

## <a name="create-documents"></a><span data-ttu-id="c8cf0-115">Создание документов</span><span class="sxs-lookup"><span data-stu-id="c8cf0-115">Create documents</span></span>

1. <span data-ttu-id="c8cf0-116">Сначала создайте класс **User**, который представляет объекты для хранения в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-116">First, create a **User** class that represents the objects to store in Azure Cosmos DB.</span></span> <span data-ttu-id="c8cf0-117">Мы также создадим подклассы **OrderHistory** (история заказов) и **ShippingPreference** (параметры доставки), которые используются в классе **User**.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-117">We will also create **OrderHistory** and **ShippingPreference** subclasses that are used within **User**.</span></span> <span data-ttu-id="c8cf0-118">Обратите внимание, документы должны иметь свойство **Id**, сериализуемое как **id** в файле JSON.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-118">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> 

    <span data-ttu-id="c8cf0-119">Чтобы создать эти классы, скопируйте и вставьте следующие классы **User**, **OrderHistory** и **ShippingPreference** под методом **BasicOperations**.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-119">To create these classes, copy and paste the following **User**, **OrderHistory**, **ShippingPreference** classes underneath the **BasicOperations** method.</span></span>

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

2. <span data-ttu-id="c8cf0-120">В окне интегрированного терминала введите следующую команду, чтобы запустить программу и убедиться, что она работает.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-120">In the integrated terminal, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

3. <span data-ttu-id="c8cf0-121">Теперь скопируйте и вставьте задачу **CreateUserDocumentIfNotExists** в классе **ShippingPreference**.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-121">Now copy and paste the **CreateUserDocumentIfNotExists** task under the **ShippingPreference** class.</span></span>

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

4. <span data-ttu-id="c8cf0-122">Затем добавьте следующий код в метод **BasicOperations**.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-122">Then add the following to the **BasicOperations** method.</span></span>

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

5. <span data-ttu-id="c8cf0-123">В окне интегрированного терминала снова введите следующую команду, чтобы запустить программу и убедиться, что она работает.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-123">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

    <span data-ttu-id="c8cf0-124">Терминал отображает следующие выходные данные, указывающее на то, что обе записи пользователя успешно созданы.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-124">The terminal displays the following output, indicating that both user records were successfully created.</span></span> 

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="read-documents"></a><span data-ttu-id="c8cf0-125">Чтение документов</span><span class="sxs-lookup"><span data-stu-id="c8cf0-125">Read documents</span></span>

1. <span data-ttu-id="c8cf0-126">Для чтения документов из базы данных скопируйте следующий код и поместите его в конце файла Program.cs.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-126">To read documents from the database, copy in the following code and place it at the end of the Program.cs file.</span></span>

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

2.  <span data-ttu-id="c8cf0-127">Скопируйте следующий код и вставьте его в конец метода **BasicOperations**, после строки `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-127">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

4. <span data-ttu-id="c8cf0-128">Сохраните файл Program.cs и в окне интегрированного терминала выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-128">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```
    <span data-ttu-id="c8cf0-129">Терминал отображает следующие выходные данные, где "Found user 1" означает, что документ найден.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-129">The terminal displays the following output, where the output "Found user 1" indicates the document was found.</span></span>

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

## <a name="replace-documents"></a><span data-ttu-id="c8cf0-130">Замена документов</span><span class="sxs-lookup"><span data-stu-id="c8cf0-130">Replace documents</span></span>
<span data-ttu-id="c8cf0-131">Azure Cosmos DB поддерживает замену документов JSON.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-131">Azure Cosmos DB supports replacing JSON documents.</span></span> <span data-ttu-id="c8cf0-132">В этом случае мы обновим запись пользователя, чтобы указать изменение фамилии.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-132">In this case, we'll update a user record to account for a change to their last name.</span></span>

1. <span data-ttu-id="c8cf0-133">Скопируйте и вставьте метод **ReplaceFamilyDocument** под кодом метода **CreateUserDocumentIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-133">Copy and paste the **ReplaceFamilyDocument** method underneath your **CreateUserDocumentIfNotExists** method.</span></span>

    ```csharp
    private async Task ReplaceUserDocument(string databaseName, string collectionName, string LastName, User updatedUser)
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, LastName), updatedUser);
        this.WriteToConsoleAndPromptToContinue("Replaced last name for {0}", LastName);
    }
    ```

2. <span data-ttu-id="c8cf0-134">Скопируйте следующий код и вставьте его в конец метода **BasicOperations**, после строки `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-134">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe.LastName, yanhe);
    ```
    <!--TODO: need to fix this as it's giving an error-->

4. <span data-ttu-id="c8cf0-135">Сохраните файл Program.cs и в окне интегрированного терминала выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-135">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```
    <span data-ttu-id="c8cf0-136">Терминал отображает следующие выходные данные, где "Replaced last name for Suh" означает, что документ заменен.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-136">The terminal displays the following output, where the output "Replaced last name for Suh" indicates the document was replaced.</span></span>

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

## <a name="delete-documents"></a><span data-ttu-id="c8cf0-137">Удаление документов</span><span class="sxs-lookup"><span data-stu-id="c8cf0-137">Delete documents</span></span>

1. <span data-ttu-id="c8cf0-138">Скопируйте и вставьте метод **DeleteUserDocument** под кодом метода **ReplaceUserDocument**.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-138">Copy and paste the **DeleteUserDocument** method underneath your **ReplaceUserDocument** method.</span></span>
    
    ```csharp
    private async Task DeleteUserDocument(string databaseName, string collectionName, string documentName)
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName), new RequestOptions { PartitionKey = new PartitionKey("User.UserId") });
        Console.WriteLine("Deleted User {0}", documentName);
    }
    ```

2. <span data-ttu-id="c8cf0-139">Скопируйте и вставьте приведенный код в метод **BasicOperations** под кодом выполнения второго запроса.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-139">Copy and paste the following code to your **BasicOperations** method underneath the second query execution.</span></span>

    ```csharp
    await this.DeleteUserDocument("Users", "WebCustomers", "1");
    ```

3. <span data-ttu-id="c8cf0-140">Сохраните файл Program.cs и в окне интегрированного терминала выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-140">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```

    <span data-ttu-id="c8cf0-141">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="c8cf0-141">Congratulations!</span></span> <span data-ttu-id="c8cf0-142">Вы успешно удалили документ Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-142">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <a name="summary"></a><span data-ttu-id="c8cf0-143">Сводка</span><span class="sxs-lookup"><span data-stu-id="c8cf0-143">Summary</span></span>

<span data-ttu-id="c8cf0-144">В этом блоке вы создали, заменили и удалили документы в базе данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8cf0-144">In this unit you created, replaced, and deleted documents in your Azure Cosmos DB database.</span></span>