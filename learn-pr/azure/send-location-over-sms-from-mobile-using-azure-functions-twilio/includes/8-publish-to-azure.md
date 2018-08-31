<span data-ttu-id="1b99b-101">Приложение и функция Azure готовы и работают в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="1b99b-101">The app and Azure Function are now complete and running locally.</span></span> <span data-ttu-id="1b99b-102">В этом блоке вы опубликуете функцию в Azure для работы в облаке.</span><span class="sxs-lookup"><span data-stu-id="1b99b-102">In this unit, you publish the function to Azure to run in the cloud.</span></span>

> <span data-ttu-id="1b99b-103">В этом блоке вы опубликуете функцию из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1b99b-103">In this unit, you will publish your function from Visual Studio.</span></span> <span data-ttu-id="1b99b-104">Это отличный способ начала работы с экспериментальными проектами, прототипами и учебными курсами, но при взаимодействии с приложением, предназначенным для эксплуатации в производственной среде, этот метод использовать **не** следует.</span><span class="sxs-lookup"><span data-stu-id="1b99b-104">This is a great way to get started for proof-of-concepts, prototypes, and learning, but for a production-quality app you should **not** use this method.</span></span> <span data-ttu-id="1b99b-105">Необходимо обратить внимание на определенные виды развертываний на основе непрерывной интеграции.</span><span class="sxs-lookup"><span data-stu-id="1b99b-105">You should use some form of CI-based deployment.</span></span> <span data-ttu-id="1b99b-106">Дополнительные сведения см. в [документации по развертываниям функций Azure](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment).</span><span class="sxs-lookup"><span data-stu-id="1b99b-106">You can read more about doing this in the [Azure Functions Deployment docs](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment).</span></span>
>
## <a name="publishing-your-app-to-azure"></a><span data-ttu-id="1b99b-107">Публикация приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="1b99b-107">Publishing your app to Azure</span></span>

<span data-ttu-id="1b99b-108">Функции Azure можно опубликовать в Azure из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1b99b-108">Azure functions can be published to Azure from inside Visual Studio.</span></span>

1. <span data-ttu-id="1b99b-109">Если локальная среда выполнения функций Azure работает, остановите ее.</span><span class="sxs-lookup"><span data-stu-id="1b99b-109">Stop the local Azure Functions runtime if it's still running from the previous unit.</span></span>

2. <span data-ttu-id="1b99b-110">Щелкните правой кнопкой мыши приложение `ImHere.Functions` в обозревателе решений и выберите пункт *Опубликовать*.</span><span class="sxs-lookup"><span data-stu-id="1b99b-110">Right-click on the `ImHere.Functions` app in the solution explorer and select *Publish...*.</span></span>

    ![Пункт "Опубликовать" контекстного меню в приложении функций](../media-drafts/8-right-click-publish.png)

3. <span data-ttu-id="1b99b-112">В диалоговом окне **Выбор целевого объекта публикации** выберите *Приложение-функция Azure* и для **Служба приложений Azure** выберите *Создать*.</span><span class="sxs-lookup"><span data-stu-id="1b99b-112">From the **Pick a publish target** dialog, select *Azure Function App*, and for **Azure App Service**, select *Create New*.</span></span> <span data-ttu-id="1b99b-113">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="1b99b-113">Click **Publish**.</span></span>

    ![Создание службы приложений Azure для публикации](../media-drafts/8-pick-publish-target.png)

4. <span data-ttu-id="1b99b-115">Если у вас несколько учетных записей Azure, выберите нужную учетную запись Azure в раскрывающемся списке в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="1b99b-115">Select your Azure account from the drop-down in the top-right corner if you have more than one Azure accounts and the right one isn't selected.</span></span>

