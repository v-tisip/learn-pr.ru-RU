<span data-ttu-id="6c5cc-101">В этом модуле вы создадите простое консольное приложение, используя интегрированный терминал, установите пакеты NuGet и будете использовать расширение Azure Cosmos DB для баз данных и коллекций, созданных в предыдущем модуле.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-101">In this module you will create a simple console app using the integrated terminal, install NuGet packages, and use the Azure Cosmos DB extension to see databases and collections created in the previous module.</span></span> <span data-ttu-id="6c5cc-102">Вы извлечете строку подключения Azure Cosmos DB из расширения и начнете разработку с использованием Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-102">You'll retrieve your Azure Cosmos DB connection string from the extension, and then start developing against Azure Cosmos DB.</span></span> 

## <a name="create-a-console-app"></a><span data-ttu-id="6c5cc-103">Создание консольного приложения</span><span class="sxs-lookup"><span data-stu-id="6c5cc-103">Create a console app</span></span>

1. <span data-ttu-id="6c5cc-104">Откройте Visual Studio Code и выберите **Файл** > **Открыть папку**.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-104">Open Visual Studio Code, and then select **File** > **Open Folder**.</span></span>

2. <span data-ttu-id="6c5cc-105">Создайте новую папку с именем **learning-module**, где будет размещен новый проект C#, и нажмите **Выбрать папку**.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-105">Create a new folder named **learning-module** where you want your new C# project to be, and then click **Select Folder**.</span></span>

2. <span data-ttu-id="6c5cc-106">Откройте интегрированный терминал в Visual Studio Code, последовательно выбрав элементы **Вид** > **Интегрированный терминал** в главном меню.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-106">Open the integrated terminal from Visual Studio Code by selecting **View** > **Integrated Terminal** from the main menu.</span></span>

3. <span data-ttu-id="6c5cc-107">В окне терминала введите **dotnet new console**.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-107">In the terminal window, type **dotnet new console**.</span></span>

    <span data-ttu-id="6c5cc-108">Эта команда создает файл **Program.cs** в вашей папке с простой уже написанной программой "Hello World", а также файл проекта C# с именем **learning-module.csproj**.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-108">This command creates a **Program.cs** file in your folder with a simple "Hello World" program already written, along with a C# project file named **learning-module.csproj**.</span></span>

4. <span data-ttu-id="6c5cc-109">В окне терминала введите следующую команду для запуска программы "Hello World!".</span><span class="sxs-lookup"><span data-stu-id="6c5cc-109">In the terminal window, type the following command to run the "Hello World" program.</span></span> 

    ```
    dotnet run
    ```

    <span data-ttu-id="6c5cc-110">В окне терминала отображается "Hello world!"</span><span class="sxs-lookup"><span data-stu-id="6c5cc-110">The terminal window displays "Hello world!"</span></span> <span data-ttu-id="6c5cc-111">в качестве выходных данных.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-111">as output.</span></span>

## <a name="connect-the-app-to-azure-cosmos-db"></a><span data-ttu-id="6c5cc-112">Подключение приложения к Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6c5cc-112">Connect the app to Azure Cosmos DB</span></span>

1. <span data-ttu-id="6c5cc-113">Войдите в Azure — нажмите **Вид** > **Палитра команд** и введите **Azure: Sign In**.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-113">Sign in to Azure by clicking **View** > **Command Palette** and typing **Azure: Sign In**.</span></span>

    <span data-ttu-id="6c5cc-114">Следуйте инструкциям на экране, чтобы скопировать и вставить код, указанный в веб-браузере, который проверяет подлинность сеанса Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-114">Follow the prompts to copy and paste the code provided in the web browser, which authenticates your Visual Studio Code session.</span></span>

2. <span data-ttu-id="6c5cc-115">Нажмите ![значок обозревателя](../media/2-setup/visual-studio-code-explorer-icon.png) значок **обозревателя** в меню слева, а затем разверните **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-115">Click the ![Explorer icon](../media/2-setup/visual-studio-code-explorer-icon.png) **Explorer** icon on the left menu, and then expand **Azure Cosmos DB**.</span></span>

