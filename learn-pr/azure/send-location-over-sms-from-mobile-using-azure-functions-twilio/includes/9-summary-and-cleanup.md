Вы успешно создали кроссплатформенное мобильное приложение с помощью Xamarin и функции Azure с привязкой к Twilio.

## <a name="clean-up-resources"></a>Очистка ресурсов

Закончив работу с этим приложением функций Azure, вы можете удалить все ресурсы, созданные в рамках этого руководства, на портале Azure.

1. В Visual Studio последовательно выберите *Вид->Cloud Explorer*.

2. В раскрывающемся списке в верхней части этой панели выберите *Группы ресурсов*.

3. Разверните подписку, которая использовалась для создания группы ресурсов. Правой кнопкой мыши щелкните группу ресурсов "ImHere" и выберите пункт *Открыть на портале*.

    ![Открытие группы ресурсов на портале из окна Cloud Explorer](../media-drafts/9-open-resource-group-in-portal.png)

4. Если необходимо, войдите на портал Azure из браузера.

5. Откроется портал с группой ресурсов "ImHere". Нажмите кнопку **Удалить группу ресурсов**.

    ![Удаление группы ресурсов](../media-drafts/9-delete-resource-group.png)

6. Введите имя группы ресурсов, чтобы подтвердить удаление, и нажмите кнопку **Удалить**.

    ![Ввод имени группы ресурсов для подтверждения удаления](../media-drafts/9-confirm-delete-resource-group.png)

## <a name="summary"></a>Сводка

Из этого руководства вы узнали, как выполнять следующие задачи:
> [!div class="checklist"]
> * Создание кроссплатформенного приложения Xamarin.Forms, которое использует Xamarin.Essentials.
> * Создание кроссплатформенного пользовательского интерфейса с помощью XAML с логикой приложения в классе ViewModel, а также привязка свойства в классе ViewModel к пользовательскому интерфейсу.
> * Определение местоположения пользователя.
> * Создание функции Azure с триггером HTTP и ее запуск в локальной среде.
> * Вызов функции Azure из мобильного приложения с передачей данных в формате JSON.
> * Привязка функции Azure к Twilio для отправки SMS-сообщений.
> * Публикация функции Azure в Azure.
