Предположим, вы выбрали Azure PowerShell в качестве решения для автоматизации. Ваши администраторы предпочитают выполнять скрипты локально, а не в Azure Cloud Shell. Команда использует компьютеры с операционными системами Linux, macOS и Windows. Вам нужно наладить работу Azure PowerShell на всех этих устройствах. 

## <a name="what-must-be-installed"></a>Что необходимо установить?
В следующем модуле будут приведены конкретные инструкции по установке, пока же рассмотрим два компонента, составляющих Azure PowerShell.

- **Основной продукт PowerShell**. Он доступен в двух вариантах: PowerShell в Windows или PowerShell Core в macOS и Linux.
- **Модуль Azure PowerShell**. Этот дополнительный модуль необходимо установить, чтобы добавить в PowerShell команды, относящиеся к Azure.

> [!NOTE]
> PowerShell входит в состав Windows (однако может быть доступно обновление). В Linux и macOS PowerShell Core необходимо установить отдельно.

После установки базового продукта добавьте модуль Azure PowerShell.

## <a name="how-to-install-powershell-core"></a>Установка PowerShell Core
В Linux и macOS необходимо установить PowerShell Core с помощью диспетчера пакетов. Рекомендуемый диспетчер пакетов зависит от ОС и дистрибутива.

> [!NOTE]
> PowerShell Core доступен в репозитории Майкрософт, поэтому сначала необходимо добавить этот репозиторий в диспетчер пакетов.

### <a name="linux"></a>Linux
В Linux диспетчер пакетов зависит от выбранного дистрибутива.

| Дистрибутивы  | Диспетчер пакетов |
|------------------|-----------------|
| Ubuntu, Debian   | `apt-get`       |
| Red Hat, CentOS  | `yum`           |
| OpenSUSE         | `zypper`        |
| Fedora           | `dnf`           |

### <a name="mac"></a>Mac
В macOS для установки PowerShell Core используется `Homebrew`.

## <a name="how-to-install-azure-powershell"></a>Установка Azure PowerShell
После установки PowerShell предпочтительным способом установки модуля Azure PowerShell является использование команды `Install-Module` из PowerShell. Для установки модулей требуется более высокий уровень привилегий.

- В Windows необходимо запустить PowerShell от имени администратора.
- В Linux и MacOS для получения повышенных привилегий используйте команду `sudo`.

## <a name="summary"></a>Сводка
В Windows оболочка PowerShell является встроенной, однако модуль Azure PowerShell необходимо установить. В Linux и macOS следует установить как PowerShell Core, так и модуль Azure PowerShell. В следующем разделе приводятся подробные инструкции по установке на некоторых распространенных платформах.