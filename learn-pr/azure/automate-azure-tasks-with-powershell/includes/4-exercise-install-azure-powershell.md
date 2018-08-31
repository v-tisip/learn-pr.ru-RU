В этом упражнении вы установите **Azure PowerShell** на локальный компьютер. Выберите подходящий раздел для вашей операционной системы.

## <a name="linux-and-mac"></a>Linux и Mac
В Linux и macOS первым шагом будет установка **PowerShell Core**.

### <a name="linux"></a>Linux
Как упоминалось в последнем разделе, установка PowerShell для Linux осуществляется с помощью диспетчера пакетов. В нашем примере мы будем использовать **Ubuntu 18.04**, но у нас есть [подробные инструкции для других версий и дистрибутивов в нашей документации](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).

PowerShell Core устанавливается в Ubuntu Linux с помощью средства управления пакетами Advanced Packaging Tool (**apt**) и командной строки Bash. 

1. Импортируйте ключ шифрования для репозитория Microsoft Ubuntu. Таким образом диспетчер пакетов сможет убедиться, что устанавливаемый пакет PowerShell Core поступает от корпорации Майкрософт.

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. Зарегистрируйте **репозиторий Microsoft Ubuntu**, чтобы диспетчер пакетов мог найти пакет PowerShell Core.

    ```bash
    sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list
    ```

1. Обновите список пакетов.

    ```bash
    sudo apt-get update
    ```

1. Установите PowerShell Core.

    ```bash
    sudo apt-get install -y powershell
    ```

1. Запустите PowerShell, чтобы убедитесь, что он успешно установлен.

    ```bash
    pwsh
    ```

### <a name="macos"></a>macOS
Затем установите **PowerShell Core** в macOS с помощью диспетчера пакетов Homebrew.

> [!IMPORTANT]
> Если команда **brew** недоступна, может потребоваться установить диспетчер пакетов Homebrew. Дополнительные сведения см. на [веб-сайте Homebrew](https://brew.sh/).

1. Установите Homebrew-Cask, чтобы получить дополнительные пакеты, включая пакет PowerShell Core:

    ```bash
    brew tap caskroom/cask
    ```
1. Установите PowerShell Core:

    ```bash
    brew cask installs powershell
    ```

1. Запустите PowerShell Core, чтобы убедитесь, что он успешно установлен:

    ```bash
    pwsh
    ```

## <a name="install-azure-powershell"></a>Установите Azure PowerShell
После установки базового продукта **PowerShell** установите **Azure PowerShell**, чтобы добавить команды, характерные для Azure.

### <a name="windows"></a>Windows
Установите Azure PowerShell в Windows с помощью команды PowerShell `Install-Module`.

> [!IMPORTANT]
> Чтобы установить Azure PowerShell, требуется PowerShell начиная с версии 5.0. Чтобы проверить версию PowerShell, используйте следующую команду: 
>
> `$PSVersionTable.PSVersion` 
>
>Если номер версии ниже, чем 5.0, следуйте инструкциям по [обновлению существующей версии Windows PowerShell](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).

1. Откройте меню **Пуск** и введите **Windows PowerShell**.
2. Щелкните правой кнопкой мыши значок **Windows PowerShell** и выберите **Запуск от имени администратора**.
3. В диалоговом окне **Контроль учетных записей пользователей** щелкните **Да**.
4. Введите следующую команду и нажмите клавишу ВВОД:

    ```powershell
    Install-Module -Name AzureRM
    ```
5. Если у вас спросят, доверяете ли вы модулям из PSGallery, ответьте **Да** или **Да для всех**.

> [!NOTE]
> Если появится сообщение об ошибке, указывающее, что версия модуля Azure PowerShell уже установлена, можно выполнить обновление до _последней_ версии с помощью команды:
> 
> `Update-Module -Name AzureRM`
> 
> Как и для команды `Install-Module`, ответьте **Да** или **Да для всех** при появлении запроса на доверие модулю.

### <a name="linux-or-macos"></a>Linux и macOS
Мы используем тот же базовый процесс для установки Azure PowerShell в macOS или Linux. Процедура будет одинаковой для обеих операционных систем. Различие заключается в создании сеанса с повышенными привилегиями PowerShell Core.

1. В окне терминала введите следующую команду, чтобы запустить PowerShell Core с повышенными привилегиями.

    ```bash
    sudo pwsh
    ```

1. Выполните следующую команду в командной строке PowerShell Core, чтобы установить Azure PowerShell.

    ```powershell
    Install-Module AzureRM.NetCore
    ```

1. Если у вас спросят, доверяете ли вы модулям из **PSGallery**, ответьте **Да** или **Да для всех**.

## <a name="summary"></a>Сводка
Вы настроили локальные компьютеры для администрирования ресурсов Azure с помощью Azure PowerShell. Теперь вы можете использовать Azure PowerShell локально для ввода команд или выполнения скриптов. Azure PowerShell будет пересылать команды в центры обработки данных Azure, где они будут выполняться в вашей подписке Azure.
