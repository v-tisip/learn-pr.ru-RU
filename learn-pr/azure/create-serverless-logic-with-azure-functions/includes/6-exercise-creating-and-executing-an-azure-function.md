В этом упражнении мы продолжим работать с примером привода и добавим логику для службы контроля температуры. В частности, мы настроим получение данных по HTTP-запросу.

## <a name="function-requirements"></a>Требования к функциям
Определим некоторые требования для нашей логики:
- температура от 0 до 25 градусов получает пометку **ОК**;
- температура от 26 до 50 градусов получает пометку **ВНИМАНИЕ**;
- температура выше 50 градусов получает пометку **ОПАСНОСТЬ**.

## <a name="adding-a-function-to-an-azure-function-app"></a>Добавление функции в приложение-функцию Azure

Как мы знаем, Azure может помочь нам в изучении принципов работы с функциями Azure. Один из веских доводов в пользу работы с функциями — это создание функции на основе одного из множества шаблонов. В этом упражнении мы воспользуемся шаблоном HttpTrigger для реализации службы контроля температуры.

1. Войдите на [портал Azure](https://portal.azure.com) с помощью учетной записи Azure.
1. Перейдите к группе ресурсов, которую вы создали в первом упражнении, выбрав **Все ресурсы** в меню слева, а затем нажмите **escalator-functions-group**.
1. На экране появятся ресурсы в выбранной группе. Откройте приложение-функцию, созданное в предыдущем упражнении, выбрав элемент **escalator-functions-xxxxxxx** (также обозначается значком со светящейся лампочкой).
  ![Доступ к приложению-функции](../images/6-access-function-app.png)
1. В колонке появятся общие сведения о вашем приложении-функции. Слева отображается дерево навигации, содержащее только заданные функции, прокси или слоты. Функции у нас еще нет, поэтому здесь будет пусто. Чтобы создать функцию, наведите указатель мыши на параметр **Функция** в дереве навигации и нажмите появившуюся кнопку **+**.
  ![Добавление навигации по функциям](../images/5-function-add-button.png)
1. В готовой форме для быстрого создания функций выберите ссылку **Пользовательская функция** в разделе **Самостоятельное создание функции**.
  ![Готовая форма для создания функций](../images/6-custom-function.png)
1. На экране появится список шаблонов. Выберите реализацию JavaScript для шаблона триггера HTTP.
  ![Шаблон триггера HTTP](../images/6-httptrigger-template.png)
1. На экране появится колонка, в которой можно определить, какой будет создан шаблон. В данном случае нас интересует создание функции JavaScript с именем **DriveGearTemperatureService**. Присвоив своей функции имя, нажмите кнопку **Создать**.
  ![Создание формы триггера HTTP](../images/6-create-httptrigger-form.png)
1. Через несколько секунд на экране появится шаблон исходного кода для функции. Получив ожидаемое имя, функция выдаст сообщение **Hello, {name}**.

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

1. В правой части представления источника вы увидите две вкладки. Все поддерживающие функцию файлы можно увидеть на вкладке **Просмотр файлов**. Чтобы просмотреть конфигурацию функции, выберите файл **function.json**. Здесь вы увидите заданный триггер HTTP, а также выходную привязку. Эта конфигурация показывает, что функция инициируется HTTP-запросом, а выходная привязка показывает, что ответ будет отправлен как HTTP-ответ.

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

## <a name="running-the-premade-azure-function"></a>Запуск готовой функции Azure

Чтобы запустить функцию, можно инициировать HTTP-запрос из cURL через командную строку. Чтобы найти URL-адрес конечной точки, вернитесь к коду функции и выберите ссылку **Получить URL-адрес функции**. Скопируйте эту ссылку в буфер обмена.  URL-адрес должен выглядеть следующим образом: https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg== ![Получить URL-адрес конечной точки](../images/6-get-function-url.png)

С помощью этого URL-адреса выполните команду cURL, чтобы инициировать функцию (заменив полученный URL-адрес на собственный):

```bash
curl --header "Content-Type: application/json" --request POST --data "{\"name\": \"Azure Function\"}" https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg==
```

![cURL-ответ готовой функции](../images/6-premadefunction-curl.png)

## <a name="adding-business-logic-to-the-function"></a>Добавление бизнес-логики в функцию

Наша функция ожидает от клиента массив показаний температуры. Вот пример текста запроса:

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

Измените код готовой функции таким образом, чтобы реализовать необходимую бизнес-логику. Откройте файл index.js и замените его следующим списком:

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

Обратите внимание на операторы журнала. При выполнении функции они будут добавлять сообщения в окне журнала.

## <a name="testing-your-business-logic"></a>Тестирование бизнес-логики

Откройте тестовое окно из всплывающего меню справа и вставьте приведенный выше пример запроса в текстовом поле для тела запроса. Нажмите кнопку **Выполнить** и просмотрите выходные данные. Можно также открыть окно журнала из нижнего всплывающего меню, чтобы увидеть операторы ведения журнала в журнале.
![Тестирование бизнес-логики](../images/6-portal-testing.png). По данным JSON в окне выходных данных видно, что к каждому из показаний было правильно добавлено наше поле состояния температуры. На панели мониторинга монитора можно также увидеть, что запрос была записан в журнал Application Insights.
![Запрос в Application Insights](../images/6-app-insights.png)
