В простой инструкции по установке драйверов virtio для виртуализации hvm, используем 
Для начала нужно обратиться на [сайт с iso образом драйверов virtio](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/stable-virtio/virtio-win.iso) 

Используем [простую инструкцию](https://blog.croc.ru/pages/viewpage.action?pageId=278498104) для установки драйверов, без затрагивания изменения в риестр.
1. Проверяем диспетчер устройств![[Device_before.png]]
2. Проверяем сведения о драйверах virtio в риестре![[empty_riestr.png]]
3. Скачиваем стабильную версию драйверов virtio с [сайта]([https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/stable-virtio/virtio-win.iso](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/stable-virtio/virtio-win.iso))
4. Открываем iso образ (монтируем диск)![[mounting.png]]
5. Открываем `Device Manager` нажимает на устройство `Action->Add legacy hardware->Next->Install hardware that I manually selected->Show All Devices->Have Disk` затем выбираем `viostor` драйвер из папки viostor ![[viostordrivers.png]]![[device_after_virtio.png]]
7. Открываем `Device Manager` нажимает на устройство `Action->Add legacy hardware->Next->Install hardware that I manually selected->Show All Devices->Have Disk` затем выбираем `NetKVM` драйвер из папки NetKVM.![[NETKVM.png]]![[device_after_netkvm.png]]
8. Выключение vm и включени hwm
Если после проделанной процедуры при запуске vm вы получаете на выходе ![[Pasted image 20250124172440.png]]
Значит простая инструкция не помогает, придётся вносить изменения в риестр. Для этого возвращаем vm в тип виртуализации hvm legacy и выполняем следующие действия:
1. Очищаем сведения в риестре по пути `(HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\viostor`![[Pasted image 20250124174713.png]]
2. Исполняем файл .reg
3. Открываем `Device Manager` нажимает на устройство `Action->Add legacy hardware->Next->Install hardware that I manually selected->Show All Devices->Have Disk` затем выбираем `viostor` драйвер из папки viostor ![[Pasted image 20250124175016.png]]
4. Выключаем vm и меняем виртуализацию на hvm. Запускаем.
5. Обновляем Оставшиеся драйвера через Add legacy hardware![[Pasted image 20250124175844.png]]