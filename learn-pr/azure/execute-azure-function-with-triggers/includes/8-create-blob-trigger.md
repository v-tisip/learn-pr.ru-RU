В этом упражнении мы создадим функцию Azure, которая отображает имя и размер большого двоичного объекта при его создании или обновлении. 

> [!NOTE]
> Чтобы выполнить это упражнение, войдите на [портал Azure](https://portal.azure.com?azure-portal=true) с действующей учетной записью.

## <a name="create-a-blob-trigger"></a>Создание триггера больших двоичных объектов

В уже существующее приложение функций Azure добавим триггер BLOB-объектов.

1. Наведите указатель мыши на параметр **Функции** и нажмите на значок плюса (+).

    ![Наведите указатель мыши на параметр "Функции" и щелкните значок плюса](../media-drafts/4-hover-function.png)

2. Выберите элемент **Пользовательская функция**, а затем **Триггер BLOB-объектов**.

3. При выборе языка укажите **C#**. 

4. Оставьте в поле **Имя** значение по умолчанию.

5. Оставьте в поле **Путь** значение по умолчанию.

6. Выберите существующую учетную запись Службы хранилища Azure или щелкните **Создать**, чтобы создать новую.

## <a name="create-a-blob-container"></a>Создание контейнера больших двоичных объектов

Теперь, когда мы создали триггер больших двоичных объектов, откройте обозреватель хранилища, чтобы создать большой двоичный объект и активировать функцию.

1. Откройте в новой вкладке учетную запись хранения, которую вы выбрали или создали. Простой способ — откройте новую вкладку портала Azure и щелкните **Учетные записи хранения** на боковой панели или выберите **Все службы** на боковой панели и выполните фильтрацию по имени. Новая вкладка нужна для того, чтобы в ходе работы переключаться между двумя используемыми службами.

2. Щелкните раздел **Обозреватель службы хранилища (предварительная версия)**. Откроется новая колонка для работы с большими двоичными объектами и файлами.

Помните, что триггер больших двоичных объектов отслеживает только то расположение, которое указано в поле **Путь**. По умолчанию наш путь должен выглядеть так:

> samples-workitems/{name}

Нам нужно создать контейнер с именем **samples-workitems**.

3. Щелкните правой кнопкой мыши **Контейнеры BLOB-объектов** и выберите **Создать контейнер BLOB-объектов**.

4. Введите имя **samples-workitems** и сохраните для уровня доступа настроенное по умолчанию значение **Частный**.

## <a name="turn-on-your-blob-trigger"></a>Включение триггера больших двоичных объектов

Теперь, когда мы создали контейнер для мониторинга, запустим нашу функцию, чтобы мы могли увидеть выходные данные при создании большого двоичного объекта.

1. Вернитесь на вкладку "Функции Azure" или откройте ее снова.

2. Выберите триггер большших двоичных объектов, чтобы открыть экран с кодом.

3. Выберите **Запуск** и проверьте результаты выполнения в открывшемся окне.

## <a name="create-a-blob"></a>Создание большого двоичного объекта

Теперь наш триггер BLOB-объектов запущен и начал прослушивание. Создадим BLOB-объект, чтобы узнавать о получении сообщений журнала.

1. В обозревателе хранилища выберите контейнер **samples-workitems**.

2. На панели инструментов выберите **Отправить**.

3. Выберите любой файл на своем компьютере.

4. Щелкните **Отправить**.

5. Вернитесь на вкладку "Функции Azure" и найдите в журнале выходных данных сообщение о том, что файл успешно отправлен.

## <a name="pause-the-function"></a>Приостановка выполнения функции

Чтобы не платить за дополнительные запросы, нажмите кнопку **Приостановить** над окном журнала.

![Приостановка выполнения функции](../media-drafts/4-pause-timer.png)


