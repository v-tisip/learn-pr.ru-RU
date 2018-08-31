<span data-ttu-id="00d6b-101">На этом этапе приложение получает данные местоположения пользователя и готово к отправке в функцию Azure.</span><span class="sxs-lookup"><span data-stu-id="00d6b-101">At this point, the app is working to get the user's location and is ready to be sent to an Azure function.</span></span> <span data-ttu-id="00d6b-102">В этом модуле вы создадите функцию Azure.</span><span class="sxs-lookup"><span data-stu-id="00d6b-102">In this unit, you build the Azure function.</span></span>

## <a name="create-an-azure-functions-project"></a><span data-ttu-id="00d6b-103">Создание проекта Функций Azure</span><span class="sxs-lookup"><span data-stu-id="00d6b-103">Create an Azure Functions project</span></span>

1. <span data-ttu-id="00d6b-104">Добавьте новый проект в решение `ImHere`, щелкнув правой кнопкой мыши решение и выбрав *Добавить-> Создать проект...*.</span><span class="sxs-lookup"><span data-stu-id="00d6b-104">Add a new project to the `ImHere` solution by right-clicking on the solution and selecting *Add->New Project...*.</span></span>

2. <span data-ttu-id="00d6b-105">В дереве в левой части окна выберите *Visual C#-> Облако*, а затем выберите *Функции Azure* на панели в центре.</span><span class="sxs-lookup"><span data-stu-id="00d6b-105">From the tree on the left-hand side, select *Visual C#->Cloud*, and then select *Azure Functions* from the panel in the center.</span></span>

3. <span data-ttu-id="00d6b-106">Назовите проект "ImHere.Functions" и нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="00d6b-106">Name the project "ImHere.Functions", and then click **OK**.</span></span>

    ![Диалоговое окно "Добавление проекта"](../media-drafts/5-add-new-functions-project.png)

4. <span data-ttu-id="00d6b-108">В диалоговом окне настройки **Создать проект** оставьте версию функций *Функции Azure v1 (.NET Framework)*.</span><span class="sxs-lookup"><span data-stu-id="00d6b-108">In the **New Project** configuration dialog, leave the Functions version set to *Azure Functions v1 (.NET Framework)*.</span></span> <span data-ttu-id="00d6b-109">Выберите *Триггер Http*, оставьте в качестве учетной записи хранения *Эмулятор хранилища* и настройте права доступа *Анонимно*.</span><span class="sxs-lookup"><span data-stu-id="00d6b-109">Select *Http Trigger*, leave the storage account set to *Storage Emulator*, and set the access rights to *Anonymous*.</span></span> <span data-ttu-id="00d6b-110">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="00d6b-110">Then click **OK**.</span></span>

    ![Диалоговое окно настройки проекта функции Azure](../media-drafts/5-configure-trigger.png)

<span data-ttu-id="00d6b-112">Новый проект будет создан с функцией по умолчанию с именем `Function1`.</span><span class="sxs-lookup"><span data-stu-id="00d6b-112">The new project will be created and have a default function called `Function1`.</span></span>

> <span data-ttu-id="00d6b-113">Эта функция была создана с анонимным доступом.</span><span class="sxs-lookup"><span data-stu-id="00d6b-113">This function was created with anonymous access.</span></span> <span data-ttu-id="00d6b-114">После публикации в Azure любой пользователь, знающий URL-адрес, сможет вызывать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="00d6b-114">Once published to Azure, anybody who knows the URL will be able to call this function.</span></span> <span data-ttu-id="00d6b-115">В реальной ситуации вы бы защитили функцию проверкой подлинности, например [Проверкой подлинности службы приложений Azure](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) или [Azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c).</span><span class="sxs-lookup"><span data-stu-id="00d6b-115">In a real-world scenario, you would protect this with some form of authentication, such as [Azure App Service authentication](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) or [Azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c).</span></span>

## <a name="create-the-function"></a><span data-ttu-id="00d6b-116">Создание функции</span><span class="sxs-lookup"><span data-stu-id="00d6b-116">Create the function</span></span>

