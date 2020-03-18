---
title: Remoteverwaltung von Geräten in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Anzeigen der für die Verwendung von TeamViewer erforderlichen Rollen, Installieren des TeamViewer Connectors und ausführliche Anleitung zur Remoteverwaltung von Geräten mit Microsoft Intune im Azure-Portal
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 72cdd888-efca-46e6-b2e7-fb9696bb2fba
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b63dbf983872dbbb1c792e1f5d00bb136da973a1
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79348847"
---
# <a name="use-teamviewer-to-remotely-administer-intune-devices"></a>Verwenden von TeamViewer für die Remoteverwaltung von Intune-Geräten

Von Intune verwaltete Geräte können mit [TeamViewer](https://www.teamviewer.com) remote verwaltet werden. TeamViewer ist ein Drittanbieterprogramm, das Sie separat erwerben können. In diesem Thema erfahren Sie, wie Sie TeamViewer in Intune konfigurieren und wie Sie ein Gerät remote verwalten können. 

## <a name="prerequisites"></a>Voraussetzungen

- Verwenden Sie ein unterstütztes Gerät. Mit Intune verwaltete Android Device Admin-, Android-Arbeitsprofil-, Windows-, iOS-/iPadOS- und macOS-Geräte unterstützen Remoteverwaltung. TeamViewer bietet möglicherweise keine Unterstützung für Windows Holographic (HoloLens), Windows Team (Surface Hub) oder Windows 10 S. Unter [TeamViewer](https://www.teamviewer.com) finden Sie für sämtliche Updates Informationen zu Unterstützungsmöglichkeiten.

> [!NOTE]
> Dedizierte und vollständig verwaltete Android-Geräte werden nicht unterstützt.

- Der Intune-Administrator im Azure-Portal muss über folgende [Intune-Rollen](../fundamentals/role-based-access-control.md) verfügen:  

  - **Aktualisieren von Remoteunterstützung:** Ermöglicht es Administratoren, die Einstellungen für den TeamViewer Connector zu ändern
  - **Anfordern von Remoteunterstützung:** Ermöglicht es Administratoren, für jeden Benutzer eine neue Remoteunterstützungssitzung zu starten. Benutzer mit dieser Rolle werden nicht durch eine Intune-Rolle innerhalb eines Bereichs beschränkt. Darüber hinaus können Benutzer- oder Gerätegruppen, denen eine Intune-Rolle innerhalb eines Bereichs zugewiesen ist, auch Remoteunterstützung anfordern. 

- Ein [TeamViewer](https://www.teamviewer.com)-Konto mit den Anmeldeinformationen. Möglicherweise unterstützen nur einige TeamViewer-Lizenzen die Integration in Intune. Weitere Informationen zu besonderen TeamViewer-Anforderungen finden Sie unter [TeamViewer Integration für Microsoft Intune in Azure](https://www.teamviewer.com/integrations/microsoft-intune/).

Durch die Verwendung von TeamViewer ermöglichen Sie es dem TeamViewer Connector für Intune TeamViewer-Sitzungen zu erstellen, Active Directory-Daten zu lesen und das Zugriffstoken des TeamViewer-Kontos zu speichern.

## <a name="configure-the-teamviewer-connector"></a>Konfigurieren des TeamViewer Connectors

Zur Bereitstellung der Remoteunterstützung für Geräte müssen Sie den TeamViewer Connector für Intune anhand der folgenden Schritte konfigurieren:

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Mandantenverwaltung** > **Connectors und Token** > **TeamViewer-Connector** aus.
3. Wählen Sie **Verbinden** aus, und akzeptieren Sie anschließend die Lizenzbedingungen.
4. Wählen Sie **Log in to TeamViewer to authorize** (Zum Autorisieren bei TeamViewer anmelden) aus.
5. Auf der TeamViewer-Website wird eine Webseite geöffnet. Geben Sie die Anmeldeinformationen für Ihre TeamViewer-Lizenz ein, und klicken Sie anschließend auf **Anmelden**.

## <a name="remotely-administer-a-device"></a>Remoteverwaltung eines Geräts

Nach der Konfiguration des Connectors können Sie ein Gerät remote verwalten. Gehen Sie wie folgt vor: 

1. Im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Klicken Sie auf **Geräte** und dann auf **Alle Geräte**.
3. Wählen Sie aus der Liste das Gerät aus, das Sie remote verwalten möchten, und navigieren Sie zu **...**  > **Neue Remoteunterstützungssitzung**.
4. Nachdem Intune eine Verbindung mit dem TeamViewer-Dienst hergestellt hat, werden Informationen über das Gerät angezeigt. Wählen Sie **Verbinden** aus, um die Remotesitzung zu starten.

![Verwenden von TeamViewer für die Remoteverwaltung eines Android-Geräts – Beispiel](./media/teamviewer-support/android-teamviewer.png)

Beim Starten einer Remotesitzung wird dem Benutzer auf seinem Gerät ein Benachrichtigungskennzeichen auf dem Symbol der Unternehmensportal-App angezeigt. Beim Öffnen der App wird ebenfalls eine Benachrichtigung angezeigt. Dann kann der Benutzer die Remoteunterstützungsanforderung annehmen.

> [!NOTE]
> Windows-Geräte, die mithilfe von Methoden wie DEM und WCD registriert werden, die nicht vom Benutzer ausgeführt werden, zeigen die TeamViewer-Benachrichtigung nicht in der Unternehmensportal-App an. In diesen Szenarios wird die Verwendung des TeamViewer-Portals empfohlen, um die Sitzung zu erstellen.

In TeamViewer können Sie einige Aktionen auf dem Gerät ausführen. Dazu zählt die Übernahme der Kontrolle über das Gerät. Alle Einzelheiten zu Ihren Möglichkeiten finden Sie im [TeamViewer-Leitfaden](https://www.teamviewer.com/support/documents/).

Wenn Sie fertig sind, schließen Sie das TeamViewer-Fenster.