3. <span data-ttu-id="6c5cc-116">Разверните свою подписку Azure > учетная запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-116">Expand your Azure subscription > Azure Cosmos DB account.</span></span> <span data-ttu-id="6c5cc-117">Если вы создали базу данных **Products** и коллекцию **Clothing** в предыдущем модуле, расширение отобразит их.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-117">If you created the **Products** database and **Clothing** collection in the previous modules, the extension displays them.</span></span>

   ![Расширение Azure Cosmos DB Visual Studio Code](../media/2-setup/azure-cosmos-db-vs-code-extension.png) 

4. <span data-ttu-id="6c5cc-119">Теперь давайте создадим новую базу данных и коллекцию для ваших клиентов.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-119">Now let's create a new database and collection for your customers.</span></span>

    <span data-ttu-id="6c5cc-120">В окне обозревателя щелкните правой кнопкой мыши учетную запись и нажмите **Создать базу данных**.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-120">In the Explorer window, right-click your account, and then click **Create Database**.</span></span> 
    
    <span data-ttu-id="6c5cc-121">В текстовом поле в верхней части экрана введите **Users** (имя базы данных) > **Ввод** > **WebCustomers** (имя коллекции) >  **Ввод** > **userId** (ключ раздела) > **Ввод** > **1000** (начальная пропускная способность) > **Ввод**.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-121">In the text box at the top of the screen, type **Users** for the database name > **Enter** > **WebCustomers** for the collection name > **Enter** > **userId** for the partition key > **Enter** > **1000** for the initial throughput capacity > **Enter**.</span></span>

    <span data-ttu-id="6c5cc-122">![Расширение Azure Cosmos DB Visual Studio Code](../media/2-setup/vs-code-azure-cosmos-db-extension.gif) <!--Retake on fresh machine without the other subscriptions showing--></span><span class="sxs-lookup"><span data-stu-id="6c5cc-122">![Azure Cosmos DB Visual Studio Code extension](../media/2-setup/vs-code-azure-cosmos-db-extension.gif) <!--Retake on fresh machine without the other subscriptions showing--></span></span>

    <span data-ttu-id="6c5cc-123">В окне обозревателя отобразятся новая база данных Users и коллекция WebCustomers.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-123">The new Users database and WebCustomers collection are displayed in the Explorer window.</span></span>

5. <span data-ttu-id="6c5cc-124">Во встроенном терминале запустите каждую из следующих команд в новой командной строке, чтобы установить необходимые пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-124">In the integrated terminal, run each of the following commands at a new prompt to install the required NuGet packages.</span></span>

    ```
    dotnet add package System.Net.Http
    dotnet add package Microsoft.Azure.DocumentDB.Core
    dotnet add package Newtonsoft.Json
    dotnet add package System.Threading.Tasks
    dotnet add package System.Linq
    dotnet add package Bogus
    dotnet restore
    ```

6. <span data-ttu-id="6c5cc-125">В верхней части панели обозревателя нажмите **Program.cs**, чтобы открыть файл.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-125">At the top of the Explorer pane, click **Program.cs** to open the file.</span></span>

7. <span data-ttu-id="6c5cc-126">Добавьте указанные ниже операторы using после `using System;`.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-126">Add the following using statements after `using System;`.</span></span>

    ```csharp
    using System.Linq;
    using System.Threading.Tasks;
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;
    ```

8. <span data-ttu-id="6c5cc-127">Добавьте следующие две константы и переменную *client* в класс Program:</span><span class="sxs-lookup"><span data-stu-id="6c5cc-127">Add the following two constants and your *client* variable to the Program class:</span></span>

    ```csharp
    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;
    ```

    <!--TODO: Use more secure method-->

