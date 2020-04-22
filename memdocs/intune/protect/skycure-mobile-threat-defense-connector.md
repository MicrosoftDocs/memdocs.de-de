---
title: Symantec-Connector mit Microsoft Intune
titleSuffix: Microsoft Intune
description: Informationen zum Integrieren von Intune in Symantec Endpoint Protection Mobile, um den Zugriff mobiler Geräte auf Ihre Unternehmensressourcen zu steuern.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: df4ce3f6-a093-432c-ab86-7a83865e389e
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6f8f3cf9ced5b613323093ed2baafcf65667997
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80275083"
---
# <a name="symantec-endpoint-protection-mobile-connector"></a>Symantec Endpoint Protection Mobile-Connector

Sie können den Zugriff mobiler Geräte auf Unternehmensressourcen mithilfe des bedingten Zugriffs basierend auf Risikobewertungen steuern, die von Symantec Endpoint Protection Mobile (SEP Mobile) vorgenommen werden, einer Mobile Threat Defense-Lösung, die in Microsoft Intune integriert werden kann. Das Risiko wird basierend auf Telemetriedaten von Geräten bewertet, auf denen SEP Mobile ausgeführt wird, wie z.B.:

- Physische Verteidigung

- Netzwerkverteidigung

- Anwendungsverteidigung

- Verteidigung gegen Sicherheitsrisiken

Sie können die SEP Mobile-Risikobewertung über Intune-Gerätekonformitätsrichtlinien aktivieren und dann Richtlinien für bedingten Zugriff verwenden, um anhand der erkannten Bedrohungen den Zugriff auf Unternehmensressourcen durch nicht konforme Geräte zulassen oder blockieren.

> [!NOTE]
> Dieser Mobile Threat Defense-Anbieter wird für nicht registrierte Geräte nicht unterstützt.

## <a name="supported-platforms"></a>Unterstützte Plattformen

- **Android 4.1 und höher**

- **iOS 8 und höher**

## <a name="pre-requisites"></a>Voraussetzungen

- Azure Active Directory Premium

- Microsoft Intune-Abonnement

- Symantec Endpoint Protection Mobile-Abonnement

Weitere Informationen erhalten Sie auf der [Symantec-Website](https://help.symantec.com/cs/sep_mobile/SEPMOBILE/v131237277_v127904070/Integrating-Microsoft-Intune-with-Endpoint-Protection-Mobile?locale=EN_US).

## <a name="how-do-intune-and-sep-mobile-help-protect-your-company-resources"></a>Wie helfen Intune und SEP Mobile beim Schutz von Unternehmensressourcen?

Die SEP Mobile-App für Android oder iOS/iPadOS erfasst Telemetriedaten des Dateisystems, Netzwerkstapels sowie von Geräten und Anwendungen, sofern verfügbar, und sendet diese dann an den Symantec-Clouddienst, mit dessen Hilfe die Anfälligkeit des Geräts für mobile Bedrohungen bewertet wird.

Die Intune-Gerätekompatibilitätsrichtlinie enthält eine Regel für SEP Mobile, die auf der SEP Mobile-Risikobewertung basiert. Wenn diese Regel aktiviert ist, bewertet Intune die Gerätekompatibilität mit der von Ihnen aktivierten Richtlinie.

Wird das Gerät als nicht kompatibel eingestuft, wird der Zugriff auf Ressourcen wie Exchange Online und SharePoint Online blockiert. Benutzer auf blockierten Geräten erhalten Anleitungen von der SEP Mobile-App, um das Problem zu beheben und den Zugriff auf Unternehmensressourcen zurückzuerlangen.

Intune unterstützt zwei Modi der Integration in SEP Mobile:

- Die **grundlegende Installation** ist ein schreibgeschützter Modus, der die Sichtbarkeit von SEP Mobile für Geräte in Intune zulässt.

- Die **vollständige Integration** ermöglicht SEP Mobile, Details zu Geräterisiken und Sicherheitsvorfällen an Intune zu melden.

## <a name="sample-scenarios"></a>Beispielszenarios

Hier einige gängige Szenarios:

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Steuern des Zugriffs basierend auf Bedrohungen durch Apps, die Schadsoftware enthalten

Wenn Apps, die Schadsoftware enthalten, auf Geräten erkannt werden, können Sie Geräte blockieren, bis die Bedrohung beseitigt ist:

- Herstellen einer Verbindung mit Unternehmens-E-Mail

- Synchronisieren von Unternehmensdateien mithilfe der OneDrive for Work-App

- Zugreifen auf Unternehmens-Apps

*Blockieren, wenn Apps mit Schadsoftware entdeckt werden:*

![Darstellung des Szenarios, wenn Apps mit Schadsoftware erkannt werden](./media/skycure-mobile-threat-defense-connector/symantec-arch-1.png)

*Nach Korrektur erteilter Zugriff:*

![Darstellung des gewährten Zugriffs nach Beseitigung von erkannten Apps mit Schadsoftware](./media/skycure-mobile-threat-defense-connector/symantec-arch-2.png)

### <a name="control-access-based-on-threat-to-network"></a>Steuern des Zugriffs basierend auf Bedrohung für das Netzwerk

Erkennen Sie Bedrohungen wie **Man-in-the-Middle** im Netzwerk, und schützen Sie den Zugriff auf WLAN-Netzwerke auf der Grundlage des Geräterisikos.

*Blockieren des Netzwerkzugriffs über WLAN:*

![Blockieren des Netzwerkzugriffs über WLAN](./media/skycure-mobile-threat-defense-connector/symantec-arch-3.png)

*Nach Korrektur erteilter Zugriff:*

![Zugriff erteilt nach der Behebung](./media/skycure-mobile-threat-defense-connector/symantec-arch-4.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Steuern des Zugriffs auf SharePoint Online basierend auf der Bedrohung für das Netzwerk

Erkennen von Bedrohungen wie **Man-in-the-Middle** im Netzwerk und Verhindern der Synchronisierung von Unternehmensdateien auf der Grundlage des Geräterisikos.

*Blockieren des Zugriffs auf SharePoint Online bei Erkennen von Bedrohungen für das Netzwerk*

![Blockieren von SharePoint Online bei Erkennung von Bedrohungen für das Netzwerk](./media/skycure-mobile-threat-defense-connector/symantec-arch-5.png)

*Nach Korrektur erteilter Zugriff:*

![Zugriff erteilt nach der Behebung für Sharepoint-Beispiel](./media/skycure-mobile-threat-defense-connector/symantec-arch-6.png)

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Symantec Endpoint Protection Mobile Threat Defense solution considers a device to be infected:
![App protection policy blocks due to detected malware](./media/skycure-mobile-threat-defense-connector/symantec-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/skycure-mobile-threat-defense-connector/symantec-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Nächste Schritte

Dies sind die Schritte, die Sie für die Integration von Intune in SEP Mobile durchführen müssen:

- [Einrichten der Skycure-Integration in Intune](skycure-mtd-connector-integration.md)

- [Hinzufügen und Zuweisen von Mobile Threat Defense-Apps (MTD) mit Intune](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Erstellen einer Mobile Threat Defense-Gerätekompatibilitätsrichtlinie (MTD) mit Intune](mtd-device-compliance-policy-create.md)

- [Aktivieren Sie den Mobile Threat Defense-Connector in Intune.](mtd-connector-enable.md)
