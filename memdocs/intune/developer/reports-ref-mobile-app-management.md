---
title: Mobile App-Verwaltung (MAM)
titleSuffix: Microsoft Intune
description: Referenzthema für die Kategorie „Verwaltung mobiler Anwendungen“ der Entitätsauflistungen in der Intune Data Warehouse-API.
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
ms.assetid: 084F11AD-F7BA-45A4-8424-45E6E4564930
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 428ee1ce93b4f6fe21c4b0180a9df222f3e23e09
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79359754"
---
# <a name="reference-for-mobile-app-management-mam-entities"></a>Verweis für MAM-Entitäten (Verwaltung mobiler Apps)

Die Kategorie **Verwaltung mobiler Apps (MAM)** enthält Entitäten für mobile Apps, z.B.:

- Apps
- Instanzen
- Eincheckstatus
- Integritätsstatus
- Richtlinienstatus
- Anmeldungsstatus
- Plattformtypen

## <a name="mamapplications"></a>mamApplications

Die Entität **mamApplication** führt branchenspezifische Apps (LOB, Line-of-Business) auf, die über die Verwaltung mobiler Geräte (MAM) ohne Registrierung in Ihrem Unternehmen verwaltet werden.

| Eigenschaft | Description | Beispiel |
|---------|------------|--------|
| mamApplicationKey |Eindeutiger Bezeichner der MAM-Anwendung. | 432 |
| mamApplicationName |Name der MAM-Anwendung. |Beispielname für MAM-Anwendung |
| mamApplicationId |Anwendungs-ID der MAM-Anwendung. | 123 |
| isDeleted |Gibt an, ob dieser MAM-App-Datensatz aktualisiert wurde <br>Wahr: MAM-App verfügt über einen neuen Datensatz mit aktualisierten Feldern in dieser Tabelle. <br>Falsch: der neueste Datensatz für diese MAM-App. |Wahr/falsch |
| startDateInclusiveUTC |Datum und Uhrzeit in UTC, als diese MAM-App im Data Warehouse erstellt wurde |23.11.2016 12:00:00 |
| deletedDateUTC |Datum und Uhrzeit in UTC, als IsDeleted in TRUE geändert wurde |23.11.2016 12:00:00 |
| rowLastModifiedDateTimeUTC |Datum und Uhrzeit in UTC, als diese MAM-App zuletzt im Data Warehouse geändert wurde |23.11.2016 12:00:00 |


## <a name="mamapplicationinstances"></a>mamApplicationInstances

Die Entität **mamApplicationInstance** führt verwaltete MAM-Apps (Mobile Application Management, Verwaltung von mobilen Anwendungen) als Singularinstanz pro Benutzer pro Gerät auf. Alle aufgeführten Benutzer und Geräte in der Entität sind geschützt, d.h., ihnen wurde mindestens eine MAM-Richtlinie zugewiesen.


|          Eigenschaft          |                                                                                                  Description                                                                                                  |               Beispiel                |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
|   applicationInstanceKey   |                                                               Eindeutiger Bezeichner für die MAM-App-Instanz im Data Warehouse – Ersatzschlüssel                                                                |                 123                  |
|           userId           |                                                                              Benutzer-ID des Benutzers, der diese MAM-App installiert hat                                                                              | b66bc706-ffff-7437-0340-032819502773 |
|   applicationInstanceId    |                                              Eindeutiger Bezeichner der MAM-App-Instanz – ähnlich wie ApplicationInstanceKey, jedoch ist der Bezeichner ein natürlicher Schlüssel                                              | b66bc706-ffff-7437-0340-032819502773 |
| mamApplicationId | Anwendungs-ID der MAM-Anwendung, die für die diese MAM-Anwendungsinstanz erstellt wurde.   | 23.11.2016 12:00:00   |
|     applicationVersion     |                                                                                     Anwendungsversion dieser MAM-App                                                                                      |                  2                   |
|        createdDate         |                                                                 Datum, als dieser Datensatz der MAM-App-Instanz erstellt wurde. Der Wert kann NULL sein.                                                                 |        23.11.2016 12:00:00        |
|          Plattform          |                                                                          Plattform des Geräts, auf dem diese MAM-App installiert wurde                                                                           |                  2                   |
|      platformVersion       |                                                                      Plattformversion des Geräts, auf dem diese MAM-App installiert wurde                                                                       |                 2.2                  |
|         sdkVersion         |                                                                            Die Version des MAM SDKs, mit der diese MAM-App umschlossen wurde                                                                            |                 3,2                  |
| mamDeviceId | Geräte-ID des Geräts, dem die MAM-Anwendungsinstanz zugeordnet ist.   | 23.11.2016 12:00:00   |
| mamDeviceType | Gerätetyp des Geräts, dem die MAM-Anwendungsinstanz zugeordnet ist.   | 23.11.2016 12:00:00   |
| mamDeviceName | Gerätename des Geräts, dem die MAM-Anwendungsinstanz zugeordnet ist.   | 23.11.2016 12:00:00   |
|         isDeleted          | Gibt an, ob dieser Datensatz der MAM-App-Instanz aktualisiert wurde <br>Wahr: Diese MAM-App-Instanz verfügt über einen neuen Datensatz mit aktualisierten Feldern in dieser Tabelle. <br>Falsch: der neueste Datensatz für diese MAM-App-Instanz. |              Wahr/falsch              |
|   startDateInclusiveUtc    |                                                              Datum und Uhrzeit in UTC, als diese MAM-App-Instanz im Data Warehouse erstellt wurde                                                               |        23.11.2016 12:00:00        |
|       deletedDateUtc       |                                                                             Datum und Uhrzeit in UTC, als IsDeleted in TRUE geändert wurde                                                                              |        23.11.2016 12:00:00        |
| rowLastModifiedDateTimeUtc |                                                           Datum und Uhrzeit in UTC, als diese MAM-App-Instanz im Data Warehouse zuletzt geändert wurde                                                            |        23.11.2016 12:00:00        |


