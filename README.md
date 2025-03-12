# README

## Popis projektu

Tento projekt je webová aplikácia na konverziu jednotiek, ktorá je nasadená pomocou Dockeru a obsahuje frontend, backend a databázový server PostgreSQL. Frontend je postavený na Nginx, backend beží na Flask frameworku a PostgreSQL slúži ako úložisko.

## Komponenty

### 1. **Databáza**

- **Názov kontajnera:** `postgres_db`
- **Obraz:** `postgres:latest`
- **Porty:** Interné
- **Popis:** Ukladá dáta o jednotkách a konverzných faktoroch

### 2. **Backend**

- **Názov kontajnera:** `backend`
- **Obraz:** Vytvorený z `backend/Dockerfile`
- **Porty:** `5000:5000`
- **Popis:** REST API postavené na Flask frameworku, spracováva požiadavky na konverziu jednotiek

### 3. **Frontend**

- **Názov kontajnera:** `frontend`
- **Obraz:** Vytvorený z `frontend/Dockerfile`
- **Porty:** `80:80`
- **Popis:** Používateľské rozhranie pre aplikáciu, obsluhované cez Nginx

### 4. **Nginx**

- **Názov kontajnera:** `nginx`
- **Obraz:** `nginx:latest`
- **Porty:** `8080:80`
- **Popis:** Reverzný proxy server, smeruje požiadavky na frontend a backend

## Inštalácia a spustenie aplikácie

1. **Príprava aplikácie:**

   ```bash
   python prepare-app.py
   ```

   Tento krok vytvorí potrebnú Docker sieť a zostaví obrazy.

2. **Spustenie aplikácie:**

   ```bash
   python start-app.py
   ```

   Tento krok spustí kontajnery na pozadí.

3. **Prístup k aplikácii:**

   - Aplikácia bude dostupná v prehliadači na adrese: [http://localhost](http://localhost)

4. **Zastavenie aplikácie:**

   ```bash
   python end-app.py
   ```

   Tento krok zastaví všetky kontajnery a vyčistí Docker sieť a objemy.

## Docker Compose

Všetky služby sú definované v súbore `docker-compose.yml`. Používa sa `bridge` sieť `converter_network` pre komunikáciu medzi kontajnermi.
