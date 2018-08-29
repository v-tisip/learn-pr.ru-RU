В этом модуле вы создадите простое консольное приложение, используя интегрированный терминал, установите пакеты NuGet и будете использовать расширение Azure Cosmos DB для баз данных и коллекций, созданных в предыдущем модуле. Вы извлечете строку подключения Azure Cosmos DB из расширения и начнете разработку с использованием Azure Cosmos DB. 

## <a name="create-a-console-app"></a>Создание консольного приложения

1. Откройте Visual Studio Code и выберите **Файл** > **Открыть папку**.

2. Создайте новую папку с именем **learning-module**, где будет размещен новый проект C#, и нажмите **Выбрать папку**.

2. Откройте интегрированный терминал в Visual Studio Code, последовательно выбрав элементы **Вид** > **Интегрированный терминал** в главном меню.

3. В окне терминала введите **dotnet new console**.

    Эта команда создает файл **Program.cs** в вашей папке с простой уже написанной программой "Hello World", а также файл проекта C# с именем **learning-module.csproj**.

4. В окне терминала введите следующую команду для запуска программы "Hello World!". 

    ```
    dotnet run
    ```

    В окне терминала отображается "Hello world!" в качестве выходных данных.

## <a name="connect-the-app-to-azure-cosmos-db"></a>Подключение приложения к Azure Cosmos DB

1. Войдите в Azure — нажмите **Вид** > **Палитра команд** и введите **Azure: Sign In**.

    Следуйте инструкциям на экране, чтобы скопировать и вставить код, указанный в веб-браузере, который проверяет подлинность сеанса Visual Studio Code.

2. Нажмите ![значок обозревателя](../media/2-setup/visual-studio-code-explorer-icon.png) значок **обозревателя** в меню слева, а затем разверните **Azure Cosmos DB**.

3. Разверните свою подписку Azure > учетная запись Azure Cosmos DB. Если вы создали базу данных **Products** и коллекцию **Clothing** в предыдущем модуле, расширение отобразит их.

   ![Расширение Azure Cosmos DB Visual Studio Code](../media/2-setup/azure-cosmos-db-vs-code-extension.png) 

4. Теперь давайте создадим новую базу данных и коллекцию для ваших клиентов.

    В окне обозревателя щелкните правой кнопкой мыши учетную запись и нажмите **Создать базу данных**. 
    
    В текстовом поле в верхней части экрана введите **Users** (имя базы данных) > **Ввод** > **WebCustomers** (имя коллекции) >  **Ввод** > **userId** (ключ раздела) > **Ввод** > **1000** (начальная пропускная способность) > **Ввод**.

    ![Расширение Azure Cosmos DB Visual Studio Code](../media/2-setup/vs-code-azure-cosmos-db-extension.gif) <!--Retake on fresh machine without the other subscriptions showing-->

    В окне обозревателя отобразятся новая база данных Users и коллекция WebCustomers.

5. Во встроенном терминале запустите каждую из следующих команд в новой командной строке, чтобы установить необходимые пакеты NuGet.

    ```
    dotnet add package System.Net.Http
    dotnet add package Microsoft.Azure.DocumentDB.Core
    dotnet add package Newtonsoft.Json
    dotnet add package System.Threading.Tasks
    dotnet add package System.Linq
    dotnet add package Bogus
    dotnet restore
    ```

6. В верхней части панели обозревателя нажмите **Program.cs**, чтобы открыть файл.

7. Добавьте указанные ниже операторы using после `using System;`.

    ```csharp
    using System.Linq;
    using System.Threading.Tasks;
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;
    ```

8. Добавьте следующие две константы и переменную *client* в класс Program:

    ```csharp
    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;
    ```

    <!--TODO: Use more secure method-->

9. Скопируйте строку подключения из расширения Azure Cosmos DB, щелкнув правой кнопкой мыши учетную запись learning-module и нажав **Скопировать строку подключения**.

    ![Расширение Azure Cosmos DB Visual Studio Code](../media/2-setup/vs-code-copy-connection-string.gif) 

10. Вставьте строку подключения в текстовый файл, а затем скопируйте часть **AccountEndpoint** из текстового файла в **EndpointUrl** в файле Program.cs.

    AccountEndpoint будет выглядеть следующим образом:

    ```csharp
    private const string EndpointUrl = "https://<account name>.documents.azure.com:443/;
    ```

12. Теперь скопируйте значение **AccountKey** из текстового значения в значение **PrimaryKey** в файле Program.cs.

12. В окне интегрированного терминала введите следующую команду, чтобы запустить программу и убедиться, что она работает.

    ```csharp
    dotnet run
    ```

13. Добавьте новую асинхронную задачу для создания нового клиента и проверьте, существует ли база данных Users, добавив следующий метод после метода main.
    
    ```csharp
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });
    }
    ```

14. В окне интегрированного терминала снова введите следующую команду, чтобы запустить программу и убедиться, что она работает.

    ```csharp
    dotnet run
    ```

15. Скопируйте и вставьте следующий код в метод **Main**, заменив текущую строку `Console.WriteLine("Hello World!");`.

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

16. В окне интегрированного терминала снова введите следующую команду, чтобы запустить программу и убедиться, что она работает.

    ```csharp
    dotnet run
    ```

    В консоли отображаются следующие выходные данные.
    
    ```
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

## <a name="summary"></a>Сводка

В этом модуле вы создадите основу для приложения Azure Cosmos DB. Вы настроили среду разработки в Visual Studio Code, создали простой проект HelloWorld, подключили проект к конечной точке Azure Cosmos DB и проверили существование базы данных и коллекции.