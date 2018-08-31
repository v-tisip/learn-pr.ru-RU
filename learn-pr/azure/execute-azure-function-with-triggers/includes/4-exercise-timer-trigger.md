<span data-ttu-id="be795-101">В этом упражнении мы создадим функцию Azure, которая вызывается каждые 20 секунд с помощью триггера таймера.</span><span class="sxs-lookup"><span data-stu-id="be795-101">In this exercise, we create an Azure function that's invoked every 20 seconds using a timer trigger.</span></span>

> [!NOTE] 
> <span data-ttu-id="be795-102">Чтобы выполнить это упражнение, войдите на [портал Azure](https://portal.azure.com/) под действующей учетной записью.</span><span class="sxs-lookup"><span data-stu-id="be795-102">To complete this exercise, make sure you're logged into the [Azure portal](https://portal.azure.com/) with a valid account.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="be795-103">Создание функции Azure</span><span class="sxs-lookup"><span data-stu-id="be795-103">Create an Azure function</span></span>

<span data-ttu-id="be795-104">Давайте сначала создадим функцию Azure на портале.</span><span class="sxs-lookup"><span data-stu-id="be795-104">Let’s start by creating an Azure function in the portal.</span></span>

1. <span data-ttu-id="be795-105">В левой области навигации выберите **Создать ресурс**.</span><span class="sxs-lookup"><span data-stu-id="be795-105">In the left navigation, select **Create a resource**.</span></span>

1. <span data-ttu-id="be795-106">Выберите **Вычисления**.</span><span class="sxs-lookup"><span data-stu-id="be795-106">Select **Compute**.</span></span>

1. <span data-ttu-id="be795-107">Найдите и выберите **Приложение-функция**.</span><span class="sxs-lookup"><span data-stu-id="be795-107">Locate and select **Function App**.</span></span> <span data-ttu-id="be795-108">Для поиска шаблона также можно использовать панель поиска.</span><span class="sxs-lookup"><span data-stu-id="be795-108">You can also optionally use the search bar to locate the template.</span></span>

    ![Выбор приложения-функции](../media-drafts/4-click-function-app.png)

1. <span data-ttu-id="be795-110">Введите уникальное **Имя приложения**.</span><span class="sxs-lookup"><span data-stu-id="be795-110">Enter a unique **App name**.</span></span>

1. <span data-ttu-id="be795-111">Выберите **подписку**.</span><span class="sxs-lookup"><span data-stu-id="be795-111">Select a **Subscription**.</span></span>

1. <span data-ttu-id="be795-112">Создайте **группу ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="be795-112">Create a new **Resource Group**.</span></span>

1. <span data-ttu-id="be795-113">Выберите **Windows** в качестве **ОС**.</span><span class="sxs-lookup"><span data-stu-id="be795-113">Choose **Windows** as your **OS**.</span></span>

1. <span data-ttu-id="be795-114">Выберите **План потребления** для параметра **План размещения**.</span><span class="sxs-lookup"><span data-stu-id="be795-114">Choose **Consumption Plan** for your **Hosting Plan**.</span></span> <span data-ttu-id="be795-115">Плата взимается за каждое выполнение функции.</span><span class="sxs-lookup"><span data-stu-id="be795-115">You're charged for each execution of your function.</span></span> <span data-ttu-id="be795-116">Ресурсы выделяются автоматически на основе рабочей нагрузки приложения.</span><span class="sxs-lookup"><span data-stu-id="be795-116">Resources are automatically allocated based on your application workload.</span></span>

1. <span data-ttu-id="be795-117">Выберите **расположение**.</span><span class="sxs-lookup"><span data-stu-id="be795-117">Select a **Location**.</span></span>

1. <span data-ttu-id="be795-118">Создайте учетную запись **хранения**.</span><span class="sxs-lookup"><span data-stu-id="be795-118">Create a new **Storage** account.</span></span> <span data-ttu-id="be795-119">(Это значение является обязательным, но мы не будем его использовать.)</span><span class="sxs-lookup"><span data-stu-id="be795-119">(This value is required, but we're not going to use it.)</span></span>

1. <span data-ttu-id="be795-120">Отключите **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="be795-120">Turn off **Application Insights**.</span></span>

1. <span data-ttu-id="be795-121">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="be795-121">Select **Create**.</span></span>

## <a name="create-a-timer-trigger"></a><span data-ttu-id="be795-122">Создание триггера таймера</span><span class="sxs-lookup"><span data-stu-id="be795-122">Create a timer trigger</span></span>

<span data-ttu-id="be795-123">Сейчас мы создадим триггер таймера внутри нашей функции Azure.</span><span class="sxs-lookup"><span data-stu-id="be795-123">Now we're going to create a timer trigger inside our Azure function.</span></span>

1. <span data-ttu-id="be795-124">После создания функции Azure выберите **Все ресурсы** в левой области навигации.</span><span class="sxs-lookup"><span data-stu-id="be795-124">After the Azure function is created, select **All resources** from the left navigation.</span></span>

1. <span data-ttu-id="be795-125">Найдите и выберите функцию Azure.</span><span class="sxs-lookup"><span data-stu-id="be795-125">Locate and select your Azure function.</span></span>

1. <span data-ttu-id="be795-126">В новой колонке наведите указатель мыши на параметр **Функции** и выберите значок со знаком плюс (+).</span><span class="sxs-lookup"><span data-stu-id="be795-126">On the new blade, point to **Functions** and select the plus (+) icon.</span></span>

    ![Наведите указатель мыши на параметр "Функции" и нажмите на значок плюса](../media-drafts/4-hover-function.png)

1. <span data-ttu-id="be795-128">Выберите **Таймер**.</span><span class="sxs-lookup"><span data-stu-id="be795-128">Select **Timer**.</span></span>

1. <span data-ttu-id="be795-129">В качестве языка выберите **CSharp**.</span><span class="sxs-lookup"><span data-stu-id="be795-129">Select **CSharp** as the language.</span></span>

1. <span data-ttu-id="be795-130">Выберите **Создать эту функцию**.</span><span class="sxs-lookup"><span data-stu-id="be795-130">Select **Create this function**.</span></span>

## <a name="configure-the-timer-trigger"></a><span data-ttu-id="be795-131">Настройка триггера таймера</span><span class="sxs-lookup"><span data-stu-id="be795-131">Configure the timer trigger</span></span>

<span data-ttu-id="be795-132">У нас есть функция Azure с логикой для вывода сообщения в окне журнала.</span><span class="sxs-lookup"><span data-stu-id="be795-132">We have an Azure function with logic to print a message to the log window.</span></span> <span data-ttu-id="be795-133">Мы собираемся настроить расписание таймера для выполнения каждые 20 секунд.</span><span class="sxs-lookup"><span data-stu-id="be795-133">We're going to set the schedule of the timer to execute every 20 seconds.</span></span>

1. <span data-ttu-id="be795-134">Выберите **Интеграция**.</span><span class="sxs-lookup"><span data-stu-id="be795-134">Select **Integrate**.</span></span>

1. <span data-ttu-id="be795-135">В поле **Расписание** введите следующее значение:</span><span class="sxs-lookup"><span data-stu-id="be795-135">Enter the following value into the **Schedule** box:</span></span>

    ```
    */20 * * * * *
    ```

1. <span data-ttu-id="be795-136">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="be795-136">Select **Save**.</span></span>

## <a name="start-the-timer"></a><span data-ttu-id="be795-137">Запуск таймера</span><span class="sxs-lookup"><span data-stu-id="be795-137">Start the timer</span></span>

<span data-ttu-id="be795-138">Теперь, когда таймер настроен, мы готовы запустить его.</span><span class="sxs-lookup"><span data-stu-id="be795-138">Now that we've configured the timer, we're ready to start it.</span></span>

1. <span data-ttu-id="be795-139">Выберите **TimerTriggerCSharp1**.</span><span class="sxs-lookup"><span data-stu-id="be795-139">Select **TimerTriggerCSharp1**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="be795-140">**TimerTriggerCSharp1** — это имя по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="be795-140">**TimerTriggerCSharp1** is a default name.</span></span> <span data-ttu-id="be795-141">Оно выбирается автоматически при создании триггера.</span><span class="sxs-lookup"><span data-stu-id="be795-141">It's automatically selected when you create the trigger.</span></span>

1. <span data-ttu-id="be795-142">Выберите **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="be795-142">Select **Run**.</span></span> 

<span data-ttu-id="be795-143">На этом этапе вы должны видеть в окне журнала сообщение, отображаемое каждые 20 секунд.</span><span class="sxs-lookup"><span data-stu-id="be795-143">At this point, you should see a message every 20 seconds in the log window.</span></span>

## <a name="clean-up"></a><span data-ttu-id="be795-144">Очистка</span><span class="sxs-lookup"><span data-stu-id="be795-144">Clean up</span></span>

<span data-ttu-id="be795-145">Чтобы с вас не взимали плату за эту функцию, остановите таймер, нажав кнопку **Пауза**, которая находится над окном журнала.</span><span class="sxs-lookup"><span data-stu-id="be795-145">To ensure that you aren't charged for this function, above the log window, select **Pause** to stop the timer.</span></span>

![Приостановить](../media-drafts/4-pause-timer.png)


