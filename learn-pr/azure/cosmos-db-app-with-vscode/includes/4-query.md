<span data-ttu-id="d00e7-101"><!--TODO: Explain how to do ExecuteNext (pages closer to SDK imp) vs ToList (continuation token)--> Итак, документы в приложении созданы, и мы можем запросить их из приложения.</span><span class="sxs-lookup"><span data-stu-id="d00e7-101"><!--TODO: Explain how to do ExecuteNext (pages closer to SDK imp) vs ToList (continuation token)--> Now that you've created documents in your application, let's query them from your application.</span></span> <span data-ttu-id="d00e7-102">Azure Cosmos DB использует запросы SQL и LINQ.</span><span class="sxs-lookup"><span data-stu-id="d00e7-102">Azure Cosmos DB uses SQL queries and LINQ queries.</span></span> <span data-ttu-id="d00e7-103">Запросы SQL и способы их выполнения на портале рассматриваются в модуле **Добавление данных и запрос данных в базе данных**.</span><span class="sxs-lookup"><span data-stu-id="d00e7-103">SQL queries and how to run them in the portal is discussed in the **Add data and query data in your database** module.</span></span> 

<span data-ttu-id="d00e7-104">Этот блок посвящен запуску запросов SQL и LINQ из приложения.</span><span class="sxs-lookup"><span data-stu-id="d00e7-104">So this unit focuses on running SQL queries and LINQ queries from your application.</span></span>

<span data-ttu-id="d00e7-105">Для тестирования этих запросов будут использоваться документы, созданные для интернет-магазина.</span><span class="sxs-lookup"><span data-stu-id="d00e7-105">We'll use the user documents you've created for your online retailer application to test these queries.</span></span>

## <a name="linq-query-basics"></a><span data-ttu-id="d00e7-106">Основы запросов LINQ</span><span class="sxs-lookup"><span data-stu-id="d00e7-106">LINQ query basics</span></span>

<span data-ttu-id="d00e7-107">LINQ является моделью программирования .NET, которая выражает вычисления в виде запросов потоков объектов.</span><span class="sxs-lookup"><span data-stu-id="d00e7-107">LINQ is a .NET programming model that expresses computations as queries on streams of objects.</span></span> <span data-ttu-id="d00e7-108">Вы можете создать объект **IQueryable**, который будет направлять запросы к службе Azure Cosmos DB, которая преобразует запросы LINQ в запросы Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d00e7-108">You can create an **IQueryable** object that directly queries Azure Cosmos DB, which translates the LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="d00e7-109">Затем запрос передается на сервер Azure Cosmos DB для получения набора результатов в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="d00e7-109">The query is then passed to the Azure Cosmos DB server to retrieve a set of results in JSON format.</span></span> <span data-ttu-id="d00e7-110">Возвращенные результаты десериализуются в поток объектов .NET на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="d00e7-110">The returned results are deserialized into a stream of .NET objects on the client side.</span></span> <span data-ttu-id="d00e7-111">Многие разработчики предпочитают запросы LINQ, так как они предоставляют единую согласованную модель программирования для работы с объектами в коде приложения и для выражения логики запросов в базе данных.</span><span class="sxs-lookup"><span data-stu-id="d00e7-111">Many developers prefer LINQ queries, as they provide a single consistent programming model across how they work with objects in application code and how they express query logic running in the database.</span></span>

<span data-ttu-id="d00e7-112">В следующей таблице показано преобразование запросов LINQ в SQL.</span><span class="sxs-lookup"><span data-stu-id="d00e7-112">The following table shows how LINQ queries are translated into SQL.</span></span>

