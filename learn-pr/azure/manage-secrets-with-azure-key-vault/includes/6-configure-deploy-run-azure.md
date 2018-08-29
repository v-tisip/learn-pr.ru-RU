Пришло время запустить наше приложение в Azure. Нам нужно создать приложение Службы приложений Azure, настроить его с использованием MSI и нашей конфигурации хранилища, а также развернуть код.

## <a name="exercise"></a>Упражнение

### <a name="create-the-app-service-plan-and-app"></a>Создание приложения и плана Службы приложений

Создание приложения Службы приложений состоит из двух этапов: сначала создается *план*, а затем — *приложение*.

Имя *плана* должно быть уникальным только в рамках вашей подписки, поэтому вы можете использовать то же имя, что и мы: **keyvault-exercise-plan**. Имя приложения должно быть уникальным на глобальном уровне, поэтому вам нужно выбрать его самостоятельно.

В Azure Cloud Shell выполните следующее:

```azurecli
az appservice plan create --name keyvault-exercise-plan --resource-group keyvault-exercise-group
az webapp create --name <your-unique-app-name> --plan keyvault-exercise-plan --resource-group keyvault-exercise-group
```

### <a name="add-configuration-to-the-app"></a>Добавление конфигурации в приложение

При развертывании в Azure мы будем следовать рекомендациям для Службы приложений, заключающимся в помещении конфигурации в параметры приложения вместо файла конфигурации.

```azurecli
az webapp config appsettings set --name <your-unique-app-name> --resource-group keyvault-exercise-group --settings VaultName=<your-unique-vault-name>
```

### <a name="enable-msi"></a>Включение MSI

Включение MSI для приложения выполняется одной строкой:

```azurecli
az webapp identity assign --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

В полученных выходных данных JSON скопируйте значение **principalId**. PrincipalId — это уникальный идентификатор нового удостоверения приложения в Azure Active Directory, который мы будем использовать в следующем шаге.

### <a name="grant-access-to-the-vault"></a>Предоставление доступа к хранилищу

Теперь нужно предоставить удостоверению приложения разрешения для получения и перечисления секретов из хранилища рабочей среды. Используйте значение **principalId**, скопированное на предыдущем шаге, в качестве значения **object-id** в приведенной ниже команде.

```azurecli
az keyvault set-policy --name <your-unique-vault-name> --object-id <your-msi-principleid> --secret-permissions get list
```

### <a name="deploy-the-app-and-try-it-out"></a>Развертывание и оценка приложения

Конфигурация настроена, и вы можете приступать к развертыванию. Приведенные ниже команды опубликуют сайт в папке `pub`, запакуют ее в `site.zip` и развернут этот ZIP-файл в Службе приложений.

> [!NOTE]
> Вам потребуется вернуться в каталог KeyVaultDemoApp с помощью команды `cd`, если вы еще это не сделали.

```console
dotnet publish -o pub
zip -j site.zip pub/*
az webapp deployment source config-zip --src site.zip --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

Получив результат, указывающий на развертывание сайта, откройте `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` в браузере. Вы должны увидеть значение секрета **reindeer_flotilla**.

Приложение завершено и развернуто.