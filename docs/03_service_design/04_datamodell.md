---
layout: default
title: 3.4 Datenmodell
parent: 3. Service Design
nav_order: 4
---

# 3.4 Datenmodell

Damit die Daten effizient und strukturiert gespeichert werden können, muss ein geeignetes Datenmodell gewählt werden. Es gibt verschiedene Datenmodelle, welche angewendet werden können und jedes hat seine eigenen Vor- und Nachteile.

## Persistent Storage

### MySQL

MySQL ist eine weit verbreitete relationale Datenbank, die SQL (Structured Query Language) für die Datenmanipulation verwendet. Sie ist ideal für Anwendungen, die komplexe Transaktionen erfordern und bei denen Beziehungen zwischen den Tabellen bestehen. Bei einer SQL-Datenbank ist die Struktur sehr strikt.

![PLANTUML](https://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/Cloud-native-engineering/sem03_docs/dev/resources/artifacts/sql_example.plantuml)

### NoSQL

NoSQL-Datenbanken sind ideal für Anwendungen, die grosse Mengen an Daten speichern und eine flexible Datenstruktur benötigen. Sie sind in der Regel einfacher zu skalieren und schneller als relationale Datenbanken.

```json
{
    "first_name": "Paul",
    "last_name": "Mustermann",
    "city": "zuerich"
    "hobbies": ["football", "swimming", "reading"]
    "cars": [
        {
            "manufacturer": "Ferrari"
            "year": 2011
            "value": 250000
            "state": "active"
        },
        {
            "manufacturer": "Opel"
            "year": 2024
            "value": 20000
            "state": "active"
        }
    ]
}
```

### KeyValueDB

KeyValue-Datenbanken sind eine Art von NoSQL-Datenbank, die Daten als Schlüssel-Wert-Paare speichert. Sie sind ideal für Anwendungen, die schnelle Lese- und Schreibvorgänge erfordern.

## Entscheidungsmatrix

Es können folgende Punkte von 1 bis 5 verteilt werden, wobei 5 die beste Bewertung darstellt. Die Bewertung ist basierend auf den Service eines URL-Shorteners abgestimmt.

| **Kriterium**      | **Relationale Datenbanken (SQL)** | **NoSQL**  | **KeyValueStore** |
| ------------------ | --------------------------------- | ---------- | ----------------- |
| **Performance**    | \*\*                              | \*\*\*     | \*\*\*\*\*        |
| **Skalierbarkeit** | \*\*\*                            | \*\*\*\*   | \*\*\*\*\*        |
| **Flexibilität**   | \*                                | \*\*\*\*\* | \*\*\*            |
| **Komplexität**    | \*\*\*\*\*                        | \*\*\*     | \*\*\*\*          |
| **GESAMTKOSTEN**   | 11                                | 15         | 17                |

Die Auswahl eines Datenbank-Management-Systems ist eine komplexe Aufgabe, da jedes System seine eigenen Stärken und Schwächen hat. In dieser Semesterarbeit wird kein spezifisches Datenbank-System festgelegt. Gemäss der Definition eines Microservice sollte jeder Service seinen eigenen Datenspeicher besitzen und die Kommunikation sollte hauptsächlich über Schnittstellen oder eine Messaging-Schicht erfolgen.

Der Redirect-Service wird eine Key-Value-Datenbank nutzen. Der Hauptgrund dafür ist die hohe Geschwindigkeit, die ein Key-Value-Store bietet, was für einen Redirect-Service äusserst vorteilhaft ist.

Der Management-Layer für URLs wird in einer SQL-Datenbank implementiert. Der zentrale Aspekt hierbei ist die Gewährleistung der Integrität, da ein Short-Code für eine URL eindeutig sein muss und nur einmal existieren darf.

## Datenbank Schema

Das Datenbankschema ist eine visuelle Darstellung der Datenbankstruktur. Es zeigt die Tabellen, die Beziehungen zwischen ihnen und die Art der Daten, die in jeder Tabelle gespeichert werden.

![PLANTUML](https://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/Cloud-native-engineering/sem03_docs/dev/resources/artifacts/sql_schema.plantuml)

Das Datenbank Schema zeigt wie sehr gut Auf, welche Daten gespeichert werden. Das Schema besteht aus vier Entitäten: User, ShortUrl, UserShortUrl und RestrictedUrl.

**User**: Diese Tabelle speichert Informationen über die Benutzer. Jeder Benutzer hat eine eindeutige user_id, die als Primärschlüssel dient. Weitere Felder sind auth0_id, first_name, last_name und enabled, die den Authentifizierungs-ID, den Vornamen, den Nachnamen und den Status des Benutzers speichern.

**ShortUrl**: Diese Tabelle speichert die kurzen URLs. Jede kurze URL hat eine eindeutige url_id, die als Primärschlüssel dient. Weitere Felder sind short_code, original_url, creation_date, expiration_date, enabled und verified, die den Kurzcode, die Original-URL, das Erstellungsdatum, das Ablaufdatum, den Status und den Verifizierungsstatus der kurzen URL speichern.

**UserShortUrl**: Diese Tabelle ist eine Zwischentabelle zwischen User und ShortUrl. Der Grund für diese Tabelle ist, dass User für shorturl zugewiesen werden können. In der Zukunft könnte zum Beispiel eine short-URL geteilt werden mit mehreren Usern. Sie hat eine eindeutige user_url_id, die als Primärschlüssel dient. Weitere Felder sind user_id, url_id und description, die die Benutzer-ID, die URL-ID und eine Beschreibung speichern.

**RestrictedUrl**: Diese Tabelle speichert Informationen über eingeschränkte URLs. Es ist somit möglich ShortCodes oder Domains zu Blockieren oder als Premium zuzuweisen. Jede eingeschränkte URL hat eine eindeutige restricted_url_id, die als Primärschlüssel dient. Weitere Felder sind short_code, domain, is_premium und is_blocked, die den Kurzcode, die Domain, den Premium-Status und den Blockierungsstatus der eingeschränkten URL speichern.
