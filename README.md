# Dokumentácia pre Unit Converter

## Komponenty projektu
Projekt obsahuje nasledujúce komponenty:
1. **Backend**:
   - Flask aplikácia (`app.py`).
   - Obsahuje konfiguračný súbor `Dockerfile` na vytvorenie backendu.
   - Používa databázu PostgreSQL na spracovanie údajov.
2. **Frontend**:
   - Statická webová aplikácia s použitím HTML, CSS a JavaScriptu (`index.html`, `styles.css`, `script.js`).
   - Obsahuje konfiguračný súbor `Dockerfile` na vytvorenie frontendu.
3. **Databáza**:
   - PostgreSQL databáza na uloženie údajov.
4. **NGINX**:
   - Reverzný proxy server na presmerovanie požiadaviek medzi frontend a backend.
5. **Docker Compose**:
   - `docker-compose.yml` súbor na koordináciu všetkých kontajnerov (frontend, backend, databáza, nginx).

## Štart aplikácie
1. Pripravte aplikáciu spustením nasledujúceho príkazu v termináli:
   ```bash
   python prepare-app.py
   ```
2. Spustite aplikáciu pomocou príkazu:
   ```bash
   python start-app.py
   ```
3. Aplikácia bude dostupná vo webovom prehliadači na adrese: [http://localhost](http://localhost)

## Ukončenie aplikácie
Aplikáciu a jej zdroje môžete zastaviť a vyčistiť spustením nasledujúceho príkazu:
   ```bash
   python end-app.py
   ```
