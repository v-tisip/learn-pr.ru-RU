<span data-ttu-id="96234-101">Наша цель — создать виртуальную машину Azure.</span><span class="sxs-lookup"><span data-stu-id="96234-101">Our goal is to create a new Azure virtual machine.</span></span> <span data-ttu-id="96234-102">Нам потребуется предоставить некоторые сведения, чтобы определить расположение ресурсов, используемую операционную систему и требуемую конфигурацию оборудования для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="96234-102">We'll need to supply several pieces of information to identify the resource location, OS to use, and the hardware configuration needed for the VM.</span></span> <span data-ttu-id="96234-103">Давайте начнем с **группы ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="96234-103">Let's start with the **resource group**.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="96234-104">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="96234-104">Create a resource group</span></span>

<span data-ttu-id="96234-105">В Azure _группы ресурсов_ служат для объединения связанных ресурсов, таких как виртуальные машины и базы данных.</span><span class="sxs-lookup"><span data-stu-id="96234-105">Azure uses _resource groups_ to group related resources such as virtual machines and databases together.</span></span> <span data-ttu-id="96234-106">Для группы ресурсов также определяется расположение (называемое регионом). От него будет зависеть то, в каком центре обработки данных размещается ресурс.</span><span class="sxs-lookup"><span data-stu-id="96234-106">The resource group also identifies a specific location (called a "region") which will decide what data center the resource is placed into.</span></span>

<span data-ttu-id="96234-107">Для эксперимента создайте группу ресурсов с именем `ExerciseResources` и поместите ее в регион `eastus`.</span><span class="sxs-lookup"><span data-stu-id="96234-107">Since we're experimenting, start by creating a new resource group named `ExerciseResources` and place it into the `eastus` region.</span></span>

> [!NOTE]
> <span data-ttu-id="96234-108">Укажите это имя в точности, так как система обучения Майкрософт будет позднее искать ресурс по нему.</span><span class="sxs-lookup"><span data-stu-id="96234-108">Make sure to use this exact name for your new resource group, because the Microsoft Learn system will be looking for this resource name later.</span></span> 

<span data-ttu-id="96234-109">В Azure Cloud Shell введите приведенную ниже команду Azure CLI, чтобы создать группу ресурсов в подписке.</span><span class="sxs-lookup"><span data-stu-id="96234-109">Type the following Azure CLI command in Azure Cloud Shell to create the resource group in your subscription.</span></span>

```azurecli
az group create --name ExerciseResources --location eastus
```

<span data-ttu-id="96234-110">Она вернет блок JSON, указывающий на то, что группа ресурсов создана.</span><span class="sxs-lookup"><span data-stu-id="96234-110">This will return a JSON block indicating the resource group has been created.</span></span> <span data-ttu-id="96234-111">Выглядеть он должен примерно так:</span><span class="sxs-lookup"><span data-stu-id="96234-111">It should look something like:</span></span>

```json
{
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources",
  "location": "eastus",
  "managedBy": null,
  "name": "ExerciseResources",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

<span data-ttu-id="96234-112">Обратите внимание на то, что в ответе возвращаются уникальный идентификатор, расположение и имя подписки.</span><span class="sxs-lookup"><span data-stu-id="96234-112">Notice that it returns the subscription unique identifier, location, and name as part of the response.</span></span> <span data-ttu-id="96234-113">С помощью этих данных можно проверить, была ли группа создана в соответствующих подписке и расположении.</span><span class="sxs-lookup"><span data-stu-id="96234-113">You can use these to verify it got created in the proper subscription and location.</span></span>

<span data-ttu-id="96234-114">Теперь, когда у вас есть группа ресурсов, создайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="96234-114">Now that we have a resource group, let's create a new virtual machine.</span></span>