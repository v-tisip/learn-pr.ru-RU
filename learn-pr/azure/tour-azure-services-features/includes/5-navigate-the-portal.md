<span data-ttu-id="8d2ea-101">Продукты Azure имеют сложную иерархию.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-101">Azure products have a deep hierarchy.</span></span> <span data-ttu-id="8d2ea-102">Предположим, вам нужно создать виртуальную машину Linux.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-102">For example, suppose you needed to create a Linux Virtual Machine.</span></span> <span data-ttu-id="8d2ea-103">Вы можете пройти по следующим уровням: **Главная** **>** **Виртуальные машины** **>** **Вычисление** **>** **Сервер Ubuntu**.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-103">You might navigate through these levels: **Home** **>** **Virtual machines** **>** **Compute** **>** **Ubuntu Server**.</span></span> <span data-ttu-id="8d2ea-104">Портал Azure оптимизирует свой пользовательский интерфейс, чтобы такая последовательность навигации была интуитивно понятной.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-104">The Azure portal optimizes its UI to make this type of navigation sequence intuitive.</span></span> <span data-ttu-id="8d2ea-105">Здесь мы рассмотрим ключевые элементы пользовательского интерфейса, благодаря которым это возможно.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-105">Here, you will survey the key UI elements that make this possible.</span></span> <span data-ttu-id="8d2ea-106">Вы будете перемещаться по меню и подменю и использовать колонки для поиска и настройки служб.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-106">You will navigate through menus and sub-menus and use blades to find and configure services.</span></span>

## <a name="azure-portal-layout"></a><span data-ttu-id="8d2ea-107">Схема портала Azure</span><span class="sxs-lookup"><span data-stu-id="8d2ea-107">Azure Portal Layout</span></span>

<span data-ttu-id="8d2ea-108">Портал Azure — это основной графический пользовательский интерфейс для управления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-108">The Azure portal is the main graphical user interface (GUI) for controlling Microsoft Azure.</span></span> <span data-ttu-id="8d2ea-109">Вы можете выполнять на портале большую часть действий по управлению, и обычно это лучший интерфейс для выполнения одиночных задач или детального изучения параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-109">You can carry out the large majority of management actions on the portal and the portal is typically the best interface for carrying out single tasks or where you want to look at the configuration options in detail.</span></span>

<span data-ttu-id="8d2ea-110">На левой панели портала находится область ресурсов, в которой перечислены основные типы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-110">On the left-hand pane of the portal is the resource pane, which lists the main resource types.</span></span> <span data-ttu-id="8d2ea-111">Обратите внимание, что на Azure значительно больше типов ресурсов, чем показано.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-111">Note that Azure has far many more resource types than just those shown.</span></span>

## <a name="using-blades-in-azure-portal"></a><span data-ttu-id="8d2ea-112">Использование колонок на портале Azure</span><span class="sxs-lookup"><span data-stu-id="8d2ea-112">Using Blades in Azure Portal</span></span>

<span data-ttu-id="8d2ea-113">На портале Azure для навигации используются колонки.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-113">The Azure Portal uses a blades model for navigation.</span></span> <span data-ttu-id="8d2ea-114">_Колонка_ — это выдвижная панель, содержащая элементы пользовательского интерфейса для одного уровня в последовательности переходов.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-114">A _blade_ is a slide-out panel containing the UI for a single level in a navigation sequence.</span></span> <span data-ttu-id="8d2ea-115">Например, каждый из элементов в этой последовательности будет представлен колонкой: **Виртуальные машины** **>** **Вычисление** **>** **Сервер Ubuntu**.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-115">For example, each of these elements in this sequence would be represented by a blade: **Virtual machines** **>** **Compute** **>** **Ubuntu Server**.</span></span>

