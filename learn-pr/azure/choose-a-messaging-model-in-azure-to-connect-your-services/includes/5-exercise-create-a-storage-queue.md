<span data-ttu-id="c4525-101">В этом упражнении вы создадите учетную запись хранения в своей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="c4525-101">In this exercise, you will create a new Storage Account in your Azure subscription.</span></span> <span data-ttu-id="c4525-102">Затем, используя Azure Cloud Shell, вы создадите очередь, добавите в нее сообщение, а затем прочтете это сообщение и удалите его из очереди.</span><span class="sxs-lookup"><span data-stu-id="c4525-102">You will then use the Azure Cloud Shell to create a new queue, add a message to it, and then read that message and remove it from the queue.</span></span>

<span data-ttu-id="c4525-103">Точно такие же действия выполняют компоненты в распределенном приложении.</span><span class="sxs-lookup"><span data-stu-id="c4525-103">These are the same actions taken by components in a distributed application.</span></span> <span data-ttu-id="c4525-104">Например, мобильное приложение может добавлять сообщение в очередь, в которой оно будет ожидать, пока веб-служба не извлечет и не обработает это сообщение.</span><span class="sxs-lookup"><span data-stu-id="c4525-104">For example, a mobile app may add a message to a queue, where it waits for a web service to retrieve it and process it.</span></span>

## <a name="create-a-storage-account"></a><span data-ttu-id="c4525-105">Создание учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="c4525-105">Create a Storage Account</span></span>

<span data-ttu-id="c4525-106">Поскольку очереди хранилища относятся к учетным записям хранения Azure общего назначения,</span><span class="sxs-lookup"><span data-stu-id="c4525-106">Since Storage queues are part of Azure general purpose Storage accounts.</span></span> <span data-ttu-id="c4525-107">для начала нужно создать учетную запись хранения:</span><span class="sxs-lookup"><span data-stu-id="c4525-107">You must start by creating a Storage account:</span></span>

