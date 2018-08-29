<span data-ttu-id="7913f-101">Вы создали новую виртуальную машину Linux, изменили ее размер, остановили и запустили ее и изменили конфигурацию с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7913f-101">You've created a new Linux virtual machine, changed its size, stopped and started it, and updated the configuration with the Azure CLI.</span></span>

## <a name="cleanup"></a><span data-ttu-id="7913f-102">Очистка</span><span class="sxs-lookup"><span data-stu-id="7913f-102">Cleanup</span></span>

<span data-ttu-id="7913f-103">Теперь, когда мы закончили работу с виртуальной машиной и она нам больше не нужна, давайте удалим ресурсы.</span><span class="sxs-lookup"><span data-stu-id="7913f-103">Now that we're finished with the VM and no longer need it, let's delete the resources.</span></span> <span data-ttu-id="7913f-104">Очистка важна, так как она высвобождает ресурсы вычисления и хранения, использование которых вы оплачиваете.</span><span class="sxs-lookup"><span data-stu-id="7913f-104">Cleanup is important for compute and storage resources that can continue to be billed against your account.</span></span> 

<span data-ttu-id="7913f-105">Вы можете удалить отдельные ресурсы с помощью команды `delete`. Но проще будет удалить все с помощью `az group delete`.</span><span class="sxs-lookup"><span data-stu-id="7913f-105">You can delete individual resources with the `delete` command, but the easiest way to remove everything is with `az group delete`.</span></span> <span data-ttu-id="7913f-106">В Azure CLI введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7913f-106">Execute the following command in the Azure CLI:</span></span>

```azurecli
az group delete --name ExerciseResources --no-wait
```

<span data-ttu-id="7913f-107">Ответьте "Да" на запрос или используйте параметр `--yes` для автоматического ответа.</span><span class="sxs-lookup"><span data-stu-id="7913f-107">Answer "yes" to the prompt when shown, or use the `--yes` parameter to auto-answer the prompt.</span></span>

<span data-ttu-id="7913f-108">Эта команда удаляет все ресурсы, связанные с группой ресурсов, и гарантированно высвобождает их в правильном порядке.</span><span class="sxs-lookup"><span data-stu-id="7913f-108">This command deletes all of the resources associated with the resource group, and is guaranteed to deallocate them in the correct order.</span></span> <span data-ttu-id="7913f-109">Параметр `--no-wait` предотвращает блокировку Azure CLI в ходе удаления.</span><span class="sxs-lookup"><span data-stu-id="7913f-109">The `--no-wait` parameter keeps the Azure CLI from blocking while the deletion takes place.</span></span> <span data-ttu-id="7913f-110">Оставьте его выключенным в ожидании удаления ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7913f-110">Leave it off to wait for the resources to be deleted.</span></span> <span data-ttu-id="7913f-111">Или используйте команду `az group wait -n ExerciseResources --deleted` позже в скрипте, чтобы дождаться завершения удаления.</span><span class="sxs-lookup"><span data-stu-id="7913f-111">Or use the `az group wait -n ExerciseResources --deleted` command later in your script to wait for the deletion to finish.</span></span>


## <a name="further-reading"></a><span data-ttu-id="7913f-112">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="7913f-112">Further reading</span></span>

* [<span data-ttu-id="7913f-113">Общие сведения об Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7913f-113">Azure CLI overview</span></span>](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)
* [<span data-ttu-id="7913f-114">Справочник по командам Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7913f-114">Azure CLI command reference</span></span>](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)