<span data-ttu-id="8d2ea-116">В каждой колонке в пользовательском интерфейсе обычно есть ряд настраиваемых параметров.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-116">Each blade within the UI typically contains a number of configurable options.</span></span> <span data-ttu-id="8d2ea-117">Некоторые из этих параметров открывают следующую колонку, которая появляется справа от уже открытой.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-117">Some of these options generate another blade, which reveals itself to the right of any existing blade.</span></span> <span data-ttu-id="8d2ea-118">В новой колонке дополнительные настраиваемые параметры могут открывать еще одну колонку и так далее.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-118">On the new blade, any further configurable options will spawn another blade, and so on.</span></span> <span data-ttu-id="8d2ea-119">В итоге у вас будет одновременно открыто несколько колонок.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-119">Pretty soon, you can end up with several blades open at the same time.</span></span> <span data-ttu-id="8d2ea-120">Колонки также можно увеличить, чтобы они заполнили весь экран.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-120">You can maximize blades as well so that they fill the entire screen.</span></span>

<span data-ttu-id="8d2ea-121">Если вы попытаетесь закрыть колонку без сохранения изменений конфигурации, появится запрос.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-121">If you try to close a blade without saving any configuration changes that you have made, then you will receive a prompt.</span></span>

## <a name="configuring-settings-in-azure-portal"></a><span data-ttu-id="8d2ea-122">Настройка параметров на портале Azure</span><span class="sxs-lookup"><span data-stu-id="8d2ea-122">Configuring Settings in Azure Portal</span></span>

<span data-ttu-id="8d2ea-123">На портале Azure отображается несколько вариантов конфигурации, главным образом в строке состояния в правой верхней части экрана.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-123">The Azure portal displays several configuration options, mostly in the status bar to the top-right of the screen.</span></span>

### <a name="notifications"></a><span data-ttu-id="8d2ea-124">Уведомления</span><span class="sxs-lookup"><span data-stu-id="8d2ea-124">Notifications</span></span>

<span data-ttu-id="8d2ea-125">Нажмите на значок колокольчика, чтобы открыть панель "Уведомления".</span><span class="sxs-lookup"><span data-stu-id="8d2ea-125">Clicking the bell icon displays the Notifications pane.</span></span> <span data-ttu-id="8d2ea-126">На этой панели указаны последние выполненные действия и их состояние.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-126">This pane lists the last actions that have been carried out, along with their status.</span></span>

![Колонка "Уведомления"](../images/2-notifications-blade.PNG)

### <a name="cloud-shell"></a><span data-ttu-id="8d2ea-128">Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="8d2ea-128">Cloud Shell</span></span>

<span data-ttu-id="8d2ea-129">Если вы щелкните значок Cloud Shell (>_), то создадите сеанс Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-129">If you click the Cloud Shell icon (>_), you will create a new cloud shell session.</span></span> <span data-ttu-id="8d2ea-130">Вам будет предложено использовать Linux Bash или PowerShell в Linux в этом сеансе.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-130">You are prompted to use either Linux Bash or PowerShell on Linux in that session.</span></span>

![Cloud Shell](../images/2-choose-shell.PNG)

### <a name="settings"></a><span data-ttu-id="8d2ea-132">Параметры</span><span class="sxs-lookup"><span data-stu-id="8d2ea-132">Settings</span></span>

<span data-ttu-id="8d2ea-133">Нажмите на значок шестеренки, чтобы изменить параметры портала Azure.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-133">Clicking on the "gear" icon to change Azure Portal settings.</span></span> <span data-ttu-id="8d2ea-134">К числу этих параметров относятся следующие:</span><span class="sxs-lookup"><span data-stu-id="8d2ea-134">These settings include:</span></span>

