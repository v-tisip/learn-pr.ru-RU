<span data-ttu-id="dcb4e-101">В приложении есть пользовательский интерфейс и класс ViewModel.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-101">The app has a UI and a ViewModel.</span></span> <span data-ttu-id="dcb4e-102">В этом блоке вы добавите возможность поиска местоположения в класс ViewModel с помощью Xamarin.Essentials.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-102">In this unit, you add location lookup to the ViewModel using Xamarin.Essentials.</span></span>

## <a name="enable-location-permissions"></a><span data-ttu-id="dcb4e-103">Включение разрешений на доступ к данным о местоположении</span><span class="sxs-lookup"><span data-stu-id="dcb4e-103">Enable location permissions</span></span>

<span data-ttu-id="dcb4e-104">Все мобильные платформы обеспечивают безопасность сведений о пользователях (например, библиотеки фотографий и данных о местоположении) и располагают определенным оборудованием, таким как камера.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-104">All mobile platforms have security around user information and certain hardware, such as the camera, photo library, and the user's location.</span></span> <span data-ttu-id="dcb4e-105">Прежде чем приложение может получить доступ к данным о местоположении, пользователь должен предоставить разрешения — либо неявно во время установки, либо во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-105">Before an app can access the user's location, the user has to grant permission - either by implicitly granting these permissions at install time or by choosing to grant a permission at runtime.</span></span> <span data-ttu-id="dcb4e-106">При просмотре приложения UWP в магазине вы увидите разрешения, необходимые приложению.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-106">When you view a UWP app on the store, the listing will show the permissions that the app needs.</span></span> <span data-ttu-id="dcb4e-107">Устанавливая приложение, вы предоставляете разрешение неявным образом.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-107">By installing the app, you implicitly grant permission.</span></span> <span data-ttu-id="dcb4e-108">Эти разрешения настраиваются в файле манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-108">These permissions are configured in an app manifest file.</span></span>

1. <span data-ttu-id="dcb4e-109">В проекте приложения `ImHere.UWP` откройте файл `Package.appxmanifest`.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-109">In the `ImHere.UWP` app project, open the `Package.appxmanifest` file.</span></span>

2. <span data-ttu-id="dcb4e-110">Перейдите на вкладку **Возможности** и выберите возможность *Расположение*.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-110">Head to the **Capabilities** tab and check the *Location* capability.</span></span>

    ![Вкладка возможностей UWP](../media-drafts/4-uwp-location-capability.png)

> <span data-ttu-id="dcb4e-112">Если требуется поддержка Android или iOS, разрешения должны быть настроены по-другому.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-112">If you want to support Android or iOS, the permissions need to be configured differently.</span></span> <span data-ttu-id="dcb4e-113">Это подробно описано в [документации о геопозиционировании в Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=android#getting-started).</span><span class="sxs-lookup"><span data-stu-id="dcb4e-113">This is detailed in the [Xamarin.Essentials Geolocation docs](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=android#getting-started).</span></span>

## <a name="query-for-the-users-location"></a><span data-ttu-id="dcb4e-114">Запрос местоположения пользователя</span><span class="sxs-lookup"><span data-stu-id="dcb4e-114">Query for the user's location</span></span>

