<span data-ttu-id="1cef5-101">В этом упражнении мы создадим функцию Azure, которая отображает имя и размер большого двоичного объекта при его создании или обновлении.</span><span class="sxs-lookup"><span data-stu-id="1cef5-101">In this exercise, we're going to create an Azure function that displays the name and size of a blob when it's created or updated.</span></span> 

> [!NOTE]
> <span data-ttu-id="1cef5-102">Чтобы выполнить это упражнение, войдите на [портал Azure](https://portal.azure.com?azure-portal=true) с действующей учетной записью.</span><span class="sxs-lookup"><span data-stu-id="1cef5-102">To complete this exercise, make sure you're signed into the [Azure portal](https://portal.azure.com?azure-portal=true) with a valid account.</span></span>

## <a name="create-a-blob-trigger"></a><span data-ttu-id="1cef5-103">Создание триггера больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="1cef5-103">Create a blob trigger</span></span>

<span data-ttu-id="1cef5-104">В уже существующее приложение функций Azure добавим триггер BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="1cef5-104">Again, let's continue using our existing Azure Functions application and add a blob trigger.</span></span>

1. <span data-ttu-id="1cef5-105">Наведите указатель мыши на параметр **Функции** и нажмите на значок плюса (+).</span><span class="sxs-lookup"><span data-stu-id="1cef5-105">Point to **Functions** and select the plus (+) icon.</span></span>

    ![Наведите указатель мыши на параметр "Функции" и щелкните значок плюса](../media-drafts/4-hover-function.png)

2. <span data-ttu-id="1cef5-107">Выберите элемент **Пользовательская функция**, а затем **Триггер BLOB-объектов**.</span><span class="sxs-lookup"><span data-stu-id="1cef5-107">Select **Custom Function** and then **Blob trigger**.</span></span>

3. <span data-ttu-id="1cef5-108">При выборе языка укажите **C#**.</span><span class="sxs-lookup"><span data-stu-id="1cef5-108">Select **C#** as the language.</span></span> 

4. <span data-ttu-id="1cef5-109">Оставьте в поле **Имя** значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1cef5-109">Leave the **Name** set to the default value.</span></span>

5. <span data-ttu-id="1cef5-110">Оставьте в поле **Путь** значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1cef5-110">Leave the **Path** set to the default value.</span></span>

6. <span data-ttu-id="1cef5-111">Выберите существующую учетную запись Службы хранилища Azure или щелкните **Создать**, чтобы создать новую.</span><span class="sxs-lookup"><span data-stu-id="1cef5-111">Select an existing Azure Storage account, or select **Create** if you want Azure to create a new account for you.</span></span>

## <a name="create-a-blob-container"></a><span data-ttu-id="1cef5-112">Создание контейнера больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="1cef5-112">Create a blob container</span></span>

<span data-ttu-id="1cef5-113">Теперь, когда мы создали триггер больших двоичных объектов, откройте обозреватель хранилища, чтобы создать большой двоичный объект и активировать функцию.</span><span class="sxs-lookup"><span data-stu-id="1cef5-113">Now that we've created a blob trigger, let's use the Storage Explorer to create a blob and trigger the function.</span></span>

1. <span data-ttu-id="1cef5-114">Откройте в новой вкладке учетную запись хранения, которую вы выбрали или создали. Простой способ — откройте новую вкладку портала Azure и щелкните **Учетные записи хранения** на боковой панели или выберите **Все службы** на боковой панели и выполните фильтрацию по имени.</span><span class="sxs-lookup"><span data-stu-id="1cef5-114">Open the storage account you used (or created) in a new tab. An easy way to do this is to open a new Azure Portal tab and click on **Storage accounts** in the sidebar, or to use **All services** in the sidebar and then filter by the name.</span></span> <span data-ttu-id="1cef5-115">Новая вкладка нужна для того, чтобы в ходе работы переключаться между двумя используемыми службами.</span><span class="sxs-lookup"><span data-stu-id="1cef5-115">We want to use a new tab so we can switch between the two services we are working with.</span></span>

2. <span data-ttu-id="1cef5-116">Щелкните раздел **Обозреватель службы хранилища (предварительная версия)**. Откроется новая колонка для работы с большими двоичными объектами и файлами.</span><span class="sxs-lookup"><span data-stu-id="1cef5-116">Click on the **Storage Explorer (preview)** section - this will open a new blade where you can work with blobs and files.</span></span>

<span data-ttu-id="1cef5-117">Помните, что триггер больших двоичных объектов отслеживает только то расположение, которое указано в поле **Путь**.</span><span class="sxs-lookup"><span data-stu-id="1cef5-117">Remember that our blob trigger is monitoring only the location described in the **Path** field.</span></span> <span data-ttu-id="1cef5-118">По умолчанию наш путь должен выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="1cef5-118">By default, our path should be:</span></span>

> <span data-ttu-id="1cef5-119">samples-workitems/{name}</span><span class="sxs-lookup"><span data-stu-id="1cef5-119">samples-workitems/{name}</span></span>

<span data-ttu-id="1cef5-120">Нам нужно создать контейнер с именем **samples-workitems**.</span><span class="sxs-lookup"><span data-stu-id="1cef5-120">We need to create a container called **samples-workitems**.</span></span>

3. <span data-ttu-id="1cef5-121">Щелкните правой кнопкой мыши **Контейнеры BLOB-объектов** и выберите **Создать контейнер BLOB-объектов**.</span><span class="sxs-lookup"><span data-stu-id="1cef5-121">Right-click **BLOB CONTAINERS** and select **Create blob container**.</span></span>

4. <span data-ttu-id="1cef5-122">Введите имя **samples-workitems** и сохраните для уровня доступа настроенное по умолчанию значение **Частный**.</span><span class="sxs-lookup"><span data-stu-id="1cef5-122">Enter **samples-workitems** as the name, leave the access level at the default **Private** setting.</span></span>

## <a name="turn-on-your-blob-trigger"></a><span data-ttu-id="1cef5-123">Включение триггера больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="1cef5-123">Turn on your blob trigger</span></span>

<span data-ttu-id="1cef5-124">Теперь, когда мы создали контейнер для мониторинга, запустим нашу функцию, чтобы мы могли увидеть выходные данные при создании большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="1cef5-124">Now that we've created our container to monitor, let's run our function so we can see output when a blob is created.</span></span>

1. <span data-ttu-id="1cef5-125">Вернитесь на вкладку "Функции Azure" или откройте ее снова.</span><span class="sxs-lookup"><span data-stu-id="1cef5-125">Switch back to the Azure Function tab (or reopen it).</span></span>

2. <span data-ttu-id="1cef5-126">Выберите триггер большших двоичных объектов, чтобы открыть экран с кодом.</span><span class="sxs-lookup"><span data-stu-id="1cef5-126">Select your blob trigger to open the code screen.</span></span>

3. <span data-ttu-id="1cef5-127">Выберите **Запуск** и проверьте результаты выполнения в открывшемся окне.</span><span class="sxs-lookup"><span data-stu-id="1cef5-127">Select **Run** - this will open the output window.</span></span>

## <a name="create-a-blob"></a><span data-ttu-id="1cef5-128">Создание большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="1cef5-128">Create a blob</span></span>

<span data-ttu-id="1cef5-129">Теперь наш триггер BLOB-объектов запущен и начал прослушивание.</span><span class="sxs-lookup"><span data-stu-id="1cef5-129">Our blob trigger is now up and listening for activity.</span></span> <span data-ttu-id="1cef5-130">Создадим BLOB-объект, чтобы узнавать о получении сообщений журнала.</span><span class="sxs-lookup"><span data-stu-id="1cef5-130">Let's create a blob to see if we get a log message.</span></span>

1. <span data-ttu-id="1cef5-131">В обозревателе хранилища выберите контейнер **samples-workitems**.</span><span class="sxs-lookup"><span data-stu-id="1cef5-131">In Storage explorer, select the **samples-workitems** container.</span></span>

2. <span data-ttu-id="1cef5-132">На панели инструментов выберите **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="1cef5-132">Select **Upload** from the toolbar.</span></span>

3. <span data-ttu-id="1cef5-133">Выберите любой файл на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="1cef5-133">Select any file from your computer.</span></span>

4. <span data-ttu-id="1cef5-134">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="1cef5-134">Select **Upload**.</span></span>

5. <span data-ttu-id="1cef5-135">Вернитесь на вкладку "Функции Azure" и найдите в журнале выходных данных сообщение о том, что файл успешно отправлен.</span><span class="sxs-lookup"><span data-stu-id="1cef5-135">Switch back to the Azure Function tab and check the output logs for a message that displays what file was uploaded.</span></span>

## <a name="pause-the-function"></a><span data-ttu-id="1cef5-136">Приостановка выполнения функции</span><span class="sxs-lookup"><span data-stu-id="1cef5-136">Pause the Function</span></span>

<span data-ttu-id="1cef5-137">Чтобы не платить за дополнительные запросы, нажмите кнопку **Приостановить** над окном журнала.</span><span class="sxs-lookup"><span data-stu-id="1cef5-137">To ensure that you aren't charged for additional requests, you can click **Pause** above the log window.</span></span>

![Приостановка выполнения функции](../media-drafts/4-pause-timer.png)


