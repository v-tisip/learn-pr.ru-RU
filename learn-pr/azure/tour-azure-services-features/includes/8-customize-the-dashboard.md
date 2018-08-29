Здесь вы научитесь создавать и изменять панели мониторинга с помощью пользовательского интерфейса портала и путем редактирования непосредственно базового файла JSON.

## <a name="what-is-a-dashboard"></a>Что такое панель мониторинга?

_Панель мониторинга_ — это настраиваемая коллекция плиток пользовательского интерфейса, отображаемых на портале Azure. Вы можете добавить, удалить плитки и разместить их так, чтобы создать нужное представление, а затем сохранить его в виде панели мониторинга. Поддерживается несколько панелей мониторинга с возможностью переключения между ними. Вы можете даже делиться панелями мониторинга с другими участниками команды.

Панели мониторинга предоставляют значительную гибкость при управлении Azure. Например, вы можете создать панели мониторинга для определенных ролей в организации, а затем использовать RBAC для управления доступом к панели мониторинга. Таким образом, у вашего администратора баз данных будет панель мониторинга с представлениями службы баз данных SQL, тогда как у администратора Azure Active Directory будут представления пользователей и групп в Azure AD.

Панели мониторинга хранятся в виде JSON-файлов. Это значит, что их можно отправить на другие компьютеры и скачать их или предоставить участникам каталога Azure. Azure хранит панели мониторинга в группах ресурсов как виртуальные машины или учетные записи хранения, которыми можно управлять на портале.

Так как панели мониторинга являются JSON-файлами, вы можете также настроить их программными способами, что делает их многофункциональными инструментами администрирования. Кроме того, некоторые типы плиток могут быть основаны на запросах и обновляться автоматически при изменении исходных данных.

## <a name="default-dashboard"></a>Панель мониторинга по умолчанию

Панель мониторинга по умолчанию называется просто панелью мониторинга. При входе на портал вы увидите эту панель мониторинга, состоящую из пяти веб-частей.

![Веб-части по умолчанию](../images/4-dashboard-default-webparts.png)

Это следующие веб-части по умолчанию

1. All resources (Все ресурсы)
2. Краткие руководства и учебники
3. Работоспособность службы
4. Marketplace
5. Начало работы в Azure

## <a name="creating-and-managing-dashboards"></a>Создание панелей мониторинга и управление ими

В верхней части панели мониторинга находятся элементы управления, которые позволяют создавать, отправлять, скачивать, изменять панель мониторинга и предоставлять к ней общий доступ. Вы можете также переключить панель мониторинга в полноэкранный режим, клонировать ее или удалить.

![Настройка элементов управления панели мониторинга](../images/7-customise-dashboard-controls.PNG)

### <a name="select-dashboard"></a>Выбор панели мониторинга

Слева находится раскрывающийся список "Выбрать панель мониторинга". Щелкните этот элемент управления, чтобы выбрать одну из заданных в учетной записи панелей мониторинга. Этот элемент управления позволяет легко задать несколько панелей мониторинга для разных целей, а затем просто переключаться с одной на другую и обратно в зависимости от того, что вам нужно сделать.

Обратите внимание, что все созданные панели мониторинга будут изначально частными: они будут видны только вам. Чтобы сделать панель мониторинга доступной в организации, нужно предоставить к ней общий доступ. Дополнительные сведения о предоставлении и отзыве доступа к панелям мониторинга см. в разделе ниже.

### <a name="create-a-new-dashboard"></a>Создание панели мониторинга

Чтобы создать панель мониторинга, просто щелкните **Создать панель мониторинга**. Появится рабочая область панели мониторинга без плиток. Теперь вы можете добавить плитки, как описано в разделе "Изменение панели мониторинга с помощью пользовательского интерфейса" ниже. После добавления и настройки плиток, а также изменения имени панели мониторинга просто щелкните **Завершить настройку**, чтобы сохранить изменения и переключиться на эту панель мониторинга.

