<span data-ttu-id="ee2ed-101">На этом этапе мобильное приложение готово и отправляет данные о местоположении и список номеров телефонов пользователя функции Azure, которая может десериализовать эти данные.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-101">At this point, the mobile app is complete and sends the user's location and list of phone numbers to an Azure function that can deserialize the data.</span></span> <span data-ttu-id="ee2ed-102">В этом модуле вы привяжете функцию Azure к Twilio для отправки SMS-сообщений.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-102">In this unit, you bind the Azure function to Twilio to send SMS messages.</span></span>

<span data-ttu-id="ee2ed-103">Функции Azure можно подключить к другим службам — службам в Azure или сторонним службам.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-103">Azure Functions can be connected to other services, either services in Azure or third-party services.</span></span> <span data-ttu-id="ee2ed-104">Эти подключения, называемые привязками, существуют в двух формах — входные и выходные привязки.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-104">These connections, called bindings, exist in two forms - input and output bindings.</span></span> <span data-ttu-id="ee2ed-105">Входные привязки предоставляют данные в функцию, а выходные получают данные из функции и отправляют их другой службе.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-105">Input bindings provide data to your function and output bindings take data from your function and send it to another service.</span></span> <span data-ttu-id="ee2ed-106">Дополнительные сведения читайте в [документации о привязках функций Azure](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).</span><span class="sxs-lookup"><span data-stu-id="ee2ed-106">You can read about bindings in the [Azure Functions Binding docs](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).</span></span>

<span data-ttu-id="ee2ed-107">Привязки для функций Azure, созданные в Visual Studio, определяются с помощью параметров функции, дополненных атрибутами.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-107">Bindings for Azure Functions created in Visual Studio are defined using parameters to the function, decorated with attributes.</span></span>

## <a name="bind-the-azure-function-to-twilio"></a><span data-ttu-id="ee2ed-108">Привязка функции Azure к Twilio</span><span class="sxs-lookup"><span data-stu-id="ee2ed-108">Bind the Azure function to Twilio</span></span>

<span data-ttu-id="ee2ed-109">Для отправки SMS сообщений через Twilio требуется выходная привязка, которая настраивается с помощью идентификатора подписки вашей учетной записи (идентификатор безопасности) и маркера проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-109">Sending SMS messages via Twilio requires an output binding that is configured with your account subscription ID (SID) and Auth Token.</span></span>

1. <span data-ttu-id="ee2ed-110">Если локальная среда выполнения функций Azure работает, остановите ее.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-110">Stop the local Azure Functions runtime if it's still running from the previous unit.</span></span>

2. <span data-ttu-id="ee2ed-111">Добавьте пакет "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet в проект `ImHere.Functions`.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-111">Add the "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet package to the `ImHere.Functions` project.</span></span> <span data-ttu-id="ee2ed-112">Этот пакет NuGet содержит соответствующие классы для привязки.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-112">This NuGet package contains the relevant classes for the binding.</span></span>

3. <span data-ttu-id="ee2ed-113">Добавьте новый параметр в статический метод `Run` в статическом классе `SendLocation` с именем `messages`.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-113">Add a new parameter to the static `Run` method on the `SendLocation` static class called `messages`.</span></span> <span data-ttu-id="ee2ed-114">Этот параметр имеет тип `ICollector<SMSMessage>`.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-114">This parameter will have a type of `ICollector<SMSMessage>`.</span></span> <span data-ttu-id="ee2ed-115">Вам потребуется добавить директиву using для пространства имен `Twilio`.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-115">You'll need to add a using directive for the `Twilio` namespace.</span></span>

    ```cs
    [FunctionName("SendLocation")]
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                      ICollector<SMSMessage> messages,
                                                      TraceWriter log)
    ```

