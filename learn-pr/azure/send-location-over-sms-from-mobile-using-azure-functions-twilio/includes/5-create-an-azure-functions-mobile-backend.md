На этом этапе приложение получает данные местоположения пользователя и готово к отправке в функцию Azure. В этом модуле вы создадите функцию Azure.

## <a name="create-an-azure-functions-project"></a>Создание проекта Функций Azure

1. Добавьте новый проект в решение `ImHere`, щелкнув правой кнопкой мыши решение и выбрав *Добавить-> Создать проект...*.

2. В дереве в левой части окна выберите *Visual C#-> Облако*, а затем выберите *Функции Azure* на панели в центре.

3. Назовите проект "ImHere.Functions" и нажмите **ОК**.

    ![Диалоговое окно "Добавление проекта"](../media-drafts/5-add-new-functions-project.png)

4. В диалоговом окне настройки **Создать проект** оставьте версию функций *Функции Azure v1 (.NET Framework)*. Выберите *Триггер Http*, оставьте в качестве учетной записи хранения *Эмулятор хранилища* и настройте права доступа *Анонимно*. Нажмите кнопку **ОК**.

    ![Диалоговое окно настройки проекта функции Azure](../media-drafts/5-configure-trigger.png)

Новый проект будет создан с функцией по умолчанию с именем `Function1`.

> Эта функция была создана с анонимным доступом. После публикации в Azure любой пользователь, знающий URL-адрес, сможет вызывать эту функцию. В реальной ситуации вы бы защитили функцию проверкой подлинности, например [Проверкой подлинности службы приложений Azure](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) или [Azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c).

## <a name="create-the-function"></a>Создание функции

Проект функций Azure создается с помощью одной функции триггера HTTP с именем `Function1`. Сама функция реализуется как статический метод `Run` в классе `Function1`.

1. Переименуйте файл в обозревателе решений с "Function1.cs" на "SendLocation.cs". Когда вам предложат переименовать все ссылки на элемент кода `Function1`, нажмите кнопку **Да**.

2. Измените имя функции в атрибуте на "SendLocation".

    ```cs
    [FunctionName("SendLocation")]
    ```

3. Удалите содержимое функции, кроме первой строки, которая записывает информационное сообщение в средство ведения журнала.

    ```cs
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                       TraceWriter log)
    {
        log.Info("C# HTTP trigger function processed a request.");
    }
    ```

## <a name="create-a-class-to-share-data-between-the-mobile-app-and-function"></a>Создание класса для обмена данными между мобильным приложением и функцией

Данные отправляются в функцию Azure в формате JSON. Мобильное приложение будет сериализовать данные в JSON, а функция будет десериализовывать их из JSON. Чтобы обеспечить согласованность данных между мобильным приложением и функцией, создайте новый проект, содержащий класс для хранения местоположения и номера телефона. На этот проект будут затем ссылаться функция и приложение.

1. Создайте новый проект в решении `ImHere`, щелкнув правой кнопкой мыши решение и выбрав *Добавить-> Создать проект...*.

2. В дереве в левой части окна выберите *Visual C#-> .NET Standard*, а затем выберите *Библиотека классов (.NET Standard)* на панели в центре.

3. Назовите проект "ImHere.Data" и нажмите **ОК**.

    ![Диалоговое окно "Добавление проекта"](../media-drafts/5-add-new-net-standard-project.png)

4. Удалите автоматически созданный файл "Class1.cs".

5. Создайте класс в проекте `ImHere.Data` с именем `PostData`, щелкнув правой кнопкой мыши проект, а затем выбрав *Добавить -> Класс...*. Назовите новый класс "PostData" и нажмите кнопку **ОК**.

6. Добавьте свойства `double` для широты и долготы, а также свойство `string[]` для номеров телефонов, куда будут отправляться сообщения.

    ```cs
    public class PostData
    {
        public double Latitude { get; set; }
        public double Longitude { get; set; }
        public string[] ToNumbers { get; set; }
    }
    ```

7. Добавьте ссылку на этот проект в проекты `ImHere.Functions` и `ImHere`, щелкнув правой кнопкой мыши по проекту и выбрав *Добавить->Ссылка...* . Выберите *Проекты* из дерева в левой части окна и установите флажок для *ImHere.Data*.

    ![Настройка ссылок на проект](../media-drafts/5-configure-project-references.png)

## <a name="read-the-data-sent-to-the-function"></a>Чтение данных, отправленных в функцию

В функции Azure параметр `req` содержит отправленный HTTP-запрос, и данные внутри этого запроса будут представлены в виде сериализованного объекта JSON `PostData`.

1. Откройте класс `SendLocation` в проекте `ImHere.Functions`.

2. Прочитайте содержимое HTTP-запроса в объект `PostData`, добавив директиву using для пространства имен `ImHere.Data`.

    ```cs
    PostData data = await req.Content.ReadAsAsync<PostData>();
    ```

3. Создайте URL-адрес Google Maps, используя широту и долготу из `PostData`.

   ```cs
   string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
   ```

4. Запишите URL-адрес.

    ```cs
    log.Info($"URL created - {url}");
    ```

5. Верните код состояния 200, чтобы показать, что функция завершена без ошибок.

    ```cs
    return req.CreateResponse(HttpStatusCode.OK);
    ```

Полная функция приведена ниже.

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

## <a name="run-the-azure-function-locally"></a>Запуск функции Azure локально

Функции могут выполняться локально с помощью локальной учетной записи хранения и локальной среды выполнения функций Azure. Это локальная среда выполнения позволяет протестировать функцию перед ее развертыванием в Azure.

1. В обозревателе решений щелкните правой кнопкой мыши проект `ImHere.Functions` и выберите пункт *Назначить начальным проектом*.

2. В меню *Отладка* выберите *Запуск без отладки*. Локальная среда выполнения функций Azure откроется в окне консоли и запустит вашу функцию, ожидая передачи данных по доступному порту в `localhost`.

    ![Выполнение функции Azure локально](../media-drafts/5-function-running-locally.png)

3. Запишите порт, который использует функция. Он потребуется вам в следующем модуле для тестирования мобильного приложения. В приведенном выше рисунке функция прослушивает порт **7071**.

    ```sh
    Listening on http://localhost:7071/
    ```

4. Пусть функция работает, чтобы вы могли протестировать мобильное приложение в следующем модуле.

## <a name="summary"></a>Сводка

В этом модуле вы узнали, как создать проект функций Azure в Visual Studio, добавили общий проект с объектом данных, который будет совместно использоваться мобильным приложением и функцией, и научились создавать базовую реализацию функции для десериализации переданных данных. Вы также узнали, как запустить функцию Azure локально. В следующем модуле вы вызовете функцию Azure из мобильного приложения.