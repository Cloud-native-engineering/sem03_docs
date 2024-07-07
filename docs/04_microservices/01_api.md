---
layout: default
title: 4.1 Backend API
parent: 4. Microservices
nav_order: 1
---

# 4.1 Backend API

Die Backend-API bildet das Herzstück des MyURL Services und ermöglicht die Verwaltung von URLs. Als Lösung für die Autorisierung wirdAuth0 eingesetzt.

## Features

Dieser Service bietet eine Reihe von Funktionen und Vorteilen, die speziell darauf ausgerichtet sind, die Benutzererfahrung zu verbessern und die Sicherheit zu gewährleisten.

- **Erweiterte Datenschutzfunktionen**: Unser Service legt grossen Wert auf den Schutz der Privatsphäre. Daher werden keine personenbezogenen Daten verwendet oder gespeichert. Der einzige Datenpunkt, der gespeichert wird, ist ein automatisch generierter Benutzername, der zum Teilen von Kurz-URLs verwendet werden kann. Dieser Benutzername kann jedoch jederzeit vom Benutzer geändert werden.
- **URL-Teilen**: Mit dem automatisch generierten Benutzernamen können Kurz-URLs problemlos geteilt werden. Dies ermöglicht es mehreren Personen, dieselben URLs zu verwalten und zu verwenden.
- **Sicherheit**: Unser Service bietet die Möglichkeit, spezifische Domains und Kurz-Codes zu sperren, als Premium zu kennzeichnen oder als verifiziert zu markieren. Dies trägt zur Sicherheit bei, indem sichergestellt wird, dass die Benutzer des Dienstes nur auf verifizierte Endpunkte zugreifen. Dies minimiert das Risiko, auf unsichere oder schädliche Websites weitergeleitet zu werden.

## CI/CD

Der CI/CD-Prozess ist darauf ausgelegt, die Qualität und Zuverlässigkeit der Software zu gewährleisten. Er besteht aus zwei Hauptphasen: Testen und Bauen von Container-Images.

- **Unit Test Cases**: In dieser Phase wird der Code gründlich getestet, um sicherzustellen, dass er wie erwartet funktioniert und keine Fehler enthält. Wir verwenden automatisierte Tests, um eine breite Abdeckung und Konsistenz zu gewährleisten. Jede Änderung am Code löst diese Tests aus, um sicherzustellen, dass die Änderungen keine bestehenden Funktionen beeinträchtigen.
- **Build & Deploy**: Nach dem der Code getestet wurde und er auf einem DEV, oder MAIN Branch mit einem Merge-Request gelandet ist, wird diese Pipeline ausgeführt. Wenn diese Pipeline im DEV-Branch ausgeführt wird, wird ein Container-Image mit dem Tag dev gebaut und im Main wird die version als latest gekennzeichnet. Wenn eine Version gebaut werden soll, so kann ein GIT-TAG auf den Main gesetzt werden. Somit wird eine das Image in einer Version publiziert.

## Testcases

Das Backend-API wird mit pytest getestet. Die Tests werden von der Pipeline automatisch ausgeführt und in der Python Version 3.10, 3.11, 3.12 getestet. Somit wird sichergestellt, dass das Backend mit mehreren Python Versionen kompatibel ist.

Die Test sind im SCM-Repo im folder 'test' ersichtlich.

### Services MOCK

In den Testfällen werden die externen Systeme, wie Auth0 und die SQS-Queue, nicht direkt getestet. Stattdessen werden diese Systeme durch Mock-Services simuliert, um die Interaktionen mit ihnen zu testen. Dies ermöglicht es, eine vorgetäuschte Antwort zu liefern oder einen Parameter von der Test-Engine zu übergeben, ohne die tatsächlichen Systeme zu beeinflussen.

- **Auth0 / JWKS**: Auth0 veröffentlicht die öffentlichen Zertifikate, mit denen die JWT-Tokens signiert wurden, über den JWKS-Endpunkt. Das Backend-API muss auf diese Zertifikate zugreifen, um die Signatur zu überprüfen. In den Testfällen wird jedoch ein Secret-Key der Anwendung direkt übergeben, anstatt dass das Backend-API auf den JWKS-Endpunkt zugreift.
- **SQS-Queue**: Um die Funktionalität der SQS-Queue nicht direkt testen zu müssen, wird ein Mock-Service verwendet. Anstatt dass eine Python-Funktion einen Aufruf an die SQS-Queue sendet, wird einfach eine vorgetäuschte Antwort ausgegeben. Dies ermöglicht es, die Interaktion mit der SQS-Queue zu testen, ohne die tatsächliche Queue zu beeinflussen.

## How to Deploy

Der Prozess für das initial Deployment ist im Git-Repo beschrieben. Es müssen ein paar spezifische ENv-Variablen gesetzt werden, um den Service zu konfigurieren.

Für ein Update des Services ist die Erstellung eines neuen Container-Images erforderlich. Dies kann erreicht werden, indem ein Versions-Tag auf dem Main-Branch des Git-Repositorys gesetzt wird. Anschliessend wird die CI/CD-Pipeline automatisch eine neue Version erstellen und diese in den GitHub Packages veröffentlichen.

Der letzte Schritt im Update-Prozess ist die Durchführung eines Blue/Green Deployments auf dem ECS-Cluster. Während dieses Deployments wird der Cluster zunächst die neue Version starten und anschliessend das Backend des Load Balancers umschalten. Dieser Prozess gewährleistet eine nahtlose Aktualisierung des Services mit minimaler/keiner Ausfallzeit.

## Sourcecode

Der Quellcode für das Backend-API ist öffentlich zugänglich und wird unter der [MIT-Lizenz](https://github.com/Cloud-native-engineering/myurl_api/blob/main/LICENSE) bereitgestellt. Diese Lizenz ermöglicht eine breite Nutzung und Anpassung des Codes.

- [GitHub - Sourcecode](https://github.com/Cloud-native-engineering/myurl_api)
