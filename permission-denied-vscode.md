#### Error: EACCES: permission denied
---

Изменение владельца файла или каталога: Если вы являетесь владельцем или имеете права суперпользователя, вы можете изменить владельца файла или каталога на себя с помощью команды chown. Например:
```
sudo chown user:user /home/user/Project/pi-config/stm-driver-install.md
sudo chown user:user /home/user/Project/pi-config/
```

---

Изменение прав доступа: Если файл или каталог уже принадлежат вам, но у вас нет прав на запись, вы можете изменить права доступа с помощью команды chmod. Например:
```
chmod u+w /home/user/Project/pi-config/stm-driver-install.md
```
