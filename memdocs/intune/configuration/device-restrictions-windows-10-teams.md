---
title: Microsoft Intune-Geräteeinschränkungen für Windows 10 Team
titleSuffix: ''
description: In diesem Artikel erfahren Sie etwas über die verfügbaren Geräteeinschränkungen für Windows 10 Team-Geräte.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 3/6/2018
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 31457667612617bb573ddfb145ed26f70de33159
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79361652"
---
# <a name="microsoft-intune-windows-10-team-device-restriction-settings"></a>Einstellungen für Geräteeinschränkungen für Windows 10 Team in Microsoft Intune

In diesem Artikel erhalten Sie Informationen zu den Einstellungen für Microsoft Intune-Geräteeinschränkungen, die Sie für Windows 10 Team-Geräte konfigurieren können.

## <a name="apps-and-experience"></a>Apps und Benutzerfreundlichkeit

- **Bildschirm aktivieren, wenn eine Person im Raum ist:** Erlaubt das automatische Aktivieren des Geräts, wenn der Sensor eine Person im Raum erkennt.
- **Anzeige von Besprechungsinformationen auf dem Willkommensbildschirm:** Aktivieren Sie diese Option, um die Informationen auszuwählen, die auf der Kachel „Besprechungen“ auf dem Willkommensbildschirm angezeigt werden. Sie können:
  - **Nur Organisator und Zeit anzeigen**
  - **Organisator, Zeit und Thema anzeigen (Thema bei privaten Besprechungen ausblenden)**
- **URL für Hintergrundbild des Willkommensbildschirms:** Aktivieren Sie diese Einstellung, um auf dem **Willkommensbildschirm** von Windows 10 Team-Geräten einen benutzerdefinierten Hintergrund aus der angegebenen URL anzuzeigen.<br>Das Bild muss im PNG-Format vorliegen und die URL muss mit **https://** beginnen.

## <a name="azure-operational-insights"></a>Azure Operational Insights

- **Azure Operational Insights:** Azure Operational Insights ist Teil der Microsoft Operations Manager-Suite und sammelt, speichert und analysiert Protokolldateidaten von Windows 10-Team-Geräten.
Sie müssen eine **Arbeitsbereichs-ID** und einen **Arbeitsbereichsschlüssel** angeben, um die Verbindung mit Azure Operational Insights herstellen zu können.

## <a name="maintenance"></a>Wartung

- **Wartungsfenster für Updates:** Konfiguriert das Fenster, in dem Updates am Gerät vorgenommen werden können. Sie können die **Startzeit** des Fensters und **Dauer in Stunden** (1 bis 5 Stunden) konfigurieren.

## <a name="wireless-projection"></a>Drahtlose Projektion

- **PIN für Funkprojektion:** Gibt an, ob Sie eine PIN eingeben müssen, bevor Sie die drahtlosen Projektionsfunktionen des Geräts verwenden können.
- **Miracast-Funkprojektion:** Aktivieren Sie diese Option, wenn Sie auf dem Gerät mit Windows 10-Team erlauben möchten, für Miracast aktivierte Geräte zum Projizieren zu verwenden.
- **Kanal für die Miracast-Funkprojektion**: Wählen Sie den Miracast-Kanal aus, der zum Herstellen der Verbindung verwendet wird.

## <a name="next-steps"></a>Nächste Schritte

Verwenden Sie die Informationen unter [Konfigurieren von Einstellungen für Geräteeinschränkungen](device-restrictions-configure.md), um das Profil zu speichern und es Benutzern und Geräten zuzuweisen.
