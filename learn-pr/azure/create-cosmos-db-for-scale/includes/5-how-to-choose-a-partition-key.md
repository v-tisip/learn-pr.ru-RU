Розничный интернет-магазин, в котором вы работаете, в ближайшем будущем планирует выйти в новый регион. Расширение приведет к увеличению клиентской базы и объема операций. Вам необходимо сделать так, чтобы ваша база данных могла справиться с таким расширением.

Стратегия секционирования позволяет гарантировать, что база данных сможет легко увеличиваться по мере необходимости и продолжать эффективно обрабатывать запросы и транзакции.

## <a name="what-is-a-partition-strategy"></a>Что такое стратегия секционирования?

Если продолжать добавлять новые данные на один сервер или в одну секцию, рано или поздно место закончится. Чтобы подготовиться к этому, необходимо реализовать стратегию секционирования, предусматривающую **горизонтальное масштабирование**, а не вертикальное. Горизонтальное масштабирование позволяет добавлять секции в базу данных, когда это требуется приложению.

Стратегия секционирования и горизонтального масштабирования в Azure Cosmos DB основана на ключе секции, значение которого задается во время создания коллекции. После того как ключ секции задан, его можно изменить, только повторно создав коллекцию. Поэтому выбор ключа — важное решение, которое следует принимать на ранних этапах процесса разработки.  

В этом модуле вы узнаете, как выбрать подходящий ключ секции, который позволит использовать возможности автоматического масштабирования в Azure Cosmos DB.

## <a name="partition-key-basics"></a>Основные сведения о ключе секции

Ключ секции представляет собой часто запрашиваемое значение в базе данных. Поэтому для розничного интернет-магазина в его качестве целесообразно использовать, например, идентификатор пользователя или идентификатор товара. Идентификатор пользователя является хорошим выбором по той причине, что приложению часто необходимо получать, помимо прочего, параметры персонализации, сведения о корзине, журнал заказов и данные профиля. Идентификатор товара — также неплохой выбор, так как приложению требуется запрашивать уровень запасов, стоимость доставки, варианты расцветки, расположение складов и т. д.

Ключ секции должен обеспечивать распределение операций по базе данных. Распределять запросы необходимо для того, чтобы избежать образования перегруженных секций. Перегруженной является такая секция, которая получает гораздо больше запросов, чем другие, из-за чего возникает узкое место. Например, для приложения электронной коммерции текущее время плохо подходит в качестве ключа секции, так как все входящие данные будут поступать в одну секцию. Идентификатор пользователя или товара подойдет лучше, так как все пользователи вашего сайта, скорее всего, будут добавлять и обновлять данные корзины и профиля приблизительно с одинаковой частотой, благодаря чему операции чтения и записи будут распределяться по всем секциям. Изменения сведений о товарах также будут происходить достаточно равномерно.

Каждый ключ секции имеет максимальное пространство для хранения, равное 10 ГБ. Это размер одной физической секции в Azure Cosmos DB. Поэтому если размер одной записи с идентификатором пользователя или товара может превышать 10 ГБ, рекомендуем использовать составной ключ. Примером составного ключа может быть запись типа "ИДПользователя-дата" со значением "ИмяКлиента-08072018". При таком подходе можно создавать новую секцию для каждого дня, в который пользователь посетил сайт.

## <a name="best-practices"></a>Рекомендации

Если вы пытаетесь определить подходящий ключ секции, но решение неочевидно, следуйте приведенным ниже советам.

* Не бойтесь использовать слишком много ключей секций. Чем больше ключей, тем выше масштабируемость.

* Чтобы выбрать оптимальный ключ секции для рабочей нагрузки с высокой интенсивностью чтения, обратите внимание на три-пять самых часто используемых запросов. Значение, которое чаще всего включается в предложение WHERE, — подходящий претендент.

* Для рабочих нагрузок с высокой интенсивностью записи необходимо проанализировать их потребности в обработке транзакций, так как ключ секции входит в область транзакций с несколькими документами.