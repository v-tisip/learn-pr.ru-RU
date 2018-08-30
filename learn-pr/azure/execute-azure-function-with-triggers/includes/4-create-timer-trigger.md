<span data-ttu-id="f38d9-101">В этом упражнении мы создадим функцию Azure, которая вызывается каждые 20 секунд с помощью триггера таймера.</span><span class="sxs-lookup"><span data-stu-id="f38d9-101">In this exercise, we create an Azure function that's invoked every 20 seconds using a timer trigger.</span></span>

> [!NOTE] 
> <span data-ttu-id="f38d9-102">Чтобы выполнить это упражнение, войдите на [портал Azure](https://portal.azure.com?azure-portal=true) с действующей учетной записью.</span><span class="sxs-lookup"><span data-stu-id="f38d9-102">To complete this exercise, make sure you're logged into the [Azure portal](https://portal.azure.com?azure-portal=true) with a valid account.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="f38d9-103">Создание функции Azure</span><span class="sxs-lookup"><span data-stu-id="f38d9-103">Create an Azure function</span></span>

<span data-ttu-id="f38d9-104">Давайте сначала создадим функцию Azure на портале.</span><span class="sxs-lookup"><span data-stu-id="f38d9-104">Let’s start by creating an Azure Function in the portal.</span></span>

1. <span data-ttu-id="f38d9-105">В области навигации слева выберите **Создать ресурс**.</span><span class="sxs-lookup"><span data-stu-id="f38d9-105">In the left navigation, select **Create a resource**.</span></span>

2. <span data-ttu-id="f38d9-106">Выберите **Вычисления**.</span><span class="sxs-lookup"><span data-stu-id="f38d9-106">Select **Compute**.</span></span>

3. <span data-ttu-id="f38d9-107">Найдите и выберите **Приложение-функция**.</span><span class="sxs-lookup"><span data-stu-id="f38d9-107">Locate and select **Function App**.</span></span> <span data-ttu-id="f38d9-108">Для поиска шаблона также можно использовать панель поиска.</span><span class="sxs-lookup"><span data-stu-id="f38d9-108">You can also optionally use the search bar to locate the template.</span></span>

    ![Выбор приложения-функции](../media-drafts/4-click-function-app.png)

4. <span data-ttu-id="f38d9-110">Введите уникальное **Имя приложения**.</span><span class="sxs-lookup"><span data-stu-id="f38d9-110">Enter a unique **App name**.</span></span>

5. <span data-ttu-id="f38d9-111">Выберите **подписку**.</span><span class="sxs-lookup"><span data-stu-id="f38d9-111">Select a **Subscription**.</span></span>

6. <span data-ttu-id="f38d9-112">Создайте **группу ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="f38d9-112">Create a new **Resource Group**.</span></span>

7. <span data-ttu-id="f38d9-113">Выберите **Windows** в качестве **ОС**.</span><span class="sxs-lookup"><span data-stu-id="f38d9-113">Choose **Windows** as your **OS**.</span></span>

8. <span data-ttu-id="f38d9-114">Выберите **План потребления** для параметра **План размещения**.</span><span class="sxs-lookup"><span data-stu-id="f38d9-114">Choose **Consumption Plan** for your **Hosting Plan**.</span></span> <span data-ttu-id="f38d9-115">Плата взимается за каждое выполнение функции.</span><span class="sxs-lookup"><span data-stu-id="f38d9-115">You're charged for each execution of your function.</span></span> <span data-ttu-id="f38d9-116">Ресурсы выделяются автоматически на основе рабочей нагрузки приложения.</span><span class="sxs-lookup"><span data-stu-id="f38d9-116">Resources are automatically allocated based on your application workload.</span></span>

9. <span data-ttu-id="f38d9-117">Выберите **расположение**.</span><span class="sxs-lookup"><span data-stu-id="f38d9-117">Select a **Location**.</span></span>

10. <span data-ttu-id="f38d9-118">Создайте учетную запись **Службы хранилища**. Вы можете указать для нее любое имя, но по умолчанию оно совпадает с именем приложения.</span><span class="sxs-lookup"><span data-stu-id="f38d9-118">Create a new **Storage** account, you can change the name if you like - it will default to a variation of the App name</span></span>

11. <span data-ttu-id="f38d9-119">Отключите **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="f38d9-119">Turn off **Application Insights**.</span></span>

12. <span data-ttu-id="f38d9-120">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f38d9-120">Select **Create**.</span></span> <span data-ttu-id="f38d9-121">Создание займет несколько минут. Вы можете следить за значком **Уведомления** на панели инструментов — для созданного ресурса здесь появится кнопка, открывающая его на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f38d9-121">This will take a few minutes to complete, you can watch the **Notifications** icon in the toolbar area - once it has finished creating the resource it will have a button there to open it in the Azure Portal.</span></span>

## <a name="create-a-timer-trigger"></a><span data-ttu-id="f38d9-122">Создание триггера таймера</span><span class="sxs-lookup"><span data-stu-id="f38d9-122">Create a timer trigger</span></span>

<span data-ttu-id="f38d9-123">Сейчас мы создадим триггер таймера внутри нашей функции Azure.</span><span class="sxs-lookup"><span data-stu-id="f38d9-123">Now we're going to create a timer trigger inside our Azure function.</span></span>

1. <span data-ttu-id="f38d9-124">После создания функции Azure выберите **Все ресурсы** в левой области навигации.</span><span class="sxs-lookup"><span data-stu-id="f38d9-124">After the Azure function is created, select **All resources** from the left navigation.</span></span>

2. <span data-ttu-id="f38d9-125">Найдите и выберите функцию Azure.</span><span class="sxs-lookup"><span data-stu-id="f38d9-125">Locate and select your Azure function.</span></span>

3. <span data-ttu-id="f38d9-126">В новой колонке наведите указатель мыши на параметр **Функции** и выберите значок со знаком плюс (+).</span><span class="sxs-lookup"><span data-stu-id="f38d9-126">On the new blade, point to **Functions** and select the plus (+) icon.</span></span>

    ![Наведите указатель мыши на параметр "Функции" и нажмите на значок плюса](../media-drafts/4-hover-function.png)

4. <span data-ttu-id="f38d9-128">Выберите **Таймер**.</span><span class="sxs-lookup"><span data-stu-id="f38d9-128">Select **Timer**.</span></span>

5. <span data-ttu-id="f38d9-129">В качестве языка выберите **CSharp**.</span><span class="sxs-lookup"><span data-stu-id="f38d9-129">Select **CSharp** as the language.</span></span>

6. <span data-ttu-id="f38d9-130">Выберите **Создать эту функцию**.</span><span class="sxs-lookup"><span data-stu-id="f38d9-130">Select **Create this function**.</span></span>

## <a name="configure-the-timer-trigger"></a><span data-ttu-id="f38d9-131">Настройка триггера таймера</span><span class="sxs-lookup"><span data-stu-id="f38d9-131">Configure the timer trigger</span></span>

<span data-ttu-id="f38d9-132">У нас есть функция Azure с логикой для вывода сообщения в окне журнала.</span><span class="sxs-lookup"><span data-stu-id="f38d9-132">We have an Azure function with logic to print a message to the log window.</span></span> <span data-ttu-id="f38d9-133">Мы собираемся настроить расписание таймера для выполнения каждые 20 секунд.</span><span class="sxs-lookup"><span data-stu-id="f38d9-133">We're going to set the schedule of the timer to execute every 20 seconds.</span></span>

1. <span data-ttu-id="f38d9-134">Выберите **Интеграция**.</span><span class="sxs-lookup"><span data-stu-id="f38d9-134">Select **Integrate**.</span></span>

2. <span data-ttu-id="f38d9-135">В поле **Расписание** введите следующее значение:</span><span class="sxs-lookup"><span data-stu-id="f38d9-135">Enter the following value into the **Schedule** box:</span></span>

    ```
    */20 * * * * *
    ```

3. <span data-ttu-id="f38d9-136">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f38d9-136">Select **Save**.</span></span>

## <a name="start-the-timer"></a><span data-ttu-id="f38d9-137">Запуск таймера</span><span class="sxs-lookup"><span data-stu-id="f38d9-137">Start the timer</span></span>

<span data-ttu-id="f38d9-138">Теперь, когда таймер настроен, мы готовы запустить его.</span><span class="sxs-lookup"><span data-stu-id="f38d9-138">Now that we've configured the timer, we're ready to start it.</span></span>

1. <span data-ttu-id="f38d9-139">Выберите **TimerTriggerCSharp1**.</span><span class="sxs-lookup"><span data-stu-id="f38d9-139">Select **TimerTriggerCSharp1**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="f38d9-140">**TimerTriggerCSharp1** — это имя по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f38d9-140">**TimerTriggerCSharp1** is a default name.</span></span> <span data-ttu-id="f38d9-141">Оно выбирается автоматически при создании триггера.</span><span class="sxs-lookup"><span data-stu-id="f38d9-141">It's automatically selected when you create the trigger.</span></span>

2. <span data-ttu-id="f38d9-142">Выберите **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="f38d9-142">Select **Run**.</span></span> 

<span data-ttu-id="f38d9-143">На этом этапе вы должны видеть в окне журнала сообщение, отображаемое каждые 20 секунд.</span><span class="sxs-lookup"><span data-stu-id="f38d9-143">At this point, you should see a message every 20 seconds in the log window.</span></span>

## <a name="clean-up"></a><span data-ttu-id="f38d9-144">Очистка</span><span class="sxs-lookup"><span data-stu-id="f38d9-144">Clean up</span></span>

<span data-ttu-id="f38d9-145">Чтобы с вас не взимали плату за эту функцию, остановите таймер, нажав кнопку **Пауза**, которая находится над окном журнала.</span><span class="sxs-lookup"><span data-stu-id="f38d9-145">To ensure that you aren't charged for this function, above the log window, select **Pause** to stop the timer.</span></span>

![Приостановить](../media-drafts/4-pause-timer.png)


