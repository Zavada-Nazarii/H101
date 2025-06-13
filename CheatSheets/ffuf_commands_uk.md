
# Команди FFUF

Цей документ містить список основних команд FFUF з поясненнями українською мовою для ефективної роботи з інструментом.

## Основні команди

1. **-u**  
   Вказує URL, до якого FFUF буде виконувати запити.  
   **Приклад**:  
   ```bash
   ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt
   ```

2. **-w**  
   Вказує шлях до wordlist'у, який використовуватиметься для брутфорсу URL.  
   **Приклад**:  
   ```bash
   ffuf -u http://example.com/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
   ```

3. **-mc**  
   Вказує HTTP-статуси, які будуть відображатися в результатах.  
   **Приклад**:  
   ```bash
   ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -mc 200,301
   ```

5. **-fs**  
   Фільтрує відповіді за розміром сторінки (в байтах).  
   **Приклад**:  
   ```bash
   ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -fs 1234
   ```

6. **-fw**  
   Фільтрує відповіді за кількістю слів на сторінці.  
   **Приклад**:  
   ```bash
   ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -fw 50
   ```

7. **-ac**  
   Вимикає автоматичне коригування запитів для пропуску надмірних відповідей (якщо їх надто багато).  
   **Приклад**:  
   ```bash
   ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -ac
   ```

8. **-b**  
   Додає куки до запиту. Це корисно для роботи з сесіями або авторизацією.  
   **Приклад**:  
   ```bash
   ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -b "sessionid=xyz"
   ```

9. **-H**  
   Додає додаткові HTTP заголовки до запиту. Це дозволяє настроїти специфічні заголовки, які можуть бути потрібні для тестування.  
   **Приклад**:  
   ```bash
   ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -H "User-Agent: Mozilla/5.0"
   ```

10. **-x**  
    Вказує проксі-сервер для перенаправлення запитів.  
    **Приклад**:  
    ```bash
    ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -x http://localhost:8080
    ```

11. **-e**  
    Додає розширення до словника. Наприклад, якщо ви хочете додавати `.php` або `.html` до ваших запитів.  
    **Приклад**:  
    ```bash
    ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -e .php,.html
    ```

12. **-mode**  
    Визначає режим роботи, наприклад, для брутфорсу URL або параметрів GET.  
    **Приклад**:  
    ```bash
    ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -mode cluster
    ```

13. **-v**  
    Виводить більш детальну інформацію про процес виконання.  
    **Приклад**:  
    ```bash
    ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -v
    ```

14. **-rate**  
    Вказує рейт ліміт перебору (кількість запитів за секунду).  
    **Приклад**:  
    ```bash
    ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -rate 10
    ```

15. **-o**  
    Зберігає результати у файл. Це дозволяє зберігати результати брутфорсу для подальшого аналізу.  
    **Приклад**:  
    ```bash
    ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -o results.json
    ```

16. **-json**  
    Форматує результати в JSON. Це дозволяє зберігати дані в зручному форматі для подальшого аналізу.  
    **Приклад**:  
    ```bash
    ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -json
    ```

