---
title: Bestimmen von Szenarien für Anwendungsfälle
titleSuffix: Microsoft Intune
description: Dieser Artikel hilft Ihnen, Szenarien für Intune-Anwendungsfälle und untergeordnete Anwendungsfälle für eine reine Cloudimplementierung von Microsoft Intune zu bestimmen.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 4b3c9af9-78da-44d2-8bd2-3f0f8885952d
ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4e98a9c25121bacf1759dc73464e3a51dfe61d9
ms.sourcegitcommit: c333fc6627f5577cde9d2fa8f59e642202a7027b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/16/2020
ms.locfileid: "84795685"
---
# <a name="identify-mobile-device-management-use-case-scenarios"></a>Bestimmen von Szenarien für Anwendungsfälle für die Verwaltung von Mobilgeräten

Das Bestimmen Ihrer Szenarien für Anwendungsfälle ist ein wichtiger Bestandteil des Planungsprozesses einer erfolgreichen Intune-Bereitstellung. Szenarien für Anwendungsfälle sind hilfreich, da Sie mit ihnen Ihre Benutzer in verwaltbare Gruppen unterteilen können, entweder nach Benutzertyp oder Rolle oder nach Besitzer des Gerät des Benutzers (z.B. das Unternehmen oder der Benutzer selbst).

Betrachten wir einige Beispiele, die Ihre Organisation beim Festlegen von Intune-Anwendungsfallszenarios, Organisationsgruppen und den einzelnen Anwendungsfällen zugeordneten mobilen Geräteplattformen unterstützen.

## <a name="device-ownership"></a>Gerätebesitz
Als Erstes können Sie die Intune-Bereitstellungsziele und sonstigen Ziele Ihrer Organisation zurate ziehen, um die Hauptanwendungsszenarien für Ihre Bereitstellung zu bestimmen. Beantworten Sie im Rahmen Ihres Intune-Bereitstellungsplans die folgenden Fragen:

- Möchten Sie unternehmenseigene Geräte unterstützen?

- Möchten Sie persönliche Geräte (BYOD) unterstützen?

Dies sind keine Entweder/Oder-Optionen. Sie finden ggf. heraus, dass Sie beide Formen des Gerätebesitzes unterstützen müssen, um die Ziele Ihrer Organisation zu erreichen. Die untergeordneten Anwendungsfälle helfen bei der Klärung, wo die verschiedenen Geräteverwaltungsrichtlinien gelten sollen.

### <a name="user-type-or-device-role"></a>Benutzertyp oder Geräterolle

Bestimmen Sie, ob es für jedes Anwendungsfallszenario untergeordnete Anwendungsfälle gibt. Zum Beispiel hat Ihre Organisation möglicherweise Anforderungen für die Unterstützung eines unternehmensweiten Anwendungsfallszenarios erkannt, das basierend auf Benutzertyp oder Geräterolle zusätzliche untergeordnete Anwendungsfälle aufweist:

- Information-Worker

- Management

- Kiosk

Hier sind einige Beispiele von Szenarien für Anwendungsfälle und untergeordnete Anwendungsfälle:

| **Anwendungsfälle** | **Untergeordnete Anwendungsfälle** |
|:---:|:---:|
| Unternehmen | Information-Worker |              
| Unternehmen | Führungskräfte |           
| Unternehmen | Kiosk |
| BYOD | Information-Worker |           
| BYOD | Führungskräfte |


## <a name="organizational-groups-for-your-scenarios"></a>Organisationsgruppen für Ihre Szenarien

Jetzt müssen Sie die Organisationsgruppen festlegen, die den einzelnen Szenarien für Anwendungsfälle und untergeordnete Anwendungsfälle zugeordnet werden. Beispiel:

| **Anwendungsfälle** | **Untergeordnete Anwendungsfälle** | **Organisationsgruppen** |
|:---:|:---:|:---:|
| Unternehmen | Information-Worker | Personalabteilung, Finanzabteilung |               
| Unternehmen | Management | Personalabteilung, Finanzabteilung |            
| Unternehmen | Kiosk | Einzelhandel |
| BYOD | Information-Worker | Marketing, Vertrieb |            
| BYOD | Management | Marketing, Vertrieb |


## <a name="mobile-device-platforms-for-your-scenarios"></a>Plattformen für mobile Geräte für Ihre Szenarien

Im nächsten Schritt bestimmen Sie die Plattformen für mobile Geräte , die den einzelnen Anwendungsfallszenarien zugeordnet sind. Es gibt möglicherweise mehr als eine.

Angenommen, im Anwendungsfallszenario Ihres Unternehmens werden die Geräteplattformen iOS/iPadOS und Android Samsung KNOX unterstützt. Ihre BYOD-Richtlinie sieht ggf. Unterstützung für weitere Plattformen für mobile Geräte wie Android (nicht Samsung KNOX) und Windows 10 Mobile vor. Ausgehend von den genannten Beispielen haben wir jedem Anwendungsfallszenario Plattformen für mobile Geräte zugeordnet.

| **Anwendungsfälle** | **Untergeordnete Anwendungsfälle** | **Gruppen** | **Geräteplattformen** |   
|:---:|:---:|:---:|:---:|
| Unternehmen | Information-Worker | Personalabteilung, Finanzabteilung | iOS/iPadOS |                                                           
| Unternehmen | Führungskräfte | Personalabteilung, Finanzabteilung | iOS/iPadOS |                                                           
| Unternehmen | Kiosk | Einzelhandel | Android |
| BYOD | Information-Worker | Marketing, Vertrieb | iOS/iPadOS |                                                           
| BYOD | Führungskräfte | Marketing, Vertrieb | iOS/iPadOS |

## <a name="next-steps"></a>Nächste Schritte

Der nächste Abschnitt enthält Hinweise für das [Identifizieren der Intune-Anforderungen für die einzelnen Anwendungsszenarien](planning-guide-requirements.md).
