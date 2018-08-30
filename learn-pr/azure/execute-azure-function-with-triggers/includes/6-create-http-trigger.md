В этом упражнении мы создадим функцию Azure, которая принимает HTTP-запрос одной строкой. Эта функция возвращает строку вызывающему объекту, сообщая, таким образом, об успешном или неудачном выполнении.

> [!NOTE]
> Чтобы выполнить это упражнение, войдите на [портал Azure](https://portal.azure.com?azure-portal=true) с действующей учетной записью.

## <a name="create-an-http-trigger"></a>Создание триггера HTTP

В уже существующее приложение функций Azure добавим триггер HTTP.

1. Наведите указатель мыши на параметр **Функции** и нажмите на значок плюса (+).

    ![Наведите указатель мыши на параметр "Функции" и нажмите на плюс](../media-drafts/4-hover-function.png)

2. Выберите **Триггер HTTP**.

3. В качестве языка выберите **C#**. 

4. Оставьте в поле **Имя** значение по умолчанию.

5. В поле **Уровень авторизации** выберите **Анонимный**.

6. Нажмите кнопку **Создать**.

7. Просмотрите автоматически созданный код, чтобы получить представление о происходящем. Параметр *req* представляет входящий запрос и содержит параметр *name*. Проверим, имеет ли параметр *name* какое-либо значение. Если значение есть, возвращается приветствие. В противном случае возвращается сообщение об ошибке.

## <a name="get-your-function-url"></a>Получение URL-адреса функции

Теперь, когда мы создали триггер HTTP, получим URL-адрес функции, чтобы приступить к подаче запроса.

1. Выберите свой триггер HTTP, чтобы открыть экран кода.

2. Справа от параметра **Выполнить** выберите **Получить URL-адрес функции**.

3. Нажмите **Копировать**.

4. Нажмите **Выполнить**, чтобы запустить функцию.

## <a name="issue-a-get-request-to-your-http-trigger"></a>Передача запроса GET в триггер HTTP

Теперь URL-адрес функции скопирован в буфер обмена. Передадим запрос GET, чтобы узнать, получим ли мы ответ.

1. Откройте новую вкладку в веб-браузере.

2. Вставьте URL-адрес в адресную строку.

3. Добавьте параметр строки запроса, в котором параметр *name* имеет указанное вами имя, например: `.../api/HttpTriggerCSharp1?name=Jesse`

4. Нажмите клавишу ВВОД, чтобы отправить запрос.

## <a name="clean-up"></a>Очистка

Чтобы с вас не взимали плату за эту функцию, нажмите кнопку **Пауза**, которая находится выше в окне журнала.

![Приостановить](../media-drafts/4-pause-timer.png)