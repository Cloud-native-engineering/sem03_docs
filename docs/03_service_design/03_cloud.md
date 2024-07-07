---
layout: default
title: 3.3 Cloud
parent: 3. Service Design
nav_order: 3
---

# 3.3 Cloud

Um für den URL-Shortener das Perfekte Zuhause zu finden werden in diesem Abschnitt die verschiedenen Cloud Provider miteinander verglichen. Dabei wird nicht nur die öffentlichen Angebote der Hyperscaler, sondern auch ihre spezifischen Free-Tier- und Education/Sandbox-Versionen angeschaut. Folgende Produkte müssen vorhanden sein:

- Managed Databases
- Managed Message Queue
- Container Runtime / Kubernetes
- Container Image Repository

## Cloud Provider

Folgende Cloud Hyperscaler werden genauer angeschaut:

### Microsoft Azure

| **Cloud Provider**         | **Produkt**                                                                                                                                                  |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Databases                  | Vielzahl von Managed Databases, SQL-/NoSQL- und KeyValue-Datenbanken <br>- Azure Database for MySQL/PostgreSQL<br>- Oracle Database@Azure<br>-Azure CosmosDB |
| Message Queue              | -Queue Storage<br>- Service Bus                                                                                                                              |
| Container Runtime          | - Azure Container Apps<br>- Azure Kubernetes Service (AKS)                                                                                                   |
| Container Image Repository | Azure Container Registry                                                                                                                                     |

### Amazon Web Services - AWS

| **Cloud Provider**         | **Produkt**                                                 |
| -------------------------- | ----------------------------------------------------------- |
| Databases                  | - RDS<br>- DynamoDB                                         |
| Message Queue              | AWS SQS                                                     |
| Container Runtime          | - Elastic Container Service<br>- Elastic Kubernetes Service |
| Container Image Repository | - Elastic Container Registry                                |

### Private Cloud

| **Cloud Provider**         | **Produkt**                                                                     |
| -------------------------- | ------------------------------------------------------------------------------- |
| Databases                  | Personal Managed, SQL/NoSQL                                                     |
| Message Queue              | Personal Managed, Apache ActiveMQ                                               |
| Container Runtime          | Personal Managed<br>- Docker<br>- Podman<br>- Kubernetes                        |
| Container Image Repository | Personal Managed<br>- Docker Registry<br>- Artifactory Container Image Registry |

## Entscheidungsmatrix

Es können folgende Punkte von 1 bis 5 verteilt werden, wobei 5 die beste Bewertung darstellt.

| **Kriterium**                          | **Private Cloud** | **Microsoft Azure** | **Microsoft Azure - Education** | **Amazon Web Services** | **AWS - Learner-Lab** | **AWS - Free Tier** |
| -------------------------------------- | ----------------- | ------------------- | ------------------------------- | ----------------------- | --------------------- | ------------------- |
| **Database Kosten**                    | \*\*              | \*\*\*              | \*\*\*                         | \*\*\*                  | \*\*\*\*\*            | \*\*\*              |
| **Database Aufwand**                   | \*                | \*\*\*\*\*          | \*\*\*\*\*                      | \*\*\*\*\*              | \*\*\*                | \*\*\*\*            |
| **Message-Queue Kosten**               | \*\*\*            | \*\*\*\*\*          | \*\*\*\*                        | \*\*\*\*\*              | \*\*\*\*\*            | \*\*\*\*\*          |
| **Message-Queue Aufwand**              | \*\*\*            | \*\*\*\*            | \*\*\*\*\*                      | \*\*\*\*                | \*\*\*                | \*\*\*\*\*          |
| **Container Runtime Kosten**           | \*\*              | \*\*\*              | \*\*\*\*                        | \*\*\*                  | \*\*\*\*\*            | \*\*                |
| **Container Runtime Aufwand**          | \*                | \*\*\*\*            | \*\*\*\*                        | \*\*\*\*                | \*\*\*\*              | \*\*\*\*            |
| **Container Image Repository Kosten**  | \*\*\*\*          | \*\*\*\*            | \*\*\*\*                        | \*\*\*\*                | \*\*\*\*\*            | \*\*                |
| **Container Image Repository Aufwand** | \*\*\*            | \*\*\*\*\*          | \*\*\*\*\*                      | \*\*\*\*\*              | \*\*\*\*\*            | \*\*\*\*            |
| **GESAMTKOSTEN**                       | 19                | 33                  | 34                              | 33                      | 35                    | 29                  |

Die Entscheidung für Amazon Web Services in der Learner-Lab Version basiert auf mehreren Faktoren, die AWS von der Azure-Cloud unterscheiden, obwohl beide Anbieter im Grunde die gleichen Dienste anbieten, die für dieses Projekt benötigt werden.

Ein Hauptfaktor ist die Kostenkontrolle. Das Learner-Lab stoppt sich automatisch nach einigen Stunden. Nach diesem Shutdown werden grosse Kostenpunkte, wie zum Beispiel die Container-Engine, gestoppt und verursachen keine weiteren Kosten. Da die Plattform zwangsweise gestoppt wird, können keine unerwarteten Kosten entstehen, da das Lab nicht mehr erreichbar ist. Dies bietet eine effektive Kostenkontrolle und verhindert unerwartete Überschreitungen des Budgets.

Insgesamt bietet AWS Learner-Lab eine kosteneffektive, kontrollierte Umgebung mit zusätzlichen Funktionen, die für dieses Projekt nützlich sein könnten. Daher wurde es als bevorzugte Cloud-Option ausgewählt. Sollte es trotzdem zu Problemen mit der AWS in dem Learner-Lab kommen, so kann einfach auf den Free-tier gewechselt werden. Dort müsste einfach stark auf die Kosten geachtet werden. Alternativ kann auf die Azure Cloud mit der Education Subscription gewechselt werden. Beide Anbieter bieten die gleichen Dienste an, die für dieses Projekt benötigt werden, was die Flexibilität bei der Wahl des Anbieters erhöht.