5. <span data-ttu-id="1b99b-116">Присвойте имя приложению функций.</span><span class="sxs-lookup"><span data-stu-id="1b99b-116">Give your Functions app a name.</span></span> <span data-ttu-id="1b99b-117">Это имя должно быть глобально уникальным во всех приложениях функций в рамках платформы Azure, поэтому используйте нечто вроде "ImHere-\<ваше_имя\>".</span><span class="sxs-lookup"><span data-stu-id="1b99b-117">This name needs to be globally unique across all the Functions apps in the whole of Azure, so use something like "ImHere-\<YourName\>".</span></span>

6. <span data-ttu-id="1b99b-118">Выберите подписку, в которой необходимо создать приложение функций.</span><span class="sxs-lookup"><span data-stu-id="1b99b-118">Select the subscription you want to create this Functions app under.</span></span>

7. <span data-ttu-id="1b99b-119">Создайте группу ресурсов для этого приложения, нажав кнопку **Создать...** рядом с раскрывающимся списком **Группа ресурсов**, и присвойте ей имя, например "ImHere".</span><span class="sxs-lookup"><span data-stu-id="1b99b-119">Create a new resource group for this Functions app by clicking the **New...** button next to the **Resource Group** drop-down and giving it a name such as "ImHere".</span></span> <span data-ttu-id="1b99b-120">Имена групп ресурсов должны быть уникальными в рамках подписки, а не глобально уникальными в пределах Azure.</span><span class="sxs-lookup"><span data-stu-id="1b99b-120">Resource group names need to be unique to your subscription, not globally unique across Azure.</span></span> <span data-ttu-id="1b99b-121">Затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1b99b-121">Then, click **OK**.</span></span>

    ![Создание группы ресурсов](../media-drafts/8-create-new-resource-group.png)

   <span data-ttu-id="1b99b-123">Создание группы ресурсов упрощает последующую очистку.</span><span class="sxs-lookup"><span data-stu-id="1b99b-123">Creating a new resource group makes it easier to clean up later.</span></span> <span data-ttu-id="1b99b-124">При удалении группы ресурсов удаляются все данные, созданные для этого приложения функций.</span><span class="sxs-lookup"><span data-stu-id="1b99b-124">You can delete the resource group and know that everything you've created for this Functions app will all be deleted at the same time.</span></span>

8. <span data-ttu-id="1b99b-125">Создайте план размещения, нажав кнопку **Создать...** рядом с раскрывающимся списком **План размещения**.</span><span class="sxs-lookup"><span data-stu-id="1b99b-125">Create a new hosting plan by clicking the **New...** button next to the **Hosting Plan** drop-down.</span></span> <span data-ttu-id="1b99b-126">Именем плана службы приложений по умолчанию будет имя вашего приложения со словом "Plan" в конце.</span><span class="sxs-lookup"><span data-stu-id="1b99b-126">The App Service plan name will default to your app name with "Plan" on the end.</span></span> <span data-ttu-id="1b99b-127">В качестве значения параметра **Расположение** задайте ближайшее к вам расположение и убедитесь, что параметру **Размер** задано значение потребления.</span><span class="sxs-lookup"><span data-stu-id="1b99b-127">Set the **Location** to the closest location to you and make sure **Size** is set to consumption.</span></span> <span data-ttu-id="1b99b-128">Затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1b99b-128">Then, click **OK**.</span></span>

    ![Настройка плана размещения](../media-drafts/8-configure-hosting-plan.png)

9. <span data-ttu-id="1b99b-130">Создайте учетную запись хранения, нажав кнопку **Создать...** рядом с раскрывающимся списком **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="1b99b-130">Create a new storage account by clicking the **New...** button next to the **Storage Account** drop-down.</span></span> <span data-ttu-id="1b99b-131">Будет указано имя по умолчанию. Оставьте все значения по умолчанию и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1b99b-131">A default name will be provided, so keep all the default values and click **OK**.</span></span>

    ![Создание учетной записи хранения](../media-drafts/8-create-storage-account.png)

