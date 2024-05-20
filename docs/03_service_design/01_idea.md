---
layout: default
title: 3.1 Anforderungen
parent: 3. Service Design
nav_order: 1
---

# 3.1 Anforderungen

Die Grundidee eines URL-Shorteners besteht darin, lange URLs in kompakte, leicht zu merkende Varianten umzuwandeln. Dies ist besonders hilfreich für die Weitergabe von Links, da die Länge der URL eine Rolle spielt.

Dabei sind folgende Aspekte zu beachten:

- **Microservices**: Die Lösung für den URL-Kürzer sollte auf Microservices basieren. Diese Teilservices sollen logisch voneinander getrennt sein, um eine lose Kopplung zu gewährleisten.
- **Skalierbarkeit & Leistung**: Es ist wichtig, sicherzustellen, dass die gesamte Plattform skalierbar ist und eine hohe Leistung bietet, um den Anforderungen gerecht zu werden.
- **Sicherheit**: Die Plattform sollte ein modernes Sicherheitskonzept implementieren, um sicherzustellen, dass jede Änderung nachvollziehbar ist und die Daten geschützt sind.
- **Public Cloud**: Der URL-Shortener wird in der Cloud betrieben.
