<span data-ttu-id="789f5-101">Часто требуется обновлять одновременно несколько документов в базе данных.</span><span class="sxs-lookup"><span data-stu-id="789f5-101">Multiple documents in your database frequently need to be updated at the same time.</span></span> <span data-ttu-id="789f5-102">В этом блоке рассматривается создание, регистрация и выполнение хранимых процедур из консольного приложения .NET.</span><span class="sxs-lookup"><span data-stu-id="789f5-102">This unit discusses how to create, register, and run stored procedures from your .NET console application.</span></span>

## <a name="create-a-stored-procedure-in-your-app"></a><span data-ttu-id="789f5-103">Создание хранимой процедуры в приложении</span><span class="sxs-lookup"><span data-stu-id="789f5-103">Create a stored procedure in your app</span></span>

<span data-ttu-id="789f5-104">Эта хранимая процедура OrderId, которая содержит список всех позиций в заказе, используется для вычисления общей суммы заказа.</span><span class="sxs-lookup"><span data-stu-id="789f5-104">In this stored procedure, the OrderId, which contains a list of all the items in the order, is used to calculate an order total.</span></span> <span data-ttu-id="789f5-105">Общая сумма заказов рассчитывается на основе суммы позиций в заказе за вычетом имеющихся у клиента дивидендов (кредитов) и с учетом кодов купонов.</span><span class="sxs-lookup"><span data-stu-id="789f5-105">The order total is calculated from the sum of the items in the order, less any dividend (credit) the customer has, and takes any coupon codes into account.</span></span>

1. <span data-ttu-id="789f5-106">Скопируйте следующий код и вставьте его в конец файла Program.cs.</span><span class="sxs-lookup"><span data-stu-id="789f5-106">Copy the following code and paste it into the end of the Program.cs file.</span></span>

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

2. <span data-ttu-id="789f5-107">Теперь скопируйте следующий код и вставьте его в конец метода **BasicOperations**.</span><span class="sxs-lookup"><span data-stu-id="789f5-107">Now copy the following code and paste it into the end of the **BasicOperations** method.</span></span>

    ```
    await this.UpdateOrderTotal("Users", "WebCustomers", "5-6235");
    ```

3. <span data-ttu-id="789f5-108">Сохраните файл Program.cs и в окне интегрированного терминала выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="789f5-108">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```

    <span data-ttu-id="789f5-109">В консоли отображаются следующие выходные данные.</span><span class="sxs-lookup"><span data-stu-id="789f5-109">The console displays the following output.</span></span>

    ```
    Order total is 90.85.
    Press any key to continue ...
    ```

## <a name="clean-up"></a><span data-ttu-id="789f5-110">Очистка</span><span class="sxs-lookup"><span data-stu-id="789f5-110">Clean up</span></span>

<span data-ttu-id="789f5-111">Если вы планируете продолжить работу с модулями в этом учебном курсе, пропустите процесс очистки либо выполните следующие действия по удалению ресурсов, чтобы с вас не взималась плата за использование службы.</span><span class="sxs-lookup"><span data-stu-id="789f5-111">If you plan to continue working on the modules in this learning path, skip the clean-up process, or else use the following steps to delete your resources to avoid incurring charges for use of the service.</span></span>

1. <span data-ttu-id="789f5-112">На портале Azure выберите **Группа ресурсов** слева, а затем выберите созданную группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="789f5-112">In the Azure portal, select **Resource groups** on the far left, and then select the resource group you created.</span></span>  

    <span data-ttu-id="789f5-113">Если меню слева свернуто, нажмите</span><span class="sxs-lookup"><span data-stu-id="789f5-113">If the left menu is collapsed, click</span></span> ![кнопку "Развернуть",](../media/5-javascript-programming/expand.png) <span data-ttu-id="789f5-115">чтобы развернуть его.</span><span class="sxs-lookup"><span data-stu-id="789f5-115">to expand it.</span></span>

   ![Метрики на портале Azure](../media/5-javascript-programming/delete-resources-select.png)

2. <span data-ttu-id="789f5-117">В новом окне выберите группу ресурсов и щелкните **Удалить группу ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="789f5-117">In the new window select the resource group, and then click **Delete resource group**.</span></span>

   ![Метрики на портале Azure](../media/5-javascript-programming/delete-resources.png)

3. <span data-ttu-id="789f5-119">В новом окне введите имя группы ресурсов, которую требуется удалить, и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="789f5-119">In the new window, type the name of the resource group to delete, and then click **Delete**.</span></span>

## <a name="summary"></a><span data-ttu-id="789f5-120">Сводка</span><span class="sxs-lookup"><span data-stu-id="789f5-120">Summary</span></span>

<span data-ttu-id="789f5-121">В этом модуле вы построили консольное приложение .NET Core, которое создает, обновляет и удаляет записи пользователей, запрашивает пользователей с помощью SQL и LINQ и выполняет хранимую процедуру для вычисления общей суммы заказа с учетом дивидендов и купонов пользователей.</span><span class="sxs-lookup"><span data-stu-id="789f5-121">In this module you've created a .NET Core console application that creates, updates, and deletes user records, queries the users by using SQL and LINQ, and runs a stored procedure to create an order total that takes the users dividends and coupons into account.</span></span>