В приложении есть пользовательский интерфейс и класс ViewModel. В этом блоке вы добавите возможность поиска местоположения в класс ViewModel с помощью Xamarin.Essentials.

## <a name="enable-location-permissions"></a>Включение разрешений на доступ к данным о местоположении

Все мобильные платформы обеспечивают безопасность сведений о пользователях (например, библиотеки фотографий и данных о местоположении) и располагают определенным оборудованием, таким как камера. Прежде чем приложение может получить доступ к данным о местоположении, пользователь должен предоставить разрешения — либо неявно во время установки, либо во время выполнения. При просмотре приложения UWP в магазине вы увидите разрешения, необходимые приложению. Устанавливая приложение, вы предоставляете разрешение неявным образом. Эти разрешения настраиваются в файле манифеста приложения.

1. В проекте приложения `ImHere.UWP` откройте файл `Package.appxmanifest`.

2. Перейдите на вкладку **Возможности** и выберите возможность *Расположение*.

    ![Вкладка возможностей UWP](../media-drafts/4-uwp-location-capability.png)

> Если требуется поддержка Android или iOS, разрешения должны быть настроены по-другому. Это подробно описано в [документации о геопозиционировании в Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=android#getting-started).

## <a name="query-for-the-users-location"></a>Запрос местоположения пользователя

Существует два способа получения сведений о местоположении пользователя — последнего известного или текущего. Получение данных о текущем местоположении может занять некоторое время, так как устройству может потребоваться получить GPS-сигнал и дождаться точных сведений о местоположении. Самым быстрым способом является получение сведений о последнем известном местоположении, обнаруженном устройством. Последнее известное местоположение потенциально менее точное, но вызвать его можно значительно быстрее. Данные о местоположении поступают в формате широты и долготы в [десятых долях градуса](https://en.wikipedia.org/wiki/Decimal_degrees) и высоты устройства в метрах над уровнем моря.

1. Откройте класс `MainViewModel` в проекте .NET Standard `ImHere`.

2. В методе `SendLocation` вызовите статический метод `GetLastKnownLocationAsync` в классе `Geolocation` пространства имен `Xamarin.Essentials`.

    ```cs
    Location location = await Geolocation.GetLastKnownLocationAsync();
    ```

3. Обновите свойство `Message` данными о местоположении пользователя (если оно определено).

    ```cs
    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
    ```

Ниже приведен полный код для этого метода.

```cs
async Task SendLocation()
{
    Location location = await Geolocation.GetLastKnownLocationAsync();

    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
}
```

Запустите приложение и нажмите кнопку **Отправить данные о местоположении**, чтобы увидеть расположение в пользовательском интерфейсе.

![Запущенное приложение с отображением местоположения пользователя](../media-drafts/4-running-app-showing-location.png)

> В этом приложении используется последнее известное местоположение. В приложении для эксплуатации в производственной среде потребуется получить сведения о текущем точном местоположении со временем ожидания, а если таковое не будет найдено, придется вернуться к последнему известному местоположению. Дополнительные сведения о том, как это сделать, см. в [документации о геопозиционировании в Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation). Это приложение не поддерживает обработку ошибок. В приложении для эксплуатации в производственной среде потребуется обрабатывать все исключения, возникающие, например, при недоступности сведений о местоположении.

## <a name="summary"></a>Сводка

В данном блоке вы узнали, как использовать Xamarin.Essentials для получения данных о местоположении пользователя. В следующем блоке вы создадите функцию Azure, которая будет выступать в качестве внутренней части для мобильного приложения.