<span data-ttu-id="a1fff-101">В этом упражнении мы создадим функцию Azure, которая отображает имя и размер BLOB-объекта при его создании или обновлении.</span><span class="sxs-lookup"><span data-stu-id="a1fff-101">In this exercise, we're going to create an Azure function that displays the name and size of a blob when it's created or updated.</span></span> 

> [!NOTE]
> <span data-ttu-id="a1fff-102">Чтобы выполнить это упражнение, войдите на [портал Azure](https://portal.azure.com/) под действующей учетной записью.</span><span class="sxs-lookup"><span data-stu-id="a1fff-102">To complete this exercise, make sure you're signed in to the [Azure portal](https://portal.azure.com/) with a valid account.</span></span>

## <a name="create-a-blob-trigger"></a><span data-ttu-id="a1fff-103">Создание триггера BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="a1fff-103">Create a blob trigger</span></span>

<span data-ttu-id="a1fff-104">В уже существующее приложение функций Azure добавим триггер BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="a1fff-104">Again, let's continue using our existing Azure Functions application and add a blob trigger.</span></span>

1. <span data-ttu-id="a1fff-105">Наведите указатель мыши на параметр **Функции** и нажмите на значок плюса (+).</span><span class="sxs-lookup"><span data-stu-id="a1fff-105">Point to **Functions** and select the plus (+) icon.</span></span>

    ![Наведите указатель мыши на параметр "Функции" и нажмите на значок плюса](../media/4-hover-function.png)

1. <span data-ttu-id="a1fff-107">Выберите **Триггер BLOB-объектов**.</span><span class="sxs-lookup"><span data-stu-id="a1fff-107">Select **Blob trigger**.</span></span>

1. <span data-ttu-id="a1fff-108">В качестве языка выберите **C#**.</span><span class="sxs-lookup"><span data-stu-id="a1fff-108">Select **C#** as the language.</span></span> 

1. <span data-ttu-id="a1fff-109">Оставьте в поле **Имя** значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a1fff-109">Leave the **Name** set to the default value.</span></span>

1. <span data-ttu-id="a1fff-110">Оставьте в поле **Путь** значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a1fff-110">Leave the **Path** set to the default value.</span></span>

1. <span data-ttu-id="a1fff-111">Выберите существующую учетную запись хранилища Azure или нажмите **Создать**, если вы хотите создать для себя учетную запись.</span><span class="sxs-lookup"><span data-stu-id="a1fff-111">Select an existing Azure Storage account, or select **Create** if you want Azure to create a new account for you.</span></span>

## <a name="download-storage-explorer"></a><span data-ttu-id="a1fff-112">Загрузка обозревателя службы хранилища</span><span class="sxs-lookup"><span data-stu-id="a1fff-112">Download Storage explorer</span></span>

<span data-ttu-id="a1fff-113">Теперь, когда мы создали триггер BLOB-объектов, загрузим обозреватель службы хранилища, который позволит нам легко создать BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="a1fff-113">Now that we've created a blob trigger, let's download Storage explorer, which will allow us to easily create a blob.</span></span>

- <span data-ttu-id="a1fff-114">Скачайте [обозреватель службы хранилища](http://storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="a1fff-114">Download [Storage explorer](http://storageexplorer.com).</span></span>

## <a name="connect-to-your-azure-storage-account"></a><span data-ttu-id="a1fff-115">Подключение к учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="a1fff-115">Connect to your Azure Storage account</span></span>

<span data-ttu-id="a1fff-116">Итак, мы скачали обозреватель службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="a1fff-116">We now have Storage explorer downloaded.</span></span> <span data-ttu-id="a1fff-117">Выполните вход с предоставленными вам учетными данными.</span><span class="sxs-lookup"><span data-stu-id="a1fff-117">Let's sign in using the credentials that were supplied.</span></span>

1. <span data-ttu-id="a1fff-118">В обозревателе службы хранилища нажмите на значок плюса (+) слева.</span><span class="sxs-lookup"><span data-stu-id="a1fff-118">In Storage explorer, select the plus (+) icon on the left.</span></span>

1. <span data-ttu-id="a1fff-119">Выберите параметр **Использовать имя и ключ учетной записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="a1fff-119">Select **Use a storage account name and key**.</span></span>

1. <span data-ttu-id="a1fff-120">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a1fff-120">Select **Next**.</span></span>

1. <span data-ttu-id="a1fff-121">В Azure выберите для триггера BLOB-объектов параметр **Интегрировать**.</span><span class="sxs-lookup"><span data-stu-id="a1fff-121">In Azure, under your blob trigger, select **Integrate**.</span></span>

1. <span data-ttu-id="a1fff-122">Выберите параметр **Документация**, чтобы развернуть представление.</span><span class="sxs-lookup"><span data-stu-id="a1fff-122">Select **Documentation** to expand the view.</span></span>

1. <span data-ttu-id="a1fff-123">Скопируйте **Имя учетной записи** и **Ключ учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="a1fff-123">Copy the **Account Name** and **Account Key**.</span></span>

1. <span data-ttu-id="a1fff-124">Вернитесь в обозреватель службы хранилища и скопированные данные в поля **Имя учетной записи** и **Ключ учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="a1fff-124">Back in Storage explorer, paste in the **Account Name** and **Account Key**.</span></span>

1. <span data-ttu-id="a1fff-125">Введите значение в поле **Отображаемое имя**.</span><span class="sxs-lookup"><span data-stu-id="a1fff-125">Enter a **Display name**.</span></span> <span data-ttu-id="a1fff-126">Оно станет именем подключения в обозревателе службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="a1fff-126">This value is the name of the connection in Storage explorer.</span></span>

1. <span data-ttu-id="a1fff-127">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a1fff-127">Select **Next**.</span></span>

1. <span data-ttu-id="a1fff-128">Нажмите кнопку **Подключиться**.</span><span class="sxs-lookup"><span data-stu-id="a1fff-128">Select **Connect**.</span></span> 

## <a name="create-a-blob-container"></a><span data-ttu-id="a1fff-129">Создание контейнера BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="a1fff-129">Create a blob container</span></span>

<span data-ttu-id="a1fff-130">Мы не подключены к своей учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="a1fff-130">We aren't connected to our Azure Storage account.</span></span> <span data-ttu-id="a1fff-131">Помните, что наш триггер BLOB-объектов осуществляет мониторинг только того расположения, которое указано в поле **Путь**.</span><span class="sxs-lookup"><span data-stu-id="a1fff-131">Remember that our blob trigger is monitoring only the location described in the **Path** field.</span></span> <span data-ttu-id="a1fff-132">По умолчанию наш путь должен выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="a1fff-132">By default, our path should be:</span></span>

> <span data-ttu-id="a1fff-133">samples-workitems/{name}</span><span class="sxs-lookup"><span data-stu-id="a1fff-133">samples-workitems/{name}</span></span>

<span data-ttu-id="a1fff-134">Нам необходимо создать контейнер с именем **samples-workitems**.</span><span class="sxs-lookup"><span data-stu-id="a1fff-134">We need to create a container called **samples-workitems**.</span></span>

1. <span data-ttu-id="a1fff-135">Разверните свою учетную запись хранения в обозревателе службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="a1fff-135">In Storage explorer, expand your storage account.</span></span> <span data-ttu-id="a1fff-136">В качестве имени должно быть указано **Отображаемое имя**, которое вы указали во время подключения.</span><span class="sxs-lookup"><span data-stu-id="a1fff-136">The name should be the **Display name** that you provided during the connection process.</span></span>

1. <span data-ttu-id="a1fff-137">Щелкните правой кнопкой мыши элемент **Контейнеры BLOB-объектов** и выберите параметр **Создать контейнер BLOB-объектов**.</span><span class="sxs-lookup"><span data-stu-id="a1fff-137">Right-click **Blob Containers** and select **Create blob container**.</span></span>

1. <span data-ttu-id="a1fff-138">Введите **samples-workitems**.</span><span class="sxs-lookup"><span data-stu-id="a1fff-138">Enter **samples-workitems**.</span></span>

## <a name="turn-on-your-blob-trigger"></a><span data-ttu-id="a1fff-139">Включение триггера BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="a1fff-139">Turn on your blob trigger</span></span>

<span data-ttu-id="a1fff-140">Теперь, когда мы создали контейнер для мониторинга, запустим нашу функцию таким образом, чтобы мы могли увидеть выходные данные при создании BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="a1fff-140">Now that we've created our container to monitor, let's run our function so we can see output when a blob is created.</span></span>

1. <span data-ttu-id="a1fff-141">Выберите свой триггер BLOB-объектов, чтобы открыть экран кода.</span><span class="sxs-lookup"><span data-stu-id="a1fff-141">Select your blob trigger to open the code screen.</span></span>

1. <span data-ttu-id="a1fff-142">Выберите **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="a1fff-142">Select **Run**.</span></span>

## <a name="create-a-blob"></a><span data-ttu-id="a1fff-143">Создание BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="a1fff-143">Create a blob</span></span>

<span data-ttu-id="a1fff-144">Теперь наш триггер BLOB-объектов запущен и начал прослушивание.</span><span class="sxs-lookup"><span data-stu-id="a1fff-144">Our blob trigger is now up and listening for activity.</span></span> <span data-ttu-id="a1fff-145">Создадим BLOB-объект, чтобы узнавать о получении сообщений журнала.</span><span class="sxs-lookup"><span data-stu-id="a1fff-145">Let's create a blob to see if we get a log message.</span></span>

1. <span data-ttu-id="a1fff-146">В обозревателе службы хранилища выберите контейнер **samples-workitems**.</span><span class="sxs-lookup"><span data-stu-id="a1fff-146">In Storage explorer, select the **samples-workitems** container.</span></span>

1. <span data-ttu-id="a1fff-147">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="a1fff-147">Select **Upload**.</span></span> 

1. <span data-ttu-id="a1fff-148">Выберите **Передать файлы**.</span><span class="sxs-lookup"><span data-stu-id="a1fff-148">Select **Upload Files**.</span></span>

1. <span data-ttu-id="a1fff-149">Выберите любой файл на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="a1fff-149">Select any file from your computer.</span></span>

1. <span data-ttu-id="a1fff-150">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="a1fff-150">Select **Upload**.</span></span>

1. <span data-ttu-id="a1fff-151">Вернитесь в Azure.</span><span class="sxs-lookup"><span data-stu-id="a1fff-151">Go back to Azure.</span></span> <span data-ttu-id="a1fff-152">Проверьте журналы на наличие сообщения, которое показывает, какой файл был отправлен.</span><span class="sxs-lookup"><span data-stu-id="a1fff-152">Check your logs for a message that displays what file was uploaded.</span></span>

## <a name="clean-up"></a><span data-ttu-id="a1fff-153">Очистка</span><span class="sxs-lookup"><span data-stu-id="a1fff-153">Clean up</span></span>

<span data-ttu-id="a1fff-154">Чтобы с вас не взимали плату за эту функцию, нажмите кнопку **Пауза**, которая находится выше в окне журнала.</span><span class="sxs-lookup"><span data-stu-id="a1fff-154">To ensure that you aren't charged for this function, select **Pause** above the log window.</span></span>

![Приостановить](../media/4-pause-timer.png)


