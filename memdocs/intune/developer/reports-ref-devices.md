---
title: Geräte – Intune Data Warehouse
titleSuffix: Microsoft Intune
description: Referenzthema für die Kategorie „Geräte“ der Entitätsauflistungen in der Intune Data Warehouse-API
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
ms.assetid: 6955E12D-70D7-4802-AE3B-8B276F01FA4F
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: ae1f0117f6dbf186b3a4bdddb393d053c33c914a
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79359793"
---
# <a name="reference-for-devices-entities"></a>Referenz für Geräteentitäten

Die Kategorie **devices** enthält Entitäten für mobile Geräte, die folgende Informationen nachverfolgen:

- Gerätetyp
- Status der Geräteregistrierung
- Gerätebesitz
- Status der Geräteverwaltung
- Status der Gerätemitgliedschaft bei Azure AD
- Anmeldungsstatus
- Informationen zur Geschichte des Geräts
- App-Inventar auf dem Gerät

## <a name="devicetypes"></a>deviceTypes

Die Entität **deviceTypes** stellt den Gerätetyp dar, auf den von anderen Data Warehouse-Entitäten verwiesen wird. Der Gerätetyp beschreibt in der Regel entweder das Gerätemodell, den Hersteller oder eine Kombination aus beidem.

| Eigenschaft  | Beschreibung |
|---------|------------|
| deviceTypeID |Der eindeutige Bezeichner des Gerätetyps |
| deviceTypeKey |Der eindeutige Bezeichner des Gerätetyps im Data Warehouse – Ersatzschlüssel |
| deviceTypeName |Gerätetyp |

### <a name="example"></a>Beispiel

| deviceTypeID  | Name | Beschreibung |
|---------|------------|--------|
| 0 |desktop- |Windows Desktop-Gerät |
| 1 |WindowsRT |WindowsRT-Gerät |
| 2 |WinMO6 |Windows Mobile 6.0-Gerät |
| 3 |Nokia |Nokia-Gerät |
| 4 |WindowsPhone |Windows Phone-Gerät |
| 5 |Mac |Mac-Gerät |
| 6 |WinCE |Windows CE-Gerät |
| 7 |WinEmbedded |Windows Embedded-Gerät |
| 8 |IPhone |iPhone-Gerät |
| 9 |IPad |iPad-Gerät |
| 10 |IPod |iPod-Gerät |
| 11 |Android |Mit dem Geräteadministrator verwaltetes Android-Gerät |
| 12 |ISocConsumer |iSoc Consumer-Gerät |
| 14 |MacMDM |Mac OS X-Gerät, das mit dem integrierten MDM-Agent verwaltet wird |
| 15 |HoloLens |HoloLens-Gerät |
| 16 |SurfaceHub |Surface Hub-Gerät |
| 17 |AndroidForWork |Android-Gerät, das mit dem Android-Profilbesitzer verwaltet wird |
| 100 |BlackBerry |Blackberry Device |
| 101 |Palm |Palm-Gerät |
| 255 |Unbekannt |Unbekannter Gerätetyp |

## <a name="enrollmentactivities"></a>enrollmentActivities 
Die Entität **enrollmentActivity** gibt die Aktivität einer Geräteregistrierung an.

| Eigenschaft                      | Beschreibung                                                               |
|-------------------------------|---------------------------------------------------------------------------|
| dateKey                       | Der Schlüssel des Datums, an dem diese Registrierungsaktivität aufgezeichnet wurde.               |
| deviceEnrollmentTypeKey       | Der Schlüssel des Typs der Registrierung.                                        |
| deviceTypeKey                 | Der Schlüssel des Gerätetyps.                                                |
| enrollmentEventStatusKey      | Der Schlüssel des Status, der auf eine erfolgreiche bzw. fehlgeschlagene Registrierung hinweist.    |
| enrollmentFailureCategoryKey  | Der Schlüssel der Kategorie des Registrierungsfehlers (bei fehlgeschlagener Registrierung).        |
| enrollmentFailureReasonKey    | Der Schlüssel des Grunds des Registrierungsfehlers (bei fehlgeschlagener Registrierung).          |
| osVersion                     | Die Betriebssystemversion des Geräts.                               |
| count                         | Die Gesamtanzahl der Registrierungsaktivitäten, die den oben genannten Klassifizierungen entsprechen.  |