## <a name="mamcheckins"></a>mamCheckins

Die Entität **mamCheckin** stellt Daten dar, die gesammelt wurden, als eine MAM-App-Instanz sich bei Intune Service gemeldet hat. 

> [!Note]  
> Wenn eine App-Instanz sich mehrmals pro Tag meldet, speichert das Data Warehouse dies als einmalige Anmeldung.

| Eigenschaft | Description | Beispiel |
|---------|------------|--------|
| dateKey |Date Key für den Zeitpunkt als das Einchecken der MAM-App im Data Warehouse aufgezeichnet wurde | 20160703 |
| applicationInstanceKey |Schlüssel der App-Instanz, der diesem Eincheckvorgang der MAM-App zugeordnet wird | 123 |
| userKey |Schlüssel des Benutzers, der diesem Eincheckvorgang der MAM-App zugeordnet wird | 4323 |
| mamApplicationKey |Anwendungsschlüssel der Anwendung, die dem Einchecken der MAM-Anwendung zugeordnet ist. | 432 |
| deviceHealthKey |Schlüssel von DeviceHealth, der diesem Eincheckvorgang der MAM-App zugeordnet wird | 321 |
| platformKey |Stellt die Plattform des Geräts dar, die diesem Eincheckvorgang der MAM-App zugeordnet wird |123 |
| effectiveAppliedPolicyKey |Stellt die effektiv angewendete Richtlinie dar, die mit der MAM-App in Verbindung gebracht wird, die eingecheckt wurde. Eine effektiv angewendete Richtlinie stammt vom Zusammenfügen aller Richtlinien, die für eine bestimmte App und einen Benutzer relevant sind. | 322 |
| pastCheckInDate |Datum und Uhrzeit, wann diese MAM-App zuletzt eingecheckt wurde. Der Wert kann NULL sein. |23.11.2016 12:00:00 |


## <a name="mamdevicehealth"></a>mamDeviceHealth

Die Entität **mamDeviceHealth** stellt Geräte dar, die bereitgestellte MAM-Richtlinien besitzen, auch wenn sie per Jailbreak manipuliert wurden.

| Eigenschaft | Description | Beispiel |
|---------|------------|--------|
| deviceHealthKey |Eindeutiger Bezeichner des Geräts, der der Integrität im Data Warehouse zugeordnet wird – Ersatzschlüssel |123 |
| deviceHealth |Eindeutiger Bezeichner des Geräts und dessen Integrität – ähnlich wie DeviceHealthKey, allerdings ist der Bezeichner ein natürlicher Schlüssel |b66bc706-ffff-7777-0340-032819502773 |
| deviceHealthName |Stellt den Status des Geräts dar. <br>Nicht verfügbar – keine Informationen zu diesem Gerät. <br>Fehlerfrei: Gerät wurde nicht per Jailbreak manipuliert. <br>Nicht Fehlerfrei: Gerät wurde per Jailbreak manipuliert. |Nicht verfügbar fehlerfrei nicht fehlerfrei |
| rowLastModifiedDateTimeUtc |Datum und Uhrzeit in UTC, als diese bestimmte MAM-Geräteintegrität im Data Warehouse zuletzt geändert wurde |23.11.2016 12:00:00 |

## <a name="mameffectivepolicies"></a>mamEffectivePolicies

Die Entität **mamEffectivePolicy** führt alle effektiven MAM-Richtlinien auf, die in Ihrer Organisation angewendet werden. Eine effektiv angewendete Richtlinie stammt vom Zusammenfügen aller Richtlinien, die für eine bestimmte App und einen Benutzer relevant sind.

| Eigenschaft | Description | Beispiel |
|---------|------------|--------|
| effectivePolicyKey |Eindeutiger Bezeichner für die effektive MAM-Richtlinie im Data Warehouse |2 |
| realPolicyKey |Eindeutiger Bezeichner der MAM-Richtlinie, die vom IT-Profi erstellt wurde. |1 |
| rowCreatedDateTimeUtc |Datum und Uhrzeit in UTC, als diese effektive MAM-Richtlinie im Data Warehouse erstellt wurde. |23.11.2016 12:00:00 |

## <a name="mamplatforms"></a>mamPlatforms

Die Entität **mamPlatform** führt Plattformnamen und -typen auf, auf denen eine MAM-App installiert wurde.


|          Eigenschaft          |                                    Description                                    |                         Beispiel                         |
|----------------------------|-----------------------------------------------------------------------------------|---------------------------------------------------------|
|        platformKey         |     Eindeutiger Bezeichner für die Plattform im Data Warehouse – Ersatzschlüssel      |                           123                           |
|          Plattform          | Eindeutiger Bezeichner der Plattform – ähnlich wie PlatformKey, es handelt sich allerdings um einen natürlichen Schlüssel |                           123                           |
|        platformName        |                                   Plattformname                                   | Nicht verfügbar <br>Keine <br>Windows <br>iOS <br>Android: |
| rowLastModifiedDateTimeUtc | Datum und Uhrzeit in UTC, als diese Plattform zuletzt im Data Warehouse geändert wurde  |                 23.11.2016 12:00:00                  |