| <span data-ttu-id="d00e7-113">Выражение LINQ</span><span class="sxs-lookup"><span data-stu-id="d00e7-113">LINQ expression</span></span> | <span data-ttu-id="d00e7-114">Преобразование в SQL</span><span class="sxs-lookup"><span data-stu-id="d00e7-114">SQL translation</span></span> |
|---|---|
| `input.Select(family => family.parents[0].familyName);`| `SELECT VALUE f.parents[0].familyName FROM Families f` |
|`input.Select(family => family.children[0].grade + c); // c is an int variable` | `SELECT VALUE f.children[0].grade + c FROM Families f` |
|`input.Select(family => new { name = family.children[0].familyName, grade = family.children[0].grade + 3});`| `SELECT VALUE {"name":f.children[0].familyName, "grade": f.children[0].grade + 3 } FROM Families f`|
|`input.Where(family=> family.parents[0].familyName == "Smith");`|`SELECT * FROM Families f WHERE f.parents[0].familyName = "Smith"`|

## <a name="run-sql-and-linq-queries"></a><span data-ttu-id="d00e7-115">Выполнение запросов SQL и LINQ</span><span class="sxs-lookup"><span data-stu-id="d00e7-115">Run SQL and LINQ queries</span></span>

1. <span data-ttu-id="d00e7-116">В следующем примере показано выполнение запроса в SQL, LINQ или лямбда-выражении LINQ в коде .NET.</span><span class="sxs-lookup"><span data-stu-id="d00e7-116">The following sample shows how a query could be performed in SQL, LINQ, or LINQ lambda from your .NET code.</span></span> <span data-ttu-id="d00e7-117">Скопируйте код и добавьте его после метода **DeleteUserDocument**.</span><span class="sxs-lookup"><span data-stu-id="d00e7-117">Copy the code and add it after your **DeleteUserDocument** method.</span></span>

    ```csharp
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };
    
            // Here we find the Andersen family via its LastName
            IQueryable<USer> userQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(u => u.LastName == "Sun");
    
            // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (User user in userQuery)
            {
                Console.WriteLine("\tRead {0}", user);
            }
    
            // Now execute the same query via direct SQL
            IQueryable<User> userQueryInSql = this.client.CreateDocumentQuery<User>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM User WHERE User.LastName = 'Sun'",
                    queryOptions);
    
            Console.WriteLine("Running direct SQL query...");
            foreach (User user in userQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", user);
            }
    
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }
    ```

2. <span data-ttu-id="d00e7-118">Скопируйте и вставьте следующий код в метод **BasicOperations** перед строкой `await this.DeleteUserDocument("Users", "WebCustomers", "1");`.</span><span class="sxs-lookup"><span data-stu-id="d00e7-118">Copy and paste the following code to your **BasicOperations** method, before the `await this.DeleteUserDocument("Users", "WebCustomers", "1");` line.</span></span>

    ```csharp
    this.ExecuteSimpleQuery("Users", "WebCustomers");
    ```

3. <span data-ttu-id="d00e7-119">Сохраните файл Program.cs и в окне интегрированного терминала выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d00e7-119">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>
    
    ```
    dotnet run
    ```

    <span data-ttu-id="d00e7-120">В консоли отображаются следующие выходные данные.</span><span class="sxs-lookup"><span data-stu-id="d00e7-120">The console displays the following output.</span></span>

    ```
    Running LINQ query...
    Running direct SQL query...
    Press any key to continue ...
    ```

    <span data-ttu-id="d00e7-121">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="d00e7-121">Congratulations!</span></span> <span data-ttu-id="d00e7-122">Вы успешно получили список пользователей Azure Cosmos DB с помощью запросов SQL и LINQ.</span><span class="sxs-lookup"><span data-stu-id="d00e7-122">You have successfully your Azure Cosmos DB collection of users by using SQL and LINQ queries.</span></span>

## <a name="summary"></a><span data-ttu-id="d00e7-123">Сводка</span><span class="sxs-lookup"><span data-stu-id="d00e7-123">Summary</span></span>

<span data-ttu-id="d00e7-124">В этом блоке вы узнали о запросах LINQ и добавили запросы LINQ и SQL в приложение для получения записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="d00e7-124">In this unit you learned about LINQ queries, and then added a LINQ and SQL query to your application to retrieve user records.</span></span>