## <a name="enrollmenteventstatuses"></a>enrollmentEventStatuses 
Die Entität **enrollmentEventStatus** gibt das Ergebnis einer Geräteregistrierung an.

| Eigenschaft                   | Beschreibung                                                                       |
|----------------------------|-----------------------------------------------------------------------------------|
| enrollmentEventStatusKey   | Eindeutiger Bezeichner des Registrierungsstatus im Data Warehouse (Ersatzschlüssel).  |
| enrollmentEventStatusName  | Die Bezeichnung des Registrierungsstatus. Siehe folgende Beispiele.                            |

### <a name="example"></a>Beispiel

| enrollmentEventStatusName  | Beschreibung                            |
|----------------------------|----------------------------------------|
| Erfolgreich                    | Eine erfolgreiche Geräteregistrierung.         |
| Failed                     | Eine fehlerhafte Geräteregistrierung.             |
| Nicht verfügbar              | Der Registrierungsstatus ist nicht verfügbar.  |

## <a name="enrollmentfailurecategories"></a>enrollmentFailureCategories 
Die Entität **enrollmentFailureCategory** gibt an, warum eine Geräteregistrierung fehlgeschlagen ist. 

| Eigenschaft                       | Beschreibung                                                                                 |
|--------------------------------|---------------------------------------------------------------------------------------------|
| enrollmentFailureCategoryKey   | Eindeutiger Bezeichner der Fehlerkategorie für die Registrierung im Data Warehouse (Ersatzschlüssel).  |
| enrollmentFailureCategoryName  | Der Name der Fehlerkategorie für die Registrierung. Siehe folgende Beispiele.                            |

### <a name="example"></a>Beispiel

| enrollmentFailureCategoryName   | Beschreibung                                                                                                   |
|---------------------------------|---------------------------------------------------------------------------------------------------------------|
| Nicht zutreffend                  | Die Fehlerkategorie für die Registrierung ist nicht anwendbar.                                                            |
| Nicht verfügbar                   | Die Fehlerkategorie für die Registrierung ist nicht verfügbar.                                                             |
| Unbekannt                         | Unbekannter Fehler.                                                                                                |
| Authentifizierung                  | Fehler bei der Authentifizierung.                                                                                        |
| Autorisierung                   | Aufruf war authentifiziert, aber nicht für eine Registrierung autorisiert.                                                         |
| AccountValidation               | Fehler beim Überprüfen des Kontos für die Registrierung. (Konto gesperrt, Registrierung nicht aktiviert)                      |
| UserValidation                  | Benutzer konnte nicht überprüft werden. (Benutzer ist nicht vorhanden, fehlende Lizenz)                                           |
| DeviceNotSupported              | Das Gerät wird für die mobile Geräteverwaltung nicht unterstützt.                                                         |
| InMaintenance                   | Das Konto befindet sich im Wartungsmodus.                                                                                    |
| BadRequest                      | Der Client hat eine Anforderung gesendet, die vom Dienst nicht verstanden bzw. unterstützt wird.                                        |
| FeatureNotSupported             | Die von dieser Registrierung verwendeten Features werden für dieses Konto nicht unterstützt.                                        |
| EnrollmentRestrictionsEnforced  | Vom Administrator konfigurierte Registrierungseinschränkungen haben diese Registrierung blockiert.                                          |
| ClientDisconnected              | Für den Client gab es eine Zeitüberschreitung, oder die Registrierung wurde vom Endbenutzer abgebrochen.                                                        |
| UserAbandonment                 | Die Registrierung wurde vom Endbenutzer vorzeitig beendet. (Der Endbenutzer hat mit dem Onboarding begonnen, aber dieses nicht rechtzeitig abgeschlossen.)  |

