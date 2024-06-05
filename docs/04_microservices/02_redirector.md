---
layout: default
title: 4.2 Redirector
parent: 4. Microservices
nav_order: 2
---

# 4.2 Redirector

Der Redirector ist verantwortlich, um die Redirects durchzuführen. Auf Lambda Function basierend ist dieser Microsrvice komplett Serverless. Der Service wird die Anfragen von einem Application Loadbalancer bekommen. Als Backend verwendet der Microservice eine DynamoDB.

## Features

- **Sichere Weiterleitung**: Der Redirector prüft, ob die Ziel-Domain verifiziert ist. Bei einer verifizierten URL erfolgt eine direkte Weiterleitung des Benutzers zur Ziel-URL. Ist die URL nicht verifiziert, wird eine Informationsseite angezeigt, auf der der Benutzer die Weiterleitung manuell über einen Button fortsetzen kann.
- **Hochverfügbarkeit**: Der Redirector bietet hohe Verfügbarkeit und skaliert automatisch entsprechend der Anforderungen.
- **Serverless**: Der Redirector ist vollständig serverlos konzipiert. Dies bedeutet, dass Kosten nur dann anfallen, wenn tatsächlich eine Weiterleitung stattfindet.

## How to Deploy

Um die Lambda-Funktion zu deployen sind folgende Schritte notwendig:

1. **Erstellung der Lambda-Funktion**: Eine neue Lambda-Funktion wird über die AWS Management Console erstellt. Im Zuge dieses Prozesses wird eine IAM-Rolle hinzugefügt, die die erforderlichen Berechtigungen für die Verbindung mit DynamoDB besitzt.

2. **Hochladen des Codes**: Der Code aus dem Verzeichnis redirector/ wird auf AWS hochgeladen.

3. **Konfiguration des Triggers**: Der Application Load Balancer wird als Trigger für die Lambda-Funktion konfiguriert. Hierfür wird in der Lambda-Konfiguration "+ Add trigger" ausgewählt und "Application Load Balancer" aus der Dropdown-Liste gewählt. Anschliessend wird der entsprechende Load Balancer ausgewählt.

## Sourcecode

Der Quellcode für den Redirector ist öffentlich zugänglich und wird unter der [MIT-Lizenz](https://github.com/Cloud-native-engineering/myurl_redirector/blob/main/LICENSE) bereitgestellt. Diese Lizenz ermöglicht eine breite Nutzung und Anpassung des Codes.

- [GitHub - Sourcecode](https://github.com/Cloud-native-engineering/myurl_redirector)
