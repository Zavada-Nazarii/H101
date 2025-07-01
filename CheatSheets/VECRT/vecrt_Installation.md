
# Установка Docker на Kali Linux для VECTR

Цей README описує процес автоматизованої установки Docker та Docker Compose на Kali Linux, із коректним репозиторієм (`bookworm`), сумісним із `kali-rolling`.

---

## 📦 Що встановлюється:

- Docker Engine
- Docker CLI
- containerd
- Docker Buildx
- Docker Compose Plugin

---

## 📋 Інструкції з використання:

1. **Завантаження скрипта**

Збережіть скрипт у файл `install_docker_kali.sh`:

```bash
curl -O https://example.com/install_docker_kali.sh
chmod +x install_docker_kali.sh
```

*(або скопіюйте вручну з цього репозиторію)*

2. **Запуск скрипта**

```bash
./install_docker_kali.sh
```

3. **Перевірка встановлення**

```bash
docker --version
docker compose version
```

4. **Запуск docker без sudo**

```bash
newgrp docker
```

---

## 📁 Вміст скрипта `install_docker_kali.sh`

```bash
#!/bin/bash

set -e

echo "[+] Оновлення системи..."
sudo apt update && sudo apt upgrade -y

echo "[+] Встановлення залежностей..."
sudo apt install -y \
    ca-certificates \
    curl \
    gnupg \
    lsb-release \
    apt-transport-https \
    software-properties-common

echo "[+] Створення директорії ключів..."
sudo install -m 0755 -d /etc/apt/keyrings

echo "[+] Додавання GPG ключа Docker..."
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo "[+] Створення файлу репозиторію..."
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/debian bookworm stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

echo "[+] Оновлення APT після додавання репозиторію..."
sudo apt update

echo "[+] Встановлення Docker Engine..."
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

echo "[+] Перевірка версії Docker:"
docker --version
docker compose version

echo "[+] Додавання користувача '$USER' до групи docker..."
sudo usermod -aG docker $USER

echo "[+] Завершено! Для застосування групи docker виконай 'newgrp docker' або перезавантаж систему."
```

---

✅ Після встановлення можна продовжити з розгортанням [VECTR](https://docs.vectr.io/Installation/)

