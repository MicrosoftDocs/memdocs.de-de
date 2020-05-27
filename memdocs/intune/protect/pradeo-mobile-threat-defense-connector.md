---
title: Mobile Threat Defense-Connector Pradeo in Intune
titleSuffix: Intune on Azure
description: Erfahren Sie, wie Sie den Pradeo Mobile Threat Defense-Connector mit Intune integrieren, um den Zugriff von mobilen Geräten auf Ihre Unternehmensressourcen zu steuern.
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
ms.assetid: cde4d389-1770-4226-85a3-a2f3b3fb92a3
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5cde4c4e90004dd9bb287b9e86f9dfcc541e4a33
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83984958"
---
# <a name="pradeo-mobile-threat-defense-connector-with-intune"></a>Mobile Threat Defense-Connector Pradeo in Intune

Sie können den Zugriff mobiler Geräte auf Unternehmensressourcen mithilfe des bedingten Zugriffs basierend auf Risikobewertungen steuern, die von Pradeo vorgenommen werden, einer Mobile Threat Defense-Lösung (MTD), die in Microsoft Intune integriert werden kann. Das Risiko wird basierend auf Telemetriedaten von Geräten bewertet, auf denen die Pradeo-App ausgeführt wird.

Sie können Richtlinien für bedingten Zugriff basierend auf der Pradeo-Risikobewertung konfigurieren, die über Intune-Gerätekonformitätsrichtlinien aktiviert wird, und so anhand der erkannten Bedrohungen den Zugriff auf Unternehmensressourcen durch nicht konforme Geräte zulassen oder blockieren.

> [!NOTE]
> Dieser Mobile Threat Defense-Anbieter wird für nicht registrierte Geräte nicht unterstützt.

## <a name="supported-platforms"></a>Unterstützte Plattformen

- **Android 4.0.3 und höher**

- **iOS 7 und höher**

## <a name="prerequisites"></a>Voraussetzungen

- Azure Active Directory Premium

- Microsoft Intune-Abonnement

- Pradeo Security für Mobile Threat Defense-Abonnements

  - Weitere Informationen finden Sie auf der [Pradeo-Website](https://www.pradeo.com/en-US/mobile-threat-protection).

## <a name="how-do-intune-and-pradeo-help-protect-your-company-resources"></a>Wie helfen Intune und Pradeo beim Schutz von Unternehmensressourcen?

Die Pradeo-App für Android oder iOS/iPadOS erfasst Telemetriedaten des Dateisystems, Netzwerkstapels sowie von Geräten und Anwendungen, sofern verfügbar, und sendet diese dann an den Pradeo-Clouddienst, mit dessen Hilfe die Anfälligkeit des Geräts für mobile Bedrohungen bewertet wird.

Die Intune-Gerätekonformitätsrichtlinie enthält eine Regel für Pradeo Mobile Threat Defense, die auf der Pradeo-Risikobewertung basiert. Wenn diese Regel aktiviert ist, bewertet Intune die Gerätekompatibilität mit der von Ihnen aktivierten Richtlinie. Wird das Gerät als nicht kompatibel eingestuft, wird der Zugriff auf Ressourcen wie Exchange Online und SharePoint Online für Benutzer blockiert. Benutzer erhalten zudem einen Leitfaden von der auf ihren Geräten installierten Pradeo-App, um das Problem zu beheben und den Zugriff auf Unternehmensressourcen zurückzuerlangen.

## <a name="sample-scenarios"></a>Beispielszenarios

Es folgen einige gängige Szenarios.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Steuern des Zugriffs basierend auf Bedrohungen durch Apps, die Schadsoftware enthalten

Wenn Apps, die Schadsoftware enthalten, auf Geräten erkannt werden, können Sie Geräte an folgenden Aktionen hindern, bis die Bedrohung beseitigt ist:

- Herstellen einer Verbindung mit Unternehmens-E-Mail

- Synchronisieren von Unternehmensdateien mithilfe der OneDrive for Work-App

- Zugreifen auf Unternehmens-Apps

*Blockieren, wenn Apps mit Schadsoftware entdeckt werden:*

![Darstellung des Szenarios, wenn Apps mit Schadsoftware erkannt werden](./media/pradeo-mobile-threat-defense-connector/pradeo-maliciousapps-blocked.png)

*Nach Korrektur erteilter Zugriff:*

![Apps mit Schadsoftware entdeckt, Zugriff gewährt](./media/pradeo-mobile-threat-defense-connector/pradeo-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Steuern des Zugriffs basierend auf Bedrohung für das Netzwerk

Erkennen von Bedrohungen wie **Man-in-the-Middle-Angriffe** für Ihr Netzwerk und Schützen des Zugriffs auf WLAN-Netzwerke basierend auf dem Geräterisiko.

*Blockieren des Netzwerkzugriffs über WLAN:*

![Blockieren des Netzwerkzugriffs über WLAN](./media/pradeo-mobile-threat-defense-connector/pradeo-network-wifi-blocked.png)

*Nach Korrektur erteilter Zugriff:*

![Darstellung des Szenarios, wenn der Zugriff nach der Behebung wieder erteilt wird](./media/pradeo-mobile-threat-defense-connector/pradeo-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Steuern des Zugriffs auf SharePoint Online basierend auf der Bedrohung für das Netzwerk

Erkennen von Bedrohungen wie **Man-in-the-Middle-Angriffe** für Ihr Netzwerk und Verhindern der Synchronisierung von Unternehmensdateien basierend auf dem Geräterisiko.

*Blockieren des Zugriffs auf SharePoint Online bei Erkennen von Bedrohungen für das Netzwerk*

![Blockieren von SharePoint Online bei Erkennung von Bedrohungen für das Netzwerk](./media/pradeo-mobile-threat-defense-connector/pradeo-network-spo-blocked.png)

*Nach Korrektur erteilter Zugriff:*

![Darstellung des Szenarios für das Sharepoint-Beispiel, wenn der Zugriff nach der Behebung wieder erteilt wird](./media/pradeo-mobile-threat-defense-connector/pradeo-network-spo-unblocked.png)

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Pradeo Mobile Threat Defense solution considers a device to be infected:

![App protection policy blocks due to detected malware](./media/pradeo-mobile-threat-defense-connector/pradeo-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/pradeo-mobile-threat-defense-connector/pradeo-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Nächste Schritte

- [Integrate Pradeo with Intune (Integrieren von Pradeo in Intune)](pradeo-mtd-connector-integration.md)

- [Einrichten von Pradeo-Apps](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Erstellen einer Pradeo-Gerätekonformitätsrichtlinie](mtd-device-compliance-policy-create.md)

- [Aktivieren eines Pradeo MTD-Connectors](mtd-connector-enable.md)
