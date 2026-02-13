# Installera PostgreSQL lokalt

## Mac

### Alternativ 1 - Homebrew (rekommenderat)

```bash
brew install postgresql@17
```

Starta PostgreSQL:

```bash
brew services start postgresql@17
```

Stoppa PostgreSQL:

```bash
brew services stop postgresql@17
```

### Alternativ 2 - Postgres.app

1. Ladda ner [Postgres.app](https://postgresapp.com/)
2. Dra appen till Applications
3. Starta appen - klicka "Initialize" för att skapa en server

## Windows

1. Ladda ner installern från [postgresql.org/download/windows](https://www.postgresql.org/download/windows/)
2. Kör installern och följ stegen:
   - Välj senaste versionen (PostgreSQL 17)
   - Behåll standardport **5432**
   - Ange ett lösenord för användaren `postgres` (kom ihåg det!)
   - Kryssa i **pgAdmin 4** om du vill ha ett grafiskt verktyg
3. Klicka "Next" genom resten och avsluta installationen

PostgreSQL startar automatiskt som en Windows-tjänst.

## Linux (Ubuntu/Debian)

```bash
sudo apt update
sudo apt install -y postgresql postgresql-contrib
```

PostgreSQL startar automatiskt. Verifiera:

```bash
sudo systemctl status postgresql
```

## Skapa databasen

Efter installationen behöver du skapa databasen `mydb`.

### Mac (Homebrew / Postgres.app)

```bash
createdb mydb
```

### Windows

Öppna **SQL Shell (psql)** från startmenyn. Logga in med lösenordet du valde under installationen och kör:

```sql
CREATE DATABASE mydb;
```

Skriv `\q` för att avsluta.

### Linux

```bash
sudo -u postgres createdb mydb
```

På Linux behöver du också skapa ett lösenord för postgres-användaren:

```bash
sudo -u postgres psql -c "ALTER USER postgres PASSWORD 'postgres';"
```

## Verifiera

Testa att ansluta till databasen:

**Mac:**

```bash
psql -d mydb
```

**Windows/Linux:**

```bash
psql -h localhost -U postgres -d mydb
```

Ange lösenordet när du blir ombedd. Om du kommer in i psql-prompten fungerar allt. Skriv `\q` för att avsluta.

## pgweb - Grafiskt webbgränssnitt

pgweb är ett enkelt webbgränssnitt för PostgreSQL som körs i webbläsaren.

### Mac

```bash
brew install pgweb
```

### Windows

Ladda ner senaste `.exe` från [github.com/sosedoff/pgweb/releases](https://github.com/sosedoff/pgweb/releases).

### Linux

Ladda ner senaste binären från [github.com/sosedoff/pgweb/releases](https://github.com/sosedoff/pgweb/releases):

```bash
# Ladda ner (byt version om det finns en nyare)
wget https://github.com/sosedoff/pgweb/releases/latest/download/pgweb_linux_amd64.zip
unzip pgweb_linux_amd64.zip
sudo mv pgweb_linux_amd64 /usr/local/bin/pgweb
```

### Starta pgweb

**Mac** (inget lösenord):

```bash
pgweb --url postgresql://localhost:5432/mydb
```

**Windows/Linux** (med lösenord):

```bash
pgweb --url postgresql://postgres:ditt_lösenord@localhost:5432/mydb
```

Öppna sedan [http://localhost:8081](http://localhost:8081) i webbläsaren.

## Uppdatera .env

Se till att `.env` i projektet matchar din installation:

**Mac** (inget lösenord krävs som standard):

```
DATABASE_URL=postgresql://localhost:5432/mydb
PORT=3000
```

**Windows** (du valde lösenord under installationen):

```
DATABASE_URL=postgresql://postgres:ditt_lösenord@localhost:5432/mydb
PORT=3000
```

**Linux** (efter att du satt lösenord enligt stegen ovan):

```
DATABASE_URL=postgresql://postgres:postgres@localhost:5432/mydb
PORT=3000
```