10. <span data-ttu-id="1b99b-133">Нажмите кнопку **Создать**, чтобы подготовить все ресурсы в Azure и опубликовать приложение функций Azure.</span><span class="sxs-lookup"><span data-stu-id="1b99b-133">Click **Create** to provision all the resources on Azure and publish your Azure Functions app.</span></span>

    ![Создание службы приложений](../media-drafts/8-create-app-service.png)

<span data-ttu-id="1b99b-135">Подготовка займет несколько минут.</span><span class="sxs-lookup"><span data-stu-id="1b99b-135">Provisioning will take a couple of minutes or so to run.</span></span> <span data-ttu-id="1b99b-136">Будут подготовлены следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="1b99b-136">The following resources will be provisioned:</span></span>

* <span data-ttu-id="1b99b-137">учетная запись хранения для хранения файлов, необходимых для приложения функций Azure;</span><span class="sxs-lookup"><span data-stu-id="1b99b-137">A storage account to store the files needed for the Azure Functions app</span></span>
* <span data-ttu-id="1b99b-138">план службы приложений для управления вычислительными ресурсами, необходимыми для приложения функций Azure;</span><span class="sxs-lookup"><span data-stu-id="1b99b-138">An App Service plan to manage the compute resources needed by the Azure Functions app</span></span>
* <span data-ttu-id="1b99b-139">служба приложения, в которой работает функция Azure.</span><span class="sxs-lookup"><span data-stu-id="1b99b-139">The App Service that runs the Azure function</span></span>

<span data-ttu-id="1b99b-140">Функция будет опубликована и станет доступна для вызова по адресу: https://<имя_приложения>.azurewebsites.net/api/SendLocation.</span><span class="sxs-lookup"><span data-stu-id="1b99b-140">The function will now be published and available to call at https://<your-app-name>.azurewebsites.net/api/SendLocation.</span></span>

## <a name="configuring-your-app"></a><span data-ttu-id="1b99b-141">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="1b99b-141">Configuring your app</span></span>

<span data-ttu-id="1b99b-142">Когда функция Azure запускалась локально, она использовала учетные данные Twilio, которые были сохранены в файле `local.settings.json`.</span><span class="sxs-lookup"><span data-stu-id="1b99b-142">When the Azure function was running locally, it was using Twilio credentials that were stored in a `local.settings.json` file.</span></span> <span data-ttu-id="1b99b-143">Как следует из имени, этот файл предназначен для локальных параметров, а не для параметров Azure.</span><span class="sxs-lookup"><span data-stu-id="1b99b-143">As the name suggests, this file is for local settings, not Azure settings.</span></span> <span data-ttu-id="1b99b-144">Прежде чем вызывать функцию Azure в Azure, необходимо настроить параметры `TwilioAccountSid` и `TwilioAuthToken`.</span><span class="sxs-lookup"><span data-stu-id="1b99b-144">Before the Azure function can be called inside Azure, the `TwilioAccountSid` and `TwilioAuthToken` settings need to be configured.</span></span>

1. <span data-ttu-id="1b99b-145">На вкладке "Публикация" щелкните параметр **Управление параметрами приложения**.</span><span class="sxs-lookup"><span data-stu-id="1b99b-145">From the Publish tab, click the **Manage Application Settings** option.</span></span>

    ![Параметр "Управление параметрами приложения"](../media-drafts/8-application-settings-option.png)

2. <span data-ttu-id="1b99b-147">Нажмите кнопку **Добавить**, чтобы добавить новый параметр.</span><span class="sxs-lookup"><span data-stu-id="1b99b-147">Click the **Add** button to add a new setting.</span></span> <span data-ttu-id="1b99b-148">Присвойте ему имя "TwilioAccountSid" и задайте в качестве значения идентификатор безопасности учетной записи Twilio.</span><span class="sxs-lookup"><span data-stu-id="1b99b-148">Name it "TwilioAccountSid" and set the value to your Twilio account SID.</span></span> <span data-ttu-id="1b99b-149">Повторите этот шаг для маркера проверки подлинности, используя имя "TwilioAuthToken".</span><span class="sxs-lookup"><span data-stu-id="1b99b-149">Repeat this step for your Auth Token using the name "TwilioAuthToken".</span></span>

    ![Задание учетных данных Twilio в параметрах приложения](../media-drafts/8-set-creds-in-app-settings.png)

