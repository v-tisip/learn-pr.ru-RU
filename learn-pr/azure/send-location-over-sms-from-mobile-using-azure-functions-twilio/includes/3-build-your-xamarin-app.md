<span data-ttu-id="2086c-101">На этом этапе мобильное приложение представляет собой простое приложение "Hello World!".</span><span class="sxs-lookup"><span data-stu-id="2086c-101">At this point, the mobile app is a simple "Hello World" app.</span></span> <span data-ttu-id="2086c-102">В этом блоке вы добавите пользовательский интерфейс и базовую логику приложения.</span><span class="sxs-lookup"><span data-stu-id="2086c-102">In this unit, you add the UI and some basic application logic.</span></span>

<span data-ttu-id="2086c-103">Пользовательский интерфейс приложения будет состоять из следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="2086c-103">The UI for the app will consist of:</span></span>

* <span data-ttu-id="2086c-104">элемент управления, в который вводится текст, для ввода некоторых телефонных номеров;</span><span class="sxs-lookup"><span data-stu-id="2086c-104">A text-entry control to enter some phone numbers.</span></span>
* <span data-ttu-id="2086c-105">кнопка для отправки данных о вашем местоположении на эти номера с помощью функции Azure;</span><span class="sxs-lookup"><span data-stu-id="2086c-105">A button to send your location to those numbers using an Azure function.</span></span>
* <span data-ttu-id="2086c-106">метка, которая будет отображать сообщение для пользователя с текущим состоянием, таким как "Данные о местоположении отправляются" и "Данные о местоположении успешно отправлены".</span><span class="sxs-lookup"><span data-stu-id="2086c-106">A label that will show a message to the user of the current status, such as the location being sent and location sent successfully.</span></span>