9. <span data-ttu-id="6c5cc-128">Скопируйте строку подключения из расширения Azure Cosmos DB, щелкнув правой кнопкой мыши учетную запись learning-module и нажав **Скопировать строку подключения**.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-128">Copy your connection string from the Azure Cosmos DB extension by right-clicking the learning-module account, and clicking **Copy Connection String**.</span></span>

    ![Расширение Azure Cosmos DB Visual Studio Code](../media/2-setup/vs-code-copy-connection-string.gif) 

10. <span data-ttu-id="6c5cc-130">Вставьте строку подключения в текстовый файл, а затем скопируйте часть **AccountEndpoint** из текстового файла в **EndpointUrl** в файле Program.cs.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-130">Paste the connection string into a text file, and then copy the **AccountEndpoint** portion from the text file into the **EndpointUrl** in Program.cs.</span></span>

    <span data-ttu-id="6c5cc-131">AccountEndpoint будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6c5cc-131">The AccountEndpoint should look like the following code:</span></span>

    ```csharp
    private const string EndpointUrl = "https://<account name>.documents.azure.com:443/;
    ```

12. <span data-ttu-id="6c5cc-132">Теперь скопируйте значение **AccountKey** из текстового значения в значение **PrimaryKey** в файле Program.cs.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-132">Now copy the **AccountKey** value from the text value into the **PrimaryKey** value in Program.cs.</span></span>

12. <span data-ttu-id="6c5cc-133">В окне интегрированного терминала введите следующую команду, чтобы запустить программу и убедиться, что она работает.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-133">In the integrated terminal, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

13. <span data-ttu-id="6c5cc-134">Добавьте новую асинхронную задачу для создания нового клиента и проверьте, существует ли база данных Users, добавив следующий метод после метода main.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-134">Add a new asynchronous task to create a new client, and check whether the Users database exists by adding the following method after the main method.</span></span>
    
    ```csharp
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });
    }
    ```

14. <span data-ttu-id="6c5cc-135">В окне интегрированного терминала снова введите следующую команду, чтобы запустить программу и убедиться, что она работает.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-135">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

15. <span data-ttu-id="6c5cc-136">Скопируйте и вставьте следующий код в метод **Main**, заменив текущую строку `Console.WriteLine("Hello World!");`.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-136">Copy and paste the following code into the **Main** method, overwriting the current `Console.WriteLine("Hello World!");` line.</span></span>

    ```csharp
    try
            {
                    Program p = new Program();
                    p.BasicOperations().Wait();
            }
            catch (DocumentClientException de)
            {
                    Exception baseException = de.GetBaseException();
                    Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
            }
            catch (Exception e)
            {
                    Exception baseException = e.GetBaseException();
                    Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
            }
            finally
            {
                    Console.WriteLine("End of demo, press any key to exit.");
                    Console.ReadKey();
            }
    ```

16. <span data-ttu-id="6c5cc-137">В окне интегрированного терминала снова введите следующую команду, чтобы запустить программу и убедиться, что она работает.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-137">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

    <span data-ttu-id="6c5cc-138">В консоли отображаются следующие выходные данные.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-138">The console displays the following output.</span></span>
    
    ```
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

## <a name="summary"></a><span data-ttu-id="6c5cc-139">Сводка</span><span class="sxs-lookup"><span data-stu-id="6c5cc-139">Summary</span></span>

<span data-ttu-id="6c5cc-140">В этом модуле вы создадите основу для приложения Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-140">In this module, you set up the groundwork for your Azure Cosmos DB application.</span></span> <span data-ttu-id="6c5cc-141">Вы настроили среду разработки в Visual Studio Code, создали простой проект HelloWorld, подключили проект к конечной точке Azure Cosmos DB и проверили существование базы данных и коллекции.</span><span class="sxs-lookup"><span data-stu-id="6c5cc-141">You set up your development environment in Visual Studio Code, created a simple HelloWorld project, connected the project to the Azure Cosmos DB endpoint, and ensured your database and collection exist.</span></span>