<span data-ttu-id="00d6b-117">Проект функций Azure создается с помощью одной функции триггера HTTP с именем `Function1`.</span><span class="sxs-lookup"><span data-stu-id="00d6b-117">The Azure Functions project is created with a single HTTP trigger function called `Function1`.</span></span> <span data-ttu-id="00d6b-118">Сама функция реализуется как статический метод `Run` в классе `Function1`.</span><span class="sxs-lookup"><span data-stu-id="00d6b-118">The function itself is implemented as a static `Run` method in the `Function1` class.</span></span>

1. <span data-ttu-id="00d6b-119">Переименуйте файл в обозревателе решений с "Function1.cs" на "SendLocation.cs".</span><span class="sxs-lookup"><span data-stu-id="00d6b-119">Rename the file in Solution Explorer from "Function1.cs" to "SendLocation.cs".</span></span> <span data-ttu-id="00d6b-120">Когда вам предложат переименовать все ссылки на элемент кода `Function1`, нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="00d6b-120">When prompted to rename all references to the code element `Function1`, click **Yes**.</span></span>

2. <span data-ttu-id="00d6b-121">Измените имя функции в атрибуте на "SendLocation".</span><span class="sxs-lookup"><span data-stu-id="00d6b-121">Rename the function name in the attribute to "SendLocation".</span></span>

    ```cs
    [FunctionName("SendLocation")]
    ```

3. <span data-ttu-id="00d6b-122">Удалите содержимое функции, кроме первой строки, которая записывает информационное сообщение в средство ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="00d6b-122">Delete the contents of the function, except the first line that writes an information message to the logger.</span></span>

    ```cs
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                       TraceWriter log)
    {
        log.Info("C# HTTP trigger function processed a request.");
    }
    ```

## <a name="create-a-class-to-share-data-between-the-mobile-app-and-function"></a><span data-ttu-id="00d6b-123">Создание класса для обмена данными между мобильным приложением и функцией</span><span class="sxs-lookup"><span data-stu-id="00d6b-123">Create a class to share data between the mobile app and function</span></span>

<span data-ttu-id="00d6b-124">Данные отправляются в функцию Azure в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="00d6b-124">When data is sent to the Azure function, it will be sent as JSON.</span></span> <span data-ttu-id="00d6b-125">Мобильное приложение будет сериализовать данные в JSON, а функция будет десериализовывать их из JSON.</span><span class="sxs-lookup"><span data-stu-id="00d6b-125">The mobile app will serialize data into JSON and the function will deserialize from JSON.</span></span> <span data-ttu-id="00d6b-126">Чтобы обеспечить согласованность данных между мобильным приложением и функцией, создайте новый проект, содержащий класс для хранения местоположения и номера телефона.</span><span class="sxs-lookup"><span data-stu-id="00d6b-126">To keep this data consistent between the mobile app and the function, create a new project that contains a class to hold the location and phone number data.</span></span> <span data-ttu-id="00d6b-127">На этот проект будут затем ссылаться функция и приложение.</span><span class="sxs-lookup"><span data-stu-id="00d6b-127">This project will then be referenced by the app and function.</span></span>

1. <span data-ttu-id="00d6b-128">Создайте новый проект в решении `ImHere`, щелкнув правой кнопкой мыши решение и выбрав *Добавить-> Создать проект...*.</span><span class="sxs-lookup"><span data-stu-id="00d6b-128">Create a new project under the `ImHere` solution by right-clicking on the solution and selecting *Add->New Project...*.</span></span>

2. <span data-ttu-id="00d6b-129">В дереве в левой части окна выберите *Visual C#-> .NET Standard*, а затем выберите *Библиотека классов (.NET Standard)* на панели в центре.</span><span class="sxs-lookup"><span data-stu-id="00d6b-129">From the tree on the left-hand side, select *Visual C#->.NET Standard*, and then select *Class Library (.NET Standard)* from the panel in the center.</span></span>

3. <span data-ttu-id="00d6b-130">Назовите проект "ImHere.Data" и нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="00d6b-130">Name the project "ImHere.Data", and then click **OK**.</span></span>

    ![Диалоговое окно "Добавление проекта"](../media-drafts/5-add-new-net-standard-project.png)

4. <span data-ttu-id="00d6b-132">Удалите автоматически созданный файл "Class1.cs".</span><span class="sxs-lookup"><span data-stu-id="00d6b-132">Delete the auto-generated "Class1.cs" file.</span></span>

