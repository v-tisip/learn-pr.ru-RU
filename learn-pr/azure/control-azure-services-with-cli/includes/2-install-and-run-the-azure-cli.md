## <a name="motivation"></a>Мотивация
Предположим, ваша организация выбрала Azure CLI в качестве программы командной строки для управления ресурсами Azure. Ваши администраторы и разработчики предпочитают выполнять команды и скрипты локально, а не в браузере. Команда использует компьютеры с операционными системами Linux, macOS и Windows. Вам нужно наладить работу Azure CLI на всех этих устройствах.

## <a name="what-is-the-azure-cli"></a>Что такое Azure CLI?
Azure CLI представляет собой программу командной строки, с помощью которой можно подключаться к Azure и выполнять команды для администрирования ресурсов Azure. Например, для перезапуска виртуальной машины используется следующая команда:

 ```bash
 az vm restart -g MyResourceGroup -n MyVm
 ```

Интерфейс Azure CLI предоставляет кроссплатформенные средства командной строки для управления ресурсами Azure. Его можно устанавливать локально на компьютерах с ОС Linux, Mac и Windows. С интерфейсом Azure CLI можно также работать в браузере посредством Azure Cloud Shell. В обоих случаях его можно использовать интерактивно или с помощью скриптов. При интерактивном использовании вы сначала запускаете оболочку, например cmd.exe в Windows или Bash в Linux или macOS, а затем выполняете команду в командной строке. Чтобы автоматизировать повторяющиеся задачи, вы объединяете команды CLI в скрипт, используя синтаксис выбранной оболочки, а затем выполняете его.

## <a name="how-to-install-azure-cli"></a>Установка Azure CLI
В Linux и macOS необходимо установить PowerShell Core с помощью диспетчера пакетов. Рекомендуемый диспетчер пакетов зависит от ОС и дистрибутива:
- Linux: **apt-get** в Ubuntu, **yum** в Red Hat и **zypper** в OpenSUSE
- Mac: **Homebrew**

Интерфейс Azure CLI доступен в репозитории Майкрософт, поэтому сначала необходимо добавить этот репозиторий в диспетчер пакетов.

В Windows для установки Azure CLI необходимо скачать и запустить файл MSI.

## <a name="using-the-azure-cli-in-scripts"></a>Использование Azure CLI в скриптах
Если вы хотите использовать команды Azure CLI в скриптах, необходимо знать все особенности оболочки или среды, применяемой для выполнения скриптов. Например, в оболочке bash для задания переменных используется следующий синтаксис:

 ```bash
 variable="string"
 variable=integer
 ```

Если для запуска скриптов Azure CLI применяется среда PowerShell, для переменных следует использовать следующий синтаксис:

 ```powershell
 $variable="string"
 $variable=integer
 ```

## <a name="summary"></a>Сводка
Прежде чем использовать интерфейс Azure CLI для управления ресурсами Azure с локального компьютера, его необходимо установить. Инструкции по установке для Windows, Linux и macOS различаются, однако после установки команды для всех платформ одинаковы. 