---
layout: default
title: 3.8 Servicekosten
parent: 3. Service Design
nav_order: 8
---

# 3.8 Servicekosten

In diesem Abschnitt werden die Kosten analysiert, die mit dem Betrieb des URL-Shortener in einer produktiven Umgebung verbunden sind. Während der Entwicklungsphase wird der Service im AWS Student-Lab gehostet und aufgebaut.

## Rahmenbedingungen

Folgende Bedingungen sollte die Plattform erlauben pro Monat:

- 50.000 Weiterleitungen (Redirects)
- Hohe Verfügbarkeit (High Availability)

## Analyse

Basierend auf den oben genannten Anforderungen wurde eine detaillierte Kostenanalyse durchgeführt. Sie können die vollständige Analyse unter folgendem Link einsehen:

- [AWS Cost Calculation - MyURL](../../resources/artifacts/MyURL-cost-calculation.pdf)

Die untenstehende Tabelle gibt einen Überblick über die erwarteten Kosten:

| **Monatlich** | **Jährlich** |
| ------------- | ------------ |
| 98.35 USD     | 1180.20 USD  |

Die Kostenanalyse zeigt deutlich die drei Hauptkostenpunkte: den Loadbalancer, die Container-Runtime und die relationale Datenbank, die für die Verwaltung benötigt wird. Diese Kosten können nicht reduziert werden, da eine der Bedingungen die hohe Verfügbarkeit des Services ist. Bei der Datenbank sind die Kosten doppelt so hoch, als wenn sie in einer einzigen Zone betrieben wird. In Bezug auf die Kosten gibt es sonst wenig zu diskutieren. Die jährlichen Kosten von etwa 1200 USD für 50.000 Weiterleitungen sind gerechtfertigt und nicht übermässig hoch. Das Hosting dieser Architektur ist somit sehr optimal und wirtschaftlich.

## FinOps Optimierung

Um die Kosten weiter zu reduzieren, könnte eine Auto-Scaling-Funktion implementiert werden. Beispielsweise könnten der SPA und die API nachts heruntergefahren oder sogar vollständig gestoppt werden. Da der SPA und die API hauptsächlich für die Verwaltung von URLs verantwortlich sind und die Umleitung serverlos mit Lambda-Funktionen durchgeführt wird, könnte der administrative Teil des Dienstes nur während der Geschäftszeiten bereitgestellt werden. Wenn wir grosszügig hochrechnen und von 10 Betriebsstunden pro Tag ausgehen, könnten wir bereits eine Kosteneinsparung von etwa 60% für den ECS-Dienst erzielen.
