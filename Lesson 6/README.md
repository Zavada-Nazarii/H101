
# 🛡️ Lab 4: Reverse Shell

📘 Середовище для виконання
Metasploitable2 + DVWA (Damn Vulnerable Web Application)
PortSwigger Web Security Academy (https://portswigger.net/web-security)

---

## 1. 🎯 Реверс шел через Metasploit
**Завдання:**  
- Використовуючи Metasploit Framework, налаштуйте реверсний шел для віддаленого сервера (наприклад, DVWA або Metasploitable2).  
- Створіть payload за допомогою `msfvenom`, використовуючи опцію для реверсного шелу.  
- Встановіть meterpreter сесію з сервером через Metasploit.  
- Виконайте basic shell команду на сервері через отриманий реверсний шел.  

**Інструменти:**  
- `msfvenom`, `msfconsole`  
- DVWA, Metasploitable2  

---

## 2. 🎯 Реверс через Bash
**Завдання:**  
- Створіть bash-скрипт для зворотного зв'язку з вашим хакерським сервером або використати вразливий для RCE об'єкт.  
- Поясніть, як використовувати механізм `bash -i` для зворотного з'єднання та які потенційні ризики виникають через відсутність належного захисту на сервері.
- Провести покращення TTY

**Інструменти:**  
- Bash, Netcat  

---

## 3. 🎯 Реверс через Flask Debug Mode
**Завдання:**  
- Націльтеся на веб-додаток, побудований за допомогою [Flask](https://github.com/Zavada-Nazarii/H101/tree/master/CheatSheets/Flask), і знайдіть спосіб активувати Debug mode.  
- Використовуйте Flask Debug mode для виконання віддалених команд на сервері.  
- Поясніть потенційні ризики використання Debug mode в Flask.

**Інструменти:**  
- Flask, Python  

---

## 4. 🎯 Реверс через WP Edit Plugin
**Завдання:**  
- Проведіть тестування безпеки плагіну WP Edit на WordPress сайті.  
- Знайдіть вразливість, яка дозволяє завантаження небезпечного файлу через плагін.  
- Використовуйте атаку на вразливість плагіна для отримання реверсного шелу.

**Інструменти:**  
- WordPress, WP Edit Plugin, Netcat  

---

## 5. 🎯 Реверс через File Upload with Bypass WAF PHP (e.g., PHP.png)
**Завдання:**  
- Створіть метод обходу WAF (Web Application Firewall), що дозволяє завантажити файл, який виглядає як зображення (.png), але містить PHP код.   [допомога тут](https://book.hacktricks.wiki/en/pentesting-web/file-upload/index.html?highlight=File%20upload#file-upload)
- Використовуйте цю вразливість для виконання реверсного шелу на сервері.  
- Поясніть, як можна обійти фільтрацію файлів, використовуючи атаку на вразливість WAF.

**Інструменти:**  
- PHP, WAF, DVWA/Metasploitable2  
- Netcat, Burp Suite
- Лабораторні для виконання із File upload vulnerabilities (не всі, бажано будь які три, але чим більше тим краще) 🧪[PortSwigger Labs](https://portswigger.net/web-security/all-labs#file-upload-vulnerabilities)

---

## 📌 Звітність:
Для кожного завдання:
- Надішліть скріншоти payload'ів та результатів.
- Поясніть, що саме відбулось.
- Якщо були труднощі — коротко опишіть їх.

---

## 📘 Корисні ресурси:
1. MIMI для [Content-Type](https://docs.w3cub.com/http/basics_of_http/mime_types/complete_list_of_mime_types.html)
2. [Команди Meterpreter](https://github.com/Zavada-Nazarii/H101/blob/master/CheatSheets/meterpreter_commands_uk.md)
3. [Команди MSFvenom](https://github.com/Zavada-Nazarii/H101/blob/master/CheatSheets/msfvenom_commands_uk.md)
4. [Вектори атак через Python-інтерпретатор](https://github.com/Zavada-Nazarii/H101/blob/master/CheatSheets/python_attack_vectors_uk.md)
