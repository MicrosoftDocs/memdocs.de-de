---
title: Einrichten des Check Point SandBlast MTD-Connectors mit Intune
titleSuffix: Microsoft Intune
description: Hier finden Sie Informationen zum Integrieren von Check Point SandBlast Mobile Threat Defense in Intune, um den Zugriff mobiler Geräte auf Ihre Unternehmensressourcen zu steuern.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 706a4228-9bdf-41e0-b8d1-64c923dd2d2b
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a0645c771b304bfb4930f5cd365b9291366499b1
ms.sourcegitcommit: 42a4a4454e56fa681f0ad39f5e585492dfbad286
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330915"
---
# <a name="check-point-sandblast-mobile-threat-defense-connector-with-intune"></a>Check Point SandBlast Mobile Threat Defense-Connector in Intune

Sie können den Zugriff mobiler Geräte auf Unternehmensressourcen mithilfe des bedingten Zugriffs basierend auf Risikobewertungen steuern, die von Check Point SandBlast Mobile vorgenommen werden, einer Mobile Threat Defense-Lösung, die in Microsoft Intune integriert werden kann. Das Risiko wird basierend auf Telemetriedaten von Geräten bewertet, auf denen die Check Point SandBlast Mobile-App ausgeführt wird.

Sie können Richtlinien für bedingten Zugriff basierend auf der Check Point SandBlast Mobile-Risikobewertung konfigurieren, die über Intune-Gerätekonformitätsrichtlinien aktiviert wird, und so anhand der erkannten Bedrohungen den Zugriff auf Unternehmensressourcen durch nicht konforme Geräte zulassen oder blockieren.

> [!NOTE]
> Dieser Mobile Threat Defense-Anbieter wird für nicht registrierte Geräte nicht unterstützt.

## <a name="supported-platforms"></a>Unterstützte Plattformen

- **Android 4.1 und höher**

- **iOS 8 und höher**

## <a name="pre-requisites"></a>Voraussetzungen

- Azure Active Directory Premium

- Microsoft Intune-Abonnement

- Check Point SandBlast Mobile Threat Defense-Abonnement
  - Weitere Informationen finden Sie auf der [CheckPoint SandBlast-Website](https://www.checkpoint.com/).

## <a name="how-do-intune-and-check-point-sandblast-mobile-help-protect-your-company-resources"></a>Wie können Sie mit Intune und Check Point SandBlast Mobile Ihre Unternehmensressourcen schützen?

Die Check Point SandBlast Mobile-App für Android und iOS/iPadOS erfasst Telemetriedaten des Dateisystems, des Netzwerkstapels sowie von Geräten und Anwendungen, sofern verfügbar, und sendet diese dann an den Check Point SandBlast-Clouddienst, mit dessen Hilfe die Anfälligkeit des Geräts für mobile Bedrohungen bewertet wird.

Die Intune-Gerätekompatibilitätsrichtlinie enthält eine Regel für Check Point SandBlast Mobile Threat Defense, die auf der Check Point SandBlast-Risikobewertung basiert. Wenn diese Regel aktiviert ist, bewertet Intune die Gerätekompatibilität mit der von Ihnen aktivierten Richtlinie. Wird das Gerät als nicht kompatibel eingestuft, wird der Zugriff auf Ressourcen wie Exchange Online und SharePoint Online für Benutzer blockiert. Benutzer erhalten zudem einen Leitfaden von der auf ihren Geräten installierten Check Point SandBlast Mobile-App, um das Problem zu beheben und den Zugriff auf Unternehmensressourcen zurückzuerlangen.

Hier einige gängige Szenarios:

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Steuern des Zugriffs basierend auf Bedrohungen durch Apps, die Schadsoftware enthalten

Wenn Apps, die Schadsoftware enthalten, auf Geräten erkannt werden, können Sie Geräte blockieren, bis die Bedrohung beseitigt ist:

- Herstellen einer Verbindung mit Unternehmens-E-Mail

- Synchronisieren von Unternehmensdateien mithilfe der OneDrive for Work-App

- Zugreifen auf Unternehmens-Apps

*Blockieren, wenn Apps mit Schadsoftware entdeckt werden:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD blockiert, wenn Apps mit Schadsoftware entdeckt werden](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-2.PNG)

*Zugriff nach Beseitigung gewährt:*

> [!div class="mx-imgBorder"]
> ![Zugriff für Check Point MTD gewährt](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-3.PNG)

### <a name="control-access-based-on-threat-to-network"></a>Steuern des Zugriffs basierend auf Bedrohung für das Netzwerk

Erkennen Sie Bedrohungen wie **Man-in-the-Middle** im Netzwerk, und schützen Sie den Zugriff auf WLAN-Netzwerke auf der Grundlage des Geräterisikos.

*Blockieren des Netzwerkzugriffs über WLAN:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD blockiert den Netzwerkzugriff über WLAN](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-4.PNG)

*Zugriff nach Beseitigung gewährt:*

> [!div class="mx-imgBorder"]
> ![Zugriff für Check Point MTD über WLAN gewährt](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-5.PNG)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Steuern des Zugriffs auf SharePoint Online basierend auf Netzwerkbedrohungen

Erkennen von Bedrohungen wie **Man-in-the-Middle** im Netzwerk und Verhindern der Synchronisierung von Unternehmensdateien auf der Grundlage des Geräterisikos.

*Blockieren des Zugriffs auf SharePoint Online bei Erkennen von Bedrohungen für das Netzwerk*

> [!div class="mx-imgBorder"]
> ![Check Point MTD blockiert den Zugriff auf SharePoint Online](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-6.PNG)

*Zugriff nach Beseitigung gewährt:*

> [!div class="mx-imgBorder"]
> ![Zugriff für Check Point MTD auf SharePoint Online gewährt](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-7.PNG)

<!-- ### Control access on unenrolled devices based on threats from malicious apps

When the Check Point Sandblast Mobile Threat Defense solution considers a device to be infected:
> [!div class="mx-imgBorder"]
> ![App protection policy blocks due to detected malware](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/sandblast-app-policy-block.png)

Access is granted on remediation:

> [!div class="mx-imgBorder"]
> ![Access is granted on remediation for App protection policy](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/sandblast-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Nächste Schritte

- [Integrieren von Check Point SandBlast in Intune](checkpoint-sandblast-mobile-mtd-connector-integration.md)

- [Einrichten von Check Point SandBlast Mobile-Apps](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Erstellen einer Mobile Threat Defense-Gerätekompatibilitätsrichtlinie (MTD) mit Intune](mtd-device-compliance-policy-create.md)

- [Aktivieren von Mobile Threat Defense in Intune](mtd-connector-enable.md)