## <a name="enrollmentfailurereasons"></a>enrollmentFailureReasons  
Die Entität **enrollmentFailureReason** gibt eine ausführlichere Ursache für einen Fehler bei der Geräteregistrierung innerhalb einer Fehlerkategorie an.  

| Eigenschaft                     | Beschreibung                                                                               |
|------------------------------|-------------------------------------------------------------------------------------------|
| enrollmentFailureReasonKey   | Eindeutiger Bezeichner für die Fehlerursache bei der Registrierung im Data Warehouse (Ersatzschlüssel).  |
| enrollmentFailureReasonName  | Die Bezeichnung der Fehlerursache bei der Registrierung. Siehe folgende Beispiele.                            |

### <a name="example"></a>Beispiel

| enrollmentFailureReasonName      | Beschreibung                                                                                                                                                                                            |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Nicht zutreffend                   | Die Fehlerursache für die Registrierung ist nicht anwendbar.                                                                                                                                                       |
| Nicht verfügbar                    | Die Fehlerursache für die Registrierung ist nicht verfügbar.                                                                                                                                                        |
| Unbekannt                          | Unbekannter Fehler.                                                                                                                                                                                         |
| UserNotLicensed                  | Der Benutzer wurde nicht in Intune gefunden oder verfügt über keine gültige Lizenz.                                                                                                                                     |
| UserUnknown                      | Der Benutzer ist Intune nicht bekannt.                                                                                                                                                                           |
| BulkAlreadyEnrolledDevice        | Nur ein Benutzer kann ein Gerät registrieren. Dieses Gerät wurde zuvor von einem anderen Benutzer registriert.                                                                                                                |
| EnrollmentOnboardingIssue        | Die Intune-Autorität für die mobile Geräteverwaltung (MDM) ist noch nicht konfiguriert.                                                                                                                                 |
| AppleChallengeIssue              | Die Installation des iOS-Verwaltungsprofils hat sich verzögert oder war fehlerhaft.                                                                                                                                         |
| AppleOnboardingIssue             | Für die Registrierung in Intune ist ein Apple-MDM-Pushzertifikat erforderlich.                                                                                                                                       |
| DeviceCap                        | Der Benutzer hat versucht, mehr Geräte zu registrieren, als maximal zulässig sind.                                                                                                                                        |
| AuthenticationRequirementNotMet  | Der Intune-Registrierungsdienst konnte diese Anforderung nicht autorisieren.                                                                                                                                            |
| UnsupportedDeviceType            | Das Gerät erfüllt nicht die Mindestanforderungen für die Intune-Registrierung.                                                                                                                                  |
| EnrollmentCriteriaNotMet         | Dieses Gerät konnte aufgrund einer konfigurierten Regel zur Einschränkung von Registrierungen nicht registriert werden.                                                                                                                          |
| BulkDeviceNotPreregistered       | Die IMEI (International Mobile Equipment Identity) bzw. die Seriennummer dieses Geräts wurde nicht gefunden.  Ohne diesen Bezeichner werden Geräte als persönliche Geräte erkannt, die zurzeit gesperrt sind.  |
| FeatureNotSupported              | Der Benutzer hat versucht, auf eine Funktion zuzugreifen, die noch nicht für alle Kunden freigegeben oder nicht mit Ihrer Intune-Konfiguration kompatibel ist.                                                            |
| UserAbandonment                  | Die Registrierung wurde vom Endbenutzer vorzeitig beendet. (Der Endbenutzer hat mit dem Onboarding begonnen, aber dieses nicht rechtzeitig abgeschlossen.)                                                                                           |
| APNSCertificateExpired           | Apple-Geräte können nicht mit einem abgelaufenen Apple-MDM-Pushzertifikat verwaltet werden.                                                                                                                            |
## <a name="ownertypes"></a>ownerTypes

