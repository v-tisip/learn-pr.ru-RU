При разработке приложения, которое должно сохранить данные, важно подумать о том, каким образом оно будет упорядочивать и хранить данные в разных учетных записях хранения, контейнерах и BLOB-объектах.

## <a name="storage-accounts"></a>учетные записи хранения;

Одной учетной записи достаточно для того, чтобы упорядочивать BLOB-объекты любым удобным образом, но для того, чтобы логически разделять траты и контролировать доступ к данным, следует использовать дополнительные учетные записи хранения.

## <a name="containers-and-blobs"></a>контейнеры и большие двоичные объекты;

Выбор стратегии для именования и упорядочивания контейнеров и BLOB-объектов должен зависеть от характера вашего приложения и данных, которые в нем хранятся.

Приложения, в которых BLOB-объекты используются в рамках схемы хранения, включающей базу данных, часто не требуют строгой организации, именования или метаданных, отражающих определенные сведения о данных приложения. Такие приложения часто используют в качестве имен BLOB-объектов идентификаторы, такие как идентификаторы GUID, и ссылаются на эти идентификаторы в записях базы данных. Для определения местонахождения BLOB-объектов и типа данных, которые в них содержатся, приложение будет использовать базу данных.

Другие приложения могут использовать хранилище BLOB-объектов Azure как систему персональных файлов, где имена контейнеров и BLOB-объектов служат для обозначения смысла и структуры. Имена BLOB-объектов в таких приложениях часто будут выглядеть как имена традиционных файлов и включать расширения (например, `.jpg`), которые показывают, какого рода данные содержат эти файлы. Они будут применять виртуальные каталоги (см. ниже) для упорядочивания BLOB-объектов и часто использовать теги метаданных для хранения информации о BLOB-объектах и контейнерах.

Выбирая способ упорядочивания и хранения BLOB-объектов и контейнеров, следует учитывать несколько важных моментов.

### <a name="naming-limitations"></a>Ограничения именования

Имена контейнеров и BLOB-объектов должны соответствовать ряду правил, включая ограничения длины и запрет на специальные символы. Более подробные сведения о правилах именования см. в разделе "Дополнительные ресурсы" в конце этого модуля.

### <a name="public-access-and-containers-as-security-boundaries"></a>Общий доступ и контейнеры как границы безопасности

По умолчанию для доступа ко всем BLOB-объектам требуется проверка подлинности. При этом отдельные контейнеры можно настроить так, чтобы BLOB-объекты из этих контейнеров можно было загружать в открытом доступе без проверки подлинности. Эта функция поддерживает самые разные варианты применения, включая размещение статических ресурсов для веб-сайтов и совместное использование файлов. Это связано с тем, что загрузка содержимого BLOB-объектов работает точно так же, как считывание любых других видов данных по сети: нужно только набрать URL-адрес BLOB-объекта в браузере или другой программе, способной отправлять запросы GET.

**Изображение общедоступного контейнера TODO с указанием URL-адреса прямого доступа**

Включение общего доступа важно для масштабируемости, поскольку данные, загружаемые непосредственно из хранилища BLOB-объектов, не генерируют в приложении трафик на стороне сервера. Даже если преимущества открытого доступа вам не нужны или для управления доступом к данным через приложение вы будете использовать базу данных, планируйте использовать отдельные контейнеры для данных, которые должны будут находиться в открытом доступе.

> [!CAUTION]
> BLOB-объекты в контейнере, настроенном на открытый доступ, может загружать любой пользователь, знающий URL-адрес их хранения, без какой-либо проверки подлинности или аудита. Не размещайте в общедоступном контейнере BLOB-объекты, не предназначенные для открытого доступа.

Помимо открытого доступа, в Azure есть функция подписанного URL-адреса, позволяющая управлять детальными разрешениями для контейнеров. Точный контроль доступа позволяет использовать сценарии, улучшающие масштабируемость, поэтому контейнеры можно в целом считать границами безопасности.

### <a name="blob-name-prefixes-virtual-directories"></a>Префиксы имен BLOB-объектов (виртуальные каталоги)

Технически контейнеры "плоские" и не поддерживают никакие вложения или иерархии. Однако, если присвоить BLOB-объектам иерархические имена, которые выглядят как пути к файлам (например, `finance/budgets/2017/q1.xls`), операция перечисления в API сможет фильтровать результаты по конкретным префиксам. Это позволит перемещаться по списку как по иерархической системе файлов и папок.

Эту функцию часто называют *виртуальными каталогами*, поскольку с ее помощью некоторые средства и клиентские библиотеки визуализируют и перемещают хранилище BLOB-объектов так, как если бы оно было файловой системой. Любое перемещение по папкам запускает отдельный вызов списка BLOB-объектов в этой папке.

**Снимок экрана TODO: обозреватель хранилища и (или) портал с папками**

Для упорядочивания сложных BLOB-объектов и перемещения между ними BLOB-объектам часто присваиваются имена, напоминающие имена файлов.

### <a name="blob-types"></a>Типы BLOB-объектов

Существуют три типа BLOB-объектов для хранения данных:

- **Блочные BLOB-объекты** состоят из блоков разного размера, которые можно передавать и загружать по отдельности и параллельно. Запись в блочный BLOB-объект включает передачу данных в блоки и отнесение данных к определенному BLOB-объекту &mdash; клиентские библиотеки делают это автоматически.
- **Добавочные BLOB-объекты** представляют собой специализированные блочные BLOB-объекты, которые поддерживают только добавление новых данных (обновление или удаление существующих данных не поддерживается), но делают это с высокой эффективностью. Добавочные BLOB-объекты идеально подходят для таких сценариев, как хранение журналов или потоковая передача данных.
- **Страничные BLOB-объекты**  предназначены для сценариев, включающих операции чтения и записи с произвольным доступом. Страничные BLOB-объекты применяются для хранения файлов виртуального жесткого диска (VHD), которые используются виртуальными машинами Azure, но отлично подходят и для любого сценария, включающего произвольный доступ.

Блочные BLOB-объекты — оптимальный вариант для большинства сценариев, которые не требуют добавочных или страничных BLOB-объектов.