
# ✅ Налаштування VECTR з власними SSL сертифікатами (usercert) у Docker

Цей файл описує повний та перевірений процес налаштування HTTPS для VECTR, встановленого у `/opt/vectr`, із використанням власних самопідписаних сертифікатів.

---

## 📁 Структура директорії

```
/opt/vectr/
├── docker-compose.yml
├── .env
└── user/
    └── certs/
        ├── ssl.crt
        └── ssl.key
```

---

## 🔧 Кроки

### 1. Перейти у VECTR-директорію

```bash
cd /opt/vectr
```

---

### 2. Створити директорію для сертифікатів

```bash
mkdir -p user/certs
```

---

### 3. Згенерувати самопідписані сертифікати

> ⚠️ Важливо! CN повинен відповідати VECTR_HOSTNAME у `.env`, наприклад `sravectr.internal`.

```bash
openssl req -x509 -newkey rsa:4096 -nodes \
  -keyout user/certs/ssl.key \
  -out user/certs/ssl.crt \
  -days 365 \
  -subj "/CN=sravectr.internal"
```

---

### 4. Внести зміни у `.env`

Встановити:

```env
VECTR_CERTPROFILE=usercert
VECTR_FEATURES_SSLCONF=false
```

---

### 5. Внести монтування сертифікатів у `docker-compose.yml`

У секцію `services.vectr-caddy-gateway:` додати:

```yaml
    volumes:
      - ./user/certs:/user/certs
```

---

### 6. Перезапустити стек

```bash
docker compose down
docker compose up -d
```

---

### 7. Додати запис у `/etc/hosts` (на ОС, з якої заходите в браузері)

```bash
192.168.141.132 sravectr.internal
```

---

### 8. Відкрити VECTR у браузері

```
https://sravectr.internal:8081
```

> 👁 Якщо браузер показує попередження — натисніть “Advanced → Proceed”.

---

## ✅ Результат

VECTR працює через HTTPS, використовуючи власні сертифікати з `./user/certs`.

---