4. <span data-ttu-id="ee2ed-116">Дополните новый параметр `messages` атрибутом `TwilioSms`.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-116">Decorate the new `messages` parameter with the `TwilioSms` attribute.</span></span> <span data-ttu-id="ee2ed-117">Этот атрибут имеет три параметра, которые необходимо задать.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-117">This attribute has three parameters you need to set.</span></span>

    | <span data-ttu-id="ee2ed-118">Параметр</span><span class="sxs-lookup"><span data-stu-id="ee2ed-118">Setting</span></span>      |  <span data-ttu-id="ee2ed-119">Значение</span><span class="sxs-lookup"><span data-stu-id="ee2ed-119">Value</span></span>   | <span data-ttu-id="ee2ed-120">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="ee2ed-120">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="ee2ed-121">**AccountSidSetting**</span><span class="sxs-lookup"><span data-stu-id="ee2ed-121">**AccountSidSetting**</span></span> | <span data-ttu-id="ee2ed-122">"TwilioAccountSid"</span><span class="sxs-lookup"><span data-stu-id="ee2ed-122">"TwilioAccountSid"</span></span> | <span data-ttu-id="ee2ed-123">Идентификатор безопасности вашей учетной записи в Twilio.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-123">The SID for your Twilio account.</span></span> <span data-ttu-id="ee2ed-124">Вместо того, чтобы задать идентификатор безопасности напрямую, этот параметр представляет собой имя значения в параметрах приложения-функции, которое будет использоваться для получения идентификатора безопасности.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-124">Rather than set the SID directly, this parameter is the name of a value in the function app settings that will be used to retrieve the SID.</span></span> |
    | <span data-ttu-id="ee2ed-125">**AuthTokenSetting**</span><span class="sxs-lookup"><span data-stu-id="ee2ed-125">**AuthTokenSetting**</span></span> | <span data-ttu-id="ee2ed-126">"TwilioAuthToken"</span><span class="sxs-lookup"><span data-stu-id="ee2ed-126">"TwilioAuthToken"</span></span> | <span data-ttu-id="ee2ed-127">Маркер проверки подлинности вашей учетной записи в Twilio.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-127">The Auth Token for your Twilio account.</span></span> <span data-ttu-id="ee2ed-128">Вместо того, чтобы задать маркер проверки подлинности напрямую, этот параметр представляет собой имя значения в параметрах приложения-функции, которое будет использоваться для получения маркера проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-128">Rather than set the Auth Token directly, this parameter is the name of a value in the function app settings that will be used to retrieve the Auth Token.</span></span> |
    | <span data-ttu-id="ee2ed-129">**from**</span><span class="sxs-lookup"><span data-stu-id="ee2ed-129">**From**</span></span> | <span data-ttu-id="ee2ed-130">Ваш номер телефона Twilio</span><span class="sxs-lookup"><span data-stu-id="ee2ed-130">Your Twilio phone number</span></span> | <span data-ttu-id="ee2ed-131">Номер телефона Twilio, на который будут отправляться SMS-сообщения, должен быть указан в международном формате (+\<код страны\>\<номер телефона\>, например +1555123456).</span><span class="sxs-lookup"><span data-stu-id="ee2ed-131">The Twilio phone number that the SMS messages will come from in international format (+\<country code\>\<phone number\>, for example "+1555123456").</span></span> |

    <span data-ttu-id="ee2ed-132">При создании учетной записи Twilio вам назначается номер телефона, с которого можно отправлять сообщения.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-132">When you create a Twilio account, you are assigned a phone number that you can send messages from.</span></span> <span data-ttu-id="ee2ed-133">Этот номер телефона в указан на панели **номеров телефонов** в Twilio.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-133">You can find this phone number on the Twilio **Phone Numbers** dashboard.</span></span> <span data-ttu-id="ee2ed-134">На сайте Twilio нажмите на многоточие в нижней части левого меню.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-134">From the Twilio site, select the ellipses at the bottom of the left-hand menu.</span></span> <span data-ttu-id="ee2ed-135">Выберите *СУПЕРСЕТЬ -> Номера телефонов*.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-135">Then, select *SUPER NETWORK->Phone Numbers*.</span></span> <span data-ttu-id="ee2ed-136">Вы можете закрепить эту панель мониторинга на левом меню, нажав на значок булавки.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-136">You can pin this dashboard to the left-hand menu using the pin icon.</span></span> <span data-ttu-id="ee2ed-137">Ваш номер Twilio будет находиться в разделе *Управление номерами -> Активные номера*.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-137">Your Twilio number will be under *Manage Numbers->Active Numbers*.</span></span> <span data-ttu-id="ee2ed-138">Номер должен быть указан без пробелов.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-138">You'll need to remove any spaces from the number.</span></span>

    ![Поиск номера Twilio](../media-drafts/7-twilio-find-number.png)

    ```cs
    [TwilioSms(AccountSidSetting = "TwilioAccountSid",
               AuthTokenSetting = "TwilioAuthToken",
               From = "+1xxxxxxxxx")]ICollector<SMSMessage> messages,
    ```

