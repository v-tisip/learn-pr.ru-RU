При создании виртуальной машины ей назначается общедоступный IP-адрес, доступный через Интернет, и частный IP-адрес, используемый в центре обработки данных Azure. С помощью средства `ssh` можно быстро проверить, запущена ли виртуальная машина Linux. Напомним, что в качестве имени администратора мы задали `aldis`. Необходимо указать именно это имя.

```azurecli
ssh 168.61.54.62 -l aldis
```

> [!NOTE]
> Пароль не требуется, так как при создании виртуальной машины мы сгенерировали пару ключей SSH. При первом доступе к виртуальной машине через оболочку появится запрос касательно подлинности узла. 
> 
> Связано это с тем, что мы обращаемся непосредственно к IP-адресу, а не к имени узла. Ответьте "да", чтобы сохранить IP-адрес как допустимый узел для подключения и разрешить установление подключения.

```
The authenticity of host '168.61.54.62 (168.61.54.62)' can't be established.
RSA key fingerprint is SHA256:hlFnTCAzgWVFiMxHK194I2ap6+5hZoj9ex8+/hoM7rE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '168.61.54.62' (RSA) to the list of known hosts.
```

Далее откроется удаленная оболочка, в которой можно вводить команды Linux.

```
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
aldis@SampleVM:~$
```

Попробуйте выполнить несколько команд. По завершении выйдите из учетной записи (введите в оболочке `logout` или `exit`).