### <a name="upload-and-download"></a>Отправка и скачивание

Кнопки **Отправить** и **Скачать** позволяют скачать текущую панель мониторинга в виде JSON-файла, настроить ее, а затем распространить и отправить или попросить другого пользователя отправить файл на портал Azure, заменив текущую панель мониторинга.

Если нажать кнопку **Скачать**, текущая панель мониторинга скачается в папку "Загрузки" по умолчанию. При открытии скачанного файла отобразится код JSON.

![Код JSON панели мониторинга](../images/7-dashboard-json-code.PNG)

После вы можете отредактировать код вручную, например изменить размеры плиток и отправить их обратно в Azure, нажав кнопку **Отправить**.

### <a name="edit-a-dashboard"></a>Изменение панели мониторинга

Дополнительные сведения см. в разделе "Изменение панели мониторинга с помощью пользовательского интерфейса".

### <a name="shareunshare-a-dashboard"></a>Предоставление и отзыв доступа к панели мониторинга

При определении новой панели мониторинга она является частной и отображается только для вашей учетной записи. Чтобы она была видна другим пользователям, нужно предоставить к ней доступ. Однако, как и с другими ресурсами Azure, нужно указать группу ресурсов (или использовать существующую), в которой будут храниться панели мониторинга. Azure создаст группу ресурсов "Панели мониторинга" в указанном вами расположении, если у вас ее нет. Если у вас есть группы ресурсов, вы можете указать одну из них для хранения панелей мониторинга.

![Общий доступ и контроль доступа 1](../images/7-share-dashboards-default.PNG)

При предоставлении шаблона появится вторая колонка **Общий доступ и контроль доступа**.

![Общий доступ и контроль доступа 2](../images/7-share-dashboards-access-control.PNG)

После вы можете щелкнуть **Управление пользователями**, чтобы указать пользователей, которые получат доступ к этой панели мониторинга.

### <a name="switching-to-a-shared-dashboard"></a>Переключение на общую панель мониторинга

Чтобы переключиться на общую панель мониторинга, щелкните список панелей мониторинга и выберите **Просмотреть все панели мониторинга**.

![Просмотр всех панелей мониторинга](../images/7-browse-dashboards.PNG)

Вы увидите колонку "Все панели мониторинга" с именами всех общих панелей мониторинга. Просто щелкните панель мониторинга, чтобы применить ее к порталу Azure.

![Общие панели мониторинга](../images/7-select-shared-dashboard.png)

### <a name="display-a-dashboard-as-a-full-screen"></a>Отображение панели мониторинга в полноэкранном режиме

Если вам нужно крупное представление панели мониторинга, нажмите кнопку **Полноэкранный режим**, чтобы отобразилась текущая панель мониторинга без меню браузера. Если часть плиток оказалась за пределами экрана, справа и внизу появятся ползунки.

После завершения работы в полноэкранном режиме нажмите клавишу ESC или щелкните **Выйти из полноэкранного режима** рядом с названием панели мониторинга вверху экрана.

### <a name="clone-a-dashboard"></a>Клонирование панели мониторинга

При клонировании панели мониторинга мгновенно создается копия с именем "Клон (имя панели мониторинга)", которая становится текущей. Клонирование — это также простой способ создания панелей мониторинга перед предоставлением к ним доступа. Например, если у вас есть практически подходящая панель мониторинга, просто клонируйте ее, затем внесите нужные изменения и предоставьте к ней доступ.

### <a name="delete-a-dashboard"></a>Удаление панели мониторинга

При удалении панели мониторинга она исчезает из списка доступных панелей. Вас попросят подтвердить удаление панели мониторинга, и вы не сможете восстановить ее после удаления.

## <a name="edit-a-dashboard-through-the-user-interface"></a>Изменение панели мониторинга с помощью пользовательского интерфейса

