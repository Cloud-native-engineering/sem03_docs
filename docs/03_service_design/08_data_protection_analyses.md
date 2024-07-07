---
layout: default
title: 3.8 Schutzbedarfsanalyse
parent: 3. Service Design
nav_order: 8
---

# 3.8 Schutzbedarfsanalyse

Der MyURL-Service ist ein URL-Shortener, der als Microservice entwickelt wurde. Er verwendet Auth0 als Identity Provider (IDP), Amazon Elastic Container Service (ECS), Simple Queue Service (SQS), Lambda-Funktionen, DynamoDB und RDS PostgreSQL. Die Schutzbedarfsanalyse für diesen Service umfasst die folgenden Aspekte:

![Security](../../resources/images/security.png)

## Welche Daten verarbeitet MyURL

Im nachfolgenden Abschnitt werden die verarbeiteten Daten detailliert beschrieben und entsprechend ihrer Sensibilität klassifiziert.

### MyURL

MyURL bildet das Kernstück des gleichnamigen Services und umfasst die gesamte Cloud-Infrastruktur, die auf AWS basiert. MyURL selbst hat keinen Zugriff auf personenbezogene Daten. Es verwendet lediglich die "sub" (Subject Identifier) aus dem JWT von Auth0, um Daten anzeigen und einem Benutzer zuordnen zu können. Der auf MyURL verwendete Benutzername wird automatisch generiert und entspricht nicht dem Auth0-Benutzernamen. Diese Entscheidung wurde aus Datenschutzgründen getroffen. Benutzer haben jedoch die Möglichkeit, ihren Benutzernamen selbst anzupassen. Darüber hinaus verarbeitet MyURL keine personenbezogenen Daten.

### Auth0

Auth0 ist für die Anmelde-Logik verantwortlich und ermöglicht die Konfiguration einer rollenbasierten Zugriffskontrolle (RBAC). Es unterstützt auch die Verwendung von Social Logins (Anmeldung mit GitHub, Microsoft-Konto etc.). Dieser Dienst speichert personenbezogene Daten, um die Anmeldung zu ermöglichen. Dazu gehören Daten wie E-Mail-Adresse, Auth0-Benutzername und Passwort sowie Informationen zur Zwei-Faktor-Authentifizierung. Diese Daten werden von Auth0 verwaltet und gespeichert.

### Klassifizierung

| Datenkategorie         | Sensibilität | Schutzbedarf | Gegenmassnahmen                                              |
| ---------------------- | ------------ | ------------ | ------------------------------------------------------------ |
| MyURL - Username       | Gering       | Gering       | Keine                                                        |
| MyURL - Short-URL      | Gering       | Gering       | keine                                                        |
| MyURL - Manager of URL | Gering       | Gering       | Es kann kein Rückschluss auf eine Person gemacht werden      |
| JWT - SUB              | Gering       | Gering       | keine                                                        |
| Auth0 - Email          | Hoch         | Hoch         | MFA bei Auth0 für Admins                                     |
| Auth0 - Username       | Gering       | Mittel       | MFA für Admins                                               |
| Auth0 - Login          | Hoch         | Hoch         | Auth0 wird regelmässig Auditiert und Admins werden überprüft |

## Datenintegrität

Da der MyURL-Service URLs verkürzt und umleitet, ist die Integrität der Daten von entscheidender Bedeutung. Eine Kompromittierung der Datenintegrität könnte dazu führen, dass Benutzer auf schädliche/falsche Websites umgeleitet werden.

## Datenschutz

Der MyURL-Service verwendet Auth0 als IDP, was bedeutet, dass Benutzerdaten gespeichert und verarbeitet werden. Es ist wichtig, dass diese Daten geschützt und nur für den vorgesehenen Zweck verwendet werden.

## Verfügbarkeit

Da der MyURL-Service als Microservice entwickelt wurde und auf ECS, SQS, Lambda, DynamoDB und RDS PostgreSQL basiert, ist die Verfügbarkeit des Services von entscheidender Bedeutung. Ein Ausfall eines dieser Services könnte dazu führen, dass der MyURL-Service nicht verfügbar ist.

Die kritischsten Services sind die DynamoDB, sowie die Lambda Funktionen, welche einen direkten einfluss auf den Redirect haben. Dieser verfügen über eine hohe Verfügbarkeit und werden von AWS bereitgestellt

## Zusammenfassung der Schutzbedarfsanalyse

Die Schutzbedarfsanalyse hat gezeigt, dass der MyURL-Service einen mittleren Schutzbedarf hat. Die Datenintegrität ist von entscheidender Bedeutung, da eine Kompromittierung dazu führen könnte, dass Benutzer auf schädliche oder falsche Websites umgeleitet werden. Der Datenschutz ist ebenfalls wichtig, da der Service Auth0 als IDP verwendet und Benutzerdaten speichert und verarbeitet. Es muss sichergestellt werden, dass diese Daten geschützt und nur für den vorgesehenen Zweck verwendet werden.

Die Verfügbarkeit des Services ist ebenfalls von entscheidender Bedeutung, da der MyURL-Service als Microservice entwickelt wurde und auf mehreren AWS-Services basiert. Ein Ausfall eines dieser Services, insbesondere der DynamoDB oder der Lambda-Funktionen, die einen direkten Einfluss auf den Redirect haben, könnte dazu führen, dass der MyURL-Service nicht verfügbar ist. Diese Services verfügen jedoch über eine hohe Verfügbarkeit und werden von AWS bereitgestellt.

Insgesamt erfordert der Schutzbedarf des MyURL-Services eine sorgfältige Überwachung und regelmässige Überprüfungen, um sicherzustellen, dass die Datenintegrität, der Datenschutz und die Verfügbarkeit jederzeit gewährleistet sind.
