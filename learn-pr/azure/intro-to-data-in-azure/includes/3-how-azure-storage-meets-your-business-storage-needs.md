Ознакомившись с преимуществами хранилища Azure, вы пришли к выводу, что оно подходит для хранения вашего портала обучения лучше всего. Теперь подробно рассмотрим преимущества и возможности хранилища Azure, чтобы узнать, соответствует ли оно потребностям вашей организации.

## <a name="how-azure-storage-can-meet-your-business-storage-needs"></a>Удовлетворение потребностей бизнеса в хранении данных с помощью службы хранилища Azure

Хранилище Azure предоставляет разные возможности, включая типы требований к хранилищам данных.

### <a name="azure-sql-database"></a>База данных SQL Azure

**База данных SQL Azure** — это надежная, полностью управляемая реляционная облачная база данных, где хранятся ваши данные. Эту функцию можно использовать для хранения часто используемых и обновляемых данных, таких как личные данные и информация об обучении сотрудников. Существующие базы данных SQL Server можно переносить без изменения приложений.

![AzureSQL](../images/Azure_SQL.png)

### <a name="azure-cosmos-db"></a>Azure Cosmos DB

Azure Cosmos DB — это признанная функция Azure, которая представляет собой глобально распределенную базу данных. Она поддерживает неструктурированные данные, позволяя создавать быстродействующие, *всегда доступные* приложения для поддержки постоянно изменяющихся данных. Эту функцию можно использовать для хранения данных, которые обновляются и обслуживаются на основе входных параметров, предоставляемых пользователями со всего мира.

![Cosmos DB](../images/Azure_cosmos_db.png)

### <a name="azure-blob-storage"></a>Хранилище больших двоичных объектов Azure

Хранилище BLOB-объектов предоставляет возможность потоковой передачи больших звуковых и видеофайлов непосредственно в браузер пользователя из любой точки мира. Хранилище BLOB-объектов также используется для хранения данных, предназначенных для резервного копирования и восстановления, аварийного восстановления и архивации. Хранилище BLOB-объектов Azure вмещает до 8 ТБ файлов для виртуальных машин.

![AzureBlob](../images/Azure_blob.png)

### <a name="azure-data-lake-storage-gen2"></a>Хранилище Azure Data Lake Gen2

Функция озера данных в хранилище Azure позволяет анализировать использование данных и формировать соответствующие отчеты. Озеро данных — это большой репозиторий, в котором хранятся как структурированные, так и неструктурированные данные.

**Хранилище Azure Data Lake Gen2** объединяет масштабируемость и экономичность хранилища объектов с надежностью и производительностью файловой системы больших объемов данных.

![Data_lake_Store_concept](../images/Data_lake_store_concept.png)

### <a name="azure-files"></a>Файлы Azure

Файлы Azure предлагают полностью управляемые общие файловые ресурсы в облаке. Приложения, работающие в Azure, могут легко обмениваться файлами между виртуальными машинами. Общие файловые ресурсы Azure можно одновременно использовать и в облачных, и в локальных развертываниях Windows, Linux и macOS.

![Azure_Files](../images/Azure_Files.png)

### <a name="azure-queue"></a>Очередь Azure

Хранилище очередей Azure — это служба хранения большого количества сообщений, к которым можно получить доступ практически из любой точки мира. Размер одного сообщения в очереди может составлять до 64 КБ, а очередь может содержать миллионы сообщений.

Очередь в основном используется:

- Для создания журнала невыполненной работы и обмена сообщениями между различными веб-серверами Azure.
- Для распределения нагрузки между различными веб-серверами и инфраструктурой и управления пиками трафика.
- Для обеспечения устойчивости к сбоям компонентов, когда несколько пользователей обращаются к данным в одно и то же время.

![Azure_Queue](../images/Azure_Queue.png)

### <a name="azure-standard-storage"></a>Служба хранилища Azure класса Standard

Виртуальные машины в Azure используют диски как место хранения операционной системы, приложений и данных. Хранилище Azure класса Standard обеспечивает поддержку надежных экономически эффективных дисков для виртуальных машин, на которых выполняются критически важные рабочие нагрузки. Данные, переданные в хранилище класса Standard, хранятся на жестких дисках.

Стандартные диски SSD и жесткие диски можно использовать для виртуальных машин при выполнении менее важных рабочих нагрузок, а премиальные диски SSD — для критически важных рабочих приложений. Они гарантируют согласованную надежность корпоративного уровня с ведущим в отрасли нулевым показателем процента брака по итогам продаж в течение одного года.

![Azure_disk](../images/Azure_disks.png)

### <a name="storage-tiers"></a>Уровни хранилища

Хранилище Azure предлагает три уровня для хранения BLOB-объектов:

1. **Горячий уровень хранилища Azure** — оптимизирован для хранения часто используемых данных. 
1. **Холодный уровень хранилища Azure** — оптимизирован для хранения данных, которые используются редко и хранятся не менее 30 дней.
1. **Архивный уровень хранилища Azure** — оптимизирован для хранения данных, которые используются редко и хранятся не менее 180 дней с гибкими требованиями к задержке. Архивное хранилище Azure идеально подходит для хранения старых версий данных, которые можно извлекать для аудита или других нечастых действий.

![Archive_Tier](../images/Archive_Storage_Tier.png)

### <a name="azure-storage-encryptionreplication"></a>Шифрование/репликация службы хранилища Azure

Хранилище Azure обеспечивает безопасность и высокий уровень доступности ваших данных за счет шифрования и репликации.

#### <a name="encryption-for-storage-services"></a>Шифрование для службы хранилища

Для ваших ресурсов доступны следующие типы шифрования:

1. **Шифрование службы хранилища Azure (SSE)** для неактивных данных помогает защитить данные в соответствии с корпоративными требованиями к обеспечению безопасности и соответствию стандартам. SSE Azure шифрует данные перед их сохранением и расшифровывает их перед извлечением. Шифрование и расшифровка прозрачны для пользователя.
1. **Шифрование на стороне клиента**, когда данные уже зашифрованы клиентскими библиотеками. Azure хранит неиспользуемые данные в зашифрованном состоянии и расшифровывает их во время извлечения.

    Эта функция шифрования гарантирует соответствие ваших данных стандартам глобальной защиты. Она подходит для хранения конфиденциальной информации, такой как личные или финансовые данные.

#### <a name="replication-for-storage-availability"></a>Репликация для доступности хранилища

Тип репликации выбирается при создании учетной записи хранения. Функция репликации обеспечивает долговечность и постоянную доступность ваших данных. Хранилище Azure обеспечивает региональную и географическую репликацию для защиты данных от стихийных бедствий и локальных катастроф, таких как пожар или наводнение.