Хотя вы можете изменить панель мониторинга, скачав JSON-файл, изменив значения в нем и отправив его обратно в Azure, этот подход не самый интуитивно понятный при разработке пользовательского интерфейса. Чтобы использовать GUI для настройки текущей панели мониторинга, нажмите кнопку **Изменить** или щелкните правой кнопкой мыши панель мониторинга и выберите **Изменить**. Панель мониторинга переключится в режим редактирования.

![Изменение панели мониторинга](../images/7-edit-dashboard.PNG)

Слева отображается коллекция плиток, число которых указано ниже. Вы можете отфильтровать коллекцию плиток по следующим критериям:

* Общие сведения
* type
* поиска
* Группа ресурсов
* Тег

![Коллекция плиток](../images/7-tile-gallery.png)

Вы можете также дополнительно уточнить каждый из этих параметров по категориям, например Azure Active Directory, Интернет вещей, Microsoft Intune и т. д.

Для добавления плиток нужно просто выбрать плитку в списке слева и перетащить ее на рабочую область. Вы можете перемещать каждую плитку, изменять ее размер или изменять данные, которые она отображает.

Рабочая область в режиме редактирования разделена на квадраты. Каждая плитка должна занимать как минимум один квадрат. Плитки прикрепляются к ближайшему набору разделителей. Все перекрывающиеся плитки будут отодвинуты в сторону. Если вы уменьшите размер плитки, прилегающие плитки будут примагничены к ним.

### <a name="change-tile-sizes"></a>Изменение размеров плиток

Некоторые плитки имеют заданный размер, и вы можете изменить их размер только программными средствами. Однако размер плиток с серым уголком можно менять с помощью перетаскивания этого уголка.

![Плитки с изменяемым размером](../images/7-resizable-tile.png)

Вы также можете щелкнуть правой кнопкой мыши контекстное меню и указать нужный размер.

![Размер плитки](../images/7-tile-size.png)

Чтобы создать панель мониторинга, просто перетащите плитки из коллекции на рабочую область и переупорядочите их.

### <a name="change-tile-settings"></a>Изменение параметров плиток

В некоторых плитках параметры можно изменять. Например, при перетаскивании плитки часов на рабочую область откроется плитка **Изменение часов**. Здесь вы сможете задать часовой пояс, а также формат (12- или 24-часовой).

![Изменение часов](../images/7-edit-clock.png)

Для многонациональных или трансконтинентальных компаний можно добавить дополнительные часы для каждого часового пояса.

### <a name="accepting-your-edits"></a>Принятие изменений

После упорядочивания плиток щелкните **Завершить настройку** или щелкните правой кнопкой мыши и выберите **Завершить настройку**.

## <a name="edit-a-dashboard-by-changing-the-json-file"></a>Изменение панели мониторинга путем изменения JSON-файла

Вы можете также изменить панель мониторинга, изменив JSON-файл. Этот подход предоставляет больше вариантов изменения параметров, но вы не увидите изменений, пока не отправите файл обратно в Azure.

![Параметры JSON](../images/7-json-code.png)

В примере выше для изменения размера плитки измените переменные colSpan и rowSpan, а затем сохраните файл и отправьте его обратно в Azure. Вы можете также отправить файл другим пользователям.

## <a name="reset-a-dashboard"></a>Сброс панели мониторинга

Вы можете сбросить любую панель мониторинга к стилю по умолчанию. В режиме редактирования щелкните правой кнопкой мыши и выберите **Сбросить до состояния по умолчанию**. В диалоговом окне вас попросят подтвердить сброс.

## <a name="summary"></a>Сводка

Панели мониторинга позволяют гибко управлять разными аспектами служб Azure на портале. С их помощью удобно отслеживать состояние служб. Так как к ним можно предоставлять доступ, они гарантируют, что все в команде увидят одинаковые данные и будут в курсе состояния критических компонентов.