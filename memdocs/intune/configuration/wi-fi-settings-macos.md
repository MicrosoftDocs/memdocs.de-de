---
title: Konfigurieren von WLAN-Einstellungen für macOS-Geräte in Microsoft Intune – Azure | Microsoft-Dokumentation
titleSuffix: ''
description: Erstellen Sie ein WLAN-Gerätekonfigurationsprofil für macOS-Geräte, oder fügen Sie eines hinzu. Erfahren Sie mehr über die verschiedenen Einstellungen, das Hinzufügen von Zertifikaten sowie das Auswählen eines EAP-Typs und einer Authentifizierungsmethode in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/10/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e1cd60b8a9a8612034972e8357d2e346d194ca3a
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85092883"
---
# <a name="add-wi-fi-settings-for-macos-devices-in-microsoft-intune"></a>Hinzufügen von WLAN-Einstellungen für macOS-Geräte in Microsoft Intune

Sie können ein Profil mit bestimmten WLAN-Einstellungen erstellen und dieses dann auf Ihren macOS-Geräten bereitstellen. Microsoft Intune bietet viele Features, darunter die Authentifizierung bei Ihrem Netzwerk, das Hinzufügen eines PKCS- oder SCEP-Zertifikats u.v.m.

Diese WLAN-Einstellungen werden in zwei Kategorien unterteilt: Grund- und Unternehmenseinstellungen.

Dieser Artikel beschreibt diese Einstellungen.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein Geräteprofil.](wi-fi-settings-configure.md)

> [!NOTE]
> Diese Einstellungen sind für alle Registrierungstypen verfügbar. Weitere Informationen zu den Registrierungstypen finden Sie unter [macOS-Registrierung](../enrollment/macos-enroll.md).

## <a name="basic-profiles"></a>Grundlegende Profile

Grundlegende oder persönliche Profile verwenden WPA/WPA2 zum Schutz der WLAN-Verbindung auf Geräten. In der Regel wird WPA/WPA2 in Heimnetzwerken oder persönlichen Netzwerken verwendet. Sie können auch einen vorinstallierten Schlüssel hinzufügen, um die Verbindung zu authentifizieren.

- **WLAN-Typ**: Wählen Sie **Standard**.
- **Netzwerkname**: Geben Sie einen Namen für diese WLAN-Verbindung ein. Dieser Wert ist der Name, der Benutzern in der Liste der verfügbaren Verbindungen auf ihren Geräten angezeigt wird.
- **SSID**: Abkürzung für **Service Set Identifier**. Diese Eigenschaft entspricht dem tatsächlichen Namen des Drahtlosnetzwerks, mit dem Geräte eine Verbindung herstellen. Den Benutzern wird beim Auswählen der Verbindung jedoch nur der Netzwerkname angezeigt, den Sie konfiguriert haben.
- **Automatisch verbinden**: Wählen Sie **Aktivieren** aus, um automatisch eine Verbindung mit diesem Netzwerk herzustellen, wenn das Gerät in Reichweite ist. Wählen Sie **Deaktivieren** aus, um zu verhindern, dass sich Geräte automatisch verbinden.
- **Ausgeblendetes Netzwerk**: Wählen Sie **Aktivieren** aus, um dieses Netzwerk in der Liste der verfügbaren Netzwerke auf dem Gerät auszublenden. Die SSID wird nicht übertragen. Wählen Sie **Deaktivieren** aus, um dieses Netzwerk in der Liste der verfügbaren Netzwerke auf dem Gerät anzuzeigen.
- **Sicherheitstyp:** Wählen Sie das Sicherheitsprotokoll zur Authentifizierung beim WLAN-Netzwerk aus. Folgende Optionen sind verfügbar:

  - **Offen (keine Authentifizierung)** : Verwenden Sie diese Option nur, wenn das Netzwerk nicht gesichert ist.
  - **WPA/WPA2-Persönlich:** Geben Sie das Kennwort unter **Vorinstallierter Schlüssel** ein. Wenn das Netzwerk Ihrer Organisation eingerichtet oder konfiguriert wird, wird auch ein Kennwort oder ein Netzwerkschlüssel konfiguriert. Geben Sie dieses Kennwort oder den Netzwerkschlüssel für den Wert des vorinstallierten Schlüssels ein.
  - **Datenverschlüsselung**

- **Proxyeinstellungen:** Folgende Optionen sind verfügbar:
  - **Keine**: Es sind keine Proxyeinstellungen konfiguriert.
  - **Manuell:** Geben Sie die **Proxyserveradresse** als IP-Adresse und die zugehörige **Portnummer** ein.
  - **Automatisch:** Verwenden Sie eine Datei, um den Proxyserver zu konfigurieren. Geben Sie die **Proxyserver-URL** ein (z.B. `http://proxy.contoso.com`), unter der die Konfigurationsdatei zu finden ist.

