Теперь, когда вы знаете, как использовать единицы запросов для определения пропускной способности базы данных и каким образом ключ секции определяет стратегии масштабирования вашей базы данных, можно приступать к созданию базы данных и коллекции.

## <a name="creating-your-database-and-collection"></a>Создание базы данных и коллекции

1. На портале Azure выберите **Обозреватель данных** из ресурсов Cosmos DB и нажмите на кнопку **Создать коллекцию** на панели инструментов.
    
    Справа появится область **Добавление коллекции**. Возможно, для того, чтобы увидеть эту область, экран нужно будет прокрутить вправо.

    ![Колонка "Добавление коллекции" в обозревателе данных на портале Azure](../media/5-create-a-database-and-collection/azure-cosmosdb-data-explorer.png)

2. На странице **Добавление коллекции** введите параметры для новой коллекции.

    Параметр | Рекомендуемое значение | ОПИСАНИЕ
    --------|-----------------|-------------
    Идентификатор базы данных      | Пользователи         | Введите *Users* в качестве имени для новой базы данных. Имена баз данных должны быть длиной от 1 до 255 символов и не могут содержать символы /, \\, #, ? или пробел.
    Идентификатор коллекции    | WebCustomers  | Введите *WebCustomers* в качестве имени для новой коллекции. Для идентификаторов коллекций предусмотрены те же требования к символам, что и для имен баз данных.
    Емкость хранилища | Без ограничений     | Используйте значение по умолчанию — **Unlimited** (Без ограничений). Это значение определяет емкость хранилища базы данных и позволяет изменять ее масштаб по мере необходимости.
    Ключ секции    | UserId        | UserID — хороший ключ секции для сценария интернет-магазина, так как многие запросы связаны с идентификаторами клиентов.
    Пропускная способность       |1000 ЕЗ        | Укажите для пропускной способности 1000 единиц запросов в секунду (ЕЗ/с). 1000 — минимальное количество единиц запросов в секунду, при котором включается автоматическое масштабирование.
    
    Флажок **подготовки пропускной способности базы данных** пока не устанавливайте, а также не добавляйте в коллекцию уникальные ключи. 
    
3. Нажмите **ОК**. В обозревателе данных отобразится новая база данных и коллекция.

    ![Обозреватель данных на портале Azure с новой базой данных и коллекцией](../media/5-create-a-database-and-collection/azure-cosmos-db-new-collection.png)

## <a name="summary"></a>Сводка

В этом модуле вы использовали свои знания о ключах секций и единицах запросов для создания базы данных и коллекции с параметрами пропускной способности и масштабирования, соответствующими нуждам вашей компании.