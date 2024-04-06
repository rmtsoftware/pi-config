#### 1. Установка утилиты ST-Link
Утилита ST-Link позволяет вам взаимодействовать с устройством STM32 через ST-Link/V2 программатор/отладчик. На Debian и производных системах её можно установить из исходного кода.

Установите зависимости:
```
sudo apt-get update
sudo apt-get install build-essential cmake libusb-1.0-0-dev
```

Клонируйте репозиторий:
```
git clone https://github.com/texane/stlink.git
```

Соберите и установите ST-Link:
```
cd stlink
make
sudo make install
sudo ldconfig
```

Это установит утилиты командной строки st-info, st-flash, st-util, которые позволяют работать с устройствами STM32 через программатор/отладчик ST-Link/V2.


#### 2. Установка инструментов для кросс-компиляции (опционально)

Установите кросс-компилятор:
```
sudo apt-get install gcc-arm-none-eabi
```

Установите другие необходимые инструменты (например, make, GDB):
```
sudo apt-get install make gdb-multiarch
```

#### 3. Настройка правил udev для ST-Link/V2 (опционально)
Для того чтобы программатор/отладчик ST-Link/V2 корректно распознавался и имел доступ без необходимости использования sudo, может потребоваться настроить правила udev.

Создайте файл правил udev:
```
echo 'SUBSYSTEM=="usb", ATTR{idVendor}=="0483", ATTR{idProduct}=="3748", MODE="0666"' | sudo tee /etc/udev/rules.d/49-stlinkv2.rules
```

Перезагрузите правила udev:
```
sudo udevadm control --reload
```

После выполнения этих шагов ваш Raspberry Pi должен быть готов к разработке программ для микроконтроллеров STM32.
