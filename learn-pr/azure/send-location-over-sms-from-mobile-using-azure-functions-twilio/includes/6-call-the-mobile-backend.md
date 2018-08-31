Вы запустили мобильное приложение и создали первоначальную версию функции Azure. В этом блоке вы вызовете функцию Azure из мобильного приложения, передавая сведения о местоположении пользователя и список телефонных номеров, на которые следует отправлять SMS-сообщения.

## <a name="calling-the-azure-function-from-the-mobile-app"></a>Вызов функции Azure из мобильного приложения

1. Откройте `MainViewModel`.

2. В этом классе добавьте закрытое поле `HttpClient` с именем `client`. Потребуется добавить ссылку на пространство имен `System.Net.Http`.

    ```cs
    HttpClient client = new HttpClient();
    ```

3. Добавьте поле константы для базового URL-адреса функции. В качестве значения задайте адрес, который прослушивает локальная среда выполнения функций Azure. После развертывания функции в Azure эту константу можно изменить на URL-адрес Azure.

    ```cs
    const string baseUrl = "http://localhost:7071";
    ```

4. После того как будет обнаружено местоположение, внутри метода `SendLocation` создайте экземпляр класса `PostData` с помощью сведений о местоположении и списка телефонных номеров, введенных пользователем. Вам потребуется добавить директиву using для пространства имен `ImHere.Data`.

    ```cs
    PostData postData = new PostData
    {
        Latitude = location.Latitude,
        Longitude = location.Longitude,
        ToNumbers = PhoneNumbers.Split('\n')
    };
    ```

    > Предполагается, что телефонные номера были введены в правильном формате по одному в строке в элементе управления `Editor`. В приложении для эксплуатации в производственной среде пришлось бы выполнить проверку на наличие одного или нескольких телефонных номеров в правильном формате.

5. Самым простым способом сериализации `PostData` в формате JSON является использование пакета NuGet Newtonsoft.JSON. Добавьте этот пакет NuGet в проект `ImHere` так же, как вы добавили Xamarin.Essentials в предыдущих блоках.

6. Сериализуйте `PostData` в `string` с помощью статического класса `JsonConvert`. Вам потребуется добавить директиву using для пространства имен `Newtonsoft.Json`. Закодируйте эту строку в класс `StringContent`, чтобы ее можно было передать в функцию Azure в виде JSON.

    ```cs
    string data = JsonConvert.SerializeObject(postData);
    StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
    ```

7. Отправьте эти данные в функцию и получите результат.

   ```cs
    HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                        content);
   ```

   Доступ к функциям Azure осуществляется с помощью `/api/<function name>`, поэтому при условии, что для локальной среды выполнения функций выбран порт 7071, функция `SendLocation` будет доступна в `http://localhost:7071/api/SendLocation`.

8. В зависимости от результата в пользовательском интерфейсе отображается соответствующее сообщение.

    ```cs
    if (result.IsSuccessStatusCode)
        Message = "Location sent successfully";
    else
        Message = $"Error - {result.ReasonPhrase}";
    ```

Полный код для новых полей и метода `SendLocation` приведен ниже.

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

## <a name="testing-it-out"></a>Тестирование

1. Убедитесь, что функция Azure выполняется в локальной среде и порт соответствует методу `SendLocation`.

2. Настройте приложение UWP как запускаемое автоматически и запустите его. Нажмите кнопку **Send Location** (Отправить данные о местоположении). В окне консоли среды выполнения функций вы увидите выходные данные — вызываемую функцию, а также журнал с созданным URL-адресом.

    ![Выходные данные вызываемой функции](../media-drafts/6-function-called.png)

3. Чтобы проверить сформированный URL-адрес, вставьте его из консоли в адресную строку браузера. Должно отобразиться ваше текущее местоположение.

## <a name="summary"></a>Сводка

В этом блоке вы узнали, как вызвать функцию Azure из мобильного приложения. Этот вызов передал сведения о местоположении пользователя и телефонные номера, введенные в формате JSON. В следующем блоке вы привяжете функцию Azure к Twilio для отправки сведений об этом местоположении в SMS-сообщении.