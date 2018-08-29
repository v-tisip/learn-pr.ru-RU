В этом модуле вы узнали, как использовать хранилище BLOB-объектов Azure для хранения данных веб-приложения. Мы привели советы по созданию стратегии использования хранилища BLOB-объектов в веб-приложении и применению SDK службы хранилища Azure для .NET Core с целью записи данных в BLOB-объекты и считывания данных из них. Созданное нами приложение принимает файлы, отправляемые пользователями, сохраняет их в хранилище BLOB-объектов и предоставляет к ним доступ для скачивания.

## <a name="cleanup"></a>Очистка

Чтобы очистить подписку Azure, выполните в Azure Cloud Shell приведенную ниже команду. Она удаляет группу ресурсов, содержащую все созданные в этом модуле ресурсы.

```console
az group delete --name blob-exercise-group
```

Чтобы очистить хранилище Cloud Shell, удалите каталог `TODO` с помощью команды `rm -rf TODO`.

## <a name="additional-resources"></a>Дополнительные ресурсы

**Перекрестные ссылки на каталог docset TODO?**

* **Безопасное хранение ключей учетной записи хранения**. Наиболее надежным решением для хранения секретных данных конфигурации является Azure Key Vault. Сведения об использовании Key Vault в приложении ASP.NET Core см. [здесь](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x). Кроме того, вы можете безопасно хранить строки подключения в параметрах приложения службы приложений и использовать [средство ASP.NET Core Secret Manager](https://docs.microsoft.com/aspnet/core/security/app-secrets?view=aspnetcore-2.1&tabs=windows) для поддержки сред разработки.
* [Отправка больших файлов с помощью потоковой передачи в ASP.NET Core](https://docs.microsoft.com/aspnet/core/mvc/models/file-uploads?view=aspnetcore-2.1#uploading-large-files-with-streaming)
* [Параллелизм BLOB-объектов: AccessConditions и аренда BLOB-объектов](https://azure.microsoft.com/blog/managing-concurrency-in-microsoft-azure-storage-2/)
* [Предоставление ограниченного доступа к объекту службы хранилища Azure с помощью подписанных URL-адресов](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1)
* [Индексация хранилища BLOB-объектов с помощью Поиска Azure](https://docs.microsoft.com/azure/search/search-howto-indexing-azure-blob-storage)
* [Ограничения для контейнеров и имен BLOB-объектов](https://docs.microsoft.com/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata#resource-names)