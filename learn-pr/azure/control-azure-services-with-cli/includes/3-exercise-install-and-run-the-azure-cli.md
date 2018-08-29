
В этом упражнении вы установите Azure CLI на локальном компьютере и выполните простую команду для проверки установки. 

## <a name="installing-the-azure-cli"></a>Установка Azure CLI
Метод, который вы используете для установки Azure CLI, зависит от операционной системы компьютера. Выберите действия для вашей операционной системы.

### <a name="linux"></a>Linux
Здесь вы устанавливаете Azure CLI на Ubuntu Linux с помощью средства управления пакетами Advanced Packaging Tool (**apt**) и командной строки Bash.

> [!NOTE]
> Ниже перечислены команды для Ubuntu версии 18.04. Если вы используете другую версию Ubuntu, необходимо добавить другой репозиторий. Дополнительные сведения см. в разделе [Установка Azure CLI 2.0 с помощью apt](https://docs.microsoft.com/cli/azure/install-azure-cli-apt).

1. Измените список источников, чтобы зарегистрировать репозиторий Майкрософт, а диспетчер пакетов мог найти пакет Azure CLI.

    ```bash
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```
1. Импортируйте ключ шифрования для репозитория Microsoft Ubuntu. Таким образом диспетчер пакетов сможет убедиться, что устанавливаемый пакет Azure CLI поступает от корпорации Майкрософт.

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. Установите Azure CLI.

    ```bash
    sudo apt-get install apt-transport-https
    sudo apt-get update && sudo apt-get install azure-cli
    ```

### <a name="macos"></a>macOS
Здесь вы устанавливаете Azure CLI в macOS с помощью диспетчера пакетов Homebrew.

> [!IMPORTANT]
> Если команда **brew** недоступна, может потребоваться установить диспетчер пакетов Homebrew. Дополнительные сведения см. на [веб-сайте Homebrew](https://brew.sh/).

1. Обновите репозиторий brew, чтобы убедиться, что вы получите последнюю версию пакета Azure CLI.

    ```bash
    brew update
    ```
1. Установите Azure CLI.

    ```bash
    brew install azure-cli
    ```

### <a name="windows"></a>Windows
Здесь вы устанавливаете Azure CLI в Windows с помощью установщика MSI.

1. Перейдите к [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows) и в диалоговом окне безопасности браузера щелкните **Запуск**.
1. В установщике примите условия лицензионного соглашения и нажмите **Установить**.
1. В диалоговом окне **Контроль учетных записей пользователей** щелкните **Да**.

## <a name="running-the-azure-cli"></a>Запуск Azure CLI
Чтобы запустить Azure CLI, откройте командную оболочку bash (Linux и macOS) или используйте командную строку или PowerShell (Windows).

1. Запустите Azure CLI и проверьте правильность установки, выполнив проверку версии.

    ```bash
    az --version
    ```

> [!NOTE]
> В Windows запуск Azure CLI с помощью PowerShell имеет некоторые преимущества по сравнению с запуском Azure CLI из командной строки. Например, PowerShell предоставляет дополнительные функции завершения с помощью Tab по сравнению с набором функций, доступных из командной строки. 

## <a name="summary"></a>Сводка
Вы настроили локальные компьютеры для администрирования ресурсов Azure с помощью Azure CLI. Теперь вы можете использовать Azure CLI локально для ввода команд или выполнения скриптов. Azure CLI будет пересылать команды в центры обработки данных Azure, где они будут выполняться в вашей подписке Azure.
