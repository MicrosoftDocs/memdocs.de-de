---
title: Benutzer – Intune Data Warehouse
titleSuffix: Microsoft Intune
description: Referenzthema für die Kategorie „Benutzer“ der Entitätsauflistungen in der Intune Data Warehouse-API.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/03/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: C29A6EEA-72B7-427E-9601-E05B408F3BB0
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: b2bb18415cbebcef98ba6a7015872467c13eb231
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79339877"
---
# <a name="reference-for-user-entity"></a>Referenz für die Benutzerentität

Die Kategorie **Users** enthält die Entität **user**, die die Eigenschaften von Benutzern und Agents im Datenmodell definiert.

## <a name="users"></a>Benutzer

Die Entität **user** listet alle Benutzer von Azure Active Directory (Azure AD) mit zugewiesenen Lizenzen in Ihrem Unternehmen auf.

Die Entitätssammlung **user** enthält Benutzerdaten. Zu diesen Datensätzen gehören Benutzerzustände während der Datensammlung, selbst wenn der Benutzer entfernt wurde. Beispielsweise kann ein Benutzer in Intune hinzugefügt und dann im Verlauf des letzten Monats entfernt worden sein. Auch wenn dieser Benutzer zum Zeitpunkt der Berichterstellung nicht vorhanden ist, liegen Angaben zu Benutzer und Zustand in den Daten aus dem vorherigen Monat vor. Sie können einen Bericht erstellen, der die Dauer der Präsenz des Benutzers in Ihren Daten zeigt.

|          Eigenschaft          |                                                                                                           Description                                                                                                          |                Beispiel               |
|:--------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:------------------------------------:|
| userKey                    | Eindeutiger Bezeichner des Benutzers im Data Warehouse – Ersatzschlüssel.                                                                                                                                                         | 123                                  |
| userId                     | Eindeutiger Bezeichner des Benutzers – ähnlich wie UserKey, ist jedoch ein natürlicher Schlüssel.                                                                                                                                                    | b66bc706-ffff-7437-0340-032819502773 |
| UserEmail                  | E-Mail-Adresse des Benutzers                                                                                                                                                                                                     | John@constoso.com                    |
| userPrincipalName                        | Benutzerprinzipalname des Benutzers                                                                                                                                                                                               | John@constoso.com                    |
| displayName                | Anzeigename des Benutzers                                                                                                                                                                                                      | John                                 |
| intuneLicensed             | Gibt an, ob dieser Benutzer über Intune lizenziert ist oder nicht.                                                                                                                                                                              | Wahr/falsch                           |
| isDeleted                  | Gibt an, ob alle Lizenzen des Benutzers abgelaufen sind und ob der Benutzer daher aus Intune entfernt wurde. Dieses Flag wird für einen einzelnen Datensatz nicht geändert. Stattdessen wird ein neuer Datensatz für einen neuen Benutzerzustand erstellt. | Wahr/falsch                           |
| RowLastModifiedDateTimeUTC | UTC-Zeitpunkt, zu dem der Datensatz im Data Warehouse zuletzt geändert wurde.                                                                                                                                                 | 23.11.2016 0:00                      |


## <a name="next-steps"></a>Nächste Schritte
- Sie können die Entitätssammlung **Aktueller Benutzer** verwenden, um die Benutzerdaten auf Benutzer zu beschränken, die derzeit aktiv sind. Weitere Informationen finden Sie unter [Referenz für die Entität „Aktueller Benutzer“](reports-ref-data-model.md).
- Informationen zur Nachverfolgung der Benutzerlebensdauer über das Data Warehouse in Intune finden Sie unter [Darstellung der Benutzerlebensdauer im Intune Data Warehouse](reports-ref-user-timeline.md).
