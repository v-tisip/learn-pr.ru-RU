Для стека компонентов MEAN требуется сервер. Это может быть компьютер под управлением Linux или виртуальная машина в вашем локальном серверном окружении или облачная виртуальная машина. В этом модуле мы настроим работу стека на виртуальной машине Ubuntu Linux, работающей в Azure.

В этом упражнении вы создадите в Azure виртуальную машину Ubuntu Linux. Вместо этого вы можете установить компоненты стека MEAN на существующей виртуальной машины или физическом компьютере. Создав виртуальную машину для этого упражнения, вы сможете собрать все компоненты в группу ресурсов Azure, чтобы упростить управление ресурсами и очистку после завершения работы.

Для создания виртуальной Машины Linux мы будем использовать командную строку Cloud Shell, интегрированную в портал Azure.

## <a name="provision-an-ubuntu-linux-vm"></a>Подготовка виртуальной машины Ubuntu Linux

1. Перейдите на [портал Azure](https://portal.azure.com?azure-portal=true).
1. Откройте Cloud Shell с помощью значка `>_` на панели инструментов портала Azure.
1. Выполните в Cloud Shell команду создания группы ресурсов Azure, куда будет входить новая виртуальная машина. Введите произвольное имя группы ресурсов вместо `<resource-group-name>` и нужное расположение Azure вместо `<resource-group-location>` (например, `westus`).

    ```bash
    az group create --name <resource-group-name> --location <resource-group-location>
    ```

    Запомните это имя группы ресурсов — оно будет использоваться в других командах.

1. Введите в Cloud Shell следующие команды, чтобы создать виртуальную машину Ubuntu Linux. Введите произвольное имя группы ресурсов вместо `<resource-group-name>`, а также имя пользователя и пароль администратора вместо `<vm-admin-username>` и `<vm-admin-password>`.

    ```bash
    az vm create \
        --resource-group <resource-group-name> \
        --name MeanDemo \
        --image UbuntuLTS \
        --admin-username <vm-admin-username> \
        --admin-password <vm-admin-password> \
        --generate-ssh-keys
    ```

    Запишите имя пользователя и пароль администратора, чтобы позднее подключиться к этой виртуальной машине.

    Выполнение этой команды занимает около 2 минут. Затем эта команда возвращает примерно такой результат:

    ```json
    {
        "fqdns": "",
        "id": "...",
        "location": "<location you chose for the resource group>",
        "macAddress": "00-0D-3A-3A-54-EC",
        "powerState": "VM running",
        "privateIpAddress": "10.0.0.4",
        "publicIpAddress": "<the public IP address of the newly created machine>",
        "resourceGroup": "<name you chose for thr resource group>",
        "zones": ""
    }
    ```

    Теперь сохраните общедоступный IP-адрес новой виртуальной машины, который потребуется для подключения к ней.

1. Попробуйте подключиться к созданной виртуальной машине.

    Откройте окно командной строки или терминала и выполните следующую команду: Замените заполнители `<vm-admin-username>` и `<vm-public-ip>` именем пользователя администратора и общедоступным IP-адресом виртуальной машину, которые вы настроили выше.

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

    При первом подключении к компьютеру вам будет предложено подтвердить, что вы доверяете удаленному компьютеру. Если вы ответите `yes`, отпечаток ключа ECDSA удаленного компьютера будет сохранен локально, чтобы все последующие подключения считались доверенными.

    Если все работает правильно, введите `exit` и закройте сеанс SSH.

1. Откройте порт 80, чтобы разрешить входящий трафик по протоколу HTTP к новому веб-приложению.

    Вернитесь к приглашению Cloud Shell на портале Azure и выполните следующую команду, указав свое имя группы ресурсов вместо `<resource-group-name>`.

    ``` bash
    az vm open-port --port 80 --resource-group <resource-group-name> --name MeanDemo
    ```

    Это действие открывает HTTP-порт на виртуальной машине с именем MeanDemo.

## <a name="summary"></a>Сводка

Теперь новая виртуальная машина Ubuntu Linux готова к работе, и вы можете подключиться к ней и установить разные компоненты стека MEAN.
