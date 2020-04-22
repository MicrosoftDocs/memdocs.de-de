---
title: Konfigurieren von VPN-Einstellungen für macOS-Geräte in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Fügen Sie ein VPN-Konfigurationsprofil (virtuelles privates Netzwerk) hinzu, oder erstellen Sie ein solches. Dies beinhaltet Verbindungsdetails, getrenntes Tunneln, benutzerdefinierte VPN-Einstellungen mit Bezeichner und Schlüssel-Wert-Paaren, Proxyeinstellungen mit Konfigurationsskript, IP- oder FQDN-Adresse sowie TCP-Port in Microsoft Intune auf Geräten, die unter macOS ausgeführt werden.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 10bea151002673b36600d4d9deaa36bb8fc3ff79
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086513"
---
# <a name="add-vpn-settings-on-macos-devices-in-microsoft-intune"></a>Hinzufügen von VPN-Einstellungen für macOS-Geräte in Microsoft Intune

In diesem Artikel werden die Intune-Einstellungen veranschaulicht, die Sie verwenden können, um VPN-Verbindungen auf macOS-Geräten zu konfigurieren.

Je nach den ausgewählten Einstellungen können nicht alle Werte in der folgenden Liste konfiguriert werden.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein Profil für die Gerätekonfiguration.](vpn-settings-configure.md)

> [!NOTE]
> Diese Einstellungen sind für alle Registrierungstypen verfügbar. Weitere Informationen zu den Registrierungstypen finden Sie unter [macOS-Registrierung](../enrollment/macos-enroll.md).

## <a name="base-vpn-settings"></a>Grundlegende VPN-Einstellungen

**Verbindungsname**: Geben Sie einen Namen für diese Verbindung ein. Benutzern wird dieser Name angezeigt, wenn sie auf ihrem Gerät die Liste der verfügbaren VPN-Verbindungen durchsuchen.
- **IP-Adresse oder FQDN:** Geben Sie die IP-Adresse oder den vollqualifizierten Domänennamen des VPN-Servers an, mit dem Geräte eine Verbindung herstellen. Beispiele: **192.168.1.1**, **vpn.contoso.com**.
- **Authentifizierungsmethode:** Wählen Sie unter folgenden Optionen aus, wie sich Geräte beim VPN-Server authentifizieren:
  - **Zertifikate:** Wählen Sie unter **Authentifizierungszertifikat** ein zuvor erstelltes SCEP- oder PKCS-Zertifikatprofil zum Authentifizieren der Verbindung aus. Weitere Informationen zu Zertifikatprofilen finden Sie unter [Konfigurieren von Zertifikaten in Microsoft Intune](../protect/certificates-configure.md).
  - **Benutzername und Kennwort:** Endbenutzer müssen einen Benutzernamen und ein Kennwort für die Anmeldung beim VPN-Server angeben.
- **Verbindungstyp**: Wählen Sie den VPN-Verbindungstyp aus der folgenden Liste von Anbietern aus:
  - **Check Point Capsule VPN**
  - **Cisco AnyConnect**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Pulse Secure**
  - **Benutzerdefiniertes VPN**
- **Tunneling teilen**: **Aktivieren** oder **Deaktivieren** Sie diese Option, mit der Geräte anhand des Datenverkehrs selbst entscheiden können, welche Verbindung verwendet werden soll. Beispiel: Ein Benutzer in einem Hotel verwendet die VPN-Verbindung zum Zugreifen auf Arbeitsdateien, jedoch das Standardnetzwerk des Hotels für normales Webbrowsen.

<!--- **Per-app VPN** - Select this option if you want to associate this VPN connection with an iOS/iPadOS or macOS app so that the connection will be opened when the app is run. You can associate the VPN profile with an app when you assign the software. For more information, see [How to assign and monitor apps](../apps/apps-deploy.md). --->

## <a name="custom-vpn-settings"></a>Benutzerdefinierte VPN-Einstellungen

Wenn Sie **Benutzerdefiniertes VPN** ausgewählt haben, konfigurieren Sie diese weiteren Einstellungen:

- **VPN-Bezeichner**: Geben Sie einen Bezeichner für die verwendete VPN-App ein. Dieser Bezeichner wird von Ihrem VPN-Anbieter bereitgestellt.
- **Geben Sie Schlüssel-Wert-Paare für die benutzerdefinierten VPN-Attribute ein:** Fügen Sie **Schlüssel** und **Werte** zum Anpassen der VPN-Verbindung hinzu, oder importieren Sie sie. Diese Werte werden in der Regel von Ihrem VPN-Anbieter bereitgestellt.

## <a name="proxy-settings"></a>Proxyeinstellungen

- **Automatisches Konfigurationsskript**: Verwenden Sie eine Datei zum Konfigurieren des Proxyservers. Geben Sie die **Proxyserver-URL** ein, die die Konfigurationsdatei enthält. Geben Sie beispielsweise `http://proxy.contoso.com` ein.
- **Adresse:** Geben Sie die Adresse des Proxyservers (als IP-Adresse) ein.
- **Portnummer:** Geben Sie die Portnummer ein, die dem Proxyserver zugeordnet ist.

## <a name="next-steps"></a>Nächste Schritte

Das Profil ist nun erstellt, führt aber noch keine Aktionen durch. Die nächsten Schritte sind das [Zuweisen von Profilen](device-profile-assign.md) und das [Überwachen deren Status](device-profile-monitor.md).

Konfigurieren Sie VPN-Einstellungen für Geräte, die unter [Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [iOS/iPadOS](vpn-settings-ios.md) und [Windows 10](vpn-settings-windows-10.md) ausgeführt werden.
