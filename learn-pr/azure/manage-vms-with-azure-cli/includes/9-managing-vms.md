<span data-ttu-id="00b78-101">Одна из основных задач при работе с виртуальными машинами — их запуск и остановка.</span><span class="sxs-lookup"><span data-stu-id="00b78-101">One of the main tasks you'll want to do to running virtual machines is to start and stop them.</span></span>

## <a name="stopping-a-vm"></a><span data-ttu-id="00b78-102">Остановка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="00b78-102">Stopping a VM</span></span>

<span data-ttu-id="00b78-103">Остановить работающую виртуальную машину можно с помощью команды `vm stop`.</span><span class="sxs-lookup"><span data-stu-id="00b78-103">We can stop a running VM with the `vm stop` command.</span></span> <span data-ttu-id="00b78-104">В ней необходимо передать имя и группу ресурсов или уникальный идентификатор виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="00b78-104">You must pass the name and resource group, or the unique ID for the VM:</span></span>

```azurecli
az vm stop -n SampleVM -g ExerciseResources
```

<span data-ttu-id="00b78-105">Чтобы проверить, остановлена ли виртуальная машина, можно попытаться проверить связь с общедоступным IP-адресом с помощью `ssh` или команды `vm get-instance-view`.</span><span class="sxs-lookup"><span data-stu-id="00b78-105">We can verify it has stopped by attempting to ping the public IP address, using `ssh`, or through the `vm get-instance-view` command.</span></span> <span data-ttu-id="00b78-106">Эта команда возвращает те же основные данные, что и `vm show`, но также предоставляет сведения о самом экземпляре.</span><span class="sxs-lookup"><span data-stu-id="00b78-106">This final approach returns the same basic data as `vm show` but includes details about the instance itself.</span></span> <span data-ttu-id="00b78-107">Чтобы узнать текущее состояние выполнения виртуальной машины, попробуйте ввести следующую команду в Azure Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="00b78-107">Try typing the following command into Azure Cloud Shell to see the current running state of your VM:</span></span>

```azurecli
az vm get-instance-view -n SampleVM -g ExerciseResources --query "instanceView.statuses[?starts_with(code, 'PowerState/')].displayStatus" -o tsv
```

<span data-ttu-id="00b78-108">Она должна вернуть результат `VM stopped`.</span><span class="sxs-lookup"><span data-stu-id="00b78-108">This command should return `VM stopped` as the result.</span></span>

## <a name="starting-a-vm"></a><span data-ttu-id="00b78-109">Запуск виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="00b78-109">Starting a VM</span></span>

<span data-ttu-id="00b78-110">Обратное можно сделать с помощью команды `vm start`.</span><span class="sxs-lookup"><span data-stu-id="00b78-110">We can do the reverse through the `vm start` command.</span></span>

```azurecli
az vm start -n SampleVM -g ExerciseResources
```

<span data-ttu-id="00b78-111">Она запускает остановленную виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="00b78-111">This command will start a stopped VM.</span></span> <span data-ttu-id="00b78-112">Проверить состояние можно с помощью запроса `vm get-instance-view`, который теперь должен вернуть `VM running`.</span><span class="sxs-lookup"><span data-stu-id="00b78-112">We can verify it through the `vm get-instance-view` query, which should now return `VM running`.</span></span>

## <a name="restarting-a-vm"></a><span data-ttu-id="00b78-113">Перезапуск виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="00b78-113">Restarting a VM</span></span>

<span data-ttu-id="00b78-114">Наконец, мы можем перезапустить виртуальную машину, если были внесены изменения, требующие перезагрузки. Для этого используем команду `vm restart`.</span><span class="sxs-lookup"><span data-stu-id="00b78-114">Finally, we can restart a VM if we have made changes that require a reboot using the `vm restart` command.</span></span> <span data-ttu-id="00b78-115">Если вы не хотите ждать, пока виртуальная машина перезагрузится, и хотите немедленно вернуть управление Azure CLI, можно добавить флаг `--no-wait`.</span><span class="sxs-lookup"><span data-stu-id="00b78-115">You can add the `--no-wait` flag if you want the Azure CLI to return immediately without waiting for the VM to reboot.</span></span>

