<span data-ttu-id="65613-101">При создании виртуальной машины ей назначается общедоступный IP-адрес, доступный через Интернет, и частный IP-адрес, используемый в центре обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="65613-101">When you create a virtual machine, it gets assigned a public IP address that is reachable over the Internet, and a private IP address used within the Azure data center.</span></span> <span data-ttu-id="65613-102">С помощью средства `ssh` можно быстро проверить, запущена ли виртуальная машина Linux.</span><span class="sxs-lookup"><span data-stu-id="65613-102">We can quickly test that the Linux VM is up and running using the `ssh` tool.</span></span> <span data-ttu-id="65613-103">Напомним, что в качестве имени администратора мы задали `aldis`. Необходимо указать именно это имя.</span><span class="sxs-lookup"><span data-stu-id="65613-103">Remember that we set our admin name to `aldis`, so we have to specify that.</span></span>

```azurecli
ssh 168.61.54.62 -l aldis
```

> [!NOTE]
> <span data-ttu-id="65613-104">Пароль не требуется, так как при создании виртуальной машины мы сгенерировали пару ключей SSH.</span><span class="sxs-lookup"><span data-stu-id="65613-104">We don't need a password because we generated an SSH key pair as part of the VM creation.</span></span> <span data-ttu-id="65613-105">При первом доступе к виртуальной машине через оболочку появится запрос касательно подлинности узла.</span><span class="sxs-lookup"><span data-stu-id="65613-105">The first time you shell into the VM, it will give you a prompt about the authenticity of the host.</span></span> 
> 
> <span data-ttu-id="65613-106">Связано это с тем, что мы обращаемся непосредственно к IP-адресу, а не к имени узла.</span><span class="sxs-lookup"><span data-stu-id="65613-106">This is because we are hitting an IP address directly instead of a host name.</span></span> <span data-ttu-id="65613-107">Ответьте "да", чтобы сохранить IP-адрес как допустимый узел для подключения и разрешить установление подключения.</span><span class="sxs-lookup"><span data-stu-id="65613-107">Answering "yes" will save the IP as a valid host for connection and allow the connection to proceed.</span></span>

```
The authenticity of host '168.61.54.62 (168.61.54.62)' can't be established.
RSA key fingerprint is SHA256:hlFnTCAzgWVFiMxHK194I2ap6+5hZoj9ex8+/hoM7rE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '168.61.54.62' (RSA) to the list of known hosts.
```

<span data-ttu-id="65613-108">Далее откроется удаленная оболочка, в которой можно вводить команды Linux.</span><span class="sxs-lookup"><span data-stu-id="65613-108">Then you'll be presented with a remote shell where you can enter Linux commands.</span></span>

```
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
aldis@SampleVM:~$
```

<span data-ttu-id="65613-109">Попробуйте выполнить несколько команд. По завершении выйдите из учетной записи (введите в оболочке `logout` или `exit`).</span><span class="sxs-lookup"><span data-stu-id="65613-109">Try a few commands as practice and when you are finished, sign out of your account (type `logout` or `exit` in the shell).</span></span>