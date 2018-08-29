<span data-ttu-id="f6e0a-101">В этом упражнении вы будете использовать клиент RDP для подключения к виртуальной машине Windows, созданной в предыдущем блоке.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-101">In this exercise, you'll use the RDP client to connect to the Windows VM that you created in the previous unit.</span></span> <span data-ttu-id="f6e0a-102">Вы можете подключиться, скачав и запустив RDP-файл на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-102">You can connect by downloading and running an RDP file from the Azure portal.</span></span> <span data-ttu-id="f6e0a-103">В этом RDP-файле будут указаны:</span><span class="sxs-lookup"><span data-stu-id="f6e0a-103">This RDP file will have:</span></span>

* <span data-ttu-id="f6e0a-104">общедоступный IP-адрес виртуальной машины;</span><span class="sxs-lookup"><span data-stu-id="f6e0a-104">The public IP address of the VM.</span></span>
* <span data-ttu-id="f6e0a-105">номер порта.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-105">The port number.</span></span>

## <a name="motivation"></a><span data-ttu-id="f6e0a-106">Мотивация</span><span class="sxs-lookup"><span data-stu-id="f6e0a-106">Motivation</span></span>

<span data-ttu-id="f6e0a-107">В этом упражнении вы являетесь учащимся и хотите узнать о добавлении ролей и компонентов на компьютер Windows Server.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-107">From our exercise scenario, you're now a student and you want to learn about adding roles and features to a Windows Server computer.</span></span> <span data-ttu-id="f6e0a-108">Однако администратор сети не разрешает выполнять эту задачу на физическом компьютере в сети, а компьютеры учебного заведения практически не поддерживают работу Windows Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-108">However, your network administrator doesn't want you to do this on a physical computer on the network, and the school's computers are too poorly specified to run Windows Hyper-V.</span></span> <span data-ttu-id="f6e0a-109">Azure предоставляет идеальное решение.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-109">Azure provides the perfect solution.</span></span>

## <a name="configure-network-and-public-ip-address-settings"></a><span data-ttu-id="f6e0a-110">Настройка параметров сети и общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="f6e0a-110">Configure network and public IP address settings</span></span>

1. <span data-ttu-id="f6e0a-111">На портале Azure должна быть открыта колонка для созданной ранее виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-111">In the Azure portal, ensure the blade for the virtual machine that you created earlier is open.</span></span> <span data-ttu-id="f6e0a-112">Если нужно открыть колонку, найдите ее на вкладке **Все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-112">You can find the blade under **All Resources** if you need to open it.</span></span>

1. <span data-ttu-id="f6e0a-113">Перейдите в раздел **Сеть**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-113">Go to the **Networking** section.</span></span> <span data-ttu-id="f6e0a-114">В верхней части этого раздела находятся ссылки на виртуальную подсеть и динамический IP-адрес, которые были созданы вместе с виртуальной машиной, так как использовались значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-114">The top of this section has links to the virtual subnet and dynamic IP address that were created along with our VM since we used the defaults.</span></span> <span data-ttu-id="f6e0a-115">Этими ссылками можно воспользоваться в случае, если требуется изменить ресурсы (например, изменить динамический адрес на статический).</span><span class="sxs-lookup"><span data-stu-id="f6e0a-115">We would follow these links if we wanted to change those resources (for example, changing to a static IP address).</span></span>

1. <span data-ttu-id="f6e0a-116">Щелкните **Добавить правило входящего порта**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-116">Click **Add inbound port rule**.</span></span>

1. <span data-ttu-id="f6e0a-117">В верхней части диалогового окна **Добавление правила безопасности для входящего трафика** щелкните **основное**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-117">At the top of the **Add inbound security rule** dialog box, click **basic**.</span></span>

1. <span data-ttu-id="f6e0a-118">В разделе **Службы** выберите **RDP**, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-118">Under **Service**, select **RDP**, and then click **Add**.</span></span>

## <a name="connect-to-the-vm-by-using-rdp"></a><span data-ttu-id="f6e0a-119">Подключение к виртуальной машине с помощью протокола RDP</span><span class="sxs-lookup"><span data-stu-id="f6e0a-119">Connect to the VM by using RDP</span></span>

<span data-ttu-id="f6e0a-120">Чтобы скачать RDP-файл и подключиться к виртуальной машине, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-120">To download the RDP file and connect to the VM, carry out the following steps.</span></span>

