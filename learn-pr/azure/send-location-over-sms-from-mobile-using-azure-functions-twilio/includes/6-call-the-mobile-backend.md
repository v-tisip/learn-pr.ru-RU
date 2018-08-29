<span data-ttu-id="ecbeb-101">Вы запустили мобильное приложение и создали первоначальную версию функции Azure.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-101">The mobile app runs and the initial version of the Azure function has been created.</span></span> <span data-ttu-id="ecbeb-102">В этом блоке вы вызовете функцию Azure из мобильного приложения, передавая сведения о местоположении пользователя и список телефонных номеров, на которые следует отправлять SMS-сообщения.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-102">In this unit, you call the Azure function from the mobile app, passing in the user's location and the list of phone numbers the user wants to send SMS messages to.</span></span>

## <a name="calling-the-azure-function-from-the-mobile-app"></a><span data-ttu-id="ecbeb-103">Вызов функции Azure из мобильного приложения</span><span class="sxs-lookup"><span data-stu-id="ecbeb-103">Calling the Azure function from the mobile app</span></span>

1. <span data-ttu-id="ecbeb-104">Откройте `MainViewModel`.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-104">Open the `MainViewModel`.</span></span>

2. <span data-ttu-id="ecbeb-105">В этом классе добавьте закрытое поле `HttpClient` с именем `client`.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-105">In this class, add a private `HttpClient` field called `client`.</span></span> <span data-ttu-id="ecbeb-106">Потребуется добавить ссылку на пространство имен `System.Net.Http`.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-106">You'll need to add a reference to the `System.Net.Http` namespace.</span></span>

    ```cs
    HttpClient client = new HttpClient();
    ```

3. <span data-ttu-id="ecbeb-107">Добавьте поле константы для базового URL-адреса функции.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-107">Add a constant field for the base URL for the function.</span></span> <span data-ttu-id="ecbeb-108">В качестве значения задайте адрес, который прослушивает локальная среда выполнения функций Azure.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-108">Set this to the address that the local Azure Functions runtime is listening on.</span></span> <span data-ttu-id="ecbeb-109">После развертывания функции в Azure эту константу можно изменить на URL-адрес Azure.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-109">Once the function is deployed to Azure, this constant can be changed to be the Azure URL.</span></span>

    ```cs
    const string baseUrl = "http://localhost:7071";
    ```

4. <span data-ttu-id="ecbeb-110">После того как будет обнаружено местоположение, внутри метода `SendLocation` создайте экземпляр класса `PostData` с помощью сведений о местоположении и списка телефонных номеров, введенных пользователем.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-110">Inside the `SendLocation` method, after the location has been found, create a new instance of `PostData` using the location and the list of phone numbers entered by the user.</span></span> <span data-ttu-id="ecbeb-111">Вам потребуется добавить директиву using для пространства имен `ImHere.Data`.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-111">You'll need to add a using directive for the `ImHere.Data` namespace.</span></span>

    ```cs
    PostData postData = new PostData
    {
        Latitude = location.Latitude,
        Longitude = location.Longitude,
        ToNumbers = PhoneNumbers.Split('\n')
    };
    ```

    > <span data-ttu-id="ecbeb-112">Предполагается, что телефонные номера были введены в правильном формате по одному в строке в элементе управления `Editor`.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-112">This assumes that the phone numbers have been entered in the correct format, one per line in the `Editor` control.</span></span> <span data-ttu-id="ecbeb-113">В приложении для эксплуатации в производственной среде пришлось бы выполнить проверку на наличие одного или нескольких телефонных номеров в правильном формате.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-113">In a production-quality app, there would be validation around this to ensure one or more phone numbers were entered and were in the correct format.</span></span>

5. <span data-ttu-id="ecbeb-114">Самым простым способом сериализации `PostData` в формате JSON является использование пакета NuGet Newtonsoft.JSON.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-114">To serialize the `PostData` as JSON, the easiest way is to use the Newtonsoft.JSON NuGet package.</span></span> <span data-ttu-id="ecbeb-115">Добавьте этот пакет NuGet в проект `ImHere` так же, как вы добавили Xamarin.Essentials в предыдущих блоках.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-115">Add this NuGet package to the `ImHere` project in the same way that you added Xamarin.Essentials in an earlier unit.</span></span>

6. <span data-ttu-id="ecbeb-116">Сериализуйте `PostData` в `string` с помощью статического класса `JsonConvert`.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-116">Serialize the `PostData` to a `string` using the `JsonConvert` static class.</span></span> <span data-ttu-id="ecbeb-117">Вам потребуется добавить директиву using для пространства имен `Newtonsoft.Json`.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-117">You'll need to add a using directive for the `Newtonsoft.Json` namespace.</span></span> <span data-ttu-id="ecbeb-118">Закодируйте эту строку в класс `StringContent`, чтобы ее можно было передать в функцию Azure в виде JSON.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-118">Encode this string into a `StringContent` class so that it can be passed to the Azure function as JSON.</span></span>

    ```cs
    string data = JsonConvert.SerializeObject(postData);
    StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
    ```

