<span data-ttu-id="22b6b-101">В этом упражнении мы создадим функцию Azure, которая принимает HTTP-запрос одной строкой.</span><span class="sxs-lookup"><span data-stu-id="22b6b-101">In this exercise, we're going to create an Azure function that accepts an HTTP request with a single string.</span></span> <span data-ttu-id="22b6b-102">Эта функция возвращает строку вызывающему объекту, сообщая, таким образом, об успешном или неудачном выполнении.</span><span class="sxs-lookup"><span data-stu-id="22b6b-102">The function returns a string back to the caller to represent success or failure.</span></span>

> [!NOTE]
> <span data-ttu-id="22b6b-103">Чтобы выполнить это упражнение, войдите на [портал Azure](https://portal.azure.com?azure-portal=true) с действующей учетной записью.</span><span class="sxs-lookup"><span data-stu-id="22b6b-103">To complete this exercise, make sure you're signed into the [Azure portal](https://portal.azure.com?azure-portal=true) with a valid account.</span></span>

## <a name="create-an-http-trigger"></a><span data-ttu-id="22b6b-104">Создание триггера HTTP</span><span class="sxs-lookup"><span data-stu-id="22b6b-104">Create an HTTP trigger</span></span>

<span data-ttu-id="22b6b-105">В уже существующее приложение функций Azure добавим триггер HTTP.</span><span class="sxs-lookup"><span data-stu-id="22b6b-105">Let's continue using our existing Azure Functions application and add an HTTP trigger.</span></span>

1. <span data-ttu-id="22b6b-106">Наведите указатель мыши на параметр **Функции** и нажмите на значок плюса (+).</span><span class="sxs-lookup"><span data-stu-id="22b6b-106">Point to **Functions** and select the plus (+) icon.</span></span>

    ![Наведите указатель мыши на параметр "Функции" и нажмите на плюс](../media-drafts/4-hover-function.png)

2. <span data-ttu-id="22b6b-108">Выберите **Триггер HTTP**.</span><span class="sxs-lookup"><span data-stu-id="22b6b-108">Select **HTTP trigger**.</span></span>

3. <span data-ttu-id="22b6b-109">В качестве языка выберите **C#**.</span><span class="sxs-lookup"><span data-stu-id="22b6b-109">Select **C#** as the language.</span></span> 

4. <span data-ttu-id="22b6b-110">Оставьте в поле **Имя** значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="22b6b-110">Leave the **Name** set to the default value.</span></span>

5. <span data-ttu-id="22b6b-111">В поле **Уровень авторизации** выберите **Анонимный**.</span><span class="sxs-lookup"><span data-stu-id="22b6b-111">Set the **Authorization level** to **Anonymous**.</span></span>

6. <span data-ttu-id="22b6b-112">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="22b6b-112">Select **Create**.</span></span>

7. <span data-ttu-id="22b6b-113">Просмотрите автоматически созданный код, чтобы получить представление о происходящем.</span><span class="sxs-lookup"><span data-stu-id="22b6b-113">Take a quick look at the auto-generated code to get an idea about what's going on.</span></span> <span data-ttu-id="22b6b-114">Параметр *req* представляет входящий запрос и содержит параметр *name*.</span><span class="sxs-lookup"><span data-stu-id="22b6b-114">The *req* parameter represents the incoming request and contains a *name* parameter.</span></span> <span data-ttu-id="22b6b-115">Проверим, имеет ли параметр *name* какое-либо значение.</span><span class="sxs-lookup"><span data-stu-id="22b6b-115">We check to see if *name* has a value.</span></span> <span data-ttu-id="22b6b-116">Если значение есть, возвращается приветствие.</span><span class="sxs-lookup"><span data-stu-id="22b6b-116">If it does, we return a greeting.</span></span> <span data-ttu-id="22b6b-117">В противном случае возвращается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="22b6b-117">Otherwise, we return an error message.</span></span>

## <a name="get-your-function-url"></a><span data-ttu-id="22b6b-118">Получение URL-адреса функции</span><span class="sxs-lookup"><span data-stu-id="22b6b-118">Get your function URL</span></span>

<span data-ttu-id="22b6b-119">Теперь, когда мы создали триггер HTTP, получим URL-адрес функции, чтобы приступить к подаче запроса.</span><span class="sxs-lookup"><span data-stu-id="22b6b-119">Now that we've created the HTTP trigger, let's get the function URL so we can begin to make a request.</span></span>

1. <span data-ttu-id="22b6b-120">Выберите свой триггер HTTP, чтобы открыть экран кода.</span><span class="sxs-lookup"><span data-stu-id="22b6b-120">Select your HTTP trigger to open the code screen.</span></span>

2. <span data-ttu-id="22b6b-121">Справа от параметра **Выполнить** выберите **Получить URL-адрес функции**.</span><span class="sxs-lookup"><span data-stu-id="22b6b-121">To the right of **Run**, select **Get function URL**.</span></span>

3. <span data-ttu-id="22b6b-122">Нажмите **Копировать**.</span><span class="sxs-lookup"><span data-stu-id="22b6b-122">Select **Copy**.</span></span>

4. <span data-ttu-id="22b6b-123">Нажмите **Выполнить**, чтобы запустить функцию.</span><span class="sxs-lookup"><span data-stu-id="22b6b-123">Select **Run** to start your function.</span></span>

## <a name="issue-a-get-request-to-your-http-trigger"></a><span data-ttu-id="22b6b-124">Передача запроса GET в триггер HTTP</span><span class="sxs-lookup"><span data-stu-id="22b6b-124">Issue a GET request to your HTTP trigger</span></span>

<span data-ttu-id="22b6b-125">Теперь URL-адрес функции скопирован в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="22b6b-125">We now have our function URL copied to our clipboard.</span></span> <span data-ttu-id="22b6b-126">Передадим запрос GET, чтобы узнать, получим ли мы ответ.</span><span class="sxs-lookup"><span data-stu-id="22b6b-126">Let's issue a GET request to see if we get a response.</span></span>

1. <span data-ttu-id="22b6b-127">Откройте новую вкладку в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="22b6b-127">Open a new tab in your web browser.</span></span>

2. <span data-ttu-id="22b6b-128">Вставьте URL-адрес в адресную строку.</span><span class="sxs-lookup"><span data-stu-id="22b6b-128">Paste the URL into the address bar.</span></span>

3. <span data-ttu-id="22b6b-129">Добавьте параметр строки запроса, в котором параметр *name* имеет указанное вами имя, например: `.../api/HttpTriggerCSharp1?name=Jesse`</span><span class="sxs-lookup"><span data-stu-id="22b6b-129">Add a query string parameter called *name* with your name for example `.../api/HttpTriggerCSharp1?name=Jesse`</span></span>

4. <span data-ttu-id="22b6b-130">Нажмите клавишу ВВОД, чтобы отправить запрос.</span><span class="sxs-lookup"><span data-stu-id="22b6b-130">Select ENTER to submit the request.</span></span>

## <a name="clean-up"></a><span data-ttu-id="22b6b-131">Очистка</span><span class="sxs-lookup"><span data-stu-id="22b6b-131">Clean up</span></span>

<span data-ttu-id="22b6b-132">Чтобы с вас не взимали плату за эту функцию, нажмите кнопку **Пауза**, которая находится выше в окне журнала.</span><span class="sxs-lookup"><span data-stu-id="22b6b-132">To ensure that you aren't charged for this function, select **Pause** above the log window.</span></span>

![Приостановить](../media-drafts/4-pause-timer.png)