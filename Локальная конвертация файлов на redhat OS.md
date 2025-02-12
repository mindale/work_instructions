Доработка документации CS - [[S3] - настройка s3-fs](https://blog.croc.ru/pages/viewpage.action?pageId=278497693)
1. Скачиваем s3-fs для манипуляции с бакетом
`sudo dnf install s3fs-fuse`
2. Создаем в каталоге `/etc/` файл, в котором указываем параметры, берем из профиля `Получить настройки доступа к API`
`<Имя Бакета>:<имя проекта в облаке КРОК>:<Учётная запись в облаке КРОК>:<SECRET KEY>`
3. Изменяем права на файл с данными (В данном примере изменяем значения для root на чтение и запись) `chmod 600 /etc/passwd-s3fs`
4. Затем создаем директорию в которой будем хранить бакеты с облака `/mnt/s3`
5. Затем монтируем файл при помощи команды
`sudo s3fs {bucketname} {/mountpoint/dir/} -o passwd_file=/etc/passwd-s3fs -o allow_other -o url=https://s3.k2.cloud`
6. Для безопасности действий при внесении данных в файл `/etc/fstab` рекомендуется создать `sudo cp /etc/fstab /etc/fstab_backup`
7. Затем в файле `/etc/fstab` вносим дополнительную строку с таким содержимым:
`s3fs#{bucketname} {mountpoint-dir} fuse _netdev,allow_other,use_path_request_style,url=https://s3.k2.cloud,passwd_file=/etc/passwd-s3fs 0 0`
![[fstab.png]]7. Если все получилось, можем перейти в папку `mnt/s3`, в которой будут храниться все файлы из бакета, которые можно копировать в свои папки.


Конвертация файлов разных форматов диска:
1. Скачиваем утилиту qemu-img при помощи команды `sudo dnf install qemu-img`
2. Конвертируем нужные файлы в нужный формат `qemu-img convert -f [формат до] -O [формат после] image.[формат] image.[формат]`
Используемые документации:
[fstab](https://help.ubuntu.ru/wiki/fstab)
[qemu-img](https://serverfault.com/questions/1145397/how-do-i-convert-a-vmdk-disk-to-qcow2-using-qemu-img-without-inflating-the-disk)
[qemu-img2](https://koobik.net/howto-convert-vmware-vm-to-kvm/)
[s3fs](https://cloud.ru/docs/s3/ug/topics/tools__s3fs.html#id1)
[s3fs-mounting-info](https://upcloud.com/resources/tutorials/mount-object-storage-cloud-server-s3fs-fuse)
