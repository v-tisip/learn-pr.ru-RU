Мы узнали, как оценить затраты до развертывания служб в Azure, но что если у вас уже есть развернутые ресурсы? Как разобраться в уже существующих расходах? Если мы развернули наше предыдущее решение в Azure и теперь хотим убедиться, что выбрали правильный размер виртуальных машин, и спрогнозировать затраты, как это сделать? Давайте взглянем на некоторые инструменты в Azure, которые помогут решить эту проблему.

## <a name="what-is-azure-advisor"></a>Что такое Azure Advisor? 

**Помощник по Azure** — это бесплатная служба, встроенная в Azure, которая предоставляет рекомендации по обеспечению высокого уровня доступности, безопасности, производительности и сокращению затрат. Помощник анализирует развернутые службы и ищет способы оптимизации среды в этих четырех областях. Мы сосредоточимся на рекомендациях по затратам, но вам лучше изучить и остальные рекомендации.

Помощник дает рекомендации по затратам в следующих областях: 

1. **Сокращение расходов за счет исключения неподготовленных каналов ExpressRoute Azure.** 
    Помощник определяет каналы ExpressRoute, которые находятся в состоянии поставщика *Не подготовлено* больше месяца, и рекомендует удалить такие каналы, если вы не планируете их подготовить с помощью поставщика соединения.

2. **Приобретение зарезервированных экземпляров для экономии средств по сравнению с применением оплаты по мере использования.** 
    Помощник рассмотрит данные об использовании виртуальной машины за последние 30 дней и определит, можете ли вы сэкономить в будущем на приобретении зарезервированных экземпляров. Он предоставит вам данные о регионах и размерах, где вы можете сэкономить больше всего средств, и покажет ожидаемую экономию в результате приобретения зарезервированных экземпляров.
    
3. **Оценка правильного размера или для завершения работы недостаточно загруженных виртуальных машин.** 
    Помощник отслеживает использование виртуальных машин на протяжении 14 дней, а затем определяет недостаточно загруженные виртуальные машины. Виртуальные машины, у которых среднее использование ресурсов ЦП составляет не больше 5 %, а использование ресурсов сети составляет не больше 7 МБ на протяжении четырех или более дней, считаются недостаточно нагруженными. Среднее пороговое значение использования ЦП регулируется до 20 %. Определив недостаточно загруженные виртуальные машины, можно изменить их размер и выбрать меньший экземпляр, чтобы сократить расходы.

Давайте посмотрим, где найти Помощник по Azure на портале. Сначала войдите на портал Azure по адресу [https://portal.azure.com](https://portal.azure.com). Щелкните **Все службы** и в категории **Средства управления** увидите **Помощник**. Или введите **Помощник** в поле фильтра, чтобы найти эту службу. 

Щелкните "Помощник", чтобы перейти на панель мониторинга Помощника, где отображаются все рекомендации для вашей подписки. Вы увидите окно для каждой категории рекомендаций. 

> [!NOTE]
> В Помощнике может не быть рекомендаций по затратам. Возможно, оценка еще не выполнена или у Помощника просто нет рекомендаций.

![Рекомендации Помощника](../images/advisor-recommendations.png)

Нажмите на поле **Расходы**, чтобы получить подробные рекомендации Помощника по затратам.

![Рекомендации Помощника по затратам](../images/advisor-cost-recommendations.png)

Нажмите на любую рекомендацию, чтобы просмотреть подробные сведения. Затем вы сможете принять конкретные меры, например изменить размер виртуальных машин, чтобы сократить расходы.

![Рекомендации Помощника по изменению размера виртуальной машины](../images/advisor-resize-vm.png)

Эти рекомендации показывают ваши неэффективные траты. Это отличный инструмент для начала работы, который можно использовать впоследствии, если вы хотите сократить затраты. В нашем примере есть возможность сэкономить около 700 долларов в месяц, следуя рекомендациям. Эта экономия суммируется, поэтому лучше периодически просматривать рекомендации по всем четырем областям.

## <a name="azure-cost-management"></a>Управление затратами Azure

Управление затратами Azure — это еще одно бесплатное встроенное средство Azure, которое показывает, как вы расходуете деньги в облаке. Вы можете просмотреть подробные данные по затратам на службы за прошлые периоды и соотнести их с настроенным бюджетом. Вы можете настраивать бюджеты, планировать отчеты и анализировать статьи расходов.

![Управление затратами](../images/cost-management.png)

## <a name="cloudyn"></a>Cloudyn 

Cloudyn, дочернее подразделение Майкрософт, позволяет отслеживать использование облака и затраты на ресурсы Azure и других поставщиков облачных услуг, включая Amazon Web Services и Google. Простые для понимания отчеты панели мониторинга помогают с распределением затрат, а также с виртуальными счетами и возвратными платежами. Cost Management помогает оптимизировать расходы на облако, выявляя недостаточно нагруженные ресурсы, которые затем можно настроить. Azure предоставляется бесплатно, но существуют платные варианты поддержки уровня "Премиум" и просмотра данных из других облаков. 

![Панель мониторинга Cloudyn](../images/cloudyn-mgt-dash.png)

## <a name="summary"></a>Сводка

Как видите, в Azure вам доступно несколько бесплатных инструментов, которые можно использовать для отслеживания и прогнозирования расходов на облачные вычисления, а также для выявления неэффективных расходов в вашей среде. Необходимо регулярно просматривать отчеты и рекомендации, предоставляемые этими инструментами, чтобы экономить на использовании облака. Теперь давайте рассмотрим некоторые практические рекомендации по сокращению затрат на инфраструктуру.