<span data-ttu-id="dcb4e-115">Существует два способа получения сведений о местоположении пользователя — последнего известного или текущего.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-115">There are two ways to get the user's location - the last known or the current.</span></span> <span data-ttu-id="dcb4e-116">Получение данных о текущем местоположении может занять некоторое время, так как устройству может потребоваться получить GPS-сигнал и дождаться точных сведений о местоположении.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-116">The current location can take some time to get because the device may need to establish a GPS link and wait for the accurate location to be retrieved.</span></span> <span data-ttu-id="dcb4e-117">Самым быстрым способом является получение сведений о последнем известном местоположении, обнаруженном устройством.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-117">The fastest way is to get the last known location detected by the device.</span></span> <span data-ttu-id="dcb4e-118">Последнее известное местоположение потенциально менее точное, но вызвать его можно значительно быстрее.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-118">The last known location is potentially less accurate but is a much faster call.</span></span> <span data-ttu-id="dcb4e-119">Данные о местоположении поступают в формате широты и долготы в [десятых долях градуса](https://en.wikipedia.org/wiki/Decimal_degrees) и высоты устройства в метрах над уровнем моря.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-119">Locations come as the latitude and longitude in [decimal degrees](https://en.wikipedia.org/wiki/Decimal_degrees) and the altitude of the device in meters above sea level.</span></span>

1. <span data-ttu-id="dcb4e-120">Откройте класс `MainViewModel` в проекте .NET Standard `ImHere`.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-120">Open the `MainViewModel` class in the `ImHere` .NET standard project.</span></span>

2. <span data-ttu-id="dcb4e-121">В методе `SendLocation` вызовите статический метод `GetLastKnownLocationAsync` в классе `Geolocation` пространства имен `Xamarin.Essentials`.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-121">In the `SendLocation` method, make a call to the `GetLastKnownLocationAsync` static method on the `Geolocation` class in the `Xamarin.Essentials` namespace.</span></span>

    ```cs
    Location location = await Geolocation.GetLastKnownLocationAsync();
    ```

3. <span data-ttu-id="dcb4e-122">Обновите свойство `Message` данными о местоположении пользователя (если оно определено).</span><span class="sxs-lookup"><span data-stu-id="dcb4e-122">Update the `Message` property with the user's location if one is found.</span></span>

    ```cs
    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
    ```

<span data-ttu-id="dcb4e-123">Ниже приведен полный код для этого метода.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-123">The full code for this method is below.</span></span>

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

<span data-ttu-id="dcb4e-124">Запустите приложение и нажмите кнопку **Отправить данные о местоположении**, чтобы увидеть расположение в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-124">Run the app and click the **Send Location** button to see the location on the UI.</span></span>

![Запущенное приложение с отображением местоположения пользователя](../media-drafts/4-running-app-showing-location.png)

> <span data-ttu-id="dcb4e-126">В этом приложении используется последнее известное местоположение.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-126">This app uses the last known location.</span></span> <span data-ttu-id="dcb4e-127">В приложении для эксплуатации в производственной среде потребуется получить сведения о текущем точном местоположении со временем ожидания, а если таковое не будет найдено, придется вернуться к последнему известному местоположению.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-127">In a production-quality app, you would want to get the current accurate location with a time-out, and if one is not found in time, fall back to the last known.</span></span> <span data-ttu-id="dcb4e-128">Дополнительные сведения о том, как это сделать, см. в [документации о геопозиционировании в Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation). Это приложение не поддерживает обработку ошибок.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-128">You can read more on how to do this in the [Xamarin.Essentials Geolocation docs](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation). This app does not have error handling.</span></span> <span data-ttu-id="dcb4e-129">В приложении для эксплуатации в производственной среде потребуется обрабатывать все исключения, возникающие, например, при недоступности сведений о местоположении.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-129">In a production-quality app, you should handle any exceptions that occur, for example, if the location was not available and an exception was thrown.</span></span>

## <a name="summary"></a><span data-ttu-id="dcb4e-130">Сводка</span><span class="sxs-lookup"><span data-stu-id="dcb4e-130">Summary</span></span>

<span data-ttu-id="dcb4e-131">В данном блоке вы узнали, как использовать Xamarin.Essentials для получения данных о местоположении пользователя.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-131">In this unit, you learned how to use Xamarin.Essentials to get the user's location.</span></span> <span data-ttu-id="dcb4e-132">В следующем блоке вы создадите функцию Azure, которая будет выступать в качестве внутренней части для мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="dcb4e-132">In the next unit, you'll create an Azure function to act as a back end for the mobile app.</span></span>