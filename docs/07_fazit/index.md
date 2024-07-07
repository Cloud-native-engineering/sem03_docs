---
layout: default
title: 7. Fazit und Zusammenfassung
nav_order: 7
---

# 7. Fazit und Zusammenfassung

Im Rahmen meiner Semesterarbeit konzentrierte ich mich auf die Entwicklung eines URL-Shorteners, wobei besonderes Augenmerk auf Sicherheit und Datenschutz gelegt wurde. Das Ziel war die Erstellung einer modernen Microservice-Architektur, für die ein geeigneter Cloud-Provider ausgewählt wurde. Zudem war die Auswahl eines optimalen Ansatzes zur Datenverarbeitung erforderlich, was die Evaluation verschiedener Datenbanken einschloss. Ein Hauptaugenmerk lag auf der Gewährleistung der Sicherheit des Services und der Daten.

Die Planung meiner Arbeit erfolgte mittels der Jira Software von Atlassian als SaaS-Lösung. Das Projekt wurde in drei agilen Sprints organisiert: Der erste Sprint fokussierte sich auf intensive Recherche und die Erarbeitung von Grundlagen, insbesondere die Erstellung eines Service-Designs. Im zweiten Sprint entstand das Minimum Viable Product (MVP), einschliesslich der Bereitstellung der Cloudinfrastruktur und der Entwicklung der Microservices. Der letzte Sprint diente der Verbesserung des MVPs und dem Abschluss der Semesterarbeit. Ein weiterer wichtiger Aspekt des Projektmanagements war das aktive Risikomanagement, das ebenfalls in Jira abgebildet wurde, ergänzt durch einen neuen Issue-Typ und ein Plugin.

Das Service-Design wurde erfolgreich entworfen und dokumentiert. Die Microservice-Architektur umfasste zahlreiche Services und Produkte. Definiert wurden das API, die Web-App, der Datahandler und der Redirector, deren Aufteilung entscheidend für Skalierung und Hochverfügbarkeit war. Besonders viel Zeit floss in die Entwicklung des APIs, eine Investition, die sich durch die nahtlose Integration in die SPA ohne Anpassungsbedarf auszahlte.

Die Präsentation war gut durchdacht und folgte einem klaren roten Faden. Der Fokus lag auf der Problemlösung durch MyURL und dessen Features, ohne zu tief in technische Details einzutauchen. Eine kurze Einführung in die Architektur und eine Demo von MyURL rundeten die Präsentation ab.

Rückblickend stellte die Komplexität der Semesterarbeit eine Herausforderung dar, jedoch hätte eine Änderung der Architektur den grundlegenden Zielen des Service-Designs nicht entsprochen. Es besteht das Potenzial für Erweiterungen, wie die Implementierung eines Admin-Interfaces für die SPA oder die Optimierung des UI/UX-Designs. Wie bei jedem Projekt traten auch hier einige Stolpersteine und Herausforderungen auf, insbesondere beim Schreiben von Testfällen für das API. Mein Ziel war es, externe Services in den Tests nicht direkt anzusprechen, um ausschliesslich die Funktionalität des APIs zu überprüfen, nicht die der externen Dienste. Daher war es notwendig, das Test-Setup so anzupassen, dass Service-Mocks verwendet werden. Eine besondere Herausforderung stellte dabei der Mock für Auth0 dar. Hier musste ich dem API beim Start den öffentlichen Teil eines Zertifikats übergeben, um die Signatur der Tokens verifizieren zu können. Beim Mocking des SQS traten hingegen keine grösseren Probleme auf, und seine Implementierung erfolgte zügig.

Trotz der Überschreitung des zeitlichen Rahmens der Semesterarbeit, waren die gewonnenen Erkenntnisse und Erfahrungen in der Praxis von unschätzbarem Wert. Sie umfassten technisches Know-how im Umgang mit Cloud-Diensten, die Funktionsweise von Single-Page-Applikationen und APIs sowie verbessertes Projektmanagement und adaptive Problemlösungskompetenzen.
