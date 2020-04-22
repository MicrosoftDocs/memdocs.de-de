---
title: Anzeigen von Gerätedetails mit Microsoft Intune – Azure | Microsoft-Dokumentation
description: Zeigen Sie Details zu Ihren Geräten an, z.B. Betriebssystem, Speicherplatz, Hersteller und Modell. Mit Microsoft Intune in Azure können Sie eine Liste der installierten Apps abrufen, Konformitätsrichtlinien überprüfen und TeamViewer einrichten. Die Vorgehensweise ähnelt der Anzeige des Bestands der Geräte, die Sie verwalten.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: e71c6bdb-d75c-404f-8e38-24a663be81c2
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed5ff548d28a5bc973c43c84861b9b256b41a203
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80696290"
---
# <a name="see-device-details-in-intune"></a>Anzeigen von Gerätedetails in Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Das Feature **Geräte** bietet zusätzliche Informationen zu den von Ihnen verwalteten Geräten, z.B. zur Hardware und zu installierten Apps.

Dieser Artikel erläutert, wie Sie all Ihre Geräte und deren Eigenschaften im Azure-Portal anzeigen.

## <a name="view-the-device-details"></a>Anzeigen der Gerätedetails

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
3. Klicken Sie auf **Geräte** > **Alle Geräte**, und wählen Sie anschließend eins der aufgeführten Geräte aus, damit dessen Gerätedetails geöffnet werden:

   - In der **Übersicht** werden der Gerätename und einige wichtige Eigenschaften des Geräts aufgeführt, z. B. ob es sich um ein privates oder Unternehmensgerät handelt, Seriennummer, primärer Benutzer und mehr. Auf diesem Gerät können Sie die folgenden Aktionen ausführen:
      - [Außerkraftsetzen](devices-wipe.md#retire)
      - [Zurücksetzen](devices-wipe.md#wipe)
      - [Löschen](devices-wipe.md#delete-devices-from-the-intune-portal)
      - [Remotesperre](device-remote-lock.md)
      - [Synchronisieren](device-sync.md)
      - [Kennung zurücksetzen](device-passcode-reset.md)
      - [Neu starten](device-restart.md) (nur Windows)
      - [Sauberer Start](device-fresh-start.md) (nur Windows)
      - [Autopilot-Zurücksetzung](/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset) (nur Windows)
      - [Schnellüberprüfung](../configuration/device-restrictions-windows-10.md) (nur Windows 10)
      - [Vollständige Überprüfung](../configuration/device-restrictions-windows-10.md) (nur Windows 10)
      - Windows Defender-Sicherheitsinformationen aktualisieren
      - [BitLocker-Schlüsselrotation](https://docs.microsoft.com/mem/intune/protect/encrypt-devices#to-rotate-the-bitlocker-recovery-key)
      - [Gerät umbenennen](device-rename.md)
      - [Neue Remoteunterstützungssitzung](https://docs.microsoft.com/mem/intune/remote-actions/teamviewer-support)
   - Verwenden Sie die **Eigenschaften**, um eine [von Ihnen erstellte Gerätekategorie](../enrollment/device-group-mapping.md) zuzuweisen, und ändern Sie den Besitz des Geräts in ein privates oder ein unternehmenseigenes Gerät.
   - Unter **Hardware** werden viele Details über das Gerät aufgeführt, z. B. die Geräte-ID, das Betriebssystem und die Version, der Speicherplatz und weitere Details.
   - Unter **Ermittelte Apps** werden alle auf dem Gerät installierten Apps aufgeführt, die von Intune gefunden wurden. Weitere Informationen finden Sie unter [Von Intune ermittelte Apps](../apps/app-discovered-apps.md).
   - Unter **Gerätekonformität** werden alle zugewiesenen Konformitätsrichtlinien aufgeführt, und es wird angezeigt, ob das Gerät mit diesen Richtlinien konform ist.
   - Unter **Gerätekonfiguration** werden alle Gerätekonfigurationsrichtlinien angezeigt, die dem Gerät zugewiesen sind, und Sie können erkennen, ob die Richtlinie erfolgreich war oder fehlgeschlagen ist.
   - **App-Konfiguration** 
   - **Konfiguration der Endpunktsicherheit**
   - **Wiederherstellungsschlüssel** zeigt die verfügbaren BitLocker-Schlüssel für das Gerät an.
   - **Verwaltete Apps** listet alle verwalteten Apps auf, die von Intune konfiguriert und auf dem Gerät bereitgestellt wurden. 

## <a name="hardware-device-details"></a>Details zum Hardwaregerätestatus
Je nach Netzbetreiber der Geräte werden möglicherweise nicht alle Details erfasst.

> [!Note]  
> Der Hardware- und Softwarebestand wird im Intune-Dienst alle 7 Tage aktualisiert.

|Detail|Description|Plattform| 
|--------------|----------------------|----|  
|Name|Der Name des Geräts.|Windows, iOS|
|Verwaltungsname|Der Gerätename, der nur in der Konsole verwendet wird. Durch das Ändern dieses Namens wird nicht gleichzeitig der Name des Geräts geändert.|Windows, iOS|
|UDID|Eindeutige Geräte-ID.|Windows, iOS|
|Intune-Geräte-ID|Eine Geräte-ID, die das Gerät eindeutig bezeichnet.|Windows, iOS|
|Seriennummer|Die vom Hersteller für das Gerät vergebene Seriennummer.|Windows, iOS|
|Freigegebenes Gerät|Wenn **Ja** ausgewählt ist, wird das Gerät für mehr als einen Benutzer freigegeben.|Windows, iOS|
|Durch den Benutzer genehmigte Registrierung|Wenn **Ja** angegeben wird, besitzt das Gerät eine vom Benutzer genehmigte Registrierung, mit der Administratoren bestimmte Sicherheitseinstellungen auf dem Gerät verwalten können.|Windows, iOS|
|Betriebssystem|Das auf dem Gerät verwendete Betriebssystem.|Windows, iOS|
|Betriebssystemversion|Die Version des Betriebssystems auf dem Gerät.|Windows, iOS|
|Betriebssystemsprache|Die für das Betriebssystem auf dem Gerät festgelegte Sprache.|Windows, iOS|
|Buildnummer|Gibt die Buildnummer des Betriebssystems an.|Android|
|Sicherheitspatchebene|Die Sicherheitspatchebene für das Gerät|Android|
|Gesamtmenge des Speicherplatzes|Der gesamte Speicherplatz auf dem Gerät (in GB).|Windows, iOS|
|Freier Speicherplatz|Der gesamte freie Speicherplatz auf dem Gerät (in GB).|Windows, iOS|
|IMEI|Die International Mobile Equipment Identity des Geräts.|Windows, iOS/iPadOS, Android|
|MEID|Der Mobile Equipment Identifier des Geräts.|Windows, iOS/iPadOS, Android|
|Hersteller|Der Hersteller des Geräts.|Windows, iOS/iPadOS, Android|
|Modell|Das Gerätemodell.|Windows, iOS/iPadOS, Android|
|Telefonnummer|Die dem Gerät zugewiesene Telefonnummer.|Windows, iOS/iPadOS, Android*|
|Netzbetreiber des Abonnenten|Der Mobilfunkanbieter des Geräts.|Windows, iOS/iPadOS, Android|
|Mobilfunktechnologie|Das vom Gerät verwendete Funksystem.|Windows, iOS/iPadOS, Android|
|WiFi-MAC|Die Media Access Control-Adresse des Geräts.|Windows, iOS/iPadOS, Android|
|ICCID|Der Integrated Circuit Card Identifier, die eindeutige Identifikationsnummer der SIM-Karte.|Windows, iOS/iPadOS, Android|
|Registrierungsdatum|Datum und Uhrzeit der Registrierung des Gerät bei Intune.|Windows, iOS/iPadOS, Android|
|Letzter Kontakt|Datum und Uhrzeit der letzten Verbindung des Gerät bei Intune.|Windows, iOS/iPadOS, Android|
|Code zur Umgehung der Aktivierungssperre|Der Code, mit dem die Aktivierungssperre deaktiviert werden kann.|iOS|
|Registriert bei Azure AD|Wenn **Ja** ausgewählt ist, wurde das Gerät bei Azure Active Directory registriert.|Windows, iOS/iPadOS, Android|
|Für Intune registriert|Wenn **Ja** angegeben wird, wurde das Gerät bei Intune registriert.|Windows, iOS/iPadOS, Android|
|Konformität|Der Konformitätszustand des Geräts.|Windows, iOS/iPadOS, Android|
|EAS aktiviert|Wenn **Ja** ausgewählt ist, ist das Gerät mit einem Exchange-Postfach synchronisiert.|Windows, iOS/iPadOS, Android|
|EAS-Aktivierungs-ID|Die Exchange ActiveSync-ID des Geräts.|Windows, iOS/iPadOS, Android|
|Überwacht|Wenn **Ja** ausgewählt ist, haben die Administratoren die Kontrolle über das Gerät verbessert.|Windows, iOS/iPadOS, Android|
|Verschlüsselt|Wenn **Ja** ausgewählt ist, werden die auf dem Gerät gespeicherten Daten verschlüsselt.|Windows, iOS/iPadOS, Android|

> [!Note]  
> Die Telefonnummer wird auf dedizierten oder vollständig verwalteten Android Enterprise-Geräten nicht inventarisiert.

## <a name="next-steps"></a>Nächste Schritte
Finden Sie heraus, welche Aktionen beim [Verwalten Ihrer Geräte](device-management.md) mit Intune noch möglich sind.
