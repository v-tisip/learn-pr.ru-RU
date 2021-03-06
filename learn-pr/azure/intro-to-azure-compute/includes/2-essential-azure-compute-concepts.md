Вашей исследовательской группе требуется выполнить обработку данных с большим объемом вычислений, но у вас нет необходимого оборудования. Участники группы решили провести анализ данных с помощью Azure.

## <a name="what-is-azure-compute"></a>Что такое служба вычислений Azure?
Служба вычислений Azure — это предоставляемая по запросу служба вычислительных ресурсов для запуска облачных приложений. Она предоставляет вычислительные ресурсы, такие как многоядерные процессоры и суперкомпьютеры, через виртуальные машины и контейнеры. Она также позволяет выполнять бессерверные вычисления для выполнения приложений без необходимости настраивать инфраструктуру или конфигурацию. Ресурсы доступны по запросу и обычно создаются за несколько минут или даже секунд. Вы платите только за используемые ресурсы и только за время их работы.

Существует три распространенных способа выполнения вычислительных операций в Azure.
1. Виртуальные машины
1. Контейнеры
1. Бессерверные вычисления

## <a name="what-are-virtual-machines"></a>Что такое виртуальные машины?

**Виртуальная машина** — это программная эмуляция физического компьютера. У нее есть виртуальный процессор, памяти, хранилище и сетевые ресурсы. В ней размещается операционная системы, поэтому вы можете устанавливать и запускать программное обеспечение так же, как на физическом компьютере. А с помощью клиента удаленного рабочего стола вы можете использовать виртуальную машину и управлять ей так, как если бы вы находились за физическим терминалом.

### <a name="virtual-machines-in-azure"></a>Виртуальные машины в Azure

Виртуальные машины можно создавать и размещать в Azure. Как правило, создание и подготовка новых виртуальных машин занимает несколько минут — для этого нужно просто выбрать предварительно настроенный образ виртуальной машины.

Выбор образа является одним из самых важных решений, принимаемых при создании виртуальной машины. Образ — это шаблон, используемый для создания виртуальной машины. Эти шаблоны уже содержат операционную систему и подчас другое программное обеспечение, такое как средства разработки или среды размещения веб-сайтов.

## <a name="what-are-containers"></a>Что такое контейнеры?

Контейнеры представляют собой среду виртуализации, но, в отличие от виртуальной машины, в них нет операционной системы. Вместо этого они ссылаются на операционную систему среды размещения, где работает контейнер. Например, если на сервере с определенным ядром Linux запущено пять контейнеров, все они работают на том же ядре. 

Контейнеры обычно содержат созданное пользователем приложение, а также будут включать в себя все библиотеки, необходимые приложению для работы на ядре среды размещения. 

Контейнеры являются облегченными компонентами и поддерживают динамическое создание, масштабирование и остановку в случае изменения среды и уровня спроса.

Преимущество использования контейнеров заключается в возможности запуска нескольких изолированных приложений на виртуальной машине. Так как сами контейнеры защищены и изолированы, вам необязательно использовать разные виртуальные машины для отдельных рабочих нагрузок.

Azure поддерживает контейнеры Docker и несколько способов управления ими. Контейнерами можно управлять вручную или с помощью служб Azure, например в службы Azure Kubernetes.

### <a name="what-is-serverless-computing"></a>Что такое бессерверные вычисления?

Бессерверные вычисления — это облачная среда выполнения для работы кода с полным абстрагированием базовой среды размещения. Вы просто создаете экземпляр службы и добавляете код — настраивать или обслуживать инфраструктуру не требуется или даже запрещается.

Бессерверные приложения нужно настроить для реагирования на события. Это может быть конечная точка REST, таймер или сообщение, полученное от другой службы Azure. Бессерверное приложение выполняется только в том случае, если оно запускается событием. 

Следить за инфраструктурой не требуется. Управление масштабированием и производительностью выполняется автоматически, и вы платите только за используемые ресурсы. Вам даже не нужно резервировать ресурсы.

В Azure существует две реализации бессерверных вычислительных ресурсов: **функции Azure**, которые могут выполнять код практически на любом современном языке, и **Azure Logic Apps** для выполнения логики, запущенной службами Azure, без написания кода.
