---
title: Häufige Endpoint Protection-Meldungen in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Häufige Meldungen und mögliche Lösungen bei der Verwendung von und Problembehandlung für Endpoint Protection und Microsoft Defender in Microsoft Intune.
keywords: ''
author: Brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/13/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: e31df2d2-bb1b-491b-9a71-04e0b18829c1
ROBOTS: ''
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3758764ae594412b35f33d07b635df78a2c26864
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912269"
---
# <a name="endpoint-protection-issues-and-possible-solutions-in-microsoft-intune"></a>Endpoint Protection-Probleme und mögliche Lösungen in Microsoft Intune

Dieser Artikel beschreibt mögliche Ursachen und Lösungen für die einige Fehler und Warnungen. Diese Informationen helfen Ihnen, Probleme bei der Verwendung von Endpoint Protection zu beheben.

## <a name="microsoft-defender-error-codes"></a>Microsoft Defender-Fehlercodes

Überprüfen Sie die Ereignisprotokolle und Fehlercodes, um [Probleme mit Microsoft Defender Antivirus zu behandeln](/windows/security/threat-protection/windows-defender-antivirus/troubleshoot-windows-defender-antivirus).

## <a name="common-intune-errors-and-possible-resolutions"></a>Häufige Intune-Fehler und mögliche Lösungen

### <a name="endpoint-protection-engine-unavailable"></a>Die Endpoint Protection-Engine ist nicht verfügbar

**Mögliche Ursache**: Die Endpoint Protection-Engine von Intune wurde beschädigt oder gelöscht.

**Mögliche Lösungen**:

- Wenn die Endpoint Protection-Engine beschädigt ist oder nicht aktualisiert wird, dann aktualisieren Sie das Programm, oder installieren Sie es neu.
- Erzwingen Sie eine sofortige Aktualisierung. Wählen Sie im Endpoint Protection-Programm (wahrscheinlich in der Taskleiste) **Aktualisieren** aus.
- Wählen Sie unter „Systemsteuerung“ > „Programme“ **Microsoft Intune Endpoint Protection-Agent** aus. Deinstallieren Sie die Anwendung.
- Während der nächsten Updatesynchronisierung wird das fehlende Programm von Microsoft Online Management Update Manager erkannt und zum geplanten Installationszeitpunkt neu installiert.

### <a name="features-are-disabled"></a>Features sind deaktiviert

Sie erhalten möglicherweise eine Meldung, dass einige Features deaktiviert wurden. Diese Meldungen können auftreten, wenn Intune Endpoint Protection oder Microsoft Defender mithilfe eines Konfigurationsprofils von einem Administrator deaktiviert wurde. Es ist auch möglich, dass die Deaktivierung von einem Endbenutzer auf dem Gerät durchgeführt wurde. Mögliche Meldungen:

`Endpoint Protection disabled`  
`Real-time protection disabled`  
`Download scanning disabled`  
`File and program activity monitoring disabled`  
`Behavior monitoring disabled`  
`Script scanning disabled`  
`Network Inspection System disabled`  

**Mögliche Lösungen**: Aktivieren Sie diese Features. Anleitungen finden Sie hier:

- [Hinzufügen von Endpoint Protection-Einstellungen](../protect/endpoint-protection-configure.md)
- [Microsoft Defender Antivirus](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus)
- [Endbenutzer: Aktivieren von Echtzeitschutz zum Zugriff auf Unternehmensressourcen](../user-help/turn-on-defender-windows.md)

### <a name="malware-definitions-out-of-date"></a>Malwaredefinitionen sind veraltet

Dieser Status wird angezeigt, wenn die Malwaredefinitionen auf dem Gerät seit mehr als 14 Tagen nicht mehr auf dem neuesten Stand sind. Beispielsweise kann die Meldung angezeigt werden, wenn das Gerät nicht mit dem Internet verbunden ist oder die Malwaredefinitionen veraltet sind.

**Mögliche Lösungen**: Wenn Malwaredefinitionen veraltet sind, können Sie die Definitionen mit [Microsoft Defender Antivirus](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) aktualisieren.

### <a name="full-scan-overdue-or-quick-scan-overdue"></a>Vollständige Überprüfung oder Schnellüberprüfung überfällig

Es wurde seit 14 Tagen keine vollständige Überprüfung oder Schnellüberprüfung mehr durchgeführt. Dieses Szenario kann auftreten, wenn das Gerät während einer vollständigen Überprüfung neu gestartet wird.

**Mögliche Lösungen**: Wenn eine Überprüfung überfällig ist, können Sie eine einmalige Überprüfung ausführen oder eine wiederholte Überprüfung planen. Weitere Informationen finden Sie unter [Microsoft Defender Antivirus](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus).

### <a name="another-endpoint-protection-application-running"></a>Eine andere Endpoint Protection-Anwendung wird ausgeführt

Eine andere Endpoint Protection-Anwendung wird ausgeführt, und das Gerät befindet sich in einem fehlerfreien Zustand.

**Mögliche Lösungen**: Wenn bereits eine andere Endpoint Protection-Anwendung installiert ist und Intune diese Anwendung erkennt, wird das Geräte möglicherweise instabil.

## <a name="next-steps"></a>Nächste Schritte

Fordern Sie [Hilfe beim Microsoft-Support](get-support.md) an, oder nutzen Sie die [Communityforen](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).