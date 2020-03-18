---
title: Konfigurieren von VPN-Einstellungen für iOS/iPadOS-Geräte in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Fügen Sie ein VPN-Konfigurationsprofil hinzu bzw. erstellen Sie dieses, indem Sie Konfigurationseinstellungen für virtuelle private Netzwerke (VPNs) verwenden, einschließlich der Verbindungsdetails, Authentifizierungsmethoden und dem getrennten Tunneln in den Grundeinstellungen; der benutzerdefinierten VPN-Einstellungen mit dem Bezeichner und den Schlüssel-Wert-Paaren; der App-bezogenen VPN-Einstellungen, die Safari-URLs und bedarfsgesteuerten VPNs mit SSIDs oder DNS-Suchdomänen enthalten; und der Proxyeinstellungen zum Einschließen von einem Konfigurationsskript, einer IP-Adresse oder FQDN-Adresse und einem TCP-Port in Microsoft Intune auf Geräten mit iOS/iPadOS.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 80ff24193c607003889c2246bb9199db795f1623
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79360456"
---
# <a name="add-vpn-settings-on-ios-and-ipados-devices-in-microsoft-intune"></a>Hinzufügen von VPN-Einstellungen auf iOS- und iPadOS-Geräten in Microsoft Intune

Microsoft Intune umfasst viele VPN-Einstellungen, die auf iOS/iPadOS-Geräten bereitgestellt werden können. Diese Einstellungen werden zum Erstellen und Konfigurieren von VPN-Verbindungen mit dem Netzwerk Ihrer Organisation verwendet. Dieser Artikel beschreibt diese Einstellungen. Einige Einstellungen sind nur für bestimmte VPN-Clients, z.B. Citrix oder Zscaler, verfügbar.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie eine Gerätekonfigurationsprofil.](vpn-settings-configure.md)

> [!NOTE]
> Diese Einstellungen sind für alle Registrierungstypen verfügbar. Weitere Informationen zu den Registrierungstypen finden Sie unter [iOS/iPadOS-Registrierung](../enrollment/ios-enroll.md).

## <a name="connection-type"></a>Verbindungstyp

Wählen Sie den VPN-Verbindungstyp aus der folgenden Liste von Anbietern aus:

- **Check Point Capsule VPN**
- **Cisco Legacy AnyConnect**: Gilt für die [Cisco Legacy AnyConnect](https://itunes.apple.com/app/cisco-legacy-anyconnect/id392790924)-App-Version 4.0.5x und ältere Versionen.
- **Cisco AnyConnect**: Gilt für die [Cisco AnyConnect](https://itunes.apple.com/app/cisco-anyconnect/id1135064690)-App-Version 4.0.7x und neuere Versionen.
- **SonicWall Mobile Connect**
- **F5 Access Legacy**: Gilt für die F5 Access-App-Version 2.1 und ältere Versionen.
- **F5 Access**: Gilt für die F5 Access-App-Version 3.0 und neuere Versionen.
- **Palo Alto Networks GlobalProtect (Legacy)** : Gilt für Palo Alto Networks GlobalProtect-App-Version 4.1 und ältere Versionen.
- **Palo Alto Networks GlobalProtect**: Gilt für Palo Alto Networks GlobalProtect-App-Version 5.0 und neuere Versionen.
- **Pulse Secure**
- **Cisco (IPsec)**
- **Citrix-VPN**
- **Citrix SSO**
- **Zscaler**: Um den bedingten Zugriff zu nutzen oder Benutzern zu ermöglichen, den Zscaler-Anmeldebildschirm zu umgehen, müssen Sie Zscaler Private Access (ZPA) in Ihr Azure AD-Konto integrieren. Ausführliche Schritte finden Sie in der [Zscaler-Dokumentation](https://help.zscaler.com/zpa/configuration-example-microsoft-azure-ad). 
- **IKEv2:** Eine Beschreibung der Eigenschaften finden Sie (in diesem Artikel) unter [IKEv2-Einstellungen](#ikev2-settings).
- **Benutzerdefiniertes VPN**

> [!NOTE]
> Cisco, Citrix, F5 und Palo Alto haben angekündigt, dass ihre Legacy-Clients mit iOS 12 nicht funktionieren. Sie sollten so schnell wie möglich auf die neuen Apps umsteigen. Weitere Informationen finden Sie im [Microsoft Intune-Blog des Supportteams](https://go.microsoft.com/fwlink/?linkid=2013806&clcid=0x409).

## <a name="base-vpn-settings"></a>Grundlegende VPN-Einstellungen

Die in der folgenden Liste gezeigten Einstellungen hängen vom ausgewählten VPN-Verbindungstyp ab.  

- **Verbindungsname:** Endbenutzern wird dieser Name angezeigt, wenn sie auf ihrem Gerät eine Liste der verfügbaren VPN-Verbindungen durchsuchen.
- **Benutzerdefinierter Domänenname** (nur Zscaler): Füllen Sie das Anmeldefeld der Zscaler-App vorab mit der Domäne auf, zu der Ihre Benutzer gehören. Wenn beispielsweise ein Benutzername `Joe@contoso.net` lautet, würde die Domäne `contoso.net` beim Öffnen der App statisch im Feld erscheinen. Wenn Sie keinen Domänennamen eingeben, wird der Domänenteil des UPN in Azure Active Directory (AD) verwendet.
- **IP-Adresse oder FQDN:** Die IP-Adresse oder der vollqualifizierte Domänenname (FQDN) des VPN-Servers, mit dem Geräte eine Verbindung herstellen. Geben Sie beispielsweise `192.168.1.1` oder `vpn.contoso.com` ein.
- **Cloudname der Organisation** (nur Zscaler): Geben Sie den Namen der Cloud ein, in der Ihre Organisation bereitgestellt wird. In der von Ihnen verwendeten URL, die Sie für die Anmeldung bei Zscaler verwenden, ist der Name enthalten.  
- **Authentifizierungsmethode**: Wählen Sie aus, wie sich Geräte beim VPN-Server authentifizieren. 
  - **Zertifikate:** Wählen Sie unter **Authentifizierungszertifikat** ein vorhandenes SCEP- oder PKCS-Zertifikatprofil zum Authentifizieren der Verbindung aus. Informationen zu Zertifikatprofilen finden Sie unter [Konfigurieren von Zertifikaten](../protect/certificates-configure.md).
  - **Benutzername und Kennwort**: Benutzer müssen einen Benutzernamen und ein Kennwort für die Anmeldung beim VPN-Server eingeben.  

    > [!NOTE]
    > Wenn Benutzername und Kennwort als Authentifizierungsmethode für Cisco IPsec VPN verwendet werden, müssen sie das SharedSecret über ein benutzerdefiniertes Apple Configurator-Profil bereitstellen.

  - **Abgeleitete Anmeldeinformation:** Verwenden Sie ein Zertifikat, das von der Smartcard eines Benutzers abgeleitet ist. Wurde kein Aussteller von abgeleiteten Anmeldeinformationen konfiguriert, werden Sie von Intune dazu aufgefordert, einen Aussteller hinzuzufügen. Weitere Informationen finden Sie unter [Verwenden abgeleiteter Anmeldeinformationen in Microsoft Intune](../protect/derived-credentials.md).

- **Ausgeschlossene URLs** (nur Zscaler): Wenn Sie mit dem Zscaler-VPN verbunden sind, sind die aufgeführten URLs außerhalb der Zscaler-Cloud erreichbar. 

- **Getrenntes Tunneln:** Wählen Sie **Aktivieren** oder **Deaktivieren** für diese Option aus, damit die Geräte anhand des Datenverkehrs selbst entscheiden können, welche Verbindung verwendet werden soll. Zum Beispiel verwendet ein Benutzer in einem Hotel die VPN-Verbindung zum Zugreifen auf Arbeitsdateien, das Standardnetzwerk des Hotels jedoch für normales Webbrowsen.

- **VPN-Bezeichner** (benutzerdefiniertes VPN, Zscaler und Citrix): Ein Bezeichner für die verwendete VPN-App, die von Ihrem VPN-Anbieter bereitgestellt wird.
- **Enter key/value pairs for your organization's custom VPN attributes** (Schlüssel-Wert-Paare für die benutzerdefinierten VPN-Attribute Ihrer Organisation eingeben) (benutzerdefiniertes VPN, Zscaler und Citrix): Hinzufügen oder Importieren von **Schlüsseln** und **Werten** zum Anpassen der VPN-Verbindung. Denken Sie daran, dass diese Werte in der Regel von Ihrem VPN-Anbieter bereitgestellt werden.

- **Netzwerkzugriffssteuerung (NAC) aktivieren** (Cisco AnyConnect, Citrix SSO, F5 Access): Wenn Sie **Ich stimme zu** auswählen, wird die Geräte-ID in das VPN-Profil aufgenommen. Diese ID kann für die Authentifizierung beim VPN verwendet werden, um Zugriff auf das Netzwerk zu ermöglichen oder zu verhindern.

    **Beim Verwenden von Cisco AnyConnect mit ISE** achten Sie auf Folgendes:

    - Wenn Sie dies noch nicht getan haben, integrieren Sie ISE für die Netzwerkzugriffssteuerung mit Intune, so wie es im Abschnitt **Konfigurieren von Microsoft Intune als MDM-Server** im [Administratorleitfaden zu Cisco Identity Services Engine](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html) beschrieben ist.
    - Aktivieren Sie die NAC im VPN-Profil.

  **Wenn Sie Citrix SSO mit Gateway verwenden**, führen Sie Folgendes durch:

  - Vergewissern Sie sich, dass Sie Citrix Gateway 12.0.59 oder höher verwenden.
  - Vergewissern Sie sich, dass Ihre Benutzer Citrix SSO 1.1.6 oder höher auf ihren Geräten installiert haben.
  - Integrieren Sie Citrix Gateway für NAC in Intune. Siehe den Citrix-Bereitstellungsleitfaden [Integrating Microsoft Intune/Enterprise Mobility Suite with NetScaler (LDAP+OTP Scenario)](https://www.citrix.com/content/dam/citrix/en_us/documents/guide/integrating-microsoft-intune-enterprise-mobility-suite-with-netscaler.pdf) (Integration von Microsoft Intune/Enterprise Mobility + Security E3 in NetScaler [Szenario mit LDAP+OTP]).
  - Aktivieren Sie die NAC im VPN-Profil.

  Achten Sie bei **Verwenden von F5 Access** auf Folgendes:

  - Vergewissern Sie sich, dass Sie F5 BIG-IP 13.1.1.5 oder höher nutzen. 
  - Integrieren Sie BIG-IP für NAC in Intune. Im F5-Leitfaden [Übersicht: Konfigurieren von APM für Gerätestatusüberprüfungen mit Endpunktverwaltungssystemen](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-client-configuration-7-1-6/6.html#guid-0bd12e12-8107-40ec-979d-c44779a8cc89).
  - Aktivieren Sie die NAC im VPN-Profil.

  Für VPN-Partner mit Unterstützung der Geräte-ID kann der VPN-Client, z. B. Citrix SSO, die ID abrufen. Anschließend kann Intune abgefragt werden, um zu bestätigen, dass das Gerät registriert ist und ob das VPN-Profil konform ist oder nicht.

  - Zum Entfernen dieser Einstellung erstellen Sie das Profil neu und wählen **Ich stimme zu** nicht aus. Anschließend weisen Sie das Profil neu zu.

## <a name="ikev2-settings"></a>IKEv2-Einstellungen

Diese Einstellungen gelten, wenn Sie **Verbindungstyp** > **IKEv2** auswählen.

- **Remote-ID:** Geben Sie die Netzwerk-IP-Adresse, den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN), den Benutzer-FQDN (UserFQDN) oder den ASN1DN des IKEv2-Servers ein. Geben Sie beispielsweise `10.0.0.3` oder `vpn.contoso.com` ein. In der Regel geben Sie den gleichen Wert wie für den [**Verbindungsnamen**](#base-vpn-settings) ein (in diesem Artikel). Dies hängt jedoch von Ihren IKEv2-Servereinstellungen ab.

- **Clientauthentifizierungstyp:** Legen Sie fest, wie sich der VPN-Client im VPN authentifizieren soll Folgende Optionen sind verfügbar:
  - **Benutzerauthentifizierung** (Standard): Die Authentifizierung im VPN erfolgt über Benutzeranmeldeinformationen.
  - **Computerauthentifizierung:** Die Authentifizierung im VPN erfolgt über Computeranmeldeinformationen.

- **Authentifizierungsmethode**: Wählen Sie den Typ der Clientanmeldeinformationen aus, die an den Server gesendet werden sollen. Folgende Optionen sind verfügbar:
  - **Zertifikate:** Es wird ein vorhandenes Zertifikatprofil für die Authentifizierung beim VPN verwendet. Stellen Sie sicher, dass dieses Zertifikatprofil dem Benutzer oder Gerät bereits zugewiesen ist. Andernfalls tritt bei der VPN-Verbindung ein Fehler auf.
    - **Zertifikattyp**: Wählen Sie den Verschlüsselungstyp aus, der vom Zertifikat verwendet werden soll. Stellen Sie sicher, dass der VPN-Server so konfiguriert ist, dass dieser Zertifikattyp akzeptiert wird. Folgende Optionen sind verfügbar:
      - **RSA** (Standardeinstellung)
      - **ECDSA256**
      - **ECDSA384**
      - **ECDSA521**

  - **Benutzername und Kennwort** (nur Benutzerauthentifizierung): Wenn Benutzer eine Verbindung mit dem VPN herstellen, werden sie aufgefordert, ihren Benutzernamen und ihr Kennwort einzugeben.
  - **Gemeinsames Geheimnis** (nur Computerauthentifizierung): Ermöglicht es Ihnen, ein gemeinsames Geheimnis einzugeben, das an den VPN-Server gesendet werden soll.
    - **Gemeinsames Geheimnis:** Geben Sie das gemeinsame Geheimnis ein, das auch als vorinstallierter Schlüssel (Pre-Shared Key, PSK) bezeichnet wird. Stellen Sie sicher, dass der Wert dem auf dem VPN-Server konfigurierten gemeinsamen geheimen Schlüssel entspricht.

- **Allgemeiner Name des Serverzertifikatausstellers:** Ermöglicht es dem VPN-Server, sich beim VPN-Client zu authentifizieren. Geben Sie den allgemeinen Namen (Common Name, CN) für den Zertifikataussteller des VPN-Serverzertifikats ein, das an den VPN-Client auf dem Gerät gesendet wird. Stellen Sie sicher, dass der CN-Wert mit der Konfiguration des VPN-Servers übereinstimmt. Andernfalls tritt bei der VPN-Verbindung ein Fehler auf.
- **Allgemeiner Name des Serverzertifikats:** Geben Sie den allgemeinen Namen des Zertifikats selbst ein. Wenn das Feld leer gelassen wird, wird die Remote-ID verwendet.

- **DPD-Rate (Dead Peer Detection):** Wählen Sie aus, wie häufig der VPN-Client überprüft, ob der VPN-Tunnel aktiv ist. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert:** Verwendet die Standardeinstellung für das iOS/iPadOS-System, was der Auswahl von **Mittel** entsprechen kann.
  - **Keine**: Deaktiviert die Dead Peer Detection.
  - **Niedrig:** Sendet alle 30 Minuten eine Keepalivenachricht.
  - **Mittel** (Standard): Sendet alle 10 Minuten eine Keepalivenachricht.
  - **Hoch**: Sendet alle 60 Sekunden eine Keepalivenachricht.

- **Minimaler TLS-Versionsbereich:** Geben Sie die minimale, zu verwendende TLS-Version ein. Geben Sie `1.0`, `1.1` oder `1.2` ein. Wenn Sie das Feld leer lassen, wird der Standardwert `1.0` verwendet.
- **Maximaler TLS-Versionsbereich:** Geben Sie die maximale, zu verwendende TLS-Version ein. Geben Sie `1.0`, `1.1` oder `1.2` ein. Wenn Sie das Feld leer lassen, wird der Standardwert `1.2` verwendet.

> [!NOTE]
> Der Mindestwert und der Höchstwert der TLS-Version müssen festgelegt werden, wenn die Benutzerauthentifizierung und Zertifikate verwendet werden.

- **Perfect Forward Secrecy (PFS):** Klicken Sie auf **Aktivieren**, um PFS zu aktivieren. PFS ist ein IP-Sicherheitsfeature, das die Auswirkung verringert, wenn ein Sitzungsschlüssel kompromittiert wird. Durch Auswahl von **Deaktivieren** (Standardeinstellung) wird kein PFS verwendet.
- **Überprüfung der Zertifikatsperre:** Klicken Sie auf **Aktivieren**, um sicherzustellen, dass die Zertifikate nicht widerrufen werden, bevor die VPN-Verbindung erfolgreich ist. Diese Überprüfung erfolgt nach dem Best-Effort-Prinzip. Wenn für den VPN-Server ein Timeout auftritt, bevor ermittelt werden kann, ob das Zertifikat gesperrt ist, wird der Zugriff gewährt. Bei Auswahl von **Deaktivieren** (Standardeinstellung) wird nicht auf gesperrte Zertifikate überprüft.

- **Sicherheitszuordnungsparameter konfigurieren:** Bei **Nicht konfiguriert** (Standardeinstellung) wird die iOS/iPadOS-Systemstandardeinstellung verwendet. Wählen Sie **Aktivieren** aus, um die beim Erstellen von Sicherheitszuordnungen mit dem VPN-Server verwendeten Parameter einzugeben:
  - **Verschlüsselungsalgorithmus:** Wählen Sie den gewünschten Algorithmus aus:
    - DES
    - 3DES
    - AES-128
    - AES-256 (Standardeinstellung)
    - AES-128-GCM
    - AES-256-GCM
  - **Integritätsalgorithmus:**  Wählen Sie den gewünschten Algorithmus aus:
    - SHA1-96
    - SHA1-160
    - SHA2-256 (Standardeinstellung)
    - SHA2-384
    - SHA2-512
  - **Diffie-Hellman-Gruppe:** Wählen Sie die gewünschte Gruppe aus. Standardmäßig ist Gruppe `2` ausgewählt.
  - **Lebensdauer (Minuten)** : Wählen Sie aus, wie lange die Sicherheitszuordnung aktiv bleibt, bis die Schlüssel rotiert werden. Geben Sie einen ganzzahligen Wert zwischen `10` und `1440` ein (1440 Minuten entsprechen 24 Stunden). Der Standardwert ist `1440`.

- **Konfigurieren Sie eine separate Gruppe von Parametern für untergeordnete Sicherheitszuordnungen**: Für iOS/iPadOS können separate Parameter für die IKE-Verbindung und zugeordnete Verbindungen konfiguriert werden. 

  Bei Festlegung auf **Nicht konfiguriert** (Standardeinstellung) werden die Werte verwendet, die Sie in der vorherigen Einstellung **Sicherheitszuordnungsparameter konfigurieren** eingegeben haben. Wählen Sie **Aktivieren** aus, um die beim Erstellen von *untergeordneten* Sicherheitszuordnungen mit dem VPN-Server zu verwendenden Parameter einzugeben:
  - **Verschlüsselungsalgorithmus:** Wählen Sie den gewünschten Algorithmus aus:
    - DES
    - 3DES
    - AES-128
    - AES-256 (Standardeinstellung)
    - AES-128-GCM
    - AES-256-GCM
  - **Integritätsalgorithmus:**  Wählen Sie den gewünschten Algorithmus aus:
    - SHA1-96
    - SHA1-160
    - SHA2-256 (Standardeinstellung)
    - SHA2-384
    - SHA2-512
  - **Diffie-Hellman-Gruppe:** Wählen Sie die gewünschte Gruppe aus. Standardmäßig ist Gruppe `2` ausgewählt.
  - **Lebensdauer (Minuten)** : Wählen Sie aus, wie lange die Sicherheitszuordnung aktiv bleibt, bis die Schlüssel rotiert werden. Geben Sie einen ganzzahligen Wert zwischen `10` und `1440` ein (1440 Minuten entsprechen 24 Stunden). Der Standardwert ist `1440`.

## <a name="automatic-vpn-settings"></a>Automatische VPN-Einstellungen

- **VPN pro App**: Aktiviert das Pro-App-VPN. VPN-Verbindungen können automatisch ausgelöst werden, wenn bestimmte Apps geöffnet sind. Apps lassen sich auch diesem VPN-Profil zuweisen. Ein Pro-App-VPN wird für IKEv2 nicht unterstützt. Weitere Informationen finden Sie in den [Anweisungen zum Einrichten des Pro-App-VPN für iOS/iPadOS-Geräte](vpn-setting-configure-per-app.md). 
  - **Anbietertyp**: Nur für „Pulse Secure“ und „Benutzerdefiniertes VPN“ verfügbar.
  - Wenn Sie **Pro-App-VPN**-Profile für iOS/iPadOS mit Pulse Secure oder einem benutzerdefinierten VPN verwenden, können Sie das Tunneln entweder auf App-Ebene (app-proxy) oder auf Paketebene (packet-tunnel) nutzen. Legen Sie für Tunneln auf App-Ebene den Wert **ProviderType** auf **app-proxy** oder für Tunneln auf Paketebene auf **packet-tunnel** fest. Wenn Sie sich nicht sicher sind, welcher Wert benutzt werden soll, lesen Sie dies in der Dokumentation Ihres VPN-Anbieters nach.
  - **Safari-URLs, die dieses VPN auslösen**: Fügen Sie eine oder mehrere Website-URLs hinzu. Wenn diese URLs mit dem Safari-Browser auf dem Gerät aufgerufen werden, wird die VPN-Verbindung automatisch aufgebaut.

- **Bedarfsgesteuertes VPN**: Konfigurieren Sie bedingte Regeln, die steuern, wann die VPN-Verbindung gestartet wird. Erstellen Sie beispielsweise eine Bedingung, in der die VPN-Verbindung nur verwendet wird, wenn ein Gerät nicht mit einem WLAN des Unternehmens verbunden ist. Oder erstellen Sie eine Bedingung. Wenn beispielsweise ein Gerät nicht auf eine von Ihnen angegebene DNS-Suchdomäne zugreifen kann, wird die VPN-Verbindung nicht gestartet.

  - **SSIDs oder DNS-Suchdomänen**: Wählen Sie aus, ob diese Bedingung **SSIDs** des Drahtlosnetzwerks oder **DNS-Suchdomänen** verwenden soll. Klicken Sie auf **Hinzufügen**, um SSIDs oder Suchdomänen zu konfigurieren.
  - **URL-Zeichenfolgentest**: (Optional) Geben Sie eine URL ein, die die Regel als Test verwenden soll. Wenn das Gerät auf diese URL ohne Umleitung zugreift, wird die VPN-Verbindung gestartet. Und das Gerät wird mit der Ziel-URL verbunden. Der Standort des URL-Zeichenfolgentests wird dem Benutzer nicht angezeigt.

    Bei einem URL-Zeichenfolgentest handelt es sich beispielsweise um eine URL eines Überwachungswebservers, der die Gerätekonformität prüft, bevor die VPN-Verbindung hergestellt wird. Alternativ testet die URL die Fähigkeit des VPN, eine Verbindung mit einem Standort herzustellen, bevor das Gerät über das VPN mit der Ziel-URL verbunden wird.
.
  - **Domänenaktion**: Wählen Sie eine der folgenden Optionen aus:
    - Bei Bedarf verbinden
    - Nie verbinden
  - **Aktion**: Wählen Sie eine der folgenden Optionen aus:
    - Verbinden
    - Verbindung auswerten
    - Ignorieren
    - Trennen

## <a name="proxy-settings"></a>Proxyeinstellungen

Wenn Sie einen Proxy verwenden, konfigurieren Sie die folgenden Einstellungen. Proxyeinstellungen sind nicht für Zscaler-VPN-Verbindungen verfügbar.  

- **Automatisches Konfigurationsskript:** Verwenden Sie eine Datei, um den Proxyserver zu konfigurieren. Geben Sie die **Proxyserver-URL** (z.B. `http://proxy.contoso.com`) ein, unter der die Konfigurationsdatei zu finden ist.
- **Adresse**: Geben Sie die IP-Adresse des vollständig qualifizierten Hostnamens des Proxyservers ein.
- **Portnummer:** Geben Sie die Portnummer ein, die dem Proxyserver zugeordnet ist.

## <a name="next-steps"></a>Nächste Schritte

Das Profil ist nun erstellt, führt aber noch keine Aktionen durch. Die nächsten Schritte sind das [Zuweisen von Benutzer- und Geräteprofilen in Microsoft Intune](device-profile-assign.md) und das [Überwachen von Geräteprofilen in Microsoft Intune](device-profile-monitor.md).

Konfigurieren Sie VPN-Einstellungen für [Android-](vpn-settings-android.md), [Android Enterprise-](vpn-settings-android-enterprise.md), [macOS-](vpn-settings-macos.md) und [Windows 10-](vpn-settings-windows-10.md)-Geräte.