5. <span data-ttu-id="ee2ed-140">Параметры приложения-функции можно настроить локально внутри файла `local.settings.json`.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-140">Function app settings can be configured locally inside the `local.settings.json` file.</span></span> <span data-ttu-id="ee2ed-141">Добавьте идентификатор безопасности учетной записи Twilio и маркер проверки подлинности в этот файл JSON, используя имена параметров, которые были переданы атрибуту `TwilioSMS`.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-141">Add your Twilio account SID and Auth Token to this JSON file using the setting names that were passed to the `TwilioSMS` attribute.</span></span>

    ```json
    {
        "IsEncrypted": false,
        "Values": {
            "AzureWebJobsStorage": "UseDevelopmentStorage=true",
            "AzureWebJobsDashboard": "UseDevelopmentStorage=true",
            "TwilioAccountSid": "<Your SID>",
            "TwilioAuthToken": "<Your Auth Token>"
        }
    }
    ```

    <span data-ttu-id="ee2ed-142">Замените значения \<Ваш ИД безопасности\> и \<Ваш маркер проверки подлинности\> значениями с панели мониторинга Twilio.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-142">Replace \<Your SID\> and \<Your Auth Token\> with the values from your Twilio dashboard.</span></span>

    > <span data-ttu-id="ee2ed-143">Эти локальные параметры будут использоваться только для локального запуска.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-143">These local settings will be only for running locally.</span></span> <span data-ttu-id="ee2ed-144">В рабочем приложении в качестве этих значений будут использоваться ваши данные для входа в локальную учетную запись разработки или тестирования.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-144">In a production app, these value would be your local development or test account credentials.</span></span> <span data-ttu-id="ee2ed-145">Когда функция Azure будет развернута в Azure, вы сможете настроить рабочие значения.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-145">Once the Azure Function has been deployed to Azure, you'll be able to configure the production values.</span></span>
    > <span data-ttu-id="ee2ed-146">Если отправить код в систему управления версиями, эти локальные значения параметров приложения будут загружены тоже, так что не загружайте фактические значения в этих файлах, если ваш код имеет открытый источник или является общедоступным.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-146">If you check your code into source control, these local application setting values will be checked in, too, so be careful not to check in any actual values in these files if your code is open source or public in any form.</span></span>

## <a name="create-the-sms-messages"></a><span data-ttu-id="ee2ed-147">Создание SMS-сообщений</span><span class="sxs-lookup"><span data-stu-id="ee2ed-147">Create the SMS messages</span></span>

<span data-ttu-id="ee2ed-148">Параметр `ICollector<SMSMessage>` — это коллекция экземпляров `SMSMessage`. Он используется для сбора SMS-сообщений, которые вы хотите отправить.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-148">The `ICollector<SMSMessage>` parameter is a collection of `SMSMessage` instances and is used to collect the SMS messages you want to send.</span></span> <span data-ttu-id="ee2ed-149">После того как функция будет выполнена, любые экземпляры `SMSMessage`, добавленные в эту коллекцию, передаются в Twilio и рассылаются соответствующим получателям.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-149">After the function has finished running, any instances of `SMSMessage` added to this collection are passed to Twilio and sent to the relevant recipients.</span></span>

1. <span data-ttu-id="ee2ed-150">В функции `SendLocation` добавьте код для циклического прохождения через телефонные номера в `PostData` и создайте SMS-сообщение для каждого из них.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-150">In the `SendLocation` function, add code to loop through the phone numbers in the `PostData` and create an SMS message for each one.</span></span>

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        SMSMessage message = new SMSMessage
        {
            Body = $"I'm here! {url}",
            To = toNo
        };
    }
    ```

    <span data-ttu-id="ee2ed-151">Сообщению нужен номер телефона для отправки и текст, который содержит URL-адрес Google Maps, созданный на основе местоположения пользователя.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-151">The message needs the phone number to send to and a body that contains the Google Maps URL created from the user's location.</span></span>

2. <span data-ttu-id="ee2ed-152">Записывайте каждое сообщение и добавляйте его в коллекцию `messages`.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-152">Log each message, and then add it to the `messages` collection.</span></span>

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        ...
        log.Info($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    ```

<span data-ttu-id="ee2ed-153">Полный метод `SendLocation` приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-153">The complete `SendLocation` method is shown below.</span></span>

