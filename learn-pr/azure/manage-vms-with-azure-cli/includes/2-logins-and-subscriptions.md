Прежде чем мы начнем, давайте рассмотрим синтаксис средства интерфейса командной строки Azure (Azure CLI). Если вы изучили модуль **Управления службами Azure с помощью Azure CLI**, то знаете, что команды Azure CLI имеют следующий формат.

```azurecli
az [command] [subcommand] [--parameter --parameter]
```

`[command]` указывает на определенную область Azure, которой вы хотите управлять. Например, вы можете управлять сведениями о подписке с помощь команды `account` или базами данных SQL с помощью команды `sql`. `[subcommand]` и `[--parameters]` зависят от команды, с которой вы работаете. 

Чтобы просмотреть список команд, подкоманд и параметров, введите часть команды. Например, при вводе `az` в командной строке появится экран справки верхнего уровня, а при вводе `az vm` отобразятся все подкоманды для виртуальных машин. Это очень удобный способ изучить средство Azure CLI.

> [!NOTE]
> Мы будем использовать Azure Cloud Shell в браузере для работы с Azure CLI. Если вы предпочитаете работать на локальном компьютере, все эти команды также можно выполнить из командной строки после [установки Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).

## <a name="log-in-to-azure"></a>Вход в Azure

Первое, что вы должны сделать при работе с Azure CLI, — войти в свою учетную запись Azure. Для этого используйте команду `login`. Если вы используете Cloud Shell, у вас будет кнопка для входа в Azure.

```azurecli
az login
```

Эта команда запустит окно браузера, где вы сможете выбрать учетную запись Майкрософт, которую хотите использовать.

## <a name="working-with-subscriptions"></a>Использование подписок

В этом модуле мы будем работать во временной подписке, созданной для изучения, но обычно вы будете использовать подписку из вашей учетной записи. Если у вас несколько подписок, вы можете вывести четко отформатированный список подписок с помощью инструкции `az account list --output table`.

```
Name                                  CloudName    SubscriptionId                        State    IsDefault
------------------------------------  -----------  ------------------------------------  -------  -----------
Contoso Legacy Resources              AzureCloud   abc13b0c-d2c4-64b2-9ac5-2f4cb819b752  Enabled  True
Visual Studio Enterprise              AzureCloud   233aebce-23c2-4572-c056-c029449e93ed  Enabled  False
```

Обратите внимание, что эта команда также задает подписку _по умолчанию_, где применяются все команды. Если вы предпочитаете работать в другой подписке, используйте команду `az account set --subscription "[name]"`. Например, мы можем установить текущую подписку `Visual Studio Enterprise` из приведенного выше списка с помощью следующей команды:

```azurecli
az account set --subscription "Visual Studio Enterprise"
```