3. <span data-ttu-id="1b99b-151">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1b99b-151">Click **OK**.</span></span>

4. <span data-ttu-id="1b99b-152">Нажмите кнопку **Опубликовать**, чтобы повторно опубликовать приложение функций Azure с новыми параметрами приложения.</span><span class="sxs-lookup"><span data-stu-id="1b99b-152">Click **Publish** to republish the Azure Functions app with the new application settings.</span></span>

    ![Кнопка "Опубликовать"](../media-drafts/8-publish-application-button.png)

## <a name="pointing-the-mobile-app-to-azure"></a><span data-ttu-id="1b99b-154">Направление мобильного приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="1b99b-154">Pointing the mobile app to Azure</span></span>

1. <span data-ttu-id="1b99b-155">На вкладке "Публикация" скопируйте **URL-адрес сайта** с помощью кнопки копирования рядом со значением.</span><span class="sxs-lookup"><span data-stu-id="1b99b-155">From the Publish tab, copy the **Site URL** using the copy button next to the value.</span></span>

    ![Копирование URL-адреса сайта на вкладке "Публикация"](../media-drafts/8-copy-site-url.png)

2. <span data-ttu-id="1b99b-157">Откройте `MainViewModel` в проекте `ImHere`.</span><span class="sxs-lookup"><span data-stu-id="1b99b-157">Open the `MainViewModel` from the `ImHere` project.</span></span>

3. <span data-ttu-id="1b99b-158">Измените значение поля `baseUrl` на URL-адрес сайта, скопированный на вкладке "Публикация".</span><span class="sxs-lookup"><span data-stu-id="1b99b-158">Update the value of the `baseUrl` field to be the site URL copied from the Publish tab.</span></span>

4. <span data-ttu-id="1b99b-159">Измените протокола для этого значения с `http` на `https`.</span><span class="sxs-lookup"><span data-stu-id="1b99b-159">Change the protocol for this value from `http` to `https`.</span></span> <span data-ttu-id="1b99b-160">URL-адрес сайта всегда указывается с помощью HTTP, но для вызова функции Azure нужно использовать HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1b99b-160">The site URL is always given using HTTP, but you have to use HTTPS to call an Azure function.</span></span>

## <a name="test-it-out"></a><span data-ttu-id="1b99b-161">Тестирование</span><span class="sxs-lookup"><span data-stu-id="1b99b-161">Test it out</span></span>

1. <span data-ttu-id="1b99b-162">Настройте приложение `ImHere.UWP` как запускаемое автоматически и запустите его.</span><span class="sxs-lookup"><span data-stu-id="1b99b-162">Set the `ImHere.UWP` app as the startup app and run it.</span></span>

2. <span data-ttu-id="1b99b-163">Введите номер телефона и нажмите кнопку **Send Location** (Отправить данные о местоположении).</span><span class="sxs-lookup"><span data-stu-id="1b99b-163">Enter a phone number and click the **Send Location** button.</span></span>

3. <span data-ttu-id="1b99b-164">Вы должны получить данные о местоположении в SMS-сообщении.</span><span class="sxs-lookup"><span data-stu-id="1b99b-164">You should receive the location as an SMS message.</span></span>

## <a name="summary"></a><span data-ttu-id="1b99b-165">Сводка</span><span class="sxs-lookup"><span data-stu-id="1b99b-165">Summary</span></span>

<span data-ttu-id="1b99b-166">В данном блоке вы узнали, как опубликовать проект функций Azure в Azure из Visual Studio и настроить параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="1b99b-166">In this unit, you learned how to publish an Azure Functions project to Azure from inside Visual Studio and configure application settings.</span></span>