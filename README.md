# PostgreSQL – Kom igång lokalt

## Innehåll
1. [Installera PostgreSQL](#1-installera-postgresql)
2. [Skapa databasen](#2-skapa-databasen)
3. [Installera & starta pgweb](#3-installera--starta-pgweb)
4. [Konfigurera .env-filen](#4-konfigurera-env-filen)

---

## 1. Installera PostgreSQL 🗂️

### Mac

**Alternativ 1 – Homebrew (rekommenderat)**
```bash
brew install postgresql@17
brew services start postgresql@17   # Starta
brew services stop postgresql@17    # Stoppa
```

**Alternativ 2 – Postgres.app**
1. Ladda ner [Postgres.app](https://postgresapp.com/)
2. Dra appen till Applications
3. Starta appen och klicka **Initialize**

---

### Windows
1. Ladda ner installern från [postgresql.org](https://www.postgresql.org/download/windows/)
2. Kör installern:
   - Välj **PostgreSQL 17**
   - Behåll standardport **5432**
   - Ange ett lösenord för `postgres` – **kom ihåg det!**
   - Kryssa i **pgAdmin 4** om du vill ha ett grafiskt verktyg
3. Slutför installationen – PostgreSQL startar automatiskt som en Windows-tjänst

---

### Linux (Ubuntu/Debian)
```bash
sudo apt update && sudo apt install -y postgresql postgresql-contrib
sudo systemctl status postgresql   # Verifiera att tjänsten är igång
```

---

## 2. Skapa databasen ✚

### Mac
```bash
createdb mydb
```

### Windows
Öppna **SQL Shell (psql)** från startmenyn, logga in och kör:
```sql
CREATE DATABASE mydb;
\q
```

### Linux
```bash
sudo -u postgres createdb mydb
sudo -u postgres psql -c "ALTER USER postgres PASSWORD 'postgres';"
```

### Verifiera anslutningen

| Platform | Kommando |
|---|---|
| Mac | `psql -d mydb` |
| Windows / Linux | `psql -h localhost -U postgres -d mydb` |

Ange lösenordet när du blir ombedd. Lyckas du komma in i psql-prompten fungerar allt. Skriv `\q` för att avsluta.

---

## 3. Installera & starta pgweb 🌐

pgweb är ett enkelt webbgränssnitt för PostgreSQL som körs direkt i webbläsaren.

### Installation

**Mac**
```bash
brew install pgweb
```

**Windows** – Ladda ner senaste `.exe` från [pgweb releases](https://github.com/sosedoff/pgweb/releases)

**Linux**
```bash
wget https://github.com/sosedoff/pgweb/releases/latest/download/pgweb_linux_amd64.zip
unzip pgweb_linux_amd64.zip
sudo mv pgweb_linux_amd64 /usr/local/bin/pgweb
```

### Starta pgweb

**Mac** (inget lösenord):
```bash
pgweb --url postgresql://localhost:5432/mydb
```

**Windows / Linux** (med lösenord):
```bash
pgweb --url postgresql://postgres:ditt_lösenord@localhost:5432/mydb
```

Öppna sedan → [http://localhost:8081](http://localhost:8081)

---

## 4. Konfigurera .env-filen 🧑🏾‍💻

Skapa eller uppdatera `.env` i projektroten:

**Mac** (inget lösenord som standard):
```env
DATABASE_URL=postgresql://localhost:5432/mydb
PORT=3000
```

**Windows**:
```env
DATABASE_URL=postgresql://postgres:ditt_lösenord@localhost:5432/mydb
PORT=3000
```

**Linux**:
```env
DATABASE_URL=postgresql://postgres:postgres@localhost:5432/mydb
PORT=3000
```
