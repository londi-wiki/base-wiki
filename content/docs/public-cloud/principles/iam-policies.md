---
weight: 999
title: "IAM Policies"
description: ""
icon: "article"
date: "2025-01-19T12:00:00+02:00"
lastmod: "2025-01-19T12:00:00+02:00"
draft: false
toc: true
---

# IAM Policies

# AWS IAM Policies: Effects & Actions

## 1. **Effects**
Das `Effect`-Attribut bestimmt, ob eine Aktion erlaubt oder verweigert wird.

### `Allow`
- Erlaubt die angegebene Aktion(en) für die spezifizierte(n) Ressource(n).
- Wird verwendet, um explizit Berechtigungen zu gewähren.

### `Deny`
- Verweigert explizit die angegebene Aktion(en), selbst wenn eine andere Richtlinie dieselbe Aktion erlaubt.
- Nützlich für Sicherheitsmassnahmen wie das Blockieren sensibler Aktionen oder bestimmter Bedingungen.

---

## 2. **Actions**
`Action` definiert, welche AWS-API-Operationen für eine Ressource erlaubt oder verweigert werden.

### **Allgemeine Platzhalter**
- `*`: Alle Aktionen eines AWS-Dienstes (z. B. `s3:*` für alle S3-Aktionen).
- `service:action`: Einzelne API-Aktion eines Dienstes (z. B. `ec2:StartInstances`).

---

## 3. **Beispiele für Actions nach AWS-Diensten**

### **Amazon S3**
- `s3:ListBucket` → Listet den Inhalt eines Buckets auf.
- `s3:GetObject` → Ermöglicht das Abrufen eines Objekts aus einem S3-Bucket.
- `s3:PutObject` → Speichert ein Objekt in einem S3-Bucket.

### **Amazon EC2**
- `ec2:DescribeInstances` → Listet EC2-Instanzen auf.
- `ec2:StartInstances` → Startet eine EC2-Instanz.
- `ec2:StopInstances` → Stoppt eine EC2-Instanz.
- `ec2:TerminateInstances` → Beendet eine EC2-Instanz.

### **AWS IAM**
- `iam:CreateUser` → Erstellt einen neuen IAM-Benutzer.
- `iam:AttachRolePolicy` → Hängt eine Richtlinie an eine IAM-Rolle an.
- `iam:DeleteUser` → Löscht einen IAM-Benutzer.

### **AWS Lambda**
- `lambda:InvokeFunction` → Führt eine Lambda-Funktion aus.
- `lambda:CreateFunction` → Erstellt eine neue Lambda-Funktion.
- `lambda:DeleteFunction` → Löscht eine Lambda-Funktion.

### **Amazon RDS**
- `rds:CreateDBInstance` → Erstellt eine neue Datenbankinstanz.
- `rds:DeleteDBInstance` → Löscht eine RDS-Datenbankinstanz.
- `rds:DescribeDBInstances` → Listet Datenbankinstanzen auf.

### **Amazon SNS**
- `sns:Publish` → Sendet eine Nachricht an ein SNS-Topic.
- `sns:Subscribe` → Abonniert ein SNS-Topic.
- `sns:Unsubscribe` → Entfernt eine Abonnierung von einem SNS-Topic.

### **Amazon SQS**
- `sqs:SendMessage` → Sendet eine Nachricht an eine SQS-Warteschlange.
- `sqs:ReceiveMessage` → Ruft eine Nachricht aus einer SQS-Warteschlange ab.
- `sqs:DeleteMessage` → Löscht eine Nachricht aus einer SQS-Warteschlange.

---

## 4. **Wildcard-Nutzung**
IAM-Policies unterstützen **Platzhalter (`*`)** für flexible Berechtigungen:

- `s3:Get*` → Erlaubt alle Aktionen, die mit `Get` beginnen (z. B. `s3:GetObject`, `s3:GetBucketPolicy`).
- `ec2:Describe*` → Erlaubt alle EC2-Deskriptionsaktionen (z. B. `ec2:DescribeInstances`, `ec2:DescribeSecurityGroups`).
- `lambda:*` → Erlaubt alle Lambda-Aktionen.

---

## 5. **Beispiel einer IAM Policy**
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket",
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": [
        "arn:aws:s3:::example-bucket",
        "arn:aws:s3:::example-bucket/*"
      ]
    }
  ]
}