* <span data-ttu-id="8d2ea-135">Время выхода</span><span class="sxs-lookup"><span data-stu-id="8d2ea-135">Logout time</span></span>
* <span data-ttu-id="8d2ea-136">Цветовая схема</span><span class="sxs-lookup"><span data-stu-id="8d2ea-136">Color scheme</span></span>
* <span data-ttu-id="8d2ea-137">Высококонтрастные темы</span><span class="sxs-lookup"><span data-stu-id="8d2ea-137">High contrast themes</span></span>
* <span data-ttu-id="8d2ea-138">Всплывающие уведомления (для мобильных устройств)</span><span class="sxs-lookup"><span data-stu-id="8d2ea-138">Toast notifications (to a mobile device)</span></span>
* <span data-ttu-id="8d2ea-139">Двойной щелчок для изменения темы</span><span class="sxs-lookup"><span data-stu-id="8d2ea-139">Double-click to change theme</span></span>
* <span data-ttu-id="8d2ea-140">Язык</span><span class="sxs-lookup"><span data-stu-id="8d2ea-140">Language</span></span>
* <span data-ttu-id="8d2ea-141">Региональный формат</span><span class="sxs-lookup"><span data-stu-id="8d2ea-141">Regional format</span></span>

![Параметры портала](../images/2-settings-blade.PNG)

<span data-ttu-id="8d2ea-143">Если вы изменили параметры, нажмите **Применить** для сохранения изменений.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-143">When you have changed settings, click **Apply** to accept your changes.</span></span>

### <a name="feedback-blade"></a><span data-ttu-id="8d2ea-144">Колонка "Обратная связь"</span><span class="sxs-lookup"><span data-stu-id="8d2ea-144">Feedback Blade</span></span>

<span data-ttu-id="8d2ea-145">Щелкните значок с улыбающимся лицом, чтобы открыть колонку **Отправьте нам отзыв**.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-145">The smiley face icon opens the **Send us feedback** blade.</span></span> <span data-ttu-id="8d2ea-146">Здесь можно отправить отзыв в корпорацию Майкрософт о службе Azure.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-146">Here you can send feedback to Microsoft about Azure.</span></span> <span data-ttu-id="8d2ea-147">Обратите внимание, что вы можете указать, может ли Майкрософт ответить на ваш отзыв по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-147">Note that you can specify whether Microsoft can respond to your feedback by email.</span></span>

![Отзыв](../images/2-feedback-blade.PNG)

### <a name="help-blade"></a><span data-ttu-id="8d2ea-149">Колонка "Справка"</span><span class="sxs-lookup"><span data-stu-id="8d2ea-149">Help Blade</span></span>

<span data-ttu-id="8d2ea-150">Щелкните вопросительный знак, чтобы открыть колонку **Справка**.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-150">Click the question mark to show the **Help** blade.</span></span> <span data-ttu-id="8d2ea-151">Здесь вы можете выбрать из нескольких разделов, в том числе:</span><span class="sxs-lookup"><span data-stu-id="8d2ea-151">Here you choose from a number of topics, including:</span></span>

* <span data-ttu-id="8d2ea-152">Новые возможности</span><span class="sxs-lookup"><span data-stu-id="8d2ea-152">What's new</span></span>
* <span data-ttu-id="8d2ea-153">Стратегия развития Azure</span><span class="sxs-lookup"><span data-stu-id="8d2ea-153">Azure roadmap</span></span>
* <span data-ttu-id="8d2ea-154">Руководство по запуску</span><span class="sxs-lookup"><span data-stu-id="8d2ea-154">Launch guided tour</span></span>
* <span data-ttu-id="8d2ea-155">Сочетания клавиш</span><span class="sxs-lookup"><span data-stu-id="8d2ea-155">Keyboard shortcuts</span></span>
* <span data-ttu-id="8d2ea-156">Показать диагностику</span><span class="sxs-lookup"><span data-stu-id="8d2ea-156">Show diagnostics</span></span>
* <span data-ttu-id="8d2ea-157">Конфиденциальность и условия</span><span class="sxs-lookup"><span data-stu-id="8d2ea-157">Privacy + terms</span></span>

### <a name="directory-and-subscription"></a><span data-ttu-id="8d2ea-158">Каталог и подписка</span><span class="sxs-lookup"><span data-stu-id="8d2ea-158">Directory and Subscription</span></span>

<span data-ttu-id="8d2ea-159">Щелкните значок книги и фильтра, чтобы открыть колонку **Каталог и подписка**.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-159">Click the Book and Filter icon to show the **Directory + subscription** blade.</span></span>