7. <span data-ttu-id="ecbeb-119">Отправьте эти данные в функцию и получите результат.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-119">Post this data to the function and get the result back.</span></span>

   ```cs
    HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                        content);
   ```

   <span data-ttu-id="ecbeb-120">Доступ к функциям Azure осуществляется с помощью `/api/<function name>`, поэтому при условии, что для локальной среды выполнения функций выбран порт 7071, функция `SendLocation` будет доступна в `http://localhost:7071/api/SendLocation`.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-120">Azure functions are accessed using `/api/<function name>`, so assuming the port chosen by the local Functions runtime is 7071, the `SendLocation` function will be accessible at `http://localhost:7071/api/SendLocation`.</span></span>

8. <span data-ttu-id="ecbeb-121">В зависимости от результата в пользовательском интерфейсе отображается соответствующее сообщение.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-121">Depending on the result, show a message on the UI.</span></span>

    ```cs
    if (result.IsSuccessStatusCode)
        Message = "Location sent successfully";
    else
        Message = $"Error - {result.ReasonPhrase}";
    ```

<span data-ttu-id="ecbeb-122">Полный код для новых полей и метода `SendLocation` приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-122">The full code for the new fields and the `SendLocation` method is below.</span></span>

```cs
HttpClient client = new HttpClient();
const string baseUrl = "http://localhost:7071";

async Task SendLocation()
{
    Location location = await Geolocation.GetLastKnownLocationAsync();

    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";

        PostData postData = new PostData
        {
            Latitude = location.Latitude,
            Longitude = location.Longitude,
            ToNumbers = PhoneNumbers.Split('\n')
        };

        string data = JsonConvert.SerializeObject(postData);
        StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
        HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                            content);

        if (result.IsSuccessStatusCode)
            Message = "Location sent successfully";
        else
            Message = $"Error - {result.ReasonPhrase}";
    }
}
```

## <a name="testing-it-out"></a><span data-ttu-id="ecbeb-123">Тестирование</span><span class="sxs-lookup"><span data-stu-id="ecbeb-123">Testing it out</span></span>

1. <span data-ttu-id="ecbeb-124">Убедитесь, что функция Azure выполняется в локальной среде и порт соответствует методу `SendLocation`.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-124">Make sure the Azure function is still running locally and the port matches the `SendLocation` method.</span></span>

2. <span data-ttu-id="ecbeb-125">Настройте приложение UWP как запускаемое автоматически и запустите его.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-125">Set the UWP app as the startup app and run it.</span></span> <span data-ttu-id="ecbeb-126">Нажмите кнопку **Send Location** (Отправить данные о местоположении).</span><span class="sxs-lookup"><span data-stu-id="ecbeb-126">Click the **Send Location** button.</span></span> <span data-ttu-id="ecbeb-127">В окне консоли среды выполнения функций вы увидите выходные данные — вызываемую функцию, а также журнал с созданным URL-адресом.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-127">You'll see output in the Functions runtime console window showing the function being called, and the logging showing the generated URL.</span></span>

    ![Выходные данные вызываемой функции](../media/6-function-called.png)

3. <span data-ttu-id="ecbeb-129">Чтобы проверить сформированный URL-адрес, вставьте его из консоли в адресную строку браузера.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-129">To test the URL generation, paste it from the console into a browser.</span></span> <span data-ttu-id="ecbeb-130">Должно отобразиться ваше текущее местоположение.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-130">It should show your current location.</span></span>

## <a name="summary"></a><span data-ttu-id="ecbeb-131">Сводка</span><span class="sxs-lookup"><span data-stu-id="ecbeb-131">Summary</span></span>

<span data-ttu-id="ecbeb-132">В этом блоке вы узнали, как вызвать функцию Azure из мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-132">In this unit, you learned how to call an Azure function from the mobile app.</span></span> <span data-ttu-id="ecbeb-133">Этот вызов передал сведения о местоположении пользователя и телефонные номера, введенные в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-133">This call passed the user's location and the phone numbers they entered as JSON.</span></span> <span data-ttu-id="ecbeb-134">В следующем блоке вы привяжете функцию Azure к Twilio для отправки сведений об этом местоположении в SMS-сообщении.</span><span class="sxs-lookup"><span data-stu-id="ecbeb-134">In the next unit, you'll bind the Azure function to Twilio to send this location as an SMS message.</span></span>