```cs
[FunctionName("SendLocation")]
public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                "get", "post",
                                                                Route = null)]HttpRequestMessage req,
                                                    [TwilioSms(AccountSidSetting = "TwilioAccountSid",
                                                                AuthTokenSetting = "TwilioAuthToken",
                                                                From = "<your Twilio phone number>")]ICollector<SMSMessage> messages,
                                                    TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");
    PostData data = await req.Content.ReadAsAsync<PostData>();
    string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
    log.Info($"URL created - {url}");
    foreach (string toNo in data.ToNumbers)
    {
        SMSMessage message = new SMSMessage
        {
            Body = $"I'm here! {url}",
            To = toNo
        };
        log.Info($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    return req.CreateResponse(HttpStatusCode.OK);
}
```

## <a name="test-it-out"></a><span data-ttu-id="ee2ed-154">Тестирование</span><span class="sxs-lookup"><span data-stu-id="ee2ed-154">Test it out</span></span>

1. <span data-ttu-id="ee2ed-155">Настройте приложение `ImHere.Functions` как начальный проект и запустите его без отладки.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-155">Set the `ImHere.Functions` app as the startup project and start it without debugging.</span></span>

2. <span data-ttu-id="ee2ed-156">Настройте приложение `ImHere.UWP` как начальный проект и запустите его.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-156">Set the `ImHere.UWP` app as the startup project and run it.</span></span>

3. <span data-ttu-id="ee2ed-157">Введите номер телефона в международном формате (+\<код страны\>\<номер телефона\>) в приложении Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-157">Enter your own phone number in international format (+\<country code\>\<phone number\>) into the Xamarin.Forms app.</span></span> <span data-ttu-id="ee2ed-158">Пробные учетные записи Twilio могут отправлять сообщения только на подтвержденные номера телефонов, поэтому сейчас вы сможете отправить сообщение только себе, если только не перейдете на платную учетную запись или не подтвердите другие номера.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-158">Twilio trial accounts can send  messages only to verified phone numbers, so for now, you'll only be able to message yourself unless you upgrade to a paid account or verify other numbers.</span></span>

4. <span data-ttu-id="ee2ed-159">Нажмите кнопку **Send Location** (Отправить данные о местоположении).</span><span class="sxs-lookup"><span data-stu-id="ee2ed-159">Click the **Send Location** button.</span></span> <span data-ttu-id="ee2ed-160">Если SMS-сообщение отправлено успешно, вы увидите сообщение в приложении Xamarin.Forms о том, что данные о местоположении успешно отправлены.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-160">If the SMS message was sent successfully, you'll see a message in the Xamarin.Forms app saying "Location sent successfully".</span></span>

    ![Приложение Xamarin.Forms, показывающее отправку данных о местоположении](../media-drafts/7-ui-location-sent.png)

5. <span data-ttu-id="ee2ed-162">В журналах консоли для функции Azure вы увидите, что сообщение создано и отправлено.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-162">In the console logs for the Azure function, you'll see the message being created and sent.</span></span> <span data-ttu-id="ee2ed-163">Если возникли ошибки (например, номер указан в неверном формате), они будут записаны здесь.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-163">If any errors occur (such as, the number is in the wrong format), they will be logged out here.</span></span>

    ![Консоль функции Azure, отображающая, что сообщение было отправлено](../media-drafts/7-function-message-sent.png)

6. <span data-ttu-id="ee2ed-165">Проверьте сообщение на телефоне.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-165">Check your phone for a message.</span></span> <span data-ttu-id="ee2ed-166">Перейдите по ссылке в сообщении, чтобы увидеть ваше местоположение.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-166">Follow the link in the message to see your location.</span></span>

    ![SMS-сообщение, полученное на мобильный телефон](../media-drafts/7-message-received.png)

## <a name="summary"></a><span data-ttu-id="ee2ed-168">Сводка</span><span class="sxs-lookup"><span data-stu-id="ee2ed-168">Summary</span></span>

<span data-ttu-id="ee2ed-169">В этом модуле вы узнали, как создать привязку Twilio для функции Azure и отправить SMS-сообщение с местоположением пользователя локально запущенной функции.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-169">In this unit, you learned how to create a Twilio binding for the Azure function and send an SMS message with the user's location to a function that was running locally.</span></span> <span data-ttu-id="ee2ed-170">В следующем модуле вы опубликуете функцию в Azure.</span><span class="sxs-lookup"><span data-stu-id="ee2ed-170">In the next unit, you publish the function to Azure.</span></span>