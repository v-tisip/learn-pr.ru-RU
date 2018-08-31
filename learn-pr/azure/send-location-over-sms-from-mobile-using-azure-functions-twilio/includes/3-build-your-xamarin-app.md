На этом этапе мобильное приложение представляет собой простое приложение "Hello World!". В этом блоке вы добавите пользовательский интерфейс и базовую логику приложения.

Пользовательский интерфейс приложения будет состоять из следующих элементов:

* элемент управления, в который вводится текст, для ввода некоторых телефонных номеров;
* кнопка для отправки данных о вашем местоположении на эти номера с помощью функции Azure;
* метка, которая будет отображать сообщение для пользователя с текущим состоянием, таким как "Данные о местоположении отправляются" и "Данные о местоположении успешно отправлены".

Xamarin.Forms поддерживает конструктивный шаблон, который называется Model-View-ViewModel (MVVM). Дополнительные сведения о шаблоне MVVM см. в [документации по Xamarin MVVM](https://docs.microsoft.com/xamarin/xamarin-forms/enterprise-application-patterns/mvvm). Его суть в том, что у каждой страницы (View) есть класс ViewModel, который предоставляет свойства и поведение.

Свойства ViewModel привязываются к компонентам пользовательского интерфейса по имени, и эта привязка обеспечивает синхронизацию данных между View и ViewModel. Например, свойство `string` в классе ViewModel с именем `Name` может быть привязано к свойству `Text` элемента управления, в который вводится текст, в пользовательском интерфейсе. Элемент управления, в который вводится текст, отображает значение в свойстве `Name`, а когда пользователь изменяет текст в пользовательском интерфейсе, свойство `Name` обновляется. При изменении значения свойства `Name` в классе ViewModel возникает событие, сообщающее о необходимости обновления пользовательского интерфейса.

Поведение ViewModel выражается в виде свойств команды, где команда является объектом, который заключает в оболочку действие, выполняемое при вызове команды. Эти команды привязываются по имени к элементам управления, например кнопкам, и вызываются при нажатии кнопки.

## <a name="create-a-base-viewmodel"></a>Создание базового класса ViewModel

Все классы ViewModel реализуют интерфейс `INotifyPropertyChanged`. Этот интерфейс содержит одно событие `PropertyChanged`, которое используется для уведомления пользовательского интерфейса об обновлениях. У этого события есть аргументы, которые содержат имя измененного свойства. Создание базового класса ViewModel, реализующего этот интерфейс и предоставляющего некоторые вспомогательные методы, является обычной практикой.

1. Создайте класс в проекте .NET Standard `ImHere` с именем `BaseViewModel`, щелкнув правой кнопкой мыши проект, а затем выбрав *Добавить -> Класс...* . Присвойте новому классу имя "BaseViewModel" и нажмите кнопку **Добавить**.

2. Сделайте класс `public` и производным от `INotifyPropertyChanged`. Вам потребуется добавить директиву using для `System.ComponentModel`.

3. Реализуйте интерфейс `INotifyPropertyChanged`, добавив событие `PropertyChanged`:

    ```cs
    public event PropertyChangedEventHandler PropertyChanged;
    ```

4. Распространенный подход к использованию свойств ViewModel заключается в том, чтобы у общедоступного свойства было закрытое резервное поле. В методе задания свойства резервное поле проверяется на соответствие новому значению. Если новое значение не совпадает, резервное поле обновляется и возникает событие `PropertyChanged`. Эту логику легко включить в метод, поэтому добавьте `Set` метод. Вам потребуется добавить директиву using для пространства имен `System.Runtime.CompilerServices`.

    ```cs
    protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
    {
        if (Equals(field, value)) return;
        field = value;
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
    ```

    Этот метод принимает ссылку на резервное поле, новое значение и имя свойства. Если поле не изменилось, метод возвращает. В противном случае поле обновляется и возникает событие `PropertyChanged`. Параметр `propertyName` метода `Set` является параметром по умолчанию и помечается атрибутом `CallerMemberName`. При вызове этого метода из метода задания свойства этот параметр обычно остается значением по умолчанию. Затем компилятор автоматически установит в качестве значения параметра имя вызывающего свойства.

Ниже приведен полный код для этого класса.

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

## <a name="create-a-viewmodel-for-the-page"></a>Создание ViewModel для страницы

`MainPage` будет содержать элемент управления, в который вводится текст, для телефонных номеров и метку для отображения сообщения. Эти элементы управления будут привязаны к свойствам в ViewModel.

1. Создайте класс с именем `MainViewModel` в проекте .NET Standard `ImHere`.

2. Сделайте этот класс общедоступным и производным от `BaseViewModel`.

3. Добавьте два свойства `string` (`PhoneNumbers` и `Message`), каждое с резервным полем. В методе задания свойства используйте метод `Set` базового класса, чтобы обновить значение и вызвать событие `PropertyChanged`.

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

4. Добавьте свойство команды только для чтения с именем `SendLocationCommand`. У этой команды будет тип `ICommand` из пространства имен `System.Windows.Input`.

    ```cs
    public ICommand SendLocationCommand { get; }
    ```

5. Добавьте конструктор в класс и в этом конструкторе инициализируйте `SendLocationCommand` как новый `Command` из пространства имен `Xamarin.Forms`. Конструктор для этой команды принимает `Action` для запуска при вызове команды, поэтому создайте метод `async` и передайте лямбда-функцию `SendLocation`, которая `await` этот вызов в конструктор. Тело метода `SendLocation` будет реализовано в следующих блоках этого модуля. Чтобы возвращать `Task`, вам потребуется добавить директиву using для пространства имен `System.Threading.Tasks`.

    ```cs
    public MainViewModel()
    {
        SendLocationCommand = new Command(async () => await SendLocation());
    }

    async Task SendLocation()
    {
    }
    ```

Ниже приведен код для этого класса.

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

## <a name="create-the-user-interface"></a>Создание пользовательского интерфейса

Пользовательские интерфейсы Xamarin.Forms можно создавать с помощью XAML.

1. Откройте файл `MainPage.xaml` в проекте `ImHere`. Страница откроется в редакторе XAML.

    ПРИМЕЧАНИЕ. Проект `ImHere.UWP` также содержит файл с именем `MainPage.xaml`. Убедитесь, что вы редактируете файл в библиотеке .NET Standard.

2. Перед привязкой элементов управления к свойствам в классе ViewModel необходимо задать экземпляр ViewModel как контекст привязки страницы. Добавьте следующий XAML в `ContentPage` верхнего уровня.

    ```xml
    <ContentPage.BindingContext>
        <local:MainViewModel/>
    </ContentPage.BindingContext>
    ```

3. Удалите содержимое `StackLayout` и добавьте в него отступы, чтобы улучшить внешний вид пользовательского интерфейса.

    ```xml
    <StackLayout Padding="20">
    </StackLayout>
    ```

4. Добавьте элемент управления `Editor`, используемый для добавления телефонных номеров в `StackLayout`, над которым находится `Label` для описания назначения этого элемента управления. `StackLayout` располагает дочерние элементы управления по горизонтали или по вертикали в порядке их добавления, поэтому если сначала добавить `Label`, он будет размещен над `Editor`. Элементы управления `Editor` поддерживают многострочный ввод данных, позволяя вводить несколько телефонных номеров по одному в каждой строке.

    ```xml
    <StackLayout Padding="20">
        <Label Text="Phone numbers to send to:" HorizontalOptions="Center"/>
        <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
    </StackLayout>
    ```

    Свойство `Text` в `Editor` привязано к свойству `PhoneNumbers` в `MainViewModel`. Синтаксис для привязки предназначен для присвоения свойству значения `"{Binding <property name>}"`. Фигурные скобки указывают компилятору XAML, что это значение является специальным, и должны обрабатываться не так, как простое `string`.

5. Под `Editor` добавьте `Button`, чтобы отправлять данные о местоположении пользователя.

    ```xml
    <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
            Command="{Binding SendLocationCommand}" />
    ```

    Свойство `Command` привязано к команде `SendLocationCommand` в ViewModel. Команда выполняется при нажатии кнопки.

6. Под `Button` добавьте `Label`, чтобы отображать сообщение о состоянии.

    ```xml
    <Label Text="{Binding Message}"
           HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    ```

Ниже приведен полный код для этой страницы.

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

Запустите приложение, чтобы увидеть новый пользовательский интерфейс. Чтобы на этом этапе проверить привязки, добавьте точки останова в свойства или метод `SendLocation`.

![Новый пользовательский интерфейс приложения](../media-drafts/3-new-ui.png)

## <a name="summary"></a>Сводка

В данном блоке вы узнали, как создать пользовательский интерфейс приложения с помощью XAML и классом ViewModel для обработки логики приложения. Вы также узнали, как привязать ViewModel к пользовательскому интерфейсу. В следующем блоке вы добавите поиск данных о местоположении в ViewModel.