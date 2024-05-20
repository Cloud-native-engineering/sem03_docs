---
layout: default
title: 3.7 Security und Datenschutz
parent: 3. Service Design
nav_order: 7
---

# 3.7 Security und Datenschutz

Dieser Abschnitt soll genauer erläutern, welche Daten der URL-Shortener verarbeitet, speichert und Auswertet. Eine Speicherung von Daten hat immer  einen Einfluss auf den Datenschutz. Um Klarheit zu schaffen werden diese Punkte in folgendem Dokument genauer beschrieben.

## Sicherheit

Grundsätzlich ist eine Authentifizierung erforderlich, wo immer sie notwendig ist, mit Ausnahme des Redirect-Services. Dieser Service bietet keine eigene API oder Schnittstelle an und hat eine separate Datenbank, wodurch er keinen Zugriff auf die administrative Datenbank und Daten hat.

Unsere Single Page Application & API verwendet mehrere Sicherheitsmassnahmen, um die Daten und Informationen unserer Benutzer zu schützen:

1. **Authentifizierung**: Jeder API-Aufruf muss authentifiziert werden. Benutzer müssen einen gültigen API-Schlüssel generieren und diesen bei jedem Aufruf mitsenden.

2. **Verschlüsselung**: Alle Daten, die über unsere API gesendet und empfangen werden, sind SSL-verschlüsselt. Dies stellt sicher, dass die Daten während der Übertragung nicht abgefangen oder manipuliert werden können.

3. **Rate Limiting**: Um Missbrauch zu verhindern und die Qualität unserer Dienstleistung zu gewährleisten, kann eine Begrenzung der Anzahl der API-Anfragen, die ein Benutzer innerhalb eines bestimmten Zeitraums senden kann, eingeführt werden.

### Sicherere Weiterleitung

Der URL-Shortener bietet eine sichere Weiterleitungsfunktion, um die Benutzer vor potenziellen Online-Bedrohungen wie Phishing und Datendiebstahl zu schützen. Diese Funktion stellt sicher, dass Benutzer nicht auf unsichere oder unzuverlässige Websites weitergeleitet werden.

Um dies zu erreichen, wird auf eine manuelle Verifikation gesetzt. Dieser Prozess beinhaltet die Überprüfung und Validierung von URLs, die bekannte Marken oder Unternehmen repräsentieren. Es ist wichtig zu beachten, dass wir uns auf die Überprüfung auf Ebene des Domainnamens konzentrieren. Das bedeutet, dass wir die Authentizität und Sicherheit der Domain überprüfen, um sicherzustellen, dass sie von einer vertrauenswürdigen Quelle stammt.

Durch diese Massnahme können wir ein zusätzliches Mass an Sicherheit bieten und dazu beitragen, das Risiko von Online-Bedrohungen für die Benutzer unseres Dienstes zu minimieren.

![PLANTUML](https://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/Cloud-native-engineering/sem03_docs/dev/resources/artifacts/safe_redirect.plantuml)

### Anmeldung

Für die Anmeldung bei unserem URL-Shortener-Dienst nutzen wir den Auth0-Service von Okta. Auth0 ist eine flexible, drop-in Lösung zur Verwaltung von Authentifizierungen und Autorisierungen. Es ermöglicht den Benutzern, sich sicher anzumelden und zu registrieren, und bietet gleichzeitig den Entwicklern eine einfache und sichere Methode zur Integration von Anmeldediensten.

Die Verwendung von Auth0 bietet mehrere Vorteile. Erstens verbessert es die Sicherheit, da Auth0 strenge Sicherheitsprotokolle und -standards einhält. Zweitens verbessert es die Benutzererfahrung, da Auth0 eine nahtlose Anmeldung und Registrierung ermöglicht. Drittens erleichtert es den Entwicklern die Arbeit, da sie sich nicht um die Implementierung und Wartung von Anmeldesystemen kümmern müssen.

Wenn sich ein Benutzer anmeldet, wird er auf die Auth0-Anmeldeseite weitergeleitet. Dort kann er seine Anmeldedaten eingeben oder sich über einen sozialen Login anmelden. Nach erfolgreicher Anmeldung wird der Benutzer zurück zu unserem Dienst geleitet und ist nun eingeloggt und bereit, unseren URL-Shortener-Dienst zu nutzen.

Durch die Verwendung von Auth0 können wir sicherstellen, dass die Anmeldedaten unserer Benutzer sicher und geschützt sind und dass die Anmeldung so einfach und nahtlos wie möglich ist.

## Datenschutz

### Welche Daten werden gespeichert

Unser URL-Shortener-Dienst erfasst und speichert folgende Daten:

- Benutzername
- Original-URL und Kurz-URL
- Minimale statistische Daten wie Klickanzahl und letzter Klick

Diese Daten werden nur erfasst und verarbeitet, um unseren URL-Shortener-Dienst bereitzustellen und zu verbessern.

### Datenübertragung und -kommunikation

Ihre Daten werden ohne Ihre ausdrückliche Zustimmung nicht an Dritte weitergegeben.

### Ihre Rechte

Sie haben das Recht, jederzeit Auskunft über Ihre bei uns gespeicherten personenbezogenen Daten zu erhalten. Sie haben ausserdem das Recht auf Berichtigung, Sperrung oder, abgesehen von der vorgeschriebenen Datenspeicherung zur Geschäftsabwicklung, Löschung Ihrer personenbezogenen Daten.

### Änderungen dieser Datenschutzrichtlinie

Wir behalten uns das Recht vor, diese Datenschutzrichtlinie jederzeit mit Wirkung für die Zukunft zu ändern. Eine jeweils aktuelle Version ist online einsehbar. Bitte suchen Sie die Website regelmässig auf und informieren Sie sich über die geltende Datenschutzrichtlinie.
