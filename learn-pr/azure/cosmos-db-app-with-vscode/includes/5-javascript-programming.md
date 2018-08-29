Часто требуется обновлять одновременно несколько документов в базе данных. В этом блоке рассматривается создание, регистрация и выполнение хранимых процедур из консольного приложения .NET.

## <a name="create-a-stored-procedure-in-your-app"></a>Создание хранимой процедуры в приложении

Эта хранимая процедура OrderId, которая содержит список всех позиций в заказе, используется для вычисления общей суммы заказа. Общая сумма заказов рассчитывается на основе суммы позиций в заказе за вычетом имеющихся у клиента дивидендов (кредитов) и с учетом кодов купонов.

1. Скопируйте следующий код и вставьте его в конец файла Program.cs.

    <!--TODO: Update sproc to take order total and check for available dividend, and use of summer coupon code, and provide updated total-->
    ```csharp
    private async Task UpdateOrderTotal(string databaseName, string collectionName, Order orderId)
    {
    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    
    
                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }
    
                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };
    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;
    
    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "ValidateDocumentAge"), document, 1920);
    }
    ```

2. Теперь скопируйте следующий код и вставьте его в конец метода **BasicOperations**.

    ```
    await this.UpdateOrderTotal("Users", "WebCustomers", "5-6235");
    ```

3. Сохраните файл Program.cs и в окне интегрированного терминала выполните следующую команду.

    ```
    dotnet run
    ```

    В консоли отображаются следующие выходные данные.

    ```
    Order total is 90.85.
    Press any key to continue ...
    ```

## <a name="clean-up"></a>Очистка

Если вы планируете продолжить работу с модулями в этом учебном курсе, пропустите процесс очистки либо выполните следующие действия по удалению ресурсов, чтобы с вас не взималась плата за использование службы.

1. На портале Azure выберите **Группа ресурсов** слева, а затем выберите созданную группу ресурсов.  

    Если меню слева свернуто, нажмите ![кнопку "Развернуть",](../media/5-javascript-programming/expand.png) чтобы развернуть его.

   ![Метрики на портале Azure](../media/5-javascript-programming/delete-resources-select.png)

2. В новом окне выберите группу ресурсов и щелкните **Удалить группу ресурсов**.

   ![Метрики на портале Azure](../media/5-javascript-programming/delete-resources.png)

3. В новом окне введите имя группы ресурсов, которую требуется удалить, и щелкните **Удалить**.

## <a name="summary"></a>Сводка

В этом модуле вы построили консольное приложение .NET Core, которое создает, обновляет и удаляет записи пользователей, запрашивает пользователей с помощью SQL и LINQ и выполняет хранимую процедуру для вычисления общей суммы заказа с учетом дивидендов и купонов пользователей.