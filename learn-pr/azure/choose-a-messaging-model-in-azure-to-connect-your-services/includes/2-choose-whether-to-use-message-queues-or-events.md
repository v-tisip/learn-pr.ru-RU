Предположим, вы планируете архитектуру распределенного приложения для обмена музыкой. Вам необходимо обеспечить максимальную надежность и масштабируемость приложения, и вы намереваетесь использовать технологии Azure для создания эффективной инфраструктуры обмена данными.

Чтобы выбрать подходящую технологию Azure, необходимо понимать, какими именно данными обмениваются компоненты приложения. Для каждого типа данных можно выбрать свою технологию Azure.

В первую очередь следует понимать, отправляются ли сообщения или события. Некоторые технологии Azure предназначены для событий, а другие — для сообщений, поэтому это принципиальный вопрос.

## <a name="what-is-a-message"></a>Что такое сообщение?

В терминах распределенных приложений **сообщения** обладают указанными ниже характеристиками.

- Сообщение содержит необработанные данные, которые создаются одним компонентом и будут использоваться другим.
- Сообщение содержит сами данные, а не просто ссылку на них.
- Отправляющий компонент предполагает, что компонент-получатель будет обрабатывать содержимое сообщения определенным образом. Целостность всей системы может зависеть от выполнения отправляющей и принимающей сторонами определенных задач.

Например, предположим, что пользователь добавляет новую песню с помощью мобильного приложения для обмена музыкой. Мобильное приложение должно отправить эту песню в веб-API, работающий в Azure. Необходимо отправить сам файл мультимедиа, а не просто оповещение о добавлении новой песни. Мобильное приложение предполагает, что веб-API сохранит новую песню в базе данных и откроет к ней доступ для других пользователей. Это пример сообщения.

## <a name="what-is-an-event"></a>Что такое событие?

**События** имеют меньший размер, чем сообщения, и чаще всего применяются для широковещательной рассылки. Компоненты, отправляющие события, называются **издателями**, а принимающие их — **подписчиками**.

Принимающие компоненты обычно решают, какие события их интересуют, и "подписываются" на них. Управление подпиской, как правило, осуществляет посредник, например Сетка событий Azure или Центр событий Azure. Когда издатель отправляет событие, посредник направляет его соответствующим подписчикам. Такая схема называется архитектурой типа "публикация-подписка". Это не единственный способ обработки событий, но наиболее распространенный.

События обладают указанными ниже характеристиками.

- Событие — это упрощенное уведомление о том, что нечто произошло.
- Событие может отправляться нескольким получателям или ни одному.
- События часто предполагают рассылку, то есть у одного издателя может быть много подписчиков.
- У издателя события нет ожиданий относительно того, какое действие предпримет принимающий компонент.
- Некоторые события являются дискретными и не связаны с другими событиями. 
- Другие входят в связанные и упорядоченные последовательности.  

Например, предположим, что отправка музыкального файла завершилась и новая песня была добавлена в базу данных. Чтобы пользователи веб-интерфейса и мобильного приложения узнали об этом, веб-API должен оповестить их. Пользователи сами решают, хотят ли они прослушать новую песню, поэтому начальное уведомление не должно содержать музыкальный файл, а только сообщать о его существовании. Отправитель не предполагает, что получатели события выполнят какое-либо конкретное действие в ответ на получение события.

Это пример дискретного события.

## <a name="how-to-choose-messages-or-events"></a>Выбор сообщений или событий

В приложении, как правило, события используются в одних целях, а сообщения — в других. Перед тем как делать выбор, следует проанализировать архитектуру приложения и все сценарии его применения, чтобы определить, в каких целях его компоненты взаимодействуют друг с другом. 

События чаще используются для широковещательной рассылки, которая может быть безрезультативной, если ни один получатель в настоящее время не подписан на них. Сообщения же обычно применяются, когда распределенному приложению требуется гарантия того, что данные будут обработаны.

Для каждого взаимодействия необходимо ответить на вопрос: предполагает ли отправляющий компонент, что получатель обработает переданное содержимое определенным образом?

Если ответ утвердительный, используйте сообщения. Если отрицательный, можно использовать события.

## <a name="summary"></a>Сводка

Компоненты распределенного приложения взаимодействуют друг с другом в различных целях. В каждом случае необходимо решить, следует ли использовать события или сообщения. От этого будет зависеть выбор соответствующей технологии Azure. 

Определив цели взаимодействия между компонентами и выбрав события или сообщения, вы можете далее решить, следует ли применять для обмена данными очереди службы хранилища Azure, Центры событий, Сетки событий или Служебную шину.