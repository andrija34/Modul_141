# M141 – DB-Systeme in Betrieb nehmen (Tag 2)

## Einführung
In diesem Auftrag wurden verschiedene Arbeiten mit MariaDB/MySQL durchgeführt. Dabei wurden Konfigurationsdateien untersucht, Datenbanken erstellt, SQL-Befehle angewendet, CSV- und SQL-Dateien importiert sowie Zeichensätze und Kollationen getestet.

Zusätzlich wurden Tabellen angepasst, Daten importiert und ein Datenbank-Dump erstellt.

---

# 1. Untersuchung der my.ini / my.cnf Dateien

## Ziel
Untersuchen der Konfigurationsdateien von MariaDB/MySQL und herausfinden, welche Dateien geladen werden.

### mysqld --verbose --help
Folgender Befehl wurde in der CMD-Konsole ausgeführt:

```cmd
mysqld --verbose --help
```

**Beschreibung:** Mit diesem Befehl werden die Suchreihenfolge der Konfigurationsdateien, geladene Gruppen, Serveroptionen und aktive Einstellungen angezeigt.

### mysql --verbose --help
Zusätzlich wurde folgender Befehl ausgeführt:

```cmd
mysql --verbose --help
```

**Beschreibung:** Mit diesem Befehl werden die Konfigurationsinformationen des MySQL/MariaDB-Clients angezeigt.

### Gefundene Konfigurationsdateien
Folgende Dateien wurden untersucht:
- `C:\xampp\mysql\bin\my.ini`
- `C:\xampp\mysql\my.ini`
- `C:\xampp\mysql\data\my.ini`

### Wichtige Abschnitte der my.ini
| Abschnitt | Beschreibung |
| :--- | :--- |
| `[mysqld]` | Enthält Servereinstellungen |
| `[client]` | Enthält Clienteinstellungen |
| `[mysqldump]` | Enthält Einstellungen für Dumps und Backups |

---

# 2. Datenbank "kollation"

## Ziel
Testen verschiedener Kollationen und Zeichensätze.

### Datenbank-Setup
```sql
CREATE DATABASE kollation;
USE kollation;
```

### SQL-Datei importieren
Die Datei `kollation.sql` wurde über phpMyAdmin importiert:
1. Datenbank `kollation` auswählen.
2. Reiter **Importieren** öffnen.
3. Datei auswählen und Import starten.

---

# 3. Kollationen testen

## Ziel
Unterschiedliche Sortierungen und Zeichensätze testen.

### SQL-Befehle
```sql
SHOW COLLATION;
SELECT * FROM tbl_personen;
SELECT * FROM tbl_personen ORDER BY Name;
```

### Getestete Kollationen
- **utf8mb4_general_ci**: Ignoriert Gross-/Kleinschreibung, schnelle Standardsortierung.
- **utf8mb4_german2_ci**: Deutsche Telefonbuchsortierung (ä = ae, ö = oe, ü = ue).
- **utf8mb4_bin_cs**: Binäre Sortierung. Gross-/Kleinschreibung wird berücksichtigt (A != a).

---

# 4. SQL-Befehlsübersicht

| Tätigkeit | SQL-Befehl | Gruppe |
| :--- | :--- | :--- |
| Daten anzeigen | `SELECT` | DQL |
| Datenbank auswählen | `USE` | DDL |
| Datenbank erstellen | `CREATE DATABASE` | DDL |
| Tabelle erstellen | `CREATE TABLE` | DDL |
| Tabelle löschen | `DROP TABLE` | DDL |
| Struktur anzeigen | `DESCRIBE` | DQL |
| Datenbanken anzeigen | `SHOW DATABASES` | DQL |
| Tabellen anzeigen | `SHOW TABLES` | DQL |
| Daten einfügen | `INSERT` | DML |
| Daten ändern | `UPDATE` | DML |
| Daten löschen | `DELETE` | DML |
| Spalte löschen | `ALTER TABLE DROP COLUMN` | DDL |

---

# 5. Datenbank "Firma"

## Ziel
Erstellen einer relationalen Datenbankstruktur.

```sql
CREATE DATABASE Firma;
USE Firma;
```

### Tabellenerstellung (Beispiel)
Folgende Tabellen wurden angelegt: `tbl_Mitarbeiter`, `tbl_Abteilungen`, `tbl_Projekte`, `tbl_TT_Mitarbeiter_Projekte`.

```sql
CREATE TABLE tbl_Abteilungen (
    ID_Abteilung INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    AbtBezeichnung VARCHAR(30) NOT NULL
) ENGINE=InnoDB;
```

---

# 6. Datenimport & Manipulation

### CSV-Import via LOAD DATA INFILE
**Datei:** `Abteilungen.txt`
```sql
LOAD DATA INFILE 'C:/Pfad/Abteilungen.txt'
INTO TABLE tbl_Abteilungen
FIELDS TERMINATED BY ';';
```
*Getestet mit ANSI, UTF-8 und UTF-8 mit BOM zur Überprüfung der Umlaute.*

### Index & Engine anpassen
```sql
-- Index löschen
ALTER TABLE tbl_plz_ort DROP INDEX plz_ort_id;

-- Engine ändern
ALTER TABLE tbl_plz_ort ENGINE=InnoDB;

-- Tabelle erweitern
ALTER TABLE tbl_mitarbeiter ADD FS_Wohnort INT;
```

### Import via SOURCE
```sql
SOURCE C:/Pfad/tbl_mitarbeiter.sql;
```

---

# 7. Analyse & Tools

### Analysebefehle
```sql
DESCRIBE tbl_mitarbeiter;
SHOW CREATE TABLE tbl_mitarbeiter;
SELECT * FROM tbl_mitarbeiter PROCEDURE ANALYSE();
```

### Import via Konsole (mysqlimport)
```cmd
mysqlimport.exe db personen.txt -v -u root -p --fields-terminated-by=','
```

---

# 8. Datenbank-Backup (Dump)

## Ziel
Erstellen eines vollständigen Backups der Datenbank "Firma".

```cmd
mysqldump.exe -u root -p --add-drop-table Firma > firma.sql
```

**Inhalt des Dumps:**
- `DROP TABLE IF EXISTS` Anweisungen
- `CREATE TABLE` Befehle
- Alle Datensätze (INSERTs)
- Komplette Tabellenstruktur

---

# Fazit
In diesem Modul wurden die Grundlagen der MariaDB/MySQL-Administration vertieft. Schwerpunkte waren die Konfiguration, verschiedene Import-Techniken, die Handhabung von Zeichensätzen sowie die Sicherung von Datenbeständen.