---
title: Integrieren der Netzwerkzugriffssteuerung mit Microsoft Intune – Azure | Microsoft-Dokumentation
description: Lösungen für die Netzwerkzugriffssteuerung überprüfen die Registrierung und Konformität von Geräten mit Intune. Die Netzwerkzugriffssteuerung umfasst bestimmte Verhaltensweisen und arbeitet mit dem bedingten Zugriff zusammen. Weitere Informationen finden Sie in den Integrationsschritten und unter der Liste mit Partnerlösungen.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: aa7ecff7-8579-4009-8fd6-e17074df67de
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5bafd916ef31bea50dabb2de5012d693039ca741
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80084823"
---
# <a name="network-access-control-nac-integration-with-intune"></a>Integrieren der Netzwerkzugriffssteuerung (NAC) mit Intune

Intune arbeitet mit Partnern der Netzwerkzugriffssteuerung zusammen, um Organisationen beim Schützen von Unternehmensdaten zu helfen, wenn Geräte versuchen, auf lokale Ressourcen zuzugreifen.

>[!IMPORTANT]
> NAC wird aktuell für vollständig verwaltete Android Enterprise-Geräte und für dedizierte Android Enterprise-Geräte nicht unterstützt.

## <a name="how-do-intune-and-nac-solutions-help-protect-your-organization-resources"></a>Wie helfen Lösungen von Intune und NAC beim Schutz der Ressourcen Ihrer Organisation?

Lösungen für die Zugriffssteuerung überprüfen den Registrierungs- und Kompatibilitätsstatus des Geräts mit Intune, um Entscheidungen bezüglich der Zugriffssteuerung zu treffen. Wenn das Gerät nicht registriert ist oder registriert ist, aber nicht den Intune-Gerätekonformitätsrichtlinien entspricht, sollte es für die Registrierung oder eine Gerätekonformitätsprüfung an Intune umgeleitet werden.

### <a name="example"></a>Beispiel

Wenn das Gerät registriert und mit Intune kompatibel ist, sollte die NAC-Lösung dem Gerät den Zugriff auf Unternehmensressourcen erlauben. Benutzern kann beispielsweise der Zugriff auf das Unternehmens-WLAN oder VPN-Ressourcen gewährt oder verweigert werden.

## <a name="feature-behaviors"></a>Featureverhalten

Geräte, die aktiv mit Intune synchronisiert werden, können nicht vom Zustand **Konform** / **Nicht konform** in **Nicht synchronisiert** (oder **Unbekannt**) wechseln. Der Zustand **Unbekannt** ist für neu registrierte Geräte reserviert, die noch nicht im Hinblick auf ihre Konformität ausgewertet wurden.

