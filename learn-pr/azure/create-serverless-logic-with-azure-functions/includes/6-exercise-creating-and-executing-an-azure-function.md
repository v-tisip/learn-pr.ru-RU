<span data-ttu-id="dc5b1-101">В этом упражнении мы продолжим работать с примером привода и добавим логику для службы контроля температуры.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-101">In this exercise, we'll continue with our gear drive example and add the logic for the temperature service.</span></span> <span data-ttu-id="dc5b1-102">В частности, мы настроим получение данных по HTTP-запросу.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-102">Specifically, we're going to receive data from an HTTP request.</span></span>

## <a name="function-requirements"></a><span data-ttu-id="dc5b1-103">Требования к функциям</span><span class="sxs-lookup"><span data-stu-id="dc5b1-103">Function requirements</span></span>
<span data-ttu-id="dc5b1-104">Определим некоторые требования для нашей логики:</span><span class="sxs-lookup"><span data-stu-id="dc5b1-104">Let's define some requirements for our logic:</span></span>
- <span data-ttu-id="dc5b1-105">температура от 0 до 25 градусов получает пометку **ОК**;</span><span class="sxs-lookup"><span data-stu-id="dc5b1-105">temperatures between 0-25 should be flagged as **OK**</span></span>
- <span data-ttu-id="dc5b1-106">температура от 26 до 50 градусов получает пометку **ВНИМАНИЕ**;</span><span class="sxs-lookup"><span data-stu-id="dc5b1-106">temperatures between 26-50 should be flagged as **CAUTION**</span></span>
- <span data-ttu-id="dc5b1-107">температура выше 50 градусов получает пометку **ОПАСНОСТЬ**.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-107">temperatures above 50 should be flagged as **DANGER**</span></span>

## <a name="adding-a-function-to-an-azure-function-app"></a><span data-ttu-id="dc5b1-108">Добавление функции в приложение-функцию Azure</span><span class="sxs-lookup"><span data-stu-id="dc5b1-108">Adding a function to an Azure function app</span></span>

<span data-ttu-id="dc5b1-109">Как мы знаем, Azure может помочь нам в изучении принципов работы с функциями Azure.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-109">As we have already learned, Azure provides a helping hand when you're learning how to work with Azure Functions.</span></span> <span data-ttu-id="dc5b1-110">Один из веских доводов в пользу работы с функциями — это создание функции на основе одного из множества шаблонов.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-110">One great feature to get your feet wet with Functions is to generate one using one of many templates.</span></span> <span data-ttu-id="dc5b1-111">В этом упражнении мы воспользуемся шаблоном HttpTrigger для реализации службы контроля температуры.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-111">In this exercise, you will be using the HttpTrigger template to implement the temperature service.</span></span>