Die Entität **enrollmentType** gibt an, ob ein Gerät einem Unternehmen oder einer Privatperson gehört oder ob der Besitzer unbekannt ist.

| Eigenschaft  | Beschreibung | Beispiel |
|---------|------------|--------|
| ownerTypeID |Eindeutiger Bezeichner des Besitzertyps | |
| ownerTypeKey |Eindeutige Bezeichner des Besitzertyps im Data Warehouse – Ersatzschlüssel | |
| ownerTypeName |Stellt den Besitzertypen der Geräte dar:  <br>Corporate (Unternehmen): Das Gerät gehört einem Unternehmen. <br>Personal (Privat): Das Gerät befindet sich im Privatbesitz (BYOD).  <br>Unknown (Unbekannt): Es liegen keine Informationen zu diesem Gerät vor. |Corporate Personal Unknown |

> [!Note]  
> Für `ownerTypeName` in AzureAD müssen Sie beim Erstellen dynamischer Gruppen für Geräte den Filterwert `deviceOwnership` als `Company` festlegen. Weitere Informationen finden Sie unter [Regeln für Geräte](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices). 

## <a name="managementstates"></a>managementStates

Die Entität **managementStates** stellt Details zum Status des Geräts bereit. Details können nützlich sein, wenn Remoteaktionen angewendet werden, das Gerät per Jailbreak oder Rootzugriff manipuliert wurde.

| Eigenschaft  | Beschreibung |
|---------|------------|
| managementStateID | Der eindeutige Bezeichner des Verwaltungsstatus |
| managementStateKey | Der eindeutige Bezeichner des Verwaltungsstatus im Data Warehouse – Ersatzschlüssel |
| managementStateName | Gibt den Status der Remoteaktion an, die auf dieses Gerät angewendet wurde |

### <a name="example"></a>Beispiel

| managementStateID  | Name | Beschreibung |
|---------|------------|--------|
| 0 |Verwaltet | Verwaltet, ohne ausstehende Remoteaktionen |
| 1 |RetirePending | Für das Gerät steht ein Befehl zum Außerkraftsetzen aus. |
| 2 |RetireFailed | Der Befehl zum Außerkraftsetzen konnte auf dem Gerät nicht ausgeführt werden. |
| 3 |WipePending | Für das Gerät steht ein Zurücksetzungsbefehl aus. |
| 4 |WipeFailed | Der Zurücksetzungsbefehl konnte auf dem Gerät nicht ausgeführt werden. |
| 5 |Unhealthy | Fehlerhafter Zustand |
| 6 |DeletePending | Für das Gerät steht ein Löschungsbefehl aus. |
| 7 |RetireIssued | Ein Befehl zum Außerkraftsetzen wurde an das Gerät ausgegeben. |
| 8 |WipeIssued | Ein Zurücksetzungsbefehl wurde ausgestellt. |
| 9 |WipeCanceled | Ein Zurücksetzungsbefehl wurde abgebrochen. |
| 10 |RetireCanceled | Ein Befehl zum Außerkraftsetzen wurde abgebrochen. |
| 11 |Discovered | Das Gerät wird von Intune neu ermittelt und erhält beim ersten Einchecken den Status „Managed“ (Verwaltet) |

## <a name="managementagenttypes"></a>managementAgentTypes

Die Entität **ManagementAgentType** stellt die Agents dar, die zum Verwalten von Geräten verwendet werden.

| Eigenschaft  | Beschreibung |
|---------|------------|
| managementAgentTypeID | Eindeutige Bezeichner des Verwaltungs-Agent-Typen |
| managementAgentTypeKey | Eindeutiger Bezeichner des Verwaltungs-Agent-Typen im Data Warehouse – Ersatzschlüssel |
| managementAgentTypeName |Gibt an, welche Art von Agent zum Verwalten des Geräts verwendet wird |

