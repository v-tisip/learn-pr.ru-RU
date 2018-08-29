Допустим, вы фотограф и у вас есть веб-сайт, где вы показываете свои фото дня. Из-за занятости вы не можете загружать фотографии в одно и то же время, но хотите уведомлять своих поклонников о загрузке новых снимков. Вы решили создать функцию Azure, которая будет автоматически публиковать сообщение в Twitter при загрузке каждого изображения в контейнер BLOB-объектов хранилища Azure.

Здесь вы узнаете, как создать триггер BLOB-объектов и настроить его для мониторинга определенного расположения в контейнере BLOB-объектов хранилища Azure.

## <a name="what-is-azure-storage"></a>Что такое хранилище Azure?

Хранилище Azure — это решение облачного хранилища Майкрософт, которое поддерживает все типы данных, включая BLOB-объекты, очереди и NoSQL. Хранилище Azure предоставляет хранилище данных, обладающее следующими свойствами:

- высокая доступность,
- Безопасность
- масштабируемость,
- Управляемые

Мы не будем долго говорить о хранилище Azure. Вместо этого мы создадим BLOB-объекты, которые будут запускать выполнение функции.

## <a name="what-is-azure-blob-storage"></a>Что такое хранилище BLOB-объектов Azure?

Хранилище BLOB-объектов Azure — это решение хранилища объекта, предназначенное для хранения больших объемов неструктурированных данных. 

Например, хранилище BLOB-объектов Azure отлично подходит для выполнения таких задач, как:

- Хранение файлов.
- Обслуживание файлов.
- Потоковая передача видео и аудио.
- Ведение журнала данных.

Существует три типа BLOB-объектов: **блочные**, **добавочные** и **страничные**. Чаще всего используются блочные BLOB-объекты. Они позволяют эффективно хранить текстовые или двоичные данные. Добавочные BLOB-объекты похожи на блочные, но предназначены для добавления таких операций, как создание постоянно обновляемого файла журнала. И, наконец, страничные BLOB-объекты состоят из страниц и предназначены для частых произвольных операций чтения и записи.

## <a name="what-is-a-blob-trigger"></a>Что такое триггер BLOB-объектов?

Триггер BLOB-объектов — это триггер, который запускает выполнение функции при передаче или обновлении файла в хранилище BLOB-объектов Azure. Для создания триггера BLOB-объектов создайте учетную запись хранения Azure и укажите расположение, которое триггер будет отслеживать.

## <a name="how-to-create-a-blob-trigger"></a>Создание триггера BLOB-объектов

Как и другие триггеры, о которых мы уже говорили, триггер BLOB-объектов создается на портале Azure. В функции Azure выберите в списке стандартных типов триггеров **триггер BLOB-объектов**. Затем введите логику, которая будет выполняться при создании или обновлении BLOB-объекта.

Один из интересующих нас параметров — это **путь**. **Путь** сообщает триггеру BLOB-объектов, какое расположение он должен отслеживать на предмет загрузки или обновления BLOB-объектов. Значение параметр **Путь** по умолчанию: 

> samples-workitems/{name}

Разделим его на две части: *samples-workitems* и *{name}*. Первая часть, *samples-workitems*, представляет контейнер BLOB-объектов, который отслеживается триггером. Вторая часть *{name}*, означает, что каждый тип файла заставляет триггер вызывать функцию. Функция вызывается, поскольку нет фильтра. Например, можно сделать так, чтобы триггер вызывал функцию только при добавлении PNG-файлов с использованием следующего синтаксиса:

> samples-workitems/{name}.png

Второй важный элемент информации в этом компоненте — это текстовое *имя*. *Имя* представляет собой параметр функции Azure, который получает имя добавляемого файла. Например, при отправке файла с именем *resume.txt* моя функция Azure получает это значение в виде строки через параметр *имя*.

## <a name="summary"></a>Сводка

Триггер BLOB-объектов вызывает функцию Azure при обнаружении действия в определенном расположении в вашей учетной записи хранилища BLOB-объектов Azure. Чтобы задать расположение для мониторинга, измените значение параметра **Путь** на портале Azure.