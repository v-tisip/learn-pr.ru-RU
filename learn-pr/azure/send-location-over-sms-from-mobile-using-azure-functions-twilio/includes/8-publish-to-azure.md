Приложение и функция Azure готовы и работают в локальной среде. В этом блоке вы опубликуете функцию в Azure для работы в облаке.

> В этом блоке вы опубликуете функцию из Visual Studio. Это отличный способ начала работы с экспериментальными проектами, прототипами и учебными курсами, но при взаимодействии с приложением, предназначенным для эксплуатации в производственной среде, этот метод использовать **не** следует. Необходимо обратить внимание на определенные виды развертываний на основе непрерывной интеграции. Дополнительные сведения см. в [документации по развертываниям функций Azure](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment).
>
## <a name="publishing-your-app-to-azure"></a>Публикация приложения в Azure

Функции Azure можно опубликовать в Azure из Visual Studio.

1. Если локальная среда выполнения функций Azure работает, остановите ее.

2. Щелкните правой кнопкой мыши приложение `ImHere.Functions` в обозревателе решений и выберите пункт *Опубликовать*.

    ![Пункт "Опубликовать" контекстного меню в приложении функций](../media-drafts/8-right-click-publish.png)

3. В диалоговом окне **Выбор целевого объекта публикации** выберите *Приложение-функция Azure* и для **Служба приложений Azure** выберите *Создать*. Щелкните **Опубликовать**.

    ![Создание службы приложений Azure для публикации](../media-drafts/8-pick-publish-target.png)

4. Если у вас несколько учетных записей Azure, выберите нужную учетную запись Azure в раскрывающемся списке в правом верхнем углу.

5. Присвойте имя приложению функций. Это имя должно быть глобально уникальным во всех приложениях функций в рамках платформы Azure, поэтому используйте нечто вроде "ImHere-\<ваше_имя\>".

6. Выберите подписку, в которой необходимо создать приложение функций.

7. Создайте группу ресурсов для этого приложения, нажав кнопку **Создать...** рядом с раскрывающимся списком **Группа ресурсов**, и присвойте ей имя, например "ImHere". Имена групп ресурсов должны быть уникальными в рамках подписки, а не глобально уникальными в пределах Azure. Затем нажмите кнопку **ОК**.

    ![Создание группы ресурсов](../media-drafts/8-create-new-resource-group.png)

   Создание группы ресурсов упрощает последующую очистку. При удалении группы ресурсов удаляются все данные, созданные для этого приложения функций.

8. Создайте план размещения, нажав кнопку **Создать...** рядом с раскрывающимся списком **План размещения**. Именем плана службы приложений по умолчанию будет имя вашего приложения со словом "Plan" в конце. В качестве значения параметра **Расположение** задайте ближайшее к вам расположение и убедитесь, что параметру **Размер** задано значение потребления. Затем нажмите кнопку **ОК**.

    ![Настройка плана размещения](../media-drafts/8-configure-hosting-plan.png)

9. Создайте учетную запись хранения, нажав кнопку **Создать...** рядом с раскрывающимся списком **Учетная запись хранения**. Будет указано имя по умолчанию. Оставьте все значения по умолчанию и нажмите кнопку **ОК**.

    ![Создание учетной записи хранения](../media-drafts/8-create-storage-account.png)

10. Нажмите кнопку **Создать**, чтобы подготовить все ресурсы в Azure и опубликовать приложение функций Azure.

    ![Создание службы приложений](../media-drafts/8-create-app-service.png)

Подготовка займет несколько минут. Будут подготовлены следующие ресурсы:

* учетная запись хранения для хранения файлов, необходимых для приложения функций Azure;
* план службы приложений для управления вычислительными ресурсами, необходимыми для приложения функций Azure;
* служба приложения, в которой работает функция Azure.

Функция будет опубликована и станет доступна для вызова по адресу: https://<имя_приложения>.azurewebsites.net/api/SendLocation.

## <a name="configuring-your-app"></a>Настройка приложения

Когда функция Azure запускалась локально, она использовала учетные данные Twilio, которые были сохранены в файле `local.settings.json`. Как следует из имени, этот файл предназначен для локальных параметров, а не для параметров Azure. Прежде чем вызывать функцию Azure в Azure, необходимо настроить параметры `TwilioAccountSid` и `TwilioAuthToken`.

1. На вкладке "Публикация" щелкните параметр **Управление параметрами приложения**.

    ![Параметр "Управление параметрами приложения"](../media-drafts/8-application-settings-option.png)

2. Нажмите кнопку **Добавить**, чтобы добавить новый параметр. Присвойте ему имя "TwilioAccountSid" и задайте в качестве значения идентификатор безопасности учетной записи Twilio. Повторите этот шаг для маркера проверки подлинности, используя имя "TwilioAuthToken".

    ![Задание учетных данных Twilio в параметрах приложения](../media-drafts/8-set-creds-in-app-settings.png)

3. Нажмите кнопку **ОК**.

4. Нажмите кнопку **Опубликовать**, чтобы повторно опубликовать приложение функций Azure с новыми параметрами приложения.

    ![Кнопка "Опубликовать"](../media-drafts/8-publish-application-button.png)

## <a name="pointing-the-mobile-app-to-azure"></a>Направление мобильного приложения в Azure

1. На вкладке "Публикация" скопируйте **URL-адрес сайта** с помощью кнопки копирования рядом со значением.

    ![Копирование URL-адреса сайта на вкладке "Публикация"](../media-drafts/8-copy-site-url.png)

2. Откройте `MainViewModel` в проекте `ImHere`.

3. Измените значение поля `baseUrl` на URL-адрес сайта, скопированный на вкладке "Публикация".

4. Измените протокола для этого значения с `http` на `https`. URL-адрес сайта всегда указывается с помощью HTTP, но для вызова функции Azure нужно использовать HTTPS.

## <a name="test-it-out"></a>Тестирование

1. Настройте приложение `ImHere.UWP` как запускаемое автоматически и запустите его.

2. Введите номер телефона и нажмите кнопку **Send Location** (Отправить данные о местоположении).

3. Вы должны получить данные о местоположении в SMS-сообщении.

## <a name="summary"></a>Сводка

В данном блоке вы узнали, как опубликовать проект функций Azure в Azure из Visual Studio и настроить параметры приложения.