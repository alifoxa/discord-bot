# Dokumentácia webovej aplikácie Unit Converter

Táto dokumentácia poskytuje prehľad o aplikácii na prevod jednotiek, opisuje jej komponenty a vysvetľuje, ako aplikáciu spustiť a pristupovať k nej prostredníctvom webového prehliadača.

## Prehľad

Aplikácia na prevod jednotiek je kontajnerové riešenie, ktoré využíva Docker na orchestráciu viacerých služieb. Používa backend založený na Flasku na konverznú logiku, frontend postavený na HTML/CSS/JavaScripte na interakciu s používateľom a reverzný proxy server Nginx na efektívne smerovanie. Aplikácia sa spolieha na databázu PostgreSQL na uchovávanie a správu údajov.

## Komponenty

- **prepare-app.py**  
  Tento skript nastaví prostredie vytvorením vyhradenej Docker siete a zostavením obrazov služieb pomocou príkazu `docker-compose build`.

- **start-app.py**  
  Tento skript spustí aplikáciu v odpojenom režime pomocou `docker-compose up -d` a automaticky otvorí predvolený webový prehliadač na zobrazenie aplikácie. Prístup k aplikácii: [tu](http://localhost)

- **end-app.py**  
  Tento skript korektne zastaví aplikáciu vypnutím všetkých kontajnerov, odstránením Docker siete, vyčistením nepoužívaných Docker objemov a odstránením obrazov súvisiacich s projektom.

- **docker-compose.yml**  
  Definuje viac-kontajnerové aplikačné služby:
  - **postgres_db:** Hosťuje databázu PostgreSQL potrebnú na ukladanie údajov.
  - **backend:** Spúšťa Flask server, ktorý obsahuje konverznú logiku a komunikuje s databázou.
  - **frontend:** Zostavuje a poskytuje používateľské rozhranie vrátane HTML, CSS a JavaScript súborov, ktoré zabezpečujú prevodné rozhranie.
  - **nginx:** Pôsobí ako reverzný proxy server, ktorý smeruje prichádzajúce webové požiadavky na príslušnú backendovú službu.

- **backend/...**
  - **app.py:** Implementuje konverznú logiku pomocou Flasku. Tento súbor sa pripája k databáze PostgreSQL, číta konverzné údaje zo súboru JSON a nastavuje API koncové body pre interakciu s frontendom.
  - **Dockerfile:** Definuje obraz pre backend službu. Používa základný obraz Pythonu, inštaluje potrebné knižnice a spúšťa aplikáciu Flask.
  - **conversion_rates.json:** Obsahuje konverzné faktory medzi rôznymi jednotkami, ktoré backend používa na výpočty. Tento súbor sa načítava pri štarte aplikácie.

- **frontend/...**  
  - **Dockerfile:** Zostavuje frontendovú aplikáciu na základe obrazu Nginx.
  - **index.html, styles.css, script.js:** Poskytujú kompletnú štruktúru, štýl a funkcionalitu používateľského rozhrania aplikácie.

- **nginx/nginx.conf**  
  Konfiguruje server Nginx na poskytovanie statického obsahu frontendu a funguje ako proxy pre API požiadavky na backend.

## Spustenie, zastavenie a vyčistenie webovej aplikácie

1. **Príprava aplikácie:**

   Spustite prípravný skript na zostavenie Docker obrazov a nastavenie siete:
   ```bash
   python prepare-app.py
   ```
   or
   ```bash
   python3 prepare-app.py
   ```
   
2. **Spustenie aplikácie:**

   Spustite aplikáciu pomocou:
   ```bash
   python start-app.py
   ```
   or
   ```bash
   python3 start-app.py
   ```
   Po spustení sa aplikácia automaticky otvorí vo vašom predvolenom webovom prehliadači. Ak sa neotvorí automaticky, manuálne prejdite na: [http://localhost](http://localhost)

3. **Zastavenie a vyčistenie:**

   Ak chcete aplikáciu zastaviť, spustite:
   ```bash
   python end-app.py
   ```
   or
   ```bash
   python3 end-app.py
   ```
   Tento príkaz ukončí bežiace kontajnery, odstráni Docker sieť a vyčistí objemy a obrazy spojené s aplikáciou.

## Pred začatím práce. Riešenie problému docker-compose
Na vašom počítači musí byť nainštalovaný Docker a Python (odporúčaná je najnovšia verzia).

### Chyba s docker-compose:
#### Inštalácia docker-compose
Ak máte staršiu verziu Dockeru alebo docker-compose nie je nainštalovaný, skúste ho nainštalovať podľa nasledujúcich krokov:

#### Pre Linux
Stiahnite binárny súbor:
 ```bash
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
Udeľte oprávnenia na spustenie:
```bash
sudo chmod +x /usr/local/bin/docker-compose
```
Skontrolujte inštaláciu:
```bash
docker-compose --version
```

#### Pre macOS
Použite Homebrew:
```bash
brew install docker-compose
```

#### Pre Windows
Ak používate Docker Desktop, docker-compose by mal byť súčasťou balíka. Ak príkaz nefunguje, skúste preinštalovať Docker Desktop.
