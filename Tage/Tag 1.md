# M141 – DB-Systeme in Betrieb nehmen

## Vergleich: MariaDB vs MySQL vs PostgreSQL

| Punkt | MariaDB | MySQL | PostgreSQL |
|---|---|---|---|
| Merkmale | Open-Source-Fork von MySQL, kompatibel mit MySQL | Sehr verbreitetes relationales DBMS von Oracle | Sehr mächtiges objektrelationales DBMS |
| Vorteile | Kostenlos, schnell, gute MySQL-Kompatibilität | Sehr verbreitet, viele Tutorials, gut für Webanwendungen | Sehr stabil, viele Funktionen, sehr gute SQL-Unterstützung |
| Nachteile | Nicht immer 100% gleich wie MySQL | Teilweise Oracle-abhängig, einige Enterprise-Funktionen kostenpflichtig | Etwas komplexer für Anfänger |
| Typische Anwendungen | Webseiten, kleinere bis mittlere Anwendungen, Open-Source-Projekte | Webseiten, Shops, CMS, Webhosting | Grosse Anwendungen, komplexe Daten, Business-Systeme |

## Andere DBMS-Modelle

| Datenbankmodell | Erklärung | Produkt | Vorteile | Nachteile | Typische Anwendungen |
|---|---|---|---|---|---|
| Document DB | Speichert Daten als Dokumente, oft JSON-ähnlich | MongoDB | Flexibles Schema, gut für moderne Apps | Nicht ideal für komplexe Joins | Webapps, APIs, Content-Systeme |
| Key-Value DB | Speichert Daten als Schlüssel-Wert-Paare | Redis | Sehr schnell, einfach | Wenig komplexe Abfragen | Cache, Sessions, Echtzeitdaten |
| Wide Column DB | Speichert Daten spaltenorientiert | Cassandra | Sehr skalierbar | Komplexer Betrieb | Big Data, grosse verteilte Systeme |
| Search DB | Optimiert für Volltextsuche | Elasticsearch | Sehr gute Suche | Nicht als Hauptdatenbank ideal | Suchfunktionen, Logs, Analyse |
| Graph DB | Speichert Knoten und Beziehungen | Neo4j | Sehr gut für Beziehungen | Spezialisiert, nicht für alles geeignet | Social Networks, Empfehlungen, Netzwerke |
| Time Series DB | Speichert zeitbasierte Messdaten | InfluxDB | Gut für viele Messwerte über Zeit | Spezialgebiet | Monitoring, Sensoren, Metriken |
| Spatial DB | Speichert geografische Daten | PostGIS | Gut für Karten und Standorte | Braucht GIS-Wissen | Karten, Navigation, Standortdaten |