## <a name="enterprise-profiles"></a>Profile für Unternehmen

Unternehmensprofile verwenden EAP (Extensible Authentication Protocol) für die Authentifizierung von WLAN-Verbindungen. EAP wird häufig von Unternehmen verwendet, da Sie Zertifikate verwenden können, um Verbindungen zu authentifizieren und zu sichern und mehr Sicherheitsoptionen zu konfigurieren.

- **WLAN-Typ**: Wählen Sie **Unternehmen** aus.
- **SSID**: Abkürzung für **Service Set Identifier**. Diese Eigenschaft entspricht dem tatsächlichen Namen des Drahtlosnetzwerks, mit dem Geräte eine Verbindung herstellen. Den Benutzern wird beim Auswählen der Verbindung jedoch nur der Netzwerkname angezeigt, den Sie konfiguriert haben.
- **Automatisch verbinden**: Wählen Sie **Aktivieren** aus, um automatisch eine Verbindung mit diesem Netzwerk herzustellen, wenn das Gerät in Reichweite ist. Wählen Sie **Deaktivieren** aus, um zu verhindern, dass sich Geräte automatisch verbinden.
- **Ausgeblendetes Netzwerk**: Wählen Sie **Aktivieren** aus, um dieses Netzwerk in der Liste der verfügbaren Netzwerke auf dem Gerät auszublenden. Die SSID wird nicht übertragen. Wählen Sie **Deaktivieren** aus, um dieses Netzwerk in der Liste der verfügbaren Netzwerke auf dem Gerät anzuzeigen.

