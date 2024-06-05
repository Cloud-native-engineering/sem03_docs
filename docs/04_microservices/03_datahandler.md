---
layout: default
title: 4.3 Datahander Redirector
parent: 4. Microservices
nav_order: 3
---

# 4.3 Datahandler Redirector

Der Datahandler ist für die Verwaltung des Inhalts in DynamoDB zuständig. Er wird aktiviert, wenn er eine Nachricht von der SQS-Queue erhält und verarbeitet diese anschliessend. Dabei führt er verschiedene Operationen auf DynamoDB aus (Erstellen, Aktualisieren, Löschen).

## Features

- **Message Queue**: Der Datahandler erhält seine Aufgaben über die Nachrichtenwarteschlange und verarbeitet diese sequenziell.
- **DynamoDB**: Als persistenter Datenspeicher dient eine NoSQL-Datenbank. Ihre schnelle Leseleistung ist optimal für einen URL-Shortener.
- **Hochverfügbarkeit**: Der Datahandler bietet hohe Verfügbarkeit und skaliert automatisch entsprechend der Anforderungen.
- **Serverless**: Der Datahandler ist vollständig serverlos konzipiert. Dies bedeutet, dass Kosten nur dann anfallen, wenn tatsächlich eine Weiterleitung stattfindet.

## How to Deploy

Um die Lambda-Funktion zu deployen sind folgende Schritte notwendig:

1. **Erstellung der Lambda-Funktion**: Eine neue Lambda-Funktion wird über die AWS Management Console erstellt. Im Zuge dieses Prozesses wird eine IAM-Rolle hinzugefügt, die die erforderlichen Berechtigungen für die Verbindung mit DynamoDB besitzt.

2. **Hochladen des Codes**: Der Code aus dem Verzeichnis datahandler/ wird auf AWS hochgeladen.

3. **Konfiguration des Triggers**: Der Application Load Balancer wird als Trigger für die Lambda-Funktion konfiguriert. Hierfür wird in der Lambda-Konfiguration "+ Add trigger" ausgewählt und "Application Load Balancer" aus der Dropdown-Liste gewählt. Anschliessend wird der entsprechende Load Balancer ausgewählt.

## Sourcecode

Der Quellcode für den Datahandler ist öffentlich zugänglich und wird unter der [MIT-Lizenz](https://github.com/Cloud-native-engineering/myurl_redirector/blob/main/LICENSE) bereitgestellt. Diese Lizenz ermöglicht eine breite Nutzung und Anpassung des Codes.

- [GitHub - Sourcecode](https://github.com/Cloud-native-engineering/myurl_redirector)
