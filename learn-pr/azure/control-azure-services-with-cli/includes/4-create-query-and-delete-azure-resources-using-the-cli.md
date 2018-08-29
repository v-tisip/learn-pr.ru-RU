## <a name="motivation"></a>Мотивация
Azure CLI позволяет писать команды и выполнять их немедленно. Вспомним, что главная цель в примере разработки программного обеспечения — развернуть новые сборки веб-приложения для тестирования. Первый шаг — создать группу ресурсов. Помните, что целью является создать эти ресурсы с помощью локально установленного Azure CLI. 

В этом модуле вы узнаете, как использовать Azure CLI для входа в подписку Azure и создания нового ресурса.

## <a name="what-azure-resources-can-be-managed-using-the-azure-cli"></a>Какими ресурсами Azure можно управлять с помощью Azure CLI?
Azure CLI позволяет управлять практически всеми аспектами каждого ресурса Azure. Вы можете работать с группами ресурсов, хранилищами, виртуальными машинами, Azure Active Directory (Azure AD), контейнерами, использовать машинное обучение и т. д.

Команды в интерфейсе командной строки разделены на группы и подгруппы. Каждая группа представляет службу, предоставляемую Azure, а подгруппы позволяют распределить команды для этих служб в логические группы. Например, группа **хранения** содержит подгруппы **учетной записи**, **BLOB-объектов**, **хранения** и **очереди**.

Как найти конкретную необходимую команду? Один из способов — использование **az find**. Например, если вы хотите найти команды для управления хранилищем **BLOB-объектов**, используется следующая команда поиска:

```bash
az find -q blob
```

Если вы уже знаете имя нужной команды, лучше использовать аргумент **--help** для этой команды. Вы получите подробные сведения о команде, а для группы команд — список доступных подкоманд. Таким образом, в нашем примере хранилища мы можем получить список подгрупп и команд для управления хранилищем BLOB-объектов следующим образом:

```bash
az storage blob --help
```

## <a name="how-to-create-an-azure-resource"></a>Как создать ресурс Azure
Для создания нового ресурса Azure обычно необходимо выполнить три действия: подключиться к подписке Azure, создать ресурс и убедиться, что создание выполнено успешно (см. ниже).

![Этапы создания ресурса с помощью Azure CLI](../media-drafts/4-create-resources-overview.png)

На каждом этапе используется своя команда Azure CLI.

### <a name="connect"></a>Подключение
Так как вы работаете с локальной установкой Azure CLI, перед выполнением команд Azure вам потребуется пройти проверку подлинности с помощью команды Azure CLI **login**. 

```bash
az login
```

Azure CLI обычно запускает браузер по умолчанию и открывает страницу входа в Azure. Если это не срабатывает, следуйте указаниям командной строки и введите код авторизации в [https://aka.ms/devicelogin](https://aka.ms/devicelogin).

После успешного входа вы будете подключены к вашей подписке Azure. 

### <a name="create"></a>Создание
Часто необходимо создать новую группу ресурсов перед созданием новой службы Azure, поэтому мы будем использовать группы ресурсов в качестве примера, чтобы показать, как создать ресурсы Azure из интерфейса командной строки.

Чтобы создать группу ресурсов, используйте команду Azure CLI **group create**. Необходимо указать имя и расположение. Имя должно быть уникальным в пределах вашей подписки. Расположение определяет место хранения метаданных для группы ресурсов. Используйте такие строки, как "West US", "North Europe" или "West India", чтобы указать расположение. Кроме того, вы можете использовать эквиваленты в одно слово, например westus, northeurope или westindia. Основной синтаксис выглядит следующим образом:

```bash
az group create --name <name> --location <location>
```

### <a name="verify"></a>Проверка
Azure CLI предоставляет **список** подкоманд для просмотра сведений о ресурсе для многих ресурсов Azure. Например, команда Azure CLI **group list** выводит список групп ресурсов Azure. Это полезно для проверки успешного создания группы ресурсов:

```bash
az group list
```

Чтобы получить более краткое представление, отформатируйте выходные данные в виде простой таблицы:

```bash
az group list --output table
```