### <a name="example"></a>Beispiel

| ManagementAgentTypeID  | Name | Beschreibung |
|---------|------------|--------|
| 1 |EAS | Das Gerät wird mithilfe von Exchange Active Sync verwaltet. |
| 2 |MDM | Das Gerät wird mit einem MDM-Agent verwaltet. |
| 3 |EasMdm | Das Gerät wird sowohl von Exchange Active Sync als auch einem MDM-Agent verwaltet. |
| 4 |IntuneClient | Das Gerät wird vom Intune-PC-Agent verwaltet. |
| 5 |EasIntuneClient | Das Gerät wird sowohl von Exchange ActiveSync als auch vom Intune-PC-Agent verwaltet. |
| 8 |ConfigManagerClient | Das Gerät wird vom Configuration Manager-Agent verwaltet. |
| 16 |Unbekannt | Unbekannter Typ von Verwaltungs-Agent |

## <a name="devices"></a>Geräte

In der Entität **devices** werden alle für die Verwaltung registrierten Geräte und ihre entsprechenden Eigenschaften aufgelistet.

|          Eigenschaft          |                                                                                       Beschreibung                                                                                      |
|:--------------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| deviceKey                  | Der eindeutige Bezeichner des Geräts im Data Warehouse – Ersatzschlüssel.                                                                                                               |
| deviceId                   | Eindeutiger Bezeichner des Geräts.                                                                                                                                                     |
| deviceName                 | Der Name des Geräts auf Plattformen, die das Benennen von Geräten ermöglichen. Auf anderen Plattformen wird von Intune ein Name anhand anderer Eigenschaften erstellt. Dieses Attribut kann nicht für alle Geräte zur Verfügung stehen. |
| deviceTypeKey              | Schlüssel des Gerätetypattributs für dieses Gerät.                                                                                                                                    |
| deviceRegistrationState    | Schlüssel des Clientregistrierungsstatus-Attributs für dieses Gerät.                                                                                                                      |
| ownerTypeKey               | Schlüssel des Besitzertypattributs für dieses Gerät: Unternehmen, persönlich oder unbekannt.                                                                                                    |
| enrolledDateTime           | Zeitpunkt der Registrierung dieses Geräts.                                                                                                                                         |
| lastSyncDateTime           | Letztes bekanntes Einchecken des Geräts mit Intune.                                                                                                                                              |
| managementAgentKey         | Der Schlüssel des Verwaltungs-Agents, der mit diesem Gerät verknüpft ist.                                                                                                                             |
| managementStateKey         | Der Schlüssel des Verwaltungsstatus, der mit diesem Gerät verknüpft ist und den neuesten Zustand einer Remoteaktion angibt oder anzeigt, ob das Gerät per Jailbreak oder Rootzugriff manipuliert wurde.                                                |
| azureADDeviceId            | Die Azure-Geräte-ID für dieses Gerät.                                                                                                                                                  |
| azureADRegistered          | Gibt an, ob das Gerät in Azure Active Directory registriert ist.                                                                                                                             |
| deviceCategoryKey          | Der Schlüssel der Kategorie, die mit diesem Gerät verknüpft ist.                                                                                                                                     |
| deviceEnrollmentType       | Der Schlüssel des Registrierungstyps, der mit diesem Gerät verknüpft ist und die Registrierungsmethode angibt.                                                                                             |
| complianceStateKey         | Der Schlüssel des Konformitätsstatus, der mit diesem Gerät verknüpft ist.                                                                                                                             |
| osVersion                  | Die Betriebssystemversion des Geräts.                                                                                                                                                |
| easDeviceId                | Exchange ActiveSync-ID des Geräts                                                                                                                                                  |
| serialNumber               | SerialNumber                                                                                                                                                                           |
| userId                     | Eindeutiger Bezeichner für den Benutzer, der dem Gerät zugeordnet ist.                                                                                                                           |
| rowLastModifiedDateTimeUTC | UTC-Zeitpunkt, zu dem dieses Gerät zuletzt in Data Warehouse geändert wurde.                                                                                                       |
| Hersteller               | Der Hersteller der CPU                                                                                                                                                             |
| model                      | Gerätemodell                                                                                                                                                                    |
| operatingSystem            | Betriebssystem des Geräts. Windows, iOS/iPadOS, Android usw.                                                                                                                                   |
| isDeleted                  | Binärwert, der anzeigt, ob das Gerät gelöscht wurde oder nicht.                                                                                                                                 |
| androidSecurityPatchLevel  | Android-Sicherheitspatchebene                                                                                                                                                           |
| MEID                       | MEID                                                                                                                                                                                   |
| isSupervised               | Gibt an, ob das Gerät überwacht wird.                                                                                                                                                               |
| freeStorageSpaceInBytes    | Freier Speicherplatz in Bytes.                                                                                                                                                                 |
| totalStorageSpaceInBytes   | Speicherplatz insgesamt in Bytes.                                                                                                                                                                |
| encryptionState            | In diesem Feld wird der Verschlüsselungsstatus des Geräts angezeigt.                                                                                                                                                      |
| subscriberCarrier          | Netzbetreiber des Abonnenten des Geräts                                                                                                                                                       |
| phoneNumber                | Telefonnummer des Geräts                                                                                                                                                             |
| IMEI                       | IMEI                                                                                                                                                                                   |
| cellularTechnology         | Mobilfunktechnologie des Geräts                                                                                                                                                    |
| WiFiMacAddress             | WiFi-MAC                                                                                                                                                                              |
| ICCID                       | Integrated Circuit Card Identifier                                                                                                                                                     |

