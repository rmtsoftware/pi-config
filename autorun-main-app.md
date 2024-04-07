## Автозапуск скрипта

---

Чтобы ваш скрипт `app.sh` запускался при старте системы на Raspberry Pi 4B с Raspberry OS и чтобы система автоматически перезапускала его, если `main.py` перестаёт работать, вы можете использовать следующий подход с использованием `systemd` для создания службы, которая будет управлять вашим скриптом.

---

#### 1. Создание файла службы systemd
Откройте терминал и создайте новый файл конфигурации службы в директории `/etc/systemd/system/`:
```
sudo nano /etc/systemd/system/app.service
```

Вставьте следующее содержимое в файл:
```
[Unit]
Description=My App Service
After=network.target

[Service]
Type=simple
User=user
WorkingDirectory=/home/user/Project/client
ExecStart=/bin/bash /home/user/Project/client/app.sh
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```
Параметр `Restart=always` указывает `systemd` автоматически перезапускать ваше приложение, если оно завершается. `RestartSec=5` определяет задержку в 5 секунд перед перезапуском.

---

#### 2. Включение и запуск службы
Перезагрузите systemd, чтобы он прочитал ваш новый файл службы:
```
sudo systemctl daemon-reload
```

Включите службу, чтобы она автоматически запускалась при загрузке системы:
```
sudo systemctl enable app.service
```

Запустите службу:
```
sudo systemctl start app.service
```

#### 3. Проверка статуса службы
```
sudo systemctl status app.service
```
Эта команда покажет текущее состояние службы, включая её активность и последние логи.

---

#### Замечание
- Убедитесь, что ваши скрипты (`app.sh` и `main.py`) имеют права на выполнение. Это можно сделать с помощью команды `chmod +x filename`.