- **EAP-Typ**: Wählen Sie die den EAP-Typ (Extensible Authentication-Protokoll) zur Authentifizierung von gesicherten Drahtlosverbindungen aus. Folgende Optionen sind verfügbar:

  - **EAP-FAST:** Geben Sie die **PAC-Einstellungen (Protected Access Credential)** ein. Bei dieser Option werden geschützte Zugriffsanmeldeinformationen verwendet, um einen authentifizierten Tunnel zwischen dem Client und dem Authentifizierungsserver zu erstellen. Folgende Optionen sind verfügbar:
    - **Nicht verwenden (PAC)**
    - **PAC verwenden:** Wenn eine PAC-Datei vorhanden ist, wird diese verwendet.
    - **PAC verwenden und bereitstellen:** Mit dieser Option wird die PAC-Datei erstellt und zu Ihren Geräten hinzugefügt.
    - **PAC anonym verwenden und bereitstellen:** Mit dieser Option wird die PAC-Datei erstellt und ohne Authentifizierung beim Server zu Ihren Geräten hinzugefügt.

  - **EAP-SIM**

  - **EAP-TLS**: Geben Sie außerdem Folgendes ein:

    - **Serververtrauensstellung** – **Zertifikatservernamen:** Fügen Sie mindestens einen allgemeinen Namen **hinzu**, der in den von der vertrauenswürdigen Zertifizierungsstelle ausgestellten Zertifikaten verwendet wird. Wenn Sie diese Informationen eingeben, können Sie das Fenster für dynamische Vertrauensstellungen umgehen, das auf Benutzergeräten bei der Verbindungsherstellung mit diesem WLAN angezeigt wird.
    - **Stammzertifikat zur Servervalidierung:** Wählen Sie mindestens ein vorhandenes, vertrauenswürdiges Stammzertifikatprofil aus. Diese Zertifikate werden dem Server bereitgestellt, wenn der Client eine Verbindung mit dem Netzwerk herstellt. Sie authentifizieren die Verbindung.

    - **Clientauthentifizierung** - **Clientzertifikat zur Clientauthentifizierung (Identitätszertifikat)** : Wählen Sie das SCEP- oder PKCS-Clientzertifikatprofil aus, das auch auf dem Gerät bereitgestellt wird. Dieses Zertifikat ist die Identität, die das Gerät dem Server zur Authentifizierung der Verbindung bereitstellt.

  - **EAP-TTLS**: Geben Sie außerdem Folgendes ein:

    - **Serververtrauensstellung** – **Zertifikatservernamen:** Fügen Sie mindestens einen allgemeinen Namen **hinzu**, der in den von der vertrauenswürdigen Zertifizierungsstelle ausgestellten Zertifikaten verwendet wird. Wenn Sie diese Informationen eingeben, können Sie das Fenster für dynamische Vertrauensstellungen umgehen, das auf Benutzergeräten bei der Verbindungsherstellung mit diesem WLAN angezeigt wird.
    - **Stammzertifikat zur Servervalidierung:** Wählen Sie mindestens ein vorhandenes, vertrauenswürdiges Stammzertifikatprofil aus. Diese Zertifikate werden dem Server bereitgestellt, wenn der Client eine Verbindung mit dem Netzwerk herstellt. Sie authentifizieren die Verbindung.

    - **Clientauthentifizierung**: Wählen Sie eine **Authentifizierungsmethode** aus. Folgende Optionen sind verfügbar:

      - **Benutzername und Kennwort**: Fordern Sie den Benutzer zur Eingabe des Benutzernamens und Kennworts für die Authentifizierung der Verbindung auf. Geben Sie außerdem Folgendes ein:
        - **Nicht-EAP-Methode (innere Identität)** : Wählen Sie aus, wie Sie die Verbindung authentifizieren möchten. Achten Sie darauf, dass Sie das gleiche Protokoll auswählen, das auch in Ihrem WLAN konfiguriert ist.

          Folgende Optionen sind verfügbar: **Unverschlüsseltes Kennwort (PAP)** , **Challenge Handshake Authentication-Protokoll (CHAP)** , **Microsoft CHAP (MS-CHAP)** oder **Microsoft CHAP Version 2 (MS-CHAP v2)**

      - **Zertifikate:** Wählen Sie das SCEP- oder PKCS-Clientzertifikatprofil aus, das auch auf dem Gerät bereitgestellt wird. Dieses Zertifikat ist die Identität, die das Gerät dem Server zur Authentifizierung der Verbindung bereitstellt.

      - **Identitätsschutz (äußere Identität)** : Geben Sie den Text ein, der als Antwort auf eine EAP-Identitätsanforderung gesendet werden soll. Dieser Text kann einen beliebigen Wert haben, z.B. `anonymous`. Während der Authentifizierung wird zuerst diese anonyme Identität gesendet und anschließend die echte Kennung über einen sicheren Tunnel.

  - **LEAP**

  - **PEAP**: Geben Sie außerdem Folgendes ein:

    - **Serververtrauensstellung** – **Zertifikatservernamen:** Fügen Sie mindestens einen allgemeinen Namen **hinzu**, der in den von der vertrauenswürdigen Zertifizierungsstelle ausgestellten Zertifikaten verwendet wird. Wenn Sie diese Informationen eingeben, können Sie das Fenster für dynamische Vertrauensstellungen umgehen, das auf Benutzergeräten bei der Verbindungsherstellung mit diesem WLAN angezeigt wird.
    - **Stammzertifikat zur Servervalidierung:** Wählen Sie mindestens ein vorhandenes, vertrauenswürdiges Stammzertifikatprofil aus. Diese Zertifikate werden dem Server bereitgestellt, wenn der Client eine Verbindung mit dem Netzwerk herstellt. Sie authentifizieren die Verbindung.

    - **Clientauthentifizierung**: Wählen Sie eine **Authentifizierungsmethode** aus. Folgende Optionen sind verfügbar:

      - **Benutzername und Kennwort**: Fordern Sie den Benutzer zur Eingabe des Benutzernamens und Kennworts für die Authentifizierung der Verbindung auf. 

      - **Zertifikate:** Wählen Sie das SCEP- oder PKCS-Clientzertifikatprofil aus, das auch auf dem Gerät bereitgestellt wird. Dieses Zertifikat ist die Identität, die das Gerät dem Server zur Authentifizierung der Verbindung bereitstellt.

      - **Identitätsschutz (äußere Identität)** : Geben Sie den Text ein, der als Antwort auf eine EAP-Identitätsanforderung gesendet werden soll. Dieser Text kann einen beliebigen Wert haben, z.B. `anonymous`. Während der Authentifizierung wird zuerst diese anonyme Identität gesendet und anschließend die echte Kennung über einen sicheren Tunnel.

- **Proxyeinstellungen:** Folgende Optionen sind verfügbar:
  - **Keine**: Es sind keine Proxyeinstellungen konfiguriert.
  - **Manuell:** Geben Sie die **Proxyserveradresse** als IP-Adresse und die zugehörige **Portnummer** ein.
  - **Automatisch:** Verwenden Sie eine Datei, um den Proxyserver zu konfigurieren. Geben Sie die **Proxyserver-URL** ein (z.B. `http://proxy.contoso.com`), unter der die Konfigurationsdatei zu finden ist.

## <a name="next-steps"></a>Nächste Schritte

Das Profil ist nun erstellt. Die nächsten Schritte sind das [Zuweisen dieses Profils](device-profile-assign.md) und das [Überwachen seines Status](device-profile-monitor.md).

Konfigurieren Sie WLAN-Einstellungen für Geräte, die unter [Android](wi-fi-settings-android.md), [Android Enterprise](wi-fi-settings-android-enterprise.md), [iOS/iPadOS](wi-fi-settings-ios.md) und [Windows 10](wi-fi-settings-windows.md) ausgeführt werden.