<span data-ttu-id="2086c-107">Xamarin.Forms поддерживает конструктивный шаблон, который называется Model-View-ViewModel (MVVM).</span><span class="sxs-lookup"><span data-stu-id="2086c-107">Xamarin.Forms supports a design pattern called Model-View-ViewModel (MVVM).</span></span> <span data-ttu-id="2086c-108">Дополнительные сведения о шаблоне MVVM см. в [документации по Xamarin MVVM](https://docs.microsoft.com/xamarin/xamarin-forms/enterprise-application-patterns/mvvm). Его суть в том, что у каждой страницы (View) есть класс ViewModel, который предоставляет свойства и поведение.</span><span class="sxs-lookup"><span data-stu-id="2086c-108">You can read more about MVVM in the [Xamarin MVVM docs](https://docs.microsoft.com/xamarin/xamarin-forms/enterprise-application-patterns/mvvm), but the essence of it is, each page (View) has a ViewModel that exposes properties and behavior.</span></span>

<span data-ttu-id="2086c-109">Свойства ViewModel привязываются к компонентам пользовательского интерфейса по имени, и эта привязка обеспечивает синхронизацию данных между View и ViewModel.</span><span class="sxs-lookup"><span data-stu-id="2086c-109">ViewModel properties are 'bound' to components on the UI by name, and this binding synchronizes data between the View and ViewModel.</span></span> <span data-ttu-id="2086c-110">Например, свойство `string` в классе ViewModel с именем `Name` может быть привязано к свойству `Text` элемента управления, в который вводится текст, в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="2086c-110">For example, a `string` property on a ViewModel called `Name` could be bound to the `Text` property of a text-entry control on the UI.</span></span> <span data-ttu-id="2086c-111">Элемент управления, в который вводится текст, отображает значение в свойстве `Name`, а когда пользователь изменяет текст в пользовательском интерфейсе, свойство `Name` обновляется.</span><span class="sxs-lookup"><span data-stu-id="2086c-111">The text-entry control shows the value in the `Name` property and, when the user changes the text in the UI, the `Name` property is updated.</span></span> <span data-ttu-id="2086c-112">При изменении значения свойства `Name` в классе ViewModel возникает событие, сообщающее о необходимости обновления пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="2086c-112">If the value of the `Name` property is changed in the ViewModel, an event is raised to tell the UI to update.</span></span>

<span data-ttu-id="2086c-113">Поведение ViewModel выражается в виде свойств команды, где команда является объектом, который заключает в оболочку действие, выполняемое при вызове команды.</span><span class="sxs-lookup"><span data-stu-id="2086c-113">ViewModel behavior is exposed as command properties, a command being an object that wraps an action that is executed when the command is invoked.</span></span> <span data-ttu-id="2086c-114">Эти команды привязываются по имени к элементам управления, например кнопкам, и вызываются при нажатии кнопки.</span><span class="sxs-lookup"><span data-stu-id="2086c-114">These commands are bound by name to controls like buttons, and tapping a button will invoke the command.</span></span>

## <a name="create-a-base-viewmodel"></a><span data-ttu-id="2086c-115">Создание базового класса ViewModel</span><span class="sxs-lookup"><span data-stu-id="2086c-115">Create a base ViewModel</span></span>

<span data-ttu-id="2086c-116">Все классы ViewModel реализуют интерфейс `INotifyPropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="2086c-116">ViewModels all implement the `INotifyPropertyChanged` interface.</span></span> <span data-ttu-id="2086c-117">Этот интерфейс содержит одно событие `PropertyChanged`, которое используется для уведомления пользовательского интерфейса об обновлениях.</span><span class="sxs-lookup"><span data-stu-id="2086c-117">This interface has a single event, `PropertyChanged`, which is used to notify the UI of any updates.</span></span> <span data-ttu-id="2086c-118">У этого события есть аргументы, которые содержат имя измененного свойства.</span><span class="sxs-lookup"><span data-stu-id="2086c-118">This event has event args that contain the name of the property that has changed.</span></span> <span data-ttu-id="2086c-119">Создание базового класса ViewModel, реализующего этот интерфейс и предоставляющего некоторые вспомогательные методы, является обычной практикой.</span><span class="sxs-lookup"><span data-stu-id="2086c-119">It's common practice to create a base ViewModel class implementing this interface and providing some helper methods.</span></span>

1. <span data-ttu-id="2086c-120">Создайте класс в проекте .NET Standard `ImHere` с именем `BaseViewModel`, щелкнув правой кнопкой мыши проект, а затем выбрав *Добавить -> Класс...* . Присвойте новому классу имя "BaseViewModel" и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2086c-120">Create a new class in the `ImHere` .NET standard project called `BaseViewModel` by right-clicking on the project, and then selecting *Add->Class...*. Name the new class "BaseViewModel" and click **Add**.</span></span>

2. <span data-ttu-id="2086c-121">Сделайте класс `public` и производным от `INotifyPropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="2086c-121">Make the class `public` and derive from `INotifyPropertyChanged`.</span></span> <span data-ttu-id="2086c-122">Вам потребуется добавить директиву using для `System.ComponentModel`.</span><span class="sxs-lookup"><span data-stu-id="2086c-122">You'll need to add a using directive for `System.ComponentModel`.</span></span>

3. <span data-ttu-id="2086c-123">Реализуйте интерфейс `INotifyPropertyChanged`, добавив событие `PropertyChanged`:</span><span class="sxs-lookup"><span data-stu-id="2086c-123">Implement the `INotifyPropertyChanged` interface by adding the `PropertyChanged` event:</span></span>

    ```cs
    public event PropertyChangedEventHandler PropertyChanged;
    ```

4. <span data-ttu-id="2086c-124">Распространенный подход к использованию свойств ViewModel заключается в том, чтобы у общедоступного свойства было закрытое резервное поле.</span><span class="sxs-lookup"><span data-stu-id="2086c-124">The common pattern for ViewModel properties is to have a public property with a private backing field.</span></span> <span data-ttu-id="2086c-125">В методе задания свойства резервное поле проверяется на соответствие новому значению.</span><span class="sxs-lookup"><span data-stu-id="2086c-125">In the property setter, the backing field is checked against the new value.</span></span> <span data-ttu-id="2086c-126">Если новое значение не совпадает, резервное поле обновляется и возникает событие `PropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="2086c-126">If the new value is different to the backing field, the backing field is updated and the `PropertyChanged` event is raised.</span></span> <span data-ttu-id="2086c-127">Эту логику легко включить в метод, поэтому добавьте `Set` метод.</span><span class="sxs-lookup"><span data-stu-id="2086c-127">This logic is easy to factor out into a method, so add the `Set` method.</span></span> <span data-ttu-id="2086c-128">Вам потребуется добавить директиву using для пространства имен `System.Runtime.CompilerServices`.</span><span class="sxs-lookup"><span data-stu-id="2086c-128">You'll need to add a using directive for the `System.Runtime.CompilerServices` namespace.</span></span>

    ```cs
    protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
    {
        if (Equals(field, value)) return;
        field = value;
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
    ```

    <span data-ttu-id="2086c-129">Этот метод принимает ссылку на резервное поле, новое значение и имя свойства.</span><span class="sxs-lookup"><span data-stu-id="2086c-129">This method takes a reference to the backing field, the new value, and the property name.</span></span> <span data-ttu-id="2086c-130">Если поле не изменилось, метод возвращает. В противном случае поле обновляется и возникает событие `PropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="2086c-130">If the field hasn't changed, the method returns, otherwise, the field is updated and the `PropertyChanged` event is raised.</span></span> <span data-ttu-id="2086c-131">Параметр `propertyName` метода `Set` является параметром по умолчанию и помечается атрибутом `CallerMemberName`.</span><span class="sxs-lookup"><span data-stu-id="2086c-131">The `propertyName` parameter on the `Set` method is a default parameter and is marked with the `CallerMemberName` attribute.</span></span> <span data-ttu-id="2086c-132">При вызове этого метода из метода задания свойства этот параметр обычно остается значением по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2086c-132">When this method is called from a property setter, this parameter is normally left as the default value.</span></span> <span data-ttu-id="2086c-133">Затем компилятор автоматически установит в качестве значения параметра имя вызывающего свойства.</span><span class="sxs-lookup"><span data-stu-id="2086c-133">The compiler will then automatically set the parameter value to be the name of the calling property.</span></span>

<span data-ttu-id="2086c-134">Ниже приведен полный код для этого класса.</span><span class="sxs-lookup"><span data-stu-id="2086c-134">The full code for this class is below.</span></span>

```cs
using System.ComponentModel;
using System.Runtime.CompilerServices;

namespace ImHere
{
    public class BaseViewModel : INotifyPropertyChanged
    {
        public event PropertyChangedEventHandler PropertyChanged;

        protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
        {
            if (Equals(field, value)) return;
            field = value;
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
        }
    }
}
```

## <a name="create-a-viewmodel-for-the-page"></a><span data-ttu-id="2086c-135">Создание ViewModel для страницы</span><span class="sxs-lookup"><span data-stu-id="2086c-135">Create a ViewModel for the page</span></span>

<span data-ttu-id="2086c-136">`MainPage` будет содержать элемент управления, в который вводится текст, для телефонных номеров и метку для отображения сообщения.</span><span class="sxs-lookup"><span data-stu-id="2086c-136">The `MainPage` will have a text-entry control for phone numbers and a label to display a message.</span></span> <span data-ttu-id="2086c-137">Эти элементы управления будут привязаны к свойствам в ViewModel.</span><span class="sxs-lookup"><span data-stu-id="2086c-137">These controls will be bound to properties on a ViewModel.</span></span>

1. <span data-ttu-id="2086c-138">Создайте класс с именем `MainViewModel` в проекте .NET Standard `ImHere`.</span><span class="sxs-lookup"><span data-stu-id="2086c-138">Create a class called `MainViewModel` in the `ImHere` .NET standard project.</span></span>

2. <span data-ttu-id="2086c-139">Сделайте этот класс общедоступным и производным от `BaseViewModel`.</span><span class="sxs-lookup"><span data-stu-id="2086c-139">Make this class public and derive from `BaseViewModel`.</span></span>

3. <span data-ttu-id="2086c-140">Добавьте два свойства `string` (`PhoneNumbers` и `Message`), каждое с резервным полем.</span><span class="sxs-lookup"><span data-stu-id="2086c-140">Add two `string` properties, `PhoneNumbers` and `Message`, each with a backing field.</span></span> <span data-ttu-id="2086c-141">В методе задания свойства используйте метод `Set` базового класса, чтобы обновить значение и вызвать событие `PropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="2086c-141">In the property setter, use the base class `Set` method to update the value and raise the `PropertyChanged` event.</span></span>

   ```cs
    string message = "";
    public string Message
    {
        get => message;
        set => Set(ref message, value);
    }

    string phoneNumbers = "";
    public string PhoneNumbers
    {
        get => phoneNumbers;
        set => Set(ref phoneNumbers, value);
    }
   ```

4. <span data-ttu-id="2086c-142">Добавьте свойство команды только для чтения с именем `SendLocationCommand`.</span><span class="sxs-lookup"><span data-stu-id="2086c-142">Add a read-only command property called `SendLocationCommand`.</span></span> <span data-ttu-id="2086c-143">У этой команды будет тип `ICommand` из пространства имен `System.Windows.Input`.</span><span class="sxs-lookup"><span data-stu-id="2086c-143">This command will have a type of `ICommand` from the `System.Windows.Input` namespace.</span></span>

    ```cs
    public ICommand SendLocationCommand { get; }
    ```

5. <span data-ttu-id="2086c-144">Добавьте конструктор в класс и в этом конструкторе инициализируйте `SendLocationCommand` как новый `Command` из пространства имен `Xamarin.Forms`.</span><span class="sxs-lookup"><span data-stu-id="2086c-144">Add a constructor to the class, and in this constructor, initialize the `SendLocationCommand` as a new `Command` from the `Xamarin.Forms` namespace.</span></span> <span data-ttu-id="2086c-145">Конструктор для этой команды принимает `Action` для запуска при вызове команды, поэтому создайте метод `async` и передайте лямбда-функцию `SendLocation`, которая `await` этот вызов в конструктор.</span><span class="sxs-lookup"><span data-stu-id="2086c-145">The constructor for this command takes an `Action` to run when the command is invoked, so create an `async` method called `SendLocation` and pass a lambda function that `await`s this call to the constructor.</span></span> <span data-ttu-id="2086c-146">Тело метода `SendLocation` будет реализовано в следующих блоках этого модуля.</span><span class="sxs-lookup"><span data-stu-id="2086c-146">The body of the `SendLocation` method will be implemented in later units in this module.</span></span> <span data-ttu-id="2086c-147">Чтобы возвращать `Task`, вам потребуется добавить директиву using для пространства имен `System.Threading.Tasks`.</span><span class="sxs-lookup"><span data-stu-id="2086c-147">You'll need to add a using directive for the `System.Threading.Tasks` namespace to be able to return a `Task`.</span></span>

    ```cs
    public MainViewModel()
    {
        SendLocationCommand = new Command(async () => await SendLocation());
    }

    async Task SendLocation()
    {
    }
    ```

<span data-ttu-id="2086c-148">Ниже приведен код для этого класса.</span><span class="sxs-lookup"><span data-stu-id="2086c-148">The code for this class is shown below.</span></span>

```cs
using System.Threading.Tasks;
using System.Windows.Input;
using Xamarin.Forms;

namespace ImHere
{
    public class MainViewModel : BaseViewModel
    {
        string message = "";
        public string Message
        {
            get => message;
            set => Set(ref message, value);
        }

        string phoneNumbers = "";
        public string PhoneNumbers
        {
            get => phoneNumbers;
            set => Set(ref phoneNumbers, value);
        }

        public MainViewModel()
        {
            SendLocationCommand = new Command(async () => await SendLocation());
        }

        public ICommand SendLocationCommand { get; }

        async Task SendLocation()
        {
        }
    }
}
```

## <a name="create-the-user-interface"></a><span data-ttu-id="2086c-149">Создание пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="2086c-149">Create the user interface</span></span>

<span data-ttu-id="2086c-150">Пользовательские интерфейсы Xamarin.Forms можно создавать с помощью XAML.</span><span class="sxs-lookup"><span data-stu-id="2086c-150">Xamarin.Forms UIs can be built using XAML.</span></span>

1. <span data-ttu-id="2086c-151">Откройте файл `MainPage.xaml` в проекте `ImHere`.</span><span class="sxs-lookup"><span data-stu-id="2086c-151">Open the `MainPage.xaml` file from the `ImHere` project.</span></span> <span data-ttu-id="2086c-152">Страница откроется в редакторе XAML.</span><span class="sxs-lookup"><span data-stu-id="2086c-152">The page will open in the XAML editor.</span></span>

    <span data-ttu-id="2086c-153">ПРИМЕЧАНИЕ. Проект `ImHere.UWP` также содержит файл с именем `MainPage.xaml`.</span><span class="sxs-lookup"><span data-stu-id="2086c-153">NOTE - The `ImHere.UWP` project also contains a file called `MainPage.xaml`.</span></span> <span data-ttu-id="2086c-154">Убедитесь, что вы редактируете файл в библиотеке .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="2086c-154">Make sure you're editing the one in the .NET standard library.</span></span>

2. <span data-ttu-id="2086c-155">Перед привязкой элементов управления к свойствам в классе ViewModel необходимо задать экземпляр ViewModel как контекст привязки страницы.</span><span class="sxs-lookup"><span data-stu-id="2086c-155">Before you can bind controls to properties on a ViewModel, you have to set an instance of the ViewModel as the binding context of the page.</span></span> <span data-ttu-id="2086c-156">Добавьте следующий XAML в `ContentPage` верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="2086c-156">Add the following XAML inside the top-level `ContentPage`.</span></span>

    ```xml
    <ContentPage.BindingContext>
        <local:MainViewModel/>
    </ContentPage.BindingContext>
    ```

3. <span data-ttu-id="2086c-157">Удалите содержимое `StackLayout` и добавьте в него отступы, чтобы улучшить внешний вид пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="2086c-157">Delete the contents of the `StackLayout` and add some padding inside it to help make the UI look better.</span></span>

    ```xml
    <StackLayout Padding="20">
    </StackLayout>
    ```

4. <span data-ttu-id="2086c-158">Добавьте элемент управления `Editor`, используемый для добавления телефонных номеров в `StackLayout`, над которым находится `Label` для описания назначения этого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="2086c-158">Add an `Editor` control that the user can use to add phone numbers to the `StackLayout`, with a `Label` above to describe what the entry control is for.</span></span> <span data-ttu-id="2086c-159">`StackLayout` располагает дочерние элементы управления по горизонтали или по вертикали в порядке их добавления, поэтому если сначала добавить `Label`, он будет размещен над `Editor`.</span><span class="sxs-lookup"><span data-stu-id="2086c-159">`StackLayout`'s stack child controls either horizontally or vertically in the order in which the controls are added, so adding the `Label` first will put it above the `Editor`.</span></span> <span data-ttu-id="2086c-160">Элементы управления `Editor` поддерживают многострочный ввод данных, позволяя вводить несколько телефонных номеров по одному в каждой строке.</span><span class="sxs-lookup"><span data-stu-id="2086c-160">`Editor` controls are multi-line entry controls, allowing the user to enter multiple phone numbers, one per line.</span></span>

    ```xml
    <StackLayout Padding="20">
        <Label Text="Phone numbers to send to:" HorizontalOptions="Center"/>
        <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
    </StackLayout>
    ```

    <span data-ttu-id="2086c-161">Свойство `Text` в `Editor` привязано к свойству `PhoneNumbers` в `MainViewModel`.</span><span class="sxs-lookup"><span data-stu-id="2086c-161">The `Text` property on the `Editor` is bound to the `PhoneNumbers` property on the `MainViewModel`.</span></span> <span data-ttu-id="2086c-162">Синтаксис для привязки предназначен для присвоения свойству значения `"{Binding <property name>}"`.</span><span class="sxs-lookup"><span data-stu-id="2086c-162">The syntax for binding is to set the property value to `"{Binding <property name>}"`.</span></span> <span data-ttu-id="2086c-163">Фигурные скобки указывают компилятору XAML, что это значение является специальным, и должны обрабатываться не так, как простое `string`.</span><span class="sxs-lookup"><span data-stu-id="2086c-163">The curly braces will tell the XAML compiler that this value is special and should be treated differently from a simple `string`.</span></span>

5. <span data-ttu-id="2086c-164">Под `Editor` добавьте `Button`, чтобы отправлять данные о местоположении пользователя.</span><span class="sxs-lookup"><span data-stu-id="2086c-164">Add a `Button` to send the user's location below the `Editor`.</span></span>

    ```xml
    <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
            Command="{Binding SendLocationCommand}" />
    ```

    <span data-ttu-id="2086c-165">Свойство `Command` привязано к команде `SendLocationCommand` в ViewModel.</span><span class="sxs-lookup"><span data-stu-id="2086c-165">The `Command` property is bound to the `SendLocationCommand` command on the ViewModel.</span></span> <span data-ttu-id="2086c-166">Команда выполняется при нажатии кнопки.</span><span class="sxs-lookup"><span data-stu-id="2086c-166">When the button is tapped, the command will be executed.</span></span>

6. <span data-ttu-id="2086c-167">Под `Button` добавьте `Label`, чтобы отображать сообщение о состоянии.</span><span class="sxs-lookup"><span data-stu-id="2086c-167">Add a `Label` to show the status message below the `Button`.</span></span>

    ```xml
    <Label Text="{Binding Message}"
           HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    ```

<span data-ttu-id="2086c-168">Ниже приведен полный код для этой страницы.</span><span class="sxs-lookup"><span data-stu-id="2086c-168">The full code for this page is below.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:ImHere"
             x:Class="ImHere.MainPage">
    <ContentPage.BindingContext>
        <local:MainViewModel/>
    </ContentPage.BindingContext>
    <StackLayout Padding="20">
        <Label Text="Phone numbers to send to:" HorizontalOptions="Center"/>
        <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
        <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
                Command="{Binding SendLocationCommand}" />
        <Label Text="{Binding Message}"
               HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    </StackLayout>
</ContentPage>
```

<span data-ttu-id="2086c-169">Запустите приложение, чтобы увидеть новый пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="2086c-169">Run the app to see the new UI.</span></span> <span data-ttu-id="2086c-170">Чтобы на этом этапе проверить привязки, добавьте точки останова в свойства или метод `SendLocation`.</span><span class="sxs-lookup"><span data-stu-id="2086c-170">If you want to validate the bindings at this point, you can do so by adding breakpoints to the properties or the `SendLocation` method.</span></span>

![Новый пользовательский интерфейс приложения](../media-drafts/3-new-ui.png)

## <a name="summary"></a><span data-ttu-id="2086c-172">Сводка</span><span class="sxs-lookup"><span data-stu-id="2086c-172">Summary</span></span>

<span data-ttu-id="2086c-173">В данном блоке вы узнали, как создать пользовательский интерфейс приложения с помощью XAML и классом ViewModel для обработки логики приложения.</span><span class="sxs-lookup"><span data-stu-id="2086c-173">In this unit, you learned how to create the UI for the app using XAML, along with a ViewModel to handle the applications logic.</span></span> <span data-ttu-id="2086c-174">Вы также узнали, как привязать ViewModel к пользовательскому интерфейсу.</span><span class="sxs-lookup"><span data-stu-id="2086c-174">You also learned how to bind the ViewModel to the UI.</span></span> <span data-ttu-id="2086c-175">В следующем блоке вы добавите поиск данных о местоположении в ViewModel.</span><span class="sxs-lookup"><span data-stu-id="2086c-175">In the next unit, you add location lookup to the ViewModel.</span></span>