---
layout: default
title: 5.1 Cloud Provisioning
parent: 5. Deployment
nav_order: 1
---

# 5.1 Cloud Provisioning

Das Provisioning-Prozess war in diesem Fall etwas eingeschränkt und beinhaltete einige manuelle Schritte. Der Hauptgrund dafür liegt in den Beschränkungen des Academy Labs. In dieser Umgebung können Tools wie Terraform und Ansible nur bedingt oder sehr eingeschränkt verwendet werden. Ein wesentliches Hindernis besteht darin, dass keine IAM-Rollen und IAM-Benutzer erstellt werden können. Insbesondere wurde das Projekt mit dem Ziel entwickelt, eine Microservice-Plattform bereitzustellen. Für einen Proof of Concept (POC) ist diese teilweise Automatisierung vollkommen ausreichend.

## Bereits existierende Grundlagen

Folgende Ressource existieren bereits und sind im Standard [AWS Academy Learner Lab](https://www.awsacademy.com/forums/s/topic/0TO4N000000cHbxWAE/aws-academy-learner-labs?language=en_US)

- VPC
  - 3 AZ
- IAM
  - Rolle "Lab Role"

Diese Cloud Ressourcen dienen als Grundlage von diesem Deployment. Ein IAM-Berechtigungskonzept war nicht im Scope dieser Arbeit.

## Elastic Container Service - ECS

Der ECS Cluster mit seinen Task-Definitionen kann mit folgenden Cloud-Formation Template deployed werden:

- [MyURL - ECS Cluster](../../resources/templates/myurl_ecs_cloudformation.json)
- [MyURL - ECS Task myurl_api](../../resources/templates/myurl_ecs_task_api.json)
- [MyURL - ECS Task myurl_app](../../resources/templates/myurl_ecs_task_app.json)

## Application Loadbalancer

Folgender Ansible Code kann verwendet werden, um den Application Loadbalancer zu deployen. Dazu muss das AWS-CLI mit dem Lab-Account angemeldet sein.

```yaml
---
- name: "MyURL deploy application Loadbalancer"
  hosts: localhost
  become: false
  gather_facts: false

  tasks:
    - name: Deploy application loadbalancer
      amazon.aws.elb_application_lb:
        name: "myurl-prod" 
        security_groups: "myurl-prod-alb"
        subnets:
          - subnet-az-a
          - subnet-az-b
        listeners:
          - Protocol: HTTP
            Port: 80
            DefaultActions:
              - Type: redirect
                RedirectConfig:
                  Protocol: HTTPS
                  Port: 443
                  Host: '#{host}'
                  Path: '/#{path}'
                  Query: '#{query}'
                  StatusCode: HTTP_301
          - Protocol: HTTPS
            Port: 443
            Certificates:
              - CertificateArn: arn:aws:iam::123456789012:server-certificate/myurl.ch
            SslPolicy: ELBSecurityPolicy-2015-05
            DefaultActions:
              - Type: forward
                TargetGroupName: myurl-prod-app
            Rules:
              - Priority: 10000
                Conditions:
                  - Field: host-header
                    Values: ["www.myurl.ch"]
                Actions:
                  - Type: forward
                    TargetGroupName: myurl-prod-app
              - Priority: 5000
                Conditions:
                  - Field: path-pattern
                    Values: ["/api/*"]
                Actions:
                  - Type: forward
                    TargetGroupName: myurl-prod-api
              - Priority: 20000
                Conditions:
                  - Field: host-header
                    Values: ["myurl.ch"]
                Actions:
                  - Type: forward
                    TargetGroupName: myurl-prod-redirector
...
```

## Public SSL Zertifikate

Der Weg um ein TLS/SSL-Zertifikat zu erlangen wurde absichtlich nicht automatisiert. Grund dafür war, dass der Benötigte Aufwand im Rahmen dieses Projektes nicht gerechtfertigt wäre.

Im Leaner Lab wurde dazu folgende Schritte gemacht:

1. Zertifikat im [AWS Certificate Manager](https://aws.amazon.com/certificate-manager/) beantragen
2. CNAMES für die Domain-Verifikation im öffentlichen DNS der dazugehörigen Domain eintragen

## Relational Database Service - RDS

Die Datenbank kann mit folgendem Ansible Playbook erstellt werden.

```yaml
---
- name: Provision PostgreSQL RDS
  hosts: localhost
  become: false
  gather_facts: false

  tasks:
    - name: Deploy PostgreSQL RDS
      amazon.aws.rds_instance:
        id: "myurl-prod"
        state: present
        engine: 14.2
        username: "{{ username }}"
        password: "{{ password }}"
        db_instance_class: "db.t3.micro"
...
```

## Lambda Function

Der Prozess um den Redirector & den Datahandler zu deployen wurde im SCM-Repository beschrieben: [myurl_redirector](https://github.com/Cloud-native-engineering/myurl_redirector)

## Simple Storage Queue - SQS

Die SQS-Queue wurde mit einfachen standard Settings deployed. Dazu kann folgendes Ansible Playbook verwendet werden:

```yaml
---
- name: Provision SQS Queue
  hosts: localhost
  become: false
  gather_facts: false

  tasks:
    - name: Deploy SQS-Queue
      community.aws.sqs_queue:
        name: "myurl-prod"
        region: "{{ myurl_region }}"
...
```

## DynamoDB

DynamoDB ist die Serverless NoSQL Datenbank. Sie zeichnet ihre schnelle lese und schreibrate aus. Genau so schnell kann eine DyamoDB-Table erstellt werden.

```yaml
---
- name: Provision DynamoDB
  hosts: localhost
  become: false
  gather_facts: false

  tasks:
    - name: Deploy DynamoDB table
      community.aws.dynamodb_table:
        name: "myurl-prod"
        region: "{{ myurl_region }}"
...
```
