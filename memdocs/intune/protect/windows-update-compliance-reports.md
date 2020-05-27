---
title: Verwenden von Berichten zur Updatekonformität für Windows Updates in Microsoft Intune
titleSuffix: Microsoft Intune
description: Verwenden von OMS-Updatekonformität zum Abrufen von Berichtsdaten für Windows Update, die mit Intune bereitgestellt werden
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: b4ef3a4c2ba539cc507ef413a4648b42e246b11d
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990906"
---
# <a name="intune-compliance-reports-for-updates"></a>Berichte zur Updatekonformität für Intune

Wenn Sie Intune verwenden, um Windows-Updates auf Windows 10-Geräten bereitzustellen, können Sie mithilfe von Intune oder der kostenlosen Lösung *Updatekonformität* Details zur Updatekonformität abrufen. Updatekonformität ist Teil der Microsoft Operations Management Suite (OMS).

## <a name="use-intune"></a>Verwenden von Intune

Gehen Sie wie folgt vor, um Richtlinienberichte zum Bereitstellungsstatus für die von Ihnen konfigurierten Windows 10-Updateringe zu prüfen:

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Übersicht** > **Softwareupdatestatus** aus. Hier finden Sie allgemeine Informationen zum Status der Updateringe, die Sie zugewiesen haben.

3. Wählen Sie **Überwachen** aus, um weitere Details anzuzeigen. Wählen Sie dann unter **Softwareupdates** die Option **Bereitstellungsstatus pro Updatering** aus, und wählen Sie den zu überprüfenden Bereitstellungsring aus.

   Wählen Sie im Abschnitt **Überwachen** einen der folgenden Berichte aus, um weitere Informationen zum Updatering anzuzeigen:

   - **Gerätestatus**: Hiermit wird der Status der Gerätekonfiguration angezeigt. Weitere Informationen finden Sie unter [Aktualisieren von deviceConfigurationDeviceStatus]( https://docs.microsoft.com/graph/api/intune-deviceconfig-deviceconfigurationdevicestatus-update?view=graph-rest-1.0).

   - **Benutzerstatus**: Hiermit werden der Benutzername, der Status und das Datum des letzten Berichts angezeigt. Weitere Informationen finden Sie unter [Auflisten von deviceConfigurationUserStatus](https://docs.microsoft.com/graph/api/intune-deviceconfig-deviceconfigurationuserstatus-list?view=graph-rest-1.0).

   - **Endbenutzer-Updatestatus**: Hiermit wird der Updatestatus der Windows-Geräte angezeigt. Weitere Informationen finden Sie unter [windowsUpdateState](https://docs.microsoft.com/graph/api/resources/intune-shared-windowsupdatestate?view=graph-rest-beta).

## <a name="use-update-compliance"></a>Verwenden der Updatekonformität

Sie können Windows 10-Updaterollouts mithilfe der [Updatekonformität](https://technet.microsoft.com/itpro/windows/manage/update-compliance-monitor) überwachen. Die Updatekonformität wird im Azure-Portal angeboten und ist für Geräte kostenlos, die die entsprechenden [Voraussetzungen](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started#update-compliance-prerequisites) erfüllen.  

Bei Verwendung dieser Lösung können Sie eine Organisations-ID für jedes Ihrer mit Intune verwalteten Windows 10-Geräte bereitstellen, für das Sie Updateüberwachungsberichte verwenden möchten.  

Die Organisations-ID können Sie in Intune mithilfe der OMA-URI-Einstellungen einer benutzerdefinierten Richtlinie konfigurieren. Siehe [Verwenden von benutzerdefinierten Einstellungen für Windows 10-Geräte in Intune](../configuration/custom-settings-windows-10.md).

Der OMA-URI-Pfad (Groß-/Kleinschreibung beachten) zum Konfigurieren der Organisations-ID lautet *./Vendor/MSFT/DMClient/Provider/MS DM Server/CommercialID*.

Unter **OMA-URI-Einstellung hinzufügen oder bearbeiten** können Sie beispielsweise folgende Werte verwenden:

- **Einstellungsname**: Kommerzielle Windows Analytics-ID
- **Einstellungsbeschreibung**: Konfigurieren der kommerziellen ID für Windows Analytics-Lösungen
- **OMA-URI** (Groß-/Kleinschreibung beachten): *./Vendor/MSFT/DMClient/Provider/MS DM Server/CommercialID*
- **Datentyp**: Zeichenfolge
- **Wert:** \<Verwenden Sie die GUID, die in Ihrem OMS-Arbeitsbereich auf der Registerkarte „Windows-Telemetrie“ angezeigt wird>

> [!NOTE]
> Weitere Informationen über MS DM-Server finden Sie unter [DMClient configuration service provider (CSP) (DMClient-Konfigurationsdienstanbieter (CSP))]( https://docs.microsoft.com/windows/client-management/mdm/dmclient-csp).

## <a name="next-steps"></a>Nächste Schritte

[Verwalten von Softwareupdates in Intune](windows-update-for-business-configure.md)