Bei Geräten, die für den Zugriff auf Ressourcen blockiert sind, sollte der blockierende Dienst alle Benutzer auf das [Verwaltungsportal](https://portal.manage.microsoft.com) umleiten, um festzustellen, warum das Gerät blockiert ist.  Wenn die Benutzer diese Seite besuchen, werden ihre Geräte erneut synchron im Hinblick auf Konformität ausgewertet.

## <a name="nac-and-conditional-access"></a>Netzwerkzugriffssteuerung und bedingter Zugriff

Die Netzwerkzugriffssteuerung nutzt bei Entscheidungen bezüglich der Zugriffssteuerung den bedingten Zugriff. Weitere Informationen finden Sie unter [Gängige Möglichkeiten für die Verwendung des bedingten Zugriffs in Intune](conditional-access-intune-common-ways-use.md).

## <a name="how-the-nac-integration-works"></a>Funktionsweise der NAC-Integration

Im Folgenden erhalten Sie einen Überblick darüber, wie die Integration der Netzwerkzugriffssteuerung funktioniert, wenn sie in Intune integriert ist. In den ersten drei Schritten 1-3 wird der Onboardingprozess erklärt. Nachdem die Lösung für die Zugriffssteuerung in Intune integriert wurde, wird in den Schritten 4-9 der laufende Betrieb beschrieben.

![Darstellung der Funktionsweise der Netzwerkzugriffssteuerung mit Intune](./media/network-access-control-integrate/ca-intune-common-ways-2.png)

1. Registrieren Sie die Lösung des NAC-Partners mit Azure Active Directory (AAD), und gewähren Sie delegierte Berechtigungen an die Intune-NAC-API.
2. Konfigurieren Sie die Lösung des NAC-Partners mit den geeigneten Einstellungen, darunter die URL für die Intune-Ermittlung.
3. Konfigurieren Sie die Lösung des NAC-Partners für die Zertifikatauthentifizierung.
4. Der Benutzer stellt eine Verbindung zum WLAN-Zugriffspunkt her oder fordert eine VPN-Verbindung an.
5. Die Lösung des NAC-Partners leitet die Geräteinformationen an Intune weiter und fragt Intune nach dem Registrierungs- und Kompatibilitätsstatus des Geräts.
6. Wenn das Gerät nicht konform oder nicht registriert ist, weist die Lösung des NAC-Partners den Benutzer an, das Gerät zu registrieren oder die Konformitätsprobleme zu beheben.
7. Das Gerät versucht bei Bedarf, seinen Konformitäts- und Registrierungszustand erneut zu überprüfen.
8. Wenn das Gerät registriert wurde und kompatibel ist, erhält die Lösung des NAC-Partners von Intune eine Statusmeldung.
9. Die Verbindung konnte erfolgreich hergestellt werden, und das Gerät erhält Zugriff auf Unternehmensressourcen.

## <a name="use-nac-for-vpn-on-your-iosipados-devices"></a>Verwenden der NAC für ein VPN auf iOS/iPadOS-Geräten

NAC steht auf den folgenden VPNs zur Verfügung, ohne dass NAC im VPN-Profil aktiviert werden muss:

- NAC für Cisco Legacy AnyConnect
- F5 Access Legacy
- Citrix VPN

NAC wird auch für Cisco AnyConnect, Citrix SSO und F5 Access unterstützt.

### <a name="to-enable-nac-for-cisco-anyconnect-for-ios"></a>Aktivieren von NAC für Cisco Any Connect für iOS

- Integrieren Sie ISE in Intune für NAC, wie im folgenden Link beschrieben wird.
- Legen Sie die Einstellung **Netzwerkzugriffssteuerung (NAC) aktivieren** im VPN-Profil auf **Ja** fest.

### <a name="to-enable-nac-for-citrix-sso"></a>Aktivieren von NAC für Citrix SSO

- Verwenden Sie Citrix Gateway 12.0.59 oder höher.  
- Benutzer müssen Citrix SSO 1.1.6 oder höher installiert haben.
- [Integrieren Sie NetScaler in Intune für die NAC](https://docs.citrix.com/en-us/netscaler-gateway/12/microsoft-intune-integration/configuring-network-access-control-device-check-for-netscaler-gateway-virtual-server-for-single-factor-authentication-deployment.html), wie in der Citrix-Produktdokumentation beschrieben wird.
- Wählen Sie im VPN-Profil **Basiseinstellungen** > **Netzwerkzugriffssteuerung (NAC) aktivieren** und **Ich stimme zu** aus.

### <a name="to-enable-nac-for-f5-access"></a>Aktivieren von NAC für F5 Access

- Verwenden Sie F5 BIG-IP 13.1.1.5 oder höher.
- Integrieren Sie BIG-IP für NAC in Intune. Im F5-Leitfaden [Übersicht: Konfigurieren von APM für Gerätestatusüberprüfungen mit Endpunktverwaltungssystemen](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-client-configuration-7-1-6/6.html#guid-0bd12e12-8107-40ec-979d-c44779a8cc89) sind die dazu erforderlichen Schritte aufgeführt.
- Wählen Sie im VPN-Profil **Basiseinstellungen** > **Netzwerkzugriffssteuerung (NAC) aktivieren** und **Ich stimme zu** aus.

Die VPN-Verbindung wird alle 24 Stunden aus Sicherheitsgründen getrennt. Die VPN-Verbindung kann sofort wiederhergestellt werden.

Microsoft und Partner arbeiten an einer NAC-Lösung für diese neueren Clients. Wenn Lösungen bereit sind, wird dieser Artikel mit zusätzlichen Informationen aktualisiert.

## <a name="next-steps"></a>Nächste Schritte

- [Integrieren von Cisco ISE mit Intune](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html)
- [Integrieren von Citrix NetScaler mit Intune](https://docs.citrix.com/en-us/netscaler-gateway/12/microsoft-intune-integration/configuring-network-access-control-device-check-for-netscaler-gateway-virtual-server-for-single-factor-authentication-deployment.html)
- [Integrieren von F5 BIG-IP Access Policy Manager in Intune](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-client-configuration-13-0-0/6.html)
- [Integrieren von HPE Aruba ClearPass mit Intune](https://support.arubanetworks.com/Documentation/tabid/77/DMXModule/512/Command/Core_Download/Default.aspx?EntryId=31271)
- [Integrate Squadra security Removable Media Manager (secRMM) with Intune (Integrieren des Squadra-Sicherheitsmanagers für entfernbare Wechselmedien mit Intune)](http://www.squadratechnologies.com/StaticContent/ProductDownload/secRMM/9.9.0.0/secRMMIntuneAccessControlSetupGuide.pdf)