<span data-ttu-id="8d2ea-160">В Azure можно иметь несколько подписок, связанных с одним каталогом.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-160">Azure allows you to have more than one subscription associated with one directory.</span></span> <span data-ttu-id="8d2ea-161">Переключаться между подписками можно в колонке "Каталог и подписка".</span><span class="sxs-lookup"><span data-stu-id="8d2ea-161">In the Directory and Subscription blade, you can change between subscriptions.</span></span> <span data-ttu-id="8d2ea-162">Здесь можно изменить подписку или выбрать другой каталог.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-162">Here, you can change your subscription, or change to another directory.</span></span>

![Каталог](../images/2-directory-blade-1.PNG)

### <a name="profile-settings"></a><span data-ttu-id="8d2ea-164">Параметры профиля</span><span class="sxs-lookup"><span data-stu-id="8d2ea-164">Profile Settings</span></span>

<span data-ttu-id="8d2ea-165">Нажмите на свое имя в правом верхнем углу, чтобы изменить настройки профиля.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-165">If you click on your name in the top right-hand corner, you can then change your profile settings.</span></span>
<span data-ttu-id="8d2ea-166">Доступные параметры:</span><span class="sxs-lookup"><span data-stu-id="8d2ea-166">Options include:</span></span>

* <span data-ttu-id="8d2ea-167">Выход из Azure</span><span class="sxs-lookup"><span data-stu-id="8d2ea-167">Sign out of Azure</span></span>
* <span data-ttu-id="8d2ea-168">Изменить пароль</span><span class="sxs-lookup"><span data-stu-id="8d2ea-168">Change password</span></span>
* <span data-ttu-id="8d2ea-169">Изменение контактных данных</span><span class="sxs-lookup"><span data-stu-id="8d2ea-169">Change contact information</span></span>
* <span data-ttu-id="8d2ea-170">Просмотр разрешений</span><span class="sxs-lookup"><span data-stu-id="8d2ea-170">View permissions</span></span>
* <span data-ttu-id="8d2ea-171">Отправка идеи группе разработчиков Azure</span><span class="sxs-lookup"><span data-stu-id="8d2ea-171">Submit an idea to the Azure team</span></span>
* <span data-ttu-id="8d2ea-172">Просмотр счетов</span><span class="sxs-lookup"><span data-stu-id="8d2ea-172">View your bill</span></span>
* <span data-ttu-id="8d2ea-173">Переход в другой каталог (отображается колонка "Каталог и подписка", как в предыдущем разделе)</span><span class="sxs-lookup"><span data-stu-id="8d2ea-173">Switch directory (shows the Directory + Subscription blade as in the previous section)</span></span>

![Параметры профиля](../images/2-portal-menu.png)

<span data-ttu-id="8d2ea-175">Если вы нажмете **Просмотреть мой счет**, откроется страница **Управление затратами и выставление счетов — Счета-фактуры**, где можно проанализировать затраты на Azure.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-175">If you now click **View my bill**, Azure takes you to the **Cost Management + Billing - Invoices** page, which helps you analyze where Azure is generating costs.</span></span>

![Страница выставления счетов](../images/2-portal-billing.PNG)

## <a name="summary"></a><span data-ttu-id="8d2ea-177">Сводка</span><span class="sxs-lookup"><span data-stu-id="8d2ea-177">Summary</span></span>

<span data-ttu-id="8d2ea-178">Azure — это большой продукт, и это отражено в пользовательском интерфейсе портала.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-178">Azure is a large product and the portal UI reflects this.</span></span> <span data-ttu-id="8d2ea-179">Чтобы разобраться в сложной структуре портала, используйте иерархию колонок.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-179">The primary way that the portal helps you navigate this complexity is with blades to indicate hierarchy.</span></span> <span data-ttu-id="8d2ea-180">Колонки позволяют вам сосредоточиться на определенной задаче и при этом четко обозначают путь до конкретной точки.</span><span class="sxs-lookup"><span data-stu-id="8d2ea-180">Blades let you focus on a specific task while clearly indicating the path you took to reach that point.</span></span>