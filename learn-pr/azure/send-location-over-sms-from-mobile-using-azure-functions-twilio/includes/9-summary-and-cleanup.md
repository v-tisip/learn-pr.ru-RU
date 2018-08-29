<span data-ttu-id="65ad5-101">Вы успешно создали кроссплатформенное мобильное приложение с помощью Xamarin и функции Azure с привязкой к Twilio.</span><span class="sxs-lookup"><span data-stu-id="65ad5-101">You've successfully created a cross-platform mobile app using Xamarin and an Azure function with a Twilio binding.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="65ad5-102">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="65ad5-102">Clean up resources</span></span>

<span data-ttu-id="65ad5-103">Закончив работу с этим приложением функций Azure, вы можете удалить все ресурсы, созданные в рамках этого руководства, на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="65ad5-103">When you're done working with this Azure Functions application, you can delete all resources created during the tutorial from the Azure portal.</span></span>

1. <span data-ttu-id="65ad5-104">В Visual Studio последовательно выберите *Вид->Cloud Explorer*.</span><span class="sxs-lookup"><span data-stu-id="65ad5-104">From Visual Studio, select *View->Cloud Explorer*.</span></span>

2. <span data-ttu-id="65ad5-105">В раскрывающемся списке в верхней части этой панели выберите *Группы ресурсов*.</span><span class="sxs-lookup"><span data-stu-id="65ad5-105">From the drop-down at the top of this panel, select *Resource Groups*.</span></span>

3. <span data-ttu-id="65ad5-106">Разверните подписку, которая использовалась для создания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="65ad5-106">Expand the subscription that you used to create the resource group.</span></span> <span data-ttu-id="65ad5-107">Правой кнопкой мыши щелкните группу ресурсов "ImHere" и выберите пункт *Открыть на портале*.</span><span class="sxs-lookup"><span data-stu-id="65ad5-107">Right-click on the "ImHere" resource group and select *Open in Portal*.</span></span>

    ![Открытие группы ресурсов на портале из окна Cloud Explorer](../media/9-open-resource-group-in-portal.png)

4. <span data-ttu-id="65ad5-109">Если необходимо, войдите на портал Azure из браузера.</span><span class="sxs-lookup"><span data-stu-id="65ad5-109">Log into the Azure portal in your browser, if necessary.</span></span>

5. <span data-ttu-id="65ad5-110">Откроется портал с группой ресурсов "ImHere".</span><span class="sxs-lookup"><span data-stu-id="65ad5-110">The portal will open on the "ImHere" resource group.</span></span> <span data-ttu-id="65ad5-111">Нажмите кнопку **Удалить группу ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="65ad5-111">Click the **Delete Resource Group** button.</span></span>

    ![Удаление группы ресурсов](../media/9-delete-resource-group.png)

6. <span data-ttu-id="65ad5-113">Введите имя группы ресурсов, чтобы подтвердить удаление, и нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="65ad5-113">Enter the name of the resource group to confirm the deletion and click **Delete**.</span></span>

    ![Ввод имени группы ресурсов для подтверждения удаления](../media/9-confirm-delete-resource-group.png)

## <a name="summary"></a><span data-ttu-id="65ad5-115">Сводка</span><span class="sxs-lookup"><span data-stu-id="65ad5-115">Summary</span></span>

<span data-ttu-id="65ad5-116">Из этого руководства вы узнали, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="65ad5-116">In this tutorial, you learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="65ad5-117">Создание кроссплатформенного приложения Xamarin.Forms, которое использует Xamarin.Essentials.</span><span class="sxs-lookup"><span data-stu-id="65ad5-117">Create a cross-platform Xamarin.Forms app that uses Xamarin.Essentials.</span></span>
> * <span data-ttu-id="65ad5-118">Создание кроссплатформенного пользовательского интерфейса с помощью XAML с логикой приложения в классе ViewModel, а также привязка свойства в классе ViewModel к пользовательскому интерфейсу.</span><span class="sxs-lookup"><span data-stu-id="65ad5-118">Create a cross-platform UI using XAML with application logic in a ViewModel, as well as bind properties in a ViewModel to the UI.</span></span>
> * <span data-ttu-id="65ad5-119">Определение местоположения пользователя.</span><span class="sxs-lookup"><span data-stu-id="65ad5-119">Detect the user's location.</span></span>
> * <span data-ttu-id="65ad5-120">Создание функции Azure с триггером HTTP и ее запуск в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="65ad5-120">Create an Azure function with an HTTP trigger and run it locally.</span></span>
> * <span data-ttu-id="65ad5-121">Вызов функции Azure из мобильного приложения с передачей данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="65ad5-121">Call an Azure function from a mobile app, passing data as JSON.</span></span>
> * <span data-ttu-id="65ad5-122">Привязка функции Azure к Twilio для отправки SMS-сообщений.</span><span class="sxs-lookup"><span data-stu-id="65ad5-122">Bind an Azure function to Twilio to send an SMS message.</span></span>
> * <span data-ttu-id="65ad5-123">Публикация функции Azure в Azure.</span><span class="sxs-lookup"><span data-stu-id="65ad5-123">Publish an Azure function to Azure.</span></span>