5. <span data-ttu-id="00d6b-133">Создайте класс в проекте `ImHere.Data` с именем `PostData`, щелкнув правой кнопкой мыши проект, а затем выбрав *Добавить -> Класс...*. Назовите новый класс "PostData" и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="00d6b-133">Create a new class in the `ImHere.Data` project called `PostData` by right-clicking on the project and then selecting *Add->Class...*. Name the new class "PostData" and click **OK**.</span></span>

6. <span data-ttu-id="00d6b-134">Добавьте свойства `double` для широты и долготы, а также свойство `string[]` для номеров телефонов, куда будут отправляться сообщения.</span><span class="sxs-lookup"><span data-stu-id="00d6b-134">Add `double` properties for the latitude and longitude, as well as a `string[]` property for the phone numbers to send to.</span></span>

    ```cs
    public class PostData
    {
        public double Latitude { get; set; }
        public double Longitude { get; set; }
        public string[] ToNumbers { get; set; }
    }
    ```

7. <span data-ttu-id="00d6b-135">Добавьте ссылку на этот проект в проекты `ImHere.Functions` и `ImHere`, щелкнув правой кнопкой мыши по проекту и выбрав *Добавить->Ссылка...* . Выберите *Проекты* из дерева в левой части окна и установите флажок для *ImHere.Data*.</span><span class="sxs-lookup"><span data-stu-id="00d6b-135">Add a reference to this project to both the `ImHere.Functions` and `ImHere` projects by right-clicking on the project and then selecting *Add->Reference...*. Select *Projects* from the tree on the left-hand side, and then check the box next to *ImHere.Data*.</span></span>

    ![Настройка ссылок на проект](../media-drafts/5-configure-project-references.png)

## <a name="read-the-data-sent-to-the-function"></a><span data-ttu-id="00d6b-137">Чтение данных, отправленных в функцию</span><span class="sxs-lookup"><span data-stu-id="00d6b-137">Read the data sent to the function</span></span>

<span data-ttu-id="00d6b-138">В функции Azure параметр `req` содержит отправленный HTTP-запрос, и данные внутри этого запроса будут представлены в виде сериализованного объекта JSON `PostData`.</span><span class="sxs-lookup"><span data-stu-id="00d6b-138">In the Azure function, the `req` parameter contains the HTTP request that was made and the data inside this request will be a JSON serialized `PostData` object.</span></span>

1. <span data-ttu-id="00d6b-139">Откройте класс `SendLocation` в проекте `ImHere.Functions`.</span><span class="sxs-lookup"><span data-stu-id="00d6b-139">Open the `SendLocation` class in the `ImHere.Functions` project.</span></span>

2. <span data-ttu-id="00d6b-140">Прочитайте содержимое HTTP-запроса в объект `PostData`, добавив директиву using для пространства имен `ImHere.Data`.</span><span class="sxs-lookup"><span data-stu-id="00d6b-140">Read the contents of the HTTP request into a `PostData` object, adding a using directive for the `ImHere.Data` namespace.</span></span>

    ```cs
    PostData data = await req.Content.ReadAsAsync<PostData>();
    ```

3. <span data-ttu-id="00d6b-141">Создайте URL-адрес Google Maps, используя широту и долготу из `PostData`.</span><span class="sxs-lookup"><span data-stu-id="00d6b-141">Construct a Google Maps URL using the latitude and longitude from the `PostData`.</span></span>

   ```cs
   string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
   ```

4. <span data-ttu-id="00d6b-142">Запишите URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="00d6b-142">Log the URL.</span></span>

    ```cs
    log.Info($"URL created - {url}");
    ```

5. <span data-ttu-id="00d6b-143">Верните код состояния 200, чтобы показать, что функция завершена без ошибок.</span><span class="sxs-lookup"><span data-stu-id="00d6b-143">Return a 200 status code to show the function completed without error.</span></span>

    ```cs
    return req.CreateResponse(HttpStatusCode.OK);
    ```

<span data-ttu-id="00d6b-144">Полная функция приведена ниже.</span><span class="sxs-lookup"><span data-stu-id="00d6b-144">The complete function is shown below.</span></span>

