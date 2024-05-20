---
layout: default
title: 3.2 Funktionsweise des Microservices
parent: 3. Service Design
nav_order: 2
---

# 3.2 Funktionsweise des Microservices

Der URL-Shortener als Gesamtplattform wird in mehrere kleine Services aufgeteilt. Dazu werden folgende [Microservice-Designprinzipien](https://developers.redhat.com/articles/2022/01/11/5-design-principles-microservices#five_design_principles_for_microservices) angewendet:

- **Single Concern**: Ein Microservice sollte nur eine Funktion haben. Es soll sichergestellt sein, dass die Microservices locker gekoppelt sind.
- **Discrete**: Anders gesagt, ein Microservice muss gut gekapselt sein. So muss zum Beispiel jeder Microservice sein eigenes Git-Repository haben samt seinen CI/CD-Pipelines. Von der Entwicklung über Tests bis zur Freigabe ist jeder Microservice isoliert.
- **Transportable**: Ein Microservice soll mit geringem Aufwand in andere Runtimes verschoben werden können. Die optimale Form ist derzeit ein Container-Image.
- **Carries its own data**: Jeder Microservice sollte seine eigene Datenspeicherung haben. Datenspeicher sollen nicht über eine DB-Schnittstelle geteilt werden, sondern über eine Schnittstelle über den Microservice (API).
- **Inherently ephemeral**: Der Grundsatz, dass ein Microservice ephemeral ist, bedeutet, dass er einfach, schnell und ohne Nebenwirkungen auf einem Ziel erstellt, zerstört und bei Bedarf wieder ausgeführt werden kann. In der Regel wird erwartet, dass Microservices ständig kommen und gehen, manchmal aufgrund von Systemausfällen oder Skalierungsanforderungen.

## Microservices

Nach diesen Design Principles wurden folgende Microservices definiert:

![PLANTUML](https://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/Cloud-native-engineering/sem03_docs/dev/resources/artifacts/service_design.plantuml)

### Web-UI - Webfrontend

Das Webfrontend-Microservice wird in einem eigenen Container bereitgestellt. Dadurch kann das Frontend automatisch skaliert werden, um die Anforderungen einer wachsenden Nutzerzahl zu erfüllen, die kürzere URLs erstellen möchten. Alle Interaktionen erfolgen über das Backend-API.

### Backend API

Die Backend-API bildet eine zentrale Komponente des Systems. Sie ermöglicht das Schreiben von Daten in die Datenbank sowie die Speicherung aller Informationen zu den verkürzten URLs. Zusätzlich werden Updates der verkürzten URLs in eine Warteschlange geschrieben, damit der Redirector stets auf dem neuesten Stand ist. Die Backend-API übernimmt ausschliesslich administrative Aufgaben - keine Weiterleitungen erfolgen darüber!

### Redirector

Der Redirector bezieht die verkürzten URLs über die Message-Queue, von der er als Consumer fungiert. Er liest die Nachrichten und speichert sie in seiner eigenen leistungsstarken Key-Value-Datenbank. Dadurch ist der Redirector eigenständig und gewährleistet eine hohe Leistungsfähigkeit.

---

[1]: [RedHat - Design principles for microservices](https://developers.redhat.com/articles/2022/01/11/5-design-principles-microservices#five_design_principles_for_microservices)