# 🛡️ Lab 2: Завдання для практичного виконання по лекції 3-4 

## 💽 1. Встановлення Metasploitable 2 

### Завдання:
1. Завантажити та розгорнути віртуальну машину Metasploitable 2 у VirtualBox або VMware.
2. Перевірити доступність хосту в мережі (наприклад, за допомогою `ping`).
3. Надати скріншот консолі, яка підтверджує, що машина працює (IP-адреса, відповідь на ping).

---

## 🔎 2. Пошук через Google Dorks 

### Завдання:
1. Використати щонайменше 3 Google Dork-запити для пошуку потенційно вразливих сайтів або файлів.
   **Приклади:**
   - `inurl:login site:.ru`
   - `intitle:index.of "backup"`
   - `filetype:sql "password"`
2. Обрати один знайдений результат і коротко описати, що було знайдено.

### Пояснення:
- Опишіть, як працюють Google Dorks.
- Додайте скріншот пошукових результатів.

---

## 🔦 3. Сканування за допомогою WPScan

### Завдання:
1. Виявити сайт на WordPress (наприклад, локальний або з hackthebox).
2. Запустити сканування WPScan:
   ```bash
   wpscan --url http://<target> --enumerate u,vp,vt --api-token <ваш_токен>
   ```
3. Зберегти результати сканування у файл та прикріпити до звіту.

### Пояснення:
- Опишіть знайдені плагіни/теми та можливі вразливості.
- Вкажіть потенційні вектори атак.

---

## 🔦 4. Сканування через CMSeek

### Завдання:
1. Знайти CMS-сайт (можна використати щось на localhost).
2. Запустити CMSeek:
   ```bash
   python3 cmseek.py
   ```
3. 📝 Надати лог/звіт сканування.

### Пояснення:
- Які CMS були виявлені?
- Яка структура сайту (папки, шаблони, версії)?
- Можливі атаки на виявлену CMS.

---

## 🔹 5. Виявлення SQL-інʼєкцій (SQLi)

### Завдання:
1. Запустити DVWA на Metasploitable2 або іншій машині.
2. Встановити рівень безпеки "Low" через DVWA Security.
3. За допомогою `sqlmap` протестувати одну з форм на наявність SQLi:
   ```bash
   sqlmap -u "http://<dvwa_ip>/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=<your_id>" --batch 
   ```
4. Зробити dump однієї з БД.
5. Спробувати реалізувати сліпу інєкцію у SQL Injection (Blind)
6. Із використанням Burp Suite пройти лабораторну [SQL injection vulnerability allowing login bypass](https://portswigger.net/web-security/sql-injection/lab-login-bypass)
7. Із використанням Burp Suite отримати version [SQL injection attack, querying the database type and version on MySQL and Microsoft](https://portswigger.net/web-security/sql-injection/examining-the-database/lab-querying-database-version-mysql-microsoft)
8. Ознайомитись із техніками [SQL injection](https://portswigger.net/web-security/all-labs#sql-injection)
9. Спробувати на тестовому сайті акунетікс sqlmap у формі авторизації із dump

### Пояснення:
- Що таке SQLi, як вона працює.
- Які параметри були вразливими.
- Результат роботи sqlmap (вивід + витягнуті дані).

---

## 📸 Підтвердження виконання

- Для кожного завдання: додати скріншоти (у форматі JPG/PNG), лог-файли або короткі текстові звіти.
- Додавайте креативу у виконанні, збільшуючи об'єми результатів або інших технік і підходів.

---

## 🔑 Інструменти для генерації паролів (казав під час лекції, що поділюсь) 

- https://github.com/Mebus/cupp
- https://github.com/jim3ma/crunch