```cs
public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                "get", "post",
                                                                Route = null)]HttpRequestMessage req,
                                                    TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");
    PostData data = await req.Content.ReadAsAsync<PostData>();
    string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
    log.Info($"URL created - {url}");
    return req.CreateResponse(HttpStatusCode.OK);
}
```

## <a name="run-the-azure-function-locally"></a><span data-ttu-id="00d6b-145">Запуск функции Azure локально</span><span class="sxs-lookup"><span data-stu-id="00d6b-145">Run the Azure function locally</span></span>

<span data-ttu-id="00d6b-146">Функции могут выполняться локально с помощью локальной учетной записи хранения и локальной среды выполнения функций Azure.</span><span class="sxs-lookup"><span data-stu-id="00d6b-146">Functions can be run locally using a local storage account and local Azure Functions runtime.</span></span> <span data-ttu-id="00d6b-147">Это локальная среда выполнения позволяет протестировать функцию перед ее развертыванием в Azure.</span><span class="sxs-lookup"><span data-stu-id="00d6b-147">This local runtime allows you to test out your function before deploying it to Azure.</span></span>

1. <span data-ttu-id="00d6b-148">В обозревателе решений щелкните правой кнопкой мыши проект `ImHere.Functions` и выберите пункт *Назначить начальным проектом*.</span><span class="sxs-lookup"><span data-stu-id="00d6b-148">Right-click on the `ImHere.Functions` project in the solution explorer, and then select *Set as StartUp project*.</span></span>

2. <span data-ttu-id="00d6b-149">В меню *Отладка* выберите *Запуск без отладки*.</span><span class="sxs-lookup"><span data-stu-id="00d6b-149">From the *Debug* menu, select *Start Without Debugging*.</span></span> <span data-ttu-id="00d6b-150">Локальная среда выполнения функций Azure откроется в окне консоли и запустит вашу функцию, ожидая передачи данных по доступному порту в `localhost`.</span><span class="sxs-lookup"><span data-stu-id="00d6b-150">The local Azure Functions runtime will launch inside a console window and start your function, listening on an available port on `localhost`.</span></span>

    ![Выполнение функции Azure локально](../media-drafts/5-function-running-locally.png)

3. <span data-ttu-id="00d6b-152">Запишите порт, который использует функция.</span><span class="sxs-lookup"><span data-stu-id="00d6b-152">Take a note of the port that the function is listening on.</span></span> <span data-ttu-id="00d6b-153">Он потребуется вам в следующем модуле для тестирования мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="00d6b-153">You'll need this in the next unit to test out the mobile app.</span></span> <span data-ttu-id="00d6b-154">В приведенном выше рисунке функция прослушивает порт **7071**.</span><span class="sxs-lookup"><span data-stu-id="00d6b-154">In the image above, the function is listening on port **7071**.</span></span>

    ```sh
    Listening on http://localhost:7071/
    ```

4. <span data-ttu-id="00d6b-155">Пусть функция работает, чтобы вы могли протестировать мобильное приложение в следующем модуле.</span><span class="sxs-lookup"><span data-stu-id="00d6b-155">Leave the function running so that you can test the mobile app in the next unit.</span></span>

## <a name="summary"></a><span data-ttu-id="00d6b-156">Сводка</span><span class="sxs-lookup"><span data-stu-id="00d6b-156">Summary</span></span>

<span data-ttu-id="00d6b-157">В этом модуле вы узнали, как создать проект функций Azure в Visual Studio, добавили общий проект с объектом данных, который будет совместно использоваться мобильным приложением и функцией, и научились создавать базовую реализацию функции для десериализации переданных данных.</span><span class="sxs-lookup"><span data-stu-id="00d6b-157">In this unit, you learned how to create an Azure Functions project in Visual Studio, added a shared project with a data object to be shared between the mobile app and the function, and learned how to create a basic implementation of the function to deserialize the data passed in.</span></span> <span data-ttu-id="00d6b-158">Вы также узнали, как запустить функцию Azure локально.</span><span class="sxs-lookup"><span data-stu-id="00d6b-158">You also learned how to run an Azure function locally.</span></span> <span data-ttu-id="00d6b-159">В следующем модуле вы вызовете функцию Azure из мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="00d6b-159">In the next unit, you'll call the Azure function from the mobile app.</span></span>