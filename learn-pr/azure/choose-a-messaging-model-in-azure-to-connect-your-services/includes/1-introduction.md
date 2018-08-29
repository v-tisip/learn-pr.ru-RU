Многие приложения состоят из программ, выполняющихся на нескольких разных компьютерах или устройствах. Для взаимодействия компонентов таких распределенных приложений необходимо пересылать сообщения по сети на большие расстояния. Слабосвязанные архитектуры даже в пределах одного сервера или центра обработки данных требуют механизмов обмена данными между компонентами. Надежный обмен сообщениями зачастую является критически важной проблемой.

Предположим, вы работаете в компании, которая разрабатывает приложение для обмена музыкой. Музыканты могут добавлять свои произведения на вашу платформу с помощью веб-интерфейса или мобильного приложения. Они также могут прослушивать и комментировать произведения других участников. Приложение состоит из веб-сайта, размещаемого вашим поставщиком услуг Интернета, мобильного приложения, запускаемого на мобильных устройствах пользователей, веб-API, работающего в Azure, и базы данных SQL Azure, в которой хранятся данные.

Вы заметили, что во время высокой нагрузки некоторые музыкальные файлы не передаются и некоторые комментарии не публикуются. Тестирование показывает, что эти проблемы вызываются потерей сообщений, передаваемых между интерфейсными компонентами и веб-API. Вы планируете решить их, используя одну из следующих технологий Azure: очереди службы хранилища, Центры событий, Сетки событий и Служебная шина.

В этом модуле вы узнаете, как выбрать подходящую технологию обмена сообщениями в Azure для каждой задачи взаимодействия в распределенном приложении.

## <a name="learning-objectives"></a>Цели обучения

- Описание событий и сообщений, а также проблем, которые можно решать с их помощью в распределенном приложении.
- Определение сценариев, в которых очередь службы хранилища Azure является оптимальной технологией обмена сообщениями для приложения.
- Определение сценариев, в которых Сетка событий Azure является оптимальной технологией обмена сообщениями для приложения.
- Определение сценариев, в которых Центр событий Azure является оптимальной технологией обмена сообщениями для приложения.
- Определение сценариев, в которых Служебная шина Azure является оптимальной технологией обмена сообщениями для приложения.