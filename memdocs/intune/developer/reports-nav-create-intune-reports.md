---
title: Verwenden des Data Warehouse von Intune
titleSuffix: Microsoft Intune
description: Verwenden Sie das Data Warehouse von Intune zum Erstellen von Berichten, die einen Einblick in Ihre mobile Unternehmensumgebung ermöglichen.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 57019B11-DF9B-4D8A-95FE-254C75398DDE
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: dad1ecb2ed86158e510b0f554e3fd7e12e21a814
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79360222"
---
# <a name="use-the-microsoft-intune-data-warehouse"></a>Verwenden des Data Warehouse von Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Verwenden Sie das Data Warehouse von Intune zum Erstellen von Berichten, die einen Einblick in Ihre mobile Unternehmensumgebung ermöglichen. Einige der Berichte enthalten beispielsweise:
- Trend der Benutzer, die sich bei Intune registrieren, sodass Sie Ihre Lizenzkäufe optimieren können
- Strukturplan für App- und BS-Versionen, damit Sie den Zustand von Mobilgeräten überprüfen können
- Trends zur Konformität der Registrierungen und Geräte, sodass Sie reibungslos Richtlinienaktualisierungen durchführen können

## <a name="data-warehouse-benefits"></a>Vorteile des Data Warehouse

Das Data Warehouse bietet Ihnen Zugriff auf mehr Informationen über Ihre mobile Umgebung als das Azure-Portal. Mit dem Data Warehouse von Intune können Sie auf Folgendes zugreifen:

- Verlaufsdaten für Intune
- Daten, die täglich aktualisiert werden
- Ein Datenmodell, das den OData-Standard verwendet

> [!Note]
> Wenn Sie eine gemeinsame Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit Microsoft Endpoint Configuration Manager und Microsoft Intune verwenden, müssen Sie Ihre Daten aus Configuration Manager abrufen. Das Intune Data Warehouse enthält nur Intune-Daten. Sie können ein Power BI-Dashboard von Configuration Manager für Ihre benutzerdefinierten Berichte verwenden. Weitere Informationen finden Sie unter [Announcing the Power BI solution template for Configuration Manager (Ankündigung der Power BI-Lösungsvorlage für Configuration Manager)](https://powerbi.microsoft.com/blog/sccm-solution-template) und [Power BI-Inhalte für Dynamics 365](https://docs.microsoft.com/dynamics365/unified-operations/dev-itpro/analytics/power-bi-home-page).

> [!Important]  
> Jetzt können Sie die Version v1.0 von Intune Data Warehouse durch Festlegen des Abfrageparameters  `api-version=v1.0`verwenden. Updates von Sammlungen in Data Warehouse bauen aufeinander auf und beschädigen keine vorhandenen Szenarios.<br><br>
> Sie können die neuesten Funktionen des Data Warehouse mithilfe der Betaversion ausprobieren. Für die Verwendung die Betaversion muss Ihre URL den Abfrageparameter  `api-version=beta` enthalten. Die Betaversion bietet Features, bevor sie als unterstützter Dienst allgemein verfügbar gemacht werden. Da Intune kontinuierlich neue Features hinzufügt, könnten sich in der Betaversion Verhalten und Datenverträge ändern. Benutzerdefinierter Code oder Berichtstools, die von der Betaversion abhängig sind, könnten mit laufenden Updates nicht mehr funktionieren.

## <a name="next-steps"></a>Nächste Schritte

- Rufen Sie einen Link ab und verwenden Sie Power BI, um Einblicke zu erhalten. Anweisungen hierzu finden Sie unter [Connect to the Intune Data Warehouse with Power BI (Verbinden mit dem Data Warehouse von Intune mit Power BI)](reports-proc-get-a-link-powerbi.md).
- Erstellen Sie mit Ihrem Link einen benutzerdefinierten Bericht mit Power BI. Weitere Anweisungen hierzu finden Sie unter [Create a report from the OData feed with Power BI (Erstellen eines Berichts aus dem OData-Feed mit Power BI)](reports-proc-create-with-odata.md).
- Weitere Informationen über die Intune Data Warehouse-API, das Datenmodell und Beziehungen zwischen Entitäten<!-- , and an example of creating a custom client to retrieve data,--> finden Sie unter [Intune Data Warehouse-API](reports-nav-intune-data-warehouse.md).