1. <span data-ttu-id="dc5b1-112">Войдите на [портал Azure](https://portal.azure.com) с помощью учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-112">Sign in to the [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
1. <span data-ttu-id="dc5b1-113">Перейдите к группе ресурсов, которую вы создали в первом упражнении, выбрав **Все ресурсы** в меню слева, а затем нажмите **escalator-functions-group**.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-113">Access the resource group you created in the first exercise by choosing **All resources** in the left-hand menu, and then selecting **escalator-functions-group**.</span></span>
1. <span data-ttu-id="dc5b1-114">На экране появятся ресурсы в выбранной группе.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-114">The resources for the group will then be displayed.</span></span> <span data-ttu-id="dc5b1-115">Откройте приложение-функцию, созданное в предыдущем упражнении, выбрав элемент **escalator-functions-xxxxxxx** (также обозначается значком со светящейся лампочкой).</span><span class="sxs-lookup"><span data-stu-id="dc5b1-115">Access the function app that you created in the previous exercise by selecting the **escalator-functions-xxxxxxx** item (also indicated by the lightning bolt icon).</span></span>
  <span data-ttu-id="dc5b1-116">![Доступ к приложению-функции](../images/6-access-function-app.png)</span><span class="sxs-lookup"><span data-stu-id="dc5b1-116">![Access the function app](../images/6-access-function-app.png)</span></span>
1. <span data-ttu-id="dc5b1-117">В колонке появятся общие сведения о вашем приложении-функции.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-117">The blade will show an overview of your function app.</span></span> <span data-ttu-id="dc5b1-118">Слева отображается дерево навигации, содержащее только заданные функции, прокси или слоты.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-118">There is also a navigation tree on the left that shows any functions, proxies or slots that are defined.</span></span> <span data-ttu-id="dc5b1-119">Функции у нас еще нет, поэтому здесь будет пусто.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-119">We don't have a function yet, so this  will be empty.</span></span> <span data-ttu-id="dc5b1-120">Чтобы создать функцию, наведите указатель мыши на параметр **Функция** в дереве навигации и нажмите появившуюся кнопку **+**.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-120">To create a function, move your mouse over **Function** in the navigation tree and click  the **+** button that appears.</span></span>
  <span data-ttu-id="dc5b1-121">![Добавление навигации по функциям](../images/5-function-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="dc5b1-121">![Add function navigation](../images/5-function-add-button.png)</span></span>
1. <span data-ttu-id="dc5b1-122">В готовой форме для быстрого создания функций выберите ссылку **Пользовательская функция** в разделе **Самостоятельное создание функции**.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-122">In the quickstart premade function form, select the **Custom function** link in the **Get started on your own** section.</span></span>
  <span data-ttu-id="dc5b1-123">![Готовая форма для создания функций](../images/6-custom-function.png)</span><span class="sxs-lookup"><span data-stu-id="dc5b1-123">![Premade function form](../images/6-custom-function.png)</span></span>
1. <span data-ttu-id="dc5b1-124">На экране появится список шаблонов.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-124">You are now presented with a list of templates.</span></span> <span data-ttu-id="dc5b1-125">Выберите реализацию JavaScript для шаблона триггера HTTP.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-125">Select the JavaScript implementation of the HTTP trigger template.</span></span>
  <span data-ttu-id="dc5b1-126">![Шаблон триггера HTTP](../images/6-httptrigger-template.png)</span><span class="sxs-lookup"><span data-stu-id="dc5b1-126">![HTTP trigger template](../images/6-httptrigger-template.png)</span></span>
1. <span data-ttu-id="dc5b1-127">На экране появится колонка, в которой можно определить, какой будет создан шаблон.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-127">A blade will appear, allowing you to define what the template will generate.</span></span> <span data-ttu-id="dc5b1-128">В данном случае нас интересует создание функции JavaScript с именем **DriveGearTemperatureService**.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-128">In this case, you are interested in generating a JavaScript function named **DriveGearTemperatureService**.</span></span> <span data-ttu-id="dc5b1-129">Присвоив своей функции имя, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-129">After you have named your function, press the **Create** button.</span></span>
  <span data-ttu-id="dc5b1-130">![Создание формы триггера HTTP](../images/6-create-httptrigger-form.png)</span><span class="sxs-lookup"><span data-stu-id="dc5b1-130">![Create HTTP trigger form](../images/6-create-httptrigger-form.png)</span></span>
1. <span data-ttu-id="dc5b1-131">Через несколько секунд на экране появится шаблон исходного кода для функции.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-131">After a few moments, you will be presented with the templated source code for your function.</span></span> <span data-ttu-id="dc5b1-132">Получив ожидаемое имя, функция выдаст сообщение **Hello, {name}**.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-132">The premade function expects a name to be passed in, and it will return **Hello, {name}**.</span></span>

    ```javascript
    module.exports = function (context, req) {
        context.log('JavaScript HTTP trigger function processed a request.');

        if (req.query.name || (req.body && req.body.name)) {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: "Hello " + (req.query.name || req.body.name)
            };
        }
        else {
            context.res = {
                status: 400,
                body: "Please pass a name on the query string or in the request body"
            };
        }
        context.done();
    };
    ```

1. <span data-ttu-id="dc5b1-133">В правой части представления источника вы увидите две вкладки.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-133">On the right-hand side of the source view, you will see two tabs.</span></span> <span data-ttu-id="dc5b1-134">Все поддерживающие функцию файлы можно увидеть на вкладке **Просмотр файлов**. Чтобы просмотреть конфигурацию функции, выберите файл **function.json**.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-134">You are able to view all the files supporting the function in the **View files** tab. You can select **function.json** to view the configuration of the function.</span></span> <span data-ttu-id="dc5b1-135">Здесь вы увидите заданный триггер HTTP, а также выходную привязку.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-135">Here you can see the httpTrigger defined, as well as the output binding.</span></span> <span data-ttu-id="dc5b1-136">Эта конфигурация показывает, что функция инициируется HTTP-запросом, а выходная привязка показывает, что ответ будет отправлен как HTTP-ответ.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-136">This configuration describes that the function is initiated by an HTTP request, and the output binding describes that the response will be sent as an HTTP response.</span></span>

    ```javascript
    {
      "disabled": false,
      "bindings": [
        {
          "authLevel": "function",
          "type": "httpTrigger",
          "direction": "in",
          "name": "req"
        },
        {
          "type": "http",
          "direction": "out",
          "name": "res"
        }
      ]
    }
    ```

## <a name="running-the-premade-azure-function"></a><span data-ttu-id="dc5b1-137">Запуск готовой функции Azure</span><span class="sxs-lookup"><span data-stu-id="dc5b1-137">Running the premade Azure function</span></span>

<span data-ttu-id="dc5b1-138">Чтобы запустить функцию, можно инициировать HTTP-запрос из cURL через командную строку.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-138">To run the function, you can initiate an HTTP request from cURL from a command prompt.</span></span> <span data-ttu-id="dc5b1-139">Чтобы найти URL-адрес конечной точки, вернитесь к коду функции и выберите ссылку **Получить URL-адрес функции**.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-139">To find the endpoint URL, return to your function code and select the **Get function URL** link.</span></span> <span data-ttu-id="dc5b1-140">Скопируйте эту ссылку в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-140">Copy this link to your clipboard.</span></span>  <span data-ttu-id="dc5b1-141">URL-адрес должен выглядеть следующим образом: https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg== ![Получить URL-адрес конечной точки](../images/6-get-function-url.png)</span><span class="sxs-lookup"><span data-stu-id="dc5b1-141">Your URL should look something similar to the following: https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg== ![Get endpoint URL](../images/6-get-function-url.png)</span></span>

<span data-ttu-id="dc5b1-142">С помощью этого URL-адреса выполните команду cURL, чтобы инициировать функцию (заменив полученный URL-адрес на собственный):</span><span class="sxs-lookup"><span data-stu-id="dc5b1-142">With that URL, run a cURL command to initiate your function (replacing the URL with your own):</span></span>

```bash
curl --header "Content-Type: application/json" --request POST --data "{\"name\": \"Azure Function\"}" https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg==
```

![cURL-ответ готовой функции](../images/6-premadefunction-curl.png)

## <a name="adding-business-logic-to-the-function"></a><span data-ttu-id="dc5b1-144">Добавление бизнес-логики в функцию</span><span class="sxs-lookup"><span data-stu-id="dc5b1-144">Adding business logic to the function</span></span>

<span data-ttu-id="dc5b1-145">Наша функция ожидает от клиента массив показаний температуры.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-145">Our function is expecting an array of temperature readings from the customer.</span></span> <span data-ttu-id="dc5b1-146">Вот пример текста запроса:</span><span class="sxs-lookup"><span data-stu-id="dc5b1-146">This is an example of the request body:</span></span>

```javascript
{
    "readings": [
        {
            "driveGearId": 1,
            "timestamp": 1534263995,
            "temperature": 23
        },
        {
            "driveGearId": 3,
            "timestamp": 1534264048,
            "temperature": 45
        },
        {
            "driveGearId": 18,
            "timestamp": 1534264050,
            "temperature": 55
        }
    ]
}
```

<span data-ttu-id="dc5b1-147">Измените код готовой функции таким образом, чтобы реализовать необходимую бизнес-логику.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-147">Modify the premade function code to implement the required business logic.</span></span> <span data-ttu-id="dc5b1-148">Откройте файл index.js и замените его следующим списком:</span><span class="sxs-lookup"><span data-stu-id="dc5b1-148">Open the index.js file, and replace it with the following listing:</span></span>

```javascript
module.exports = function (context, req) {
    context.log('Drive Gear Temperature Service triggered');
    if (req.body && req.body.readings) {
        for(var i=0; i<req.body.readings.length; i++){
            var reading = req.body.readings[i];
            if(reading.temperature<=25){
                context.log('Reading is OK');
                reading.status = 'OK';
                continue;
            }
            if(reading.temperature<=50){
                context.log('Reading is CAUTION');
                reading.status = 'CAUTION';
                continue;
            }
            context.log('Reading is DANGER');
            reading.status = 'DANGER'
        }
        context.res = {
            // status: 200, /* Defaults to 200 */
            body: {
                "readings": req.body.readings
            }
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please send an array of readings in the request body"
        };
    }
    context.done();
};
```

<span data-ttu-id="dc5b1-149">Обратите внимание на операторы журнала.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-149">Notice the log statements.</span></span> <span data-ttu-id="dc5b1-150">При выполнении функции они будут добавлять сообщения в окне журнала.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-150">When the function runs, they will add messages in the log window.</span></span>

## <a name="testing-your-business-logic"></a><span data-ttu-id="dc5b1-151">Тестирование бизнес-логики</span><span class="sxs-lookup"><span data-stu-id="dc5b1-151">Testing your business logic</span></span>

<span data-ttu-id="dc5b1-152">Откройте тестовое окно из всплывающего меню справа и вставьте приведенный выше пример запроса в текстовом поле для тела запроса.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-152">Open the test window from the right-hand side flyout menu, and paste the sample request from above into the request body text box.</span></span> <span data-ttu-id="dc5b1-153">Нажмите кнопку **Выполнить** и просмотрите выходные данные.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-153">Press the **Run** button and view the output.</span></span> <span data-ttu-id="dc5b1-154">Можно также открыть окно журнала из нижнего всплывающего меню, чтобы увидеть операторы ведения журнала в журнале.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-154">You can also open the log window from the bottom flyout menu to see the logging statements in the log.</span></span>
<span data-ttu-id="dc5b1-155">![Тестирование бизнес-логики](../images/6-portal-testing.png). По данным JSON в окне выходных данных видно, что к каждому из показаний было правильно добавлено наше поле состояния температуры.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-155">![Testing the business Logic](../images/6-portal-testing.png) You can see from the JSON data in the output window that our temperature status field has been added to each of the readings correctly.</span></span> <span data-ttu-id="dc5b1-156">На панели мониторинга монитора можно также увидеть, что запрос была записан в журнал Application Insights.</span><span class="sxs-lookup"><span data-stu-id="dc5b1-156">You may also visit the Monitor dashboard to see that the request has been logged to Application Insights.</span></span>
<span data-ttu-id="dc5b1-157">![Запрос в Application Insights](../images/6-app-insights.png)</span><span class="sxs-lookup"><span data-stu-id="dc5b1-157">![Request in Application Insights](../images/6-app-insights.png)</span></span>