### <a name="download-the-rdp-file"></a><span data-ttu-id="f6e0a-121">Скачивание RDP-файла</span><span class="sxs-lookup"><span data-stu-id="f6e0a-121">Download the RDP file</span></span>

1. <span data-ttu-id="f6e0a-122">В разделе **Обзор** колонки виртуальной машины щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-122">In the **Overview** section of the virtual machine's blade, click **Connect**.</span></span>

1. <span data-ttu-id="f6e0a-123">В колонке **Подключение к виртуальной машине** запомните значения параметров **IP-адрес** и **Номер порта**, а затем щелкните **Скачать RDP-файл**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-123">In the **Connect to virtual machine** blade, note the **IP address** and **Port number** settings, then click **Download RDP File**.</span></span>

1. <span data-ttu-id="f6e0a-124">В браузере щелкните **Открыть** или **Запустить**, чтобы открыть RDP-файл.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-124">In your browser, click **Open** or **Run** to open the RDP file.</span></span>

### <a name="connect-to-the-windows-vm"></a><span data-ttu-id="f6e0a-125">Подключение к виртуальной машине Windows</span><span class="sxs-lookup"><span data-stu-id="f6e0a-125">Connect to the Windows VM</span></span>

1. <span data-ttu-id="f6e0a-126">В диалоговом окне **Подключение к удаленному рабочему столу** обратите внимание на предупреждение системы безопасности и IP-адрес удаленного компьютера, а затем нажмите кнопку **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-126">In the **Remote Desktop Connection** dialog box, note the security warning and the remote computer IP address, then click **Connect**.</span></span>

1. <span data-ttu-id="f6e0a-127">В диалоговом окне **Безопасность Windows** введите имя пользователя и пароль, которые использовались на шагах 6 и 7.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-127">In the **Windows Security** dialog box, enter your user name and password that you used in steps 6 and 7.</span></span>

1. <span data-ttu-id="f6e0a-128">Во втором диалоговом окне **Подключение к удаленному рабочему столу** обратите внимание на ошибки сертификата, а затем нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-128">In the second **Remote Desktop Connection** dialog box, note the certificate errors, then click **Yes**.</span></span>

   > [!Note]
   > <span data-ttu-id="f6e0a-129">Отображение рабочего стола виртуальной машины может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-129">The virtual machine desktop takes a while to appear.</span></span> <span data-ttu-id="f6e0a-130">Это связано с тем, что образ B1 является недоопределенным.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-130">This effect is because the B1 image is under-specified.</span></span> <span data-ttu-id="f6e0a-131">Может появиться сообщение о нехватке памяти.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-131">You may receive a message about low memory allocation.</span></span>

1. <span data-ttu-id="f6e0a-132">В диалоговом окне **Сети** нажмите кнопку **Нет**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-132">In the **Networks** dialog, click **No**.</span></span>

### <a name="resize-the-vm-in-the-azure-portal"></a><span data-ttu-id="f6e0a-133">Изменение размера виртуальной машины на портале Azure</span><span class="sxs-lookup"><span data-stu-id="f6e0a-133">Resize the VM in the Azure portal</span></span>

1. <span data-ttu-id="f6e0a-134">Вернитесь на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-134">Switch back to the Azure portal.</span></span> <span data-ttu-id="f6e0a-135">На странице свойств виртуальной машины в разделе **Свойства** щелкните **Размер**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-135">On the virtual machine properties page, under **Settings**, click **Size**.</span></span>

1. <span data-ttu-id="f6e0a-136">Щелкните **D2s_v3** (2 виртуальных ЦП, 8 ГБ ОЗУ), а затем нажмите **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-136">Click **D2s_v3** (2 vCPUs, 8-GB RAM), and then click **Select**.</span></span> <span data-ttu-id="f6e0a-137">Появится сообщение об изменении размера виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-137">A resizing virtual machine message will display.</span></span> <span data-ttu-id="f6e0a-138">В окне RDP будет завершена работа виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-138">The VM in the RDP window will also close down.</span></span>

1. <span data-ttu-id="f6e0a-139">Вернитесь на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-139">Switch back to the Azure portal.</span></span> <span data-ttu-id="f6e0a-140">На левой панели щелкните элемент **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-140">In the left pane, click **Virtual machines**.</span></span>

