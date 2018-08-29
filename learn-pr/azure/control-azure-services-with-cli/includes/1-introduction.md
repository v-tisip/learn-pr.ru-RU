## <a name="motivation"></a>Мотивация
Портал Azure отлично подходит для выполнения отдельных задач, а также для быстрого просмотра состояния ресурсов. Однако для задач, которые требуется повторять каждый день или даже час, использование командной строки и набора протестированных команд или сценариев позволит справиться с работой быстрее и избежать ошибок. 

Предположим, вы работаете в компании, которая разрабатывает веб-приложения Azure. Они размещаются в Azure, что дает им все преимущества автоматически настраиваемой системы безопасности, балансировки нагрузки, управления и т. п. Сейчас вы тестируете веб-приложение, которое делает прогнозы продаж на основе различных входных данных из разных баз данных и других источников. Ваши разработчики используют компьютеры под управлением Windows, Linux и Mac, а для хранения ежедневных сборок приложений используют репозиторий GitHub. 

В рамках тестирования нужно сравнить производительность приложения для разных источников данных, а также для различных типов подключений к данным. Вы заметили, что когда разработчики используют портал Azure для создания нового тестового экземпляра приложения, они не всегда задают одни и те же параметры. Вы планируете решить эту проблему с помощью набора стандартных команд развертывания для каждого теста приложения, который может быть автоматизирован при необходимости и будет работать одинаково на всех компьютерах, используемых командой по программному обеспечению.

В этом модуле вы узнаете, как управлять ресурсами Azure с помощью Azure CLI. 

## <a name="learning-objectives"></a>Цели обучения
> [!div class="checklist"]
> * Установка Azure CLI в Linux, macOS и Windows
> * Подключение к подписке Azure с помощью Azure CLI
> * Создание ресурсов Azure с помощью Azure CLI

## <a name="prerequisites"></a>Предварительные требования
- Опыт работы с интерфейсом командной строки, таким как PowerShell или Bash
- Знания о ключевых понятиях Azure, таких как группы ресурсов
- Опыт по администрированию ресурсов Azure с помощью портала Azure

## <a name="expected-duration"></a>Ожидаемая длительность

30 минут