1. <span data-ttu-id="c4525-108">Откройте браузер, перейдите на [портал Azure](http://portal.azure.com) и выполните вход со своими обычными учетными данными.</span><span class="sxs-lookup"><span data-stu-id="c4525-108">In a browser, navigate to the [Azure Portal](http://portal.azure.com) and sign in with your normal credentials.</span></span>
1. <span data-ttu-id="c4525-109">В верхнем левом углу выберите **Все службы**.</span><span class="sxs-lookup"><span data-stu-id="c4525-109">In the top left, click **All services**.</span></span>
1. <span data-ttu-id="c4525-110">Прокрутите экран вниз до раздела **Хранилище** и выберите **Учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="c4525-110">Scroll down to the **Storage** section, and then click **Storage accounts**.</span></span>
1. <span data-ttu-id="c4525-111">В верхнем левом углу колонки **Учетные записи хранения** выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c4525-111">At the top left of the **Storage accounts** blade, click **Add**.</span></span>

    ![Создание учетной записи хранения](../images/5-create-a-storage-account-1.png)

1. <span data-ttu-id="c4525-113">В текстовом поле **Имя** введите уникальное имя для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="c4525-113">In the **Name** text box, type a unique name for the storage account.</span></span>
1. <span data-ttu-id="c4525-114">Убедитесь, что в разделе **Модель развертывания** выбран параметр **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="c4525-114">Under **Deployment model**, ensure that **Resource Manager** is selected.</span></span>
1. <span data-ttu-id="c4525-115">В раскрывающемся списке **Тип учетной записи** выберите параметр **Общего назначения версии 2**.</span><span class="sxs-lookup"><span data-stu-id="c4525-115">In the **Account kind** drop-down list, select **Storage (general purpose v2)**.</span></span>
1. <span data-ttu-id="c4525-116">В раскрывающемся списке **Расположение** выберите ближайший к вам регион.</span><span class="sxs-lookup"><span data-stu-id="c4525-116">In the **Location** drop-down list, select a region near you.</span></span>
1. <span data-ttu-id="c4525-117">В раскрывающемся списке **Репликация** выберите параметр **Локально избыточное хранилище**.</span><span class="sxs-lookup"><span data-stu-id="c4525-117">In the **Replication** drop-down list, select **Locally-redundant storage (LRS)**.</span></span>
1. <span data-ttu-id="c4525-118">В разделе **Производительность** выберите вариант **Стандарт**.</span><span class="sxs-lookup"><span data-stu-id="c4525-118">Under **Performance**, select **Standard**.</span></span>
1. <span data-ttu-id="c4525-119">В разделе **Уровень доступа** выберите вариант **Холодный**.</span><span class="sxs-lookup"><span data-stu-id="c4525-119">Under **Access tier**, select **Cool**.</span></span>
1. <span data-ttu-id="c4525-120">В разделе **Требуется безопасное перемещение** выберите вариант **Отключено**.</span><span class="sxs-lookup"><span data-stu-id="c4525-120">Under **Secure transfer required** select, **Disabled**.</span></span>
1. <span data-ttu-id="c4525-121">В разделе **Подписка** выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="c4525-121">Under **Subscription**, select your subscription.</span></span>

    ![Создание учетной записи хранения](../images/5-create-a-storage-account-2.png)

1. <span data-ttu-id="c4525-123">В разделе **Группа ресурсов** выберите **Создать**, а затем в текстовом поле введите **MusicSharingResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="c4525-123">Under **Resource group** select **Create new**, and then in the textbox type **MusicSharingResourceGroup**.</span></span>
1. <span data-ttu-id="c4525-124">В разделе **Виртуальные сети** выберите вариант **Отключено**, а затем нажмите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c4525-124">Under **Virtual networks** select **Disabled** and then click **Create**.</span></span>

    ![Создание учетной записи хранения](../images/5-create-a-storage-account-3.png)

<span data-ttu-id="c4525-126">Azure создаст новую учетную запись хранения и новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c4525-126">Azure creates the new storage account and the new resource group.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="c4525-127">Создание очереди</span><span class="sxs-lookup"><span data-stu-id="c4525-127">Create a Queue</span></span>

<span data-ttu-id="c4525-128">После создания учетной записи хранения можно добавить в нее новую очередь.</span><span class="sxs-lookup"><span data-stu-id="c4525-128">Now that the Storage Account has been created, you can add a new queue to it.</span></span> <span data-ttu-id="c4525-129">Для создания очереди используются команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c4525-129">You must create the queue by using PowerShell commands:</span></span>

1. <span data-ttu-id="c4525-130">В правом верхнем углу портала нажмите на ссылку **Cloud Shell**.</span><span class="sxs-lookup"><span data-stu-id="c4525-130">In the top right of the portal, click the **Cloud Shell** link.</span></span>

    ![Запуск Cloud Shell](../images/5-create-a-storage-queue-1.png)

1. <span data-ttu-id="c4525-132">На экране **Добро пожаловать в Azure Cloud Shell** нажмите **PowerShell (Linux)**.</span><span class="sxs-lookup"><span data-stu-id="c4525-132">In the **Welcome to Azure Cloud Shell** screen, click **PowerShell (Linux)**.</span></span>
1. <span data-ttu-id="c4525-133">На появившемся экране **У вас не подключены хранилища** нажмите **Создать хранилище**.</span><span class="sxs-lookup"><span data-stu-id="c4525-133">If the **You have no storage mounted** screen appears, click **Create storage**.</span></span>
1. <span data-ttu-id="c4525-134">Когда появится запрос `PS Azure` о получении учетной записи хранения, введите следующую команду, заменив `<storageaccountname>` на уникальное имя вашей учетной записи хранения, и нажмите клавишу ВВОД:</span><span class="sxs-lookup"><span data-stu-id="c4525-134">When the `PS Azure` prompt appears, to obtain the storage account, type the following command, substituting `<storageaccountname>` with the unique name of your storage account, and then press Enter:</span></span>

    ```powershell
    $storageaccount = Get-AzureRmStorageAccount -Name <storageaccountname> -ResourceGroup  MusicSharingResourceGroup
    ```

1. <span data-ttu-id="c4525-135">Чтобы получить контекст учетной записи хранения, введите следующую команду и нажмите клавишу ВВОД:</span><span class="sxs-lookup"><span data-stu-id="c4525-135">To obtain the context of the storage account, type the following command and then press Enter:</span></span>

    ```powershell
    $context = $storageaccount.Context
    ```

1. <span data-ttu-id="c4525-136">Чтобы создать новую очередь, введите следующую команду и нажмите клавишу ВВОД:</span><span class="sxs-lookup"><span data-stu-id="c4525-136">To create a new queue, type the following command and then press Enter:</span></span>

    ```powershell
    $messageQueue = New-AzureStorageQueue -Name musicsharingmessages -Context $context
    ```

## <a name="add-a-message-to-the-queue"></a><span data-ttu-id="c4525-137">Добавление сообщения в очередь</span><span class="sxs-lookup"><span data-stu-id="c4525-137">Add a Message to the Queue</span></span>

<span data-ttu-id="c4525-138">Теперь, когда вы создали очередь в учетной записи хранения, можно добавить в нее сообщение.</span><span class="sxs-lookup"><span data-stu-id="c4525-138">Now that you have created a queue in the storage account, you can add a message to it.</span></span>

1. <span data-ttu-id="c4525-139">Чтобы создать сообщение, введите следующую команду и нажмите клавишу ВВОД:</span><span class="sxs-lookup"><span data-stu-id="c4525-139">To create a new message, type the following command and then press Enter:</span></span>

    ```powershell
    $newSongMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList "A new song has been added."
    ```

1. <span data-ttu-id="c4525-140">Чтобы добавить новое сообщение в новую очередь, введите следующую команду и нажмите клавишу ВВОД:</span><span class="sxs-lookup"><span data-stu-id="c4525-140">To add the new message to the new queue, type the following command and then press Enter:</span></span>

    ```powershell
    $messageQueue.CloudQueue.AddMessageAsync($newSongMessage)
    ```

1. <span data-ttu-id="c4525-141">На портале Azure щелкните **Все ресурсы** в панели навигации слева.</span><span class="sxs-lookup"><span data-stu-id="c4525-141">In the Azure Portal, in the navigation on the left, click **All resources**.</span></span>
1. <span data-ttu-id="c4525-142">В списке ресурсов выберите учетную запись хранения, которую вы создали ранее.</span><span class="sxs-lookup"><span data-stu-id="c4525-142">In the list of resources, click the storage account you created earlier.</span></span>
1. <span data-ttu-id="c4525-143">В колонке учетной записи хранения выберите **Обозреватель службы хранилища (предварительная версия)**.</span><span class="sxs-lookup"><span data-stu-id="c4525-143">In the storage account blade, click **Storage Explorer (Preview)**.</span></span>
1. <span data-ttu-id="c4525-144">В обозревателе службы хранилища в разделе **ОЧЕРЕДИ** выберите **musicsharingmessages**.</span><span class="sxs-lookup"><span data-stu-id="c4525-144">In the Storage Explorer, under **QUEUES**, click **musicsharingmessages**.</span></span> <span data-ttu-id="c4525-145">В обозревателе службы хранилища появится добавленное вами сообщение.</span><span class="sxs-lookup"><span data-stu-id="c4525-145">The Storage Explorer displays the message you just added.</span></span>

## <a name="retrieve-and-remove-the-message"></a><span data-ttu-id="c4525-146">Получение и удаление сообщения</span><span class="sxs-lookup"><span data-stu-id="c4525-146">Retrieve and Remove the Message</span></span>

<span data-ttu-id="c4525-147">Компонент назначения для сообщения в очереди хранилища должен извлечь сообщение в начале очереди, обработать его и удалить из очереди, чтобы его не получили другие компоненты:</span><span class="sxs-lookup"><span data-stu-id="c4525-147">A destination component for a message in a Storage queue, must retrieve the message at the front of the queue, process it, and then delete it from the queue so that other components do not retrieve it:</span></span>

1. <span data-ttu-id="c4525-148">В Azure Cloud Shell введите следующую команду, чтобы получить сообщение в начале очереди, и нажмите клавишу ВВОД:</span><span class="sxs-lookup"><span data-stu-id="c4525-148">In the Azure Cloud Shell, to get the message at the front of the queue, type the following command and then press Enter:</span></span>

    ```powershell
    $retrievedMessage = $messageQueue.CloudQueue.GetMessageAsync().Result
    ```

1. <span data-ttu-id="c4525-149">Чтобы отобразить сообщение, введите следующую команду и нажмите клавишу ВВОД:</span><span class="sxs-lookup"><span data-stu-id="c4525-149">To display the message, type the following command and then press Enter:</span></span>

    ```powershell
    $retrievedMessage.AsString
    ```

1. <span data-ttu-id="c4525-150">Чтобы отобразить все свойства сообщения, введите следующую команду и нажмите клавишу ВВОД:</span><span class="sxs-lookup"><span data-stu-id="c4525-150">To display all the properties of the message, type the following command and then press Enter:</span></span>

    ```powershell
    $retrievedMessage
    ```

1. <span data-ttu-id="c4525-151">Чтобы удалить сообщение из очереди, введите следующую команду и нажмите клавишу ВВОД:</span><span class="sxs-lookup"><span data-stu-id="c4525-151">To remove the message from the queue, type the following command and then press Enter:</span></span>

    ```powershell
    $messageQueue.CloudQueue.DeleteMessageAsync($retrievedMessage)
    ```

1. <span data-ttu-id="c4525-152">На портале Azure обновите экран очереди — для этого в колонке учетной записи хранения выберите **Обзор**, а затем **Обозреватель службы хранилища**.</span><span class="sxs-lookup"><span data-stu-id="c4525-152">In the Azure Portal, to refresh the queue display, in the Storage Account blade, click **Overview** and then click **Storage Explorer**.</span></span>
1. <span data-ttu-id="c4525-153">В разделе **ОЧЕРЕДИ** выберите **musicsharingmessages**.</span><span class="sxs-lookup"><span data-stu-id="c4525-153">Under **QUEUES**, click **musicsharingmessages**.</span></span> <span data-ttu-id="c4525-154">Обозреватель службы хранилища показывает, что очередь пуста, поскольку единственное сообщение вы удалили.</span><span class="sxs-lookup"><span data-stu-id="c4525-154">The Storage Explorer shows that the queue is empty because you removed the only message.</span></span>

## <a name="cleanup"></a><span data-ttu-id="c4525-155">Очистка</span><span class="sxs-lookup"><span data-stu-id="c4525-155">Cleanup</span></span>

<span data-ttu-id="c4525-156">Чтобы удалить все ресурсы, созданные во время этого упражнения, введите в Azure Cloud Shell следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c4525-156">To remove all resources created during this exercise enter the following command in the Azure Cloud Shell</span></span> 
```powershell
Remove-AzureRmResourceGroup -Name "MusicSharingResourceGroup" -Force
```


## <a name="summary"></a><span data-ttu-id="c4525-157">Сводка</span><span class="sxs-lookup"><span data-stu-id="c4525-157">Summary</span></span>

<span data-ttu-id="c4525-158">Вы создали учетную запись хранения в своей подписке Azure и добавили в нее новую очередь.</span><span class="sxs-lookup"><span data-stu-id="c4525-158">Here, you created a Storage Account in your Azure subscription and created a new queue in it.</span></span> <span data-ttu-id="c4525-159">Вы также использовали PowerShell для имитации действий компонентов распределенного приложения, когда добавили сообщение в очередь, а затем извлекли его и удалили.</span><span class="sxs-lookup"><span data-stu-id="c4525-159">You also used PowerShell to simulate the actions of distributed application components by adding a message to the queue and then retrieving and removing it.</span></span>

<span data-ttu-id="c4525-160">Очереди учетной записи хранения Azure — отличный вариант для передачи сообщений между компонентами распределенного приложения.</span><span class="sxs-lookup"><span data-stu-id="c4525-160">Azure Storage Account queues are a good solution when you want to pass messages between the components of a distributed application.</span></span> <span data-ttu-id="c4525-161">Не выбирайте очереди хранилища, если собираетесь публиковать события.</span><span class="sxs-lookup"><span data-stu-id="c4525-161">Do not choose Storage queues when you want to publish events.</span></span>