1. <span data-ttu-id="f6e0a-141">Подождите, пока в разделе **Виртуальные машины** состояние виртуальной машины изменится на **Запущена**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-141">Under **Virtual machines**, wait until your VM shows a status of **Running**.</span></span> <span data-ttu-id="f6e0a-142">Может потребоваться нажать кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-142">You may need to click **Refresh**.</span></span>

1. <span data-ttu-id="f6e0a-143">Щелкните имя виртуальной машины, а затем в разделе **Параметры** щелкните **Размер**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-143">Click the virtual machine's name, then in **Settings**, click **Size**.</span></span> <span data-ttu-id="f6e0a-144">Обратите внимание, что теперь виртуальная машина имеет размер **D2s_v3**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-144">Note the VM size is now set to **D2s_v3**.</span></span>

### <a name="reconnect-to-the-resized-vm"></a><span data-ttu-id="f6e0a-145">Повторное подключение к виртуальной машине с измененным размером</span><span class="sxs-lookup"><span data-stu-id="f6e0a-145">Reconnect to the resized VM</span></span>

1. <span data-ttu-id="f6e0a-146">Щелкните элемент **Виртуальные машины** и выберите свою виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-146">Click **Virtual machines**, then click your VM.</span></span> <span data-ttu-id="f6e0a-147">Обратите внимание, что значение параметра **Общедоступный IP-адрес** могло измениться.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-147">Note the **Public IP Address** value has probably changed.</span></span> <span data-ttu-id="f6e0a-148">Нажмите кнопку **Подключить**, а затем в браузере нажмите кнопку **Запустить** или **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-148">Click **Connect**, and then click **Run** or **Open** in your browser.</span></span>

1. <span data-ttu-id="f6e0a-149">В диалоговом окне **Подключение к удаленному рабочему столу** обратите внимание на предупреждение системы безопасности и IP-адрес удаленного компьютера, а затем нажмите кнопку **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-149">In the **Remote Desktop Connection** dialog box, note the security warning and the remote computer IP address, then click **Connect**.</span></span>

1. <span data-ttu-id="f6e0a-150">В диалоговом окне **Безопасность Windows** введите имя пользователя и пароль, которые использовались на шагах 6 и 7.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-150">In the **Windows Security** dialog box, enter your user name and password that you used in steps 6 and 7.</span></span>

1. <span data-ttu-id="f6e0a-151">Во втором диалоговом окне **Подключение к удаленному рабочему столу** обратите внимание на ошибки сертификата, а затем нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-151">In the second **Remote Desktop Connection** dialog box, note the certificate errors, then click **Yes**.</span></span> <span data-ttu-id="f6e0a-152">Обратите внимание, насколько оперативнее виртуальная машина реагирует на процесс входа.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-152">Notice how much more responsive the virtual machine is to the sign-in process.</span></span>

1. <span data-ttu-id="f6e0a-153">Правой кнопкой мыши щелкните панель задач и выберите пункт **Диспетчер задач**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-153">Right-click the taskbar and click **Task Manager**.</span></span>

1. <span data-ttu-id="f6e0a-154">В окне **Диспетчер задач** щелкните **Подробности**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-154">In the **Task Manager** window, click **More details**.</span></span>

1. <span data-ttu-id="f6e0a-155">Откройте вкладку **Производительность**. Обратите внимание, что общий объем доступной памяти составляет 8 ГБ, из которой используется примерно 1,2 ГБ.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-155">Click the **Performance** tab. Note the total available memory is 8 GB of which about 1.2 GB will be in use.</span></span> <span data-ttu-id="f6e0a-156">Закройте **диспетчер задач**.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-156">Close **Task Manager**.</span></span>

## <a name="summary"></a><span data-ttu-id="f6e0a-157">Сводка</span><span class="sxs-lookup"><span data-stu-id="f6e0a-157">Summary</span></span>

<span data-ttu-id="f6e0a-158">Вы подключились к виртуальной машине Windows по протоколу RDP.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-158">You have connected to a Windows VM by using RDP.</span></span> <span data-ttu-id="f6e0a-159">Получив доступ к пользовательскому интерфейсу рабочего стола, вы можете управлять этой виртуальной машиной так же, как любым компьютером Windows.</span><span class="sxs-lookup"><span data-stu-id="f6e0a-159">With Desktop UI access, you can administer this VM as you would any Windows computer.</span></span>