## <a name="devicepropertyhistories"></a>devicePropertyHistories

Die Entität **devicePropertyHistory** hat die gleichen Eigenschaften wie die Gerätetabellen und die täglichen Momentaufnahmen der einzelnen Gerätedatensätze pro Tag für die letzten 90 Tage. Die DateKey-Spalte gibt den Tag für jede Zeile an.

|          Eigenschaft          |                                                                                      Beschreibung                                                                                     |
|:--------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| dateKey                    | Verweis auf die Datumstabelle, die den Tag angibt                                                                                                                                          |
| deviceKey                  | Der eindeutige Bezeichner des Geräts in Data Warehouse – Ersatzschlüssel. Dies ist ein Verweis auf die Gerätetabelle, die die Intune-Geräte-ID enthält.                               |
| deviceName                 | Der Name des Geräts auf Plattformen, die das Benennen von Geräten ermöglichen. Auf anderen Plattformen wird von Intune einen Namen aus anderen Eigenschaften erstellt. Dieses Attribut kann nicht für alle Geräte zur Verfügung stehen. |
| deviceRegistrationStateKey | Schlüssel des Attributs für den Geräteregistrierungsstatus dieses Geräts.                                                                                                                    |
| ownerTypeKey               | Schlüssel des Besitzertypattributs für dieses Gerät: Unternehmen, persönlich oder unbekannt.                                                                                                  |
| managementStateKey         | Der Schlüssel des Verwaltungsstatus, der mit diesem Gerät verknüpft ist und den neuesten Zustand einer Remoteaktion angibt oder anzeigt, ob das Gerät per Jailbreak oder Rootzugriff manipuliert wurde.                                                |
| azureADRegistered          | Gibt an, ob das Gerät in Azure Active Directory registriert ist.                                                                                                                             |
| complianceStateKey         | Ein Schlüssel zum Konformitätsstatus.                                                                                                                                                            |
| OSVersion                  | Betriebssystemversion                                                                                                                                                                          |
| jailBroken                 | Gibt an, ob das Gerät mit Jailbreak oder Rooting manipuliert wurde.                                                                                                                                         |
| deviceCategoryKey          | Schlüssel des Gerätekategorieattributs für dieses Gerät. 

