<!--TODO: Explain how to do ExecuteNext (pages closer to SDK imp) vs ToList (continuation token)--> Итак, документы в приложении созданы, и мы можем запросить их из приложения. Azure Cosmos DB использует запросы SQL и LINQ. Запросы SQL и способы их выполнения на портале рассматриваются в модуле **Добавление данных и запрос данных в базе данных**. 

Этот блок посвящен запуску запросов SQL и LINQ из приложения.

Для тестирования этих запросов будут использоваться документы, созданные для интернет-магазина.

## <a name="linq-query-basics"></a>Основы запросов LINQ

LINQ является моделью программирования .NET, которая выражает вычисления в виде запросов потоков объектов. Вы можете создать объект **IQueryable**, который будет направлять запросы к службе Azure Cosmos DB, которая преобразует запросы LINQ в запросы Cosmos DB. Затем запрос передается на сервер Azure Cosmos DB для получения набора результатов в формате JSON. Возвращенные результаты десериализуются в поток объектов .NET на стороне клиента. Многие разработчики предпочитают запросы LINQ, так как они предоставляют единую согласованную модель программирования для работы с объектами в коде приложения и для выражения логики запросов в базе данных.

В следующей таблице показано преобразование запросов LINQ в SQL.

| Выражение LINQ | Преобразование в SQL |
|---|---|
| `input.Select(family => family.parents[0].familyName);`| `SELECT VALUE f.parents[0].familyName FROM Families f` |
|`input.Select(family => family.children[0].grade + c); // c is an int variable` | `SELECT VALUE f.children[0].grade + c FROM Families f` |
|`input.Select(family => new { name = family.children[0].familyName, grade = family.children[0].grade + 3});`| `SELECT VALUE {"name":f.children[0].familyName, "grade": f.children[0].grade + 3 } FROM Families f`|
|`input.Where(family=> family.parents[0].familyName == "Smith");`|`SELECT * FROM Families f WHERE f.parents[0].familyName = "Smith"`|

## <a name="run-sql-and-linq-queries"></a>Выполнение запросов SQL и LINQ

1. В следующем примере показано выполнение запроса в SQL, LINQ или лямбда-выражении LINQ в коде .NET. Скопируйте код и добавьте его после метода **DeleteUserDocument**.

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

2. Скопируйте и вставьте следующий код в метод **BasicOperations** перед строкой `await this.DeleteUserDocument("Users", "WebCustomers", "1");`.

    ```csharp
    this.ExecuteSimpleQuery("Users", "WebCustomers");
    ```

3. Сохраните файл Program.cs и в окне интегрированного терминала выполните следующую команду.
    
    ```
    dotnet run
    ```

    В консоли отображаются следующие выходные данные.

    ```
    Running LINQ query...
    Running direct SQL query...
    Press any key to continue ...
    ```

    Поздравляем! Вы успешно получили список пользователей Azure Cosmos DB с помощью запросов SQL и LINQ.

## <a name="summary"></a>Сводка

В этом блоке вы узнали о запросах LINQ и добавили запросы LINQ и SQL в приложение для получения записей пользователей.