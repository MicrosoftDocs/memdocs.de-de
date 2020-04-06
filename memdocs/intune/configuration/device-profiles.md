---
title: 'Gerätefunktionen und -einstellungen in Microsoft Intune: Azure | Microsoft-Dokumentation'
description: Übersicht über die unterschiedlichen Microsoft Intune-Geräteprofile. Sie erhalten Informationen zu Funktionen, Einschränkungen, E-Mail-Adressen, WLAN, VPN, Bildungswesen, Zertifikaten, zum Upgrade von Windows 10, BitLocker und Microsoft Defender, Windows Information Protection sowie zu administrativen Vorlagen und benutzerdefinierten Einstellungen für die Gerätekonfiguration im Endpoint Manager Admin Center. Verwenden Sie diese Profile zum Verwalten und Schützen von Daten und Geräten in Ihrem Unternehmen.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 386e59fe3a7156a8bb74ed39a1b2fcad6ad91dad
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359303"
---
# <a name="apply-features-and-settings-on-your-devices-using-device-profiles-in-microsoft-intune"></a>Anwenden von Einstellungen und Funktionen auf Ihren Geräten mit Geräteprofilen in Microsoft Intune

Microsoft Intune umfasst Einstellungen und Funktionen, die Sie auf unterschiedlichen Geräten in Ihrer Organisation aktivieren oder deaktivieren können. Diese Einstellungen und Funktionen werden zu „Konfigurationsprofilen“ hinzugefügt. Sie können Profile für unterschiedliche Geräte und Plattformen einrichten, z. B. für iOS/iPadOS, Android-Geräteadministrator, Android Enterprise und Windows. Verwenden Sie Intune, um das Profil Geräten zuzuweisen.

Im Rahmen Ihrer MDM-Lösung (Mobile Device Management, Verwaltung mobiler Geräte) können Sie diese Konfigurationsprofile verwenden, um verschiedene Aufgaben zu erledigen. Beispiele für Profile:

- Verwenden Sie auf Windows 10-Geräten eine Profilvorlage, die ActiveX-Steuerelemente im Internet Explorer blockiert.
- Ermöglichen Sie es Benutzern auf iOS/iPadOS- und macOS-Geräten, AirPrint-Drucker in Ihrer Organisation zu verwenden.
- Gewähren oder verhindern Sie den Zugriff per Bluetooth auf das Gerät.
- Erstellen Sie ein WLAN- oder VPN-Profil, das verschiedenen Geräten den Zugriff auf Ihr Unternehmensnetzwerk ermöglicht.
- Verwalten Sie Softwareupdates, auch wenn sie installiert werden.
- Führen Sie ein Android-Gerät als dediziertes Kioskgerät aus, auf dem bei Bedarf auch mehr als eine App ausgeführt werden kann.

In diesem Artikel erhalten Sie einen Überblick über die unterschiedlichen Arten von Profilen, die Sie erstellen können. Verwenden Sie diese Profile, um bestimmte Funktionen auf den Geräten zuzulassen oder zu verhindern.

## <a name="administrative-templates"></a>Administrative Vorlagen

[Administrative Vorlagen](administrative-templates-windows.md) enthalten Hunderte von Einstellungen, die Sie für Internet Explorer, OneDrive, Remotedesktop, Word, Excel oder andere Office-Programme konfigurieren können.

Diese Vorlagen bieten Administratoren eine vereinfachte Ansicht der Einstellungen ähnlich wie die Gruppenrichtlinie, sind aber vollständig cloudbasiert.

Dieses Features unterstützt folgende Betriebssysteme:

- Windows 10 und höher

## <a name="certificates"></a>Zertifikate

[Zertifikate](../protect/certificates-configure.md) konfigurieren vertrauenswürdige SCEP- und PKCS-Zertifikate, die Geräten zugewiesen werden. Diese Zertifikate authentifizieren WLAN-, VPN- und E-Mail-Profile.

Dieses Features unterstützt folgende Betriebssysteme:

- Android-Geräteadministrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows Phone 8.1
- Windows 8.1
- Windows 10 und höher

## <a name="custom-profile"></a>Benutzerdefiniertes Profil

Mithilfe von [benutzerdefinierten Einstellungen](custom-settings-configure.md) können Administratoren Geräteeinstellungen zuweisen, die nicht in Intune integriert sind. So können beispielsweise auf Android-Geräten OMA-URI-Werte eingegeben werden. Auf iOS/iPadOS-Geräten können Sie eine Konfigurationsdatei importieren, die Sie in Apple Configurator erstellt haben.

Dieses Features unterstützt folgende Betriebssysteme:

- Android-Geräteadministrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows Phone 8.1

## <a name="delivery-optimization"></a>Übermittlungsoptimierung

[Übermittlungsoptimierung](delivery-optimization-windows.md) macht das Bereitstellen von Softwareupdates benutzerfreundlicher. Diese Einstellungen ersetzen die **Softwareupdates** > **Windows 10-Updatering**-Einstellungen.

Verwenden Sie diese Einstellungen, um zu steuern, wie Softwareupdates auf Geräte in Ihrer Organisation heruntergeladen werden. Beispielsweise können Sie Benutzer ihre eigenen Updates erhalten lassen, oder Updates, die die Übermittlungsoptimierungs-Clouddienste in einem Geräteprofil verwenden.

Dieses Features unterstützt folgende Betriebssysteme:

- Windows 10 und höher

## <a name="derived-credential"></a>Abgeleitete Anmeldeinformation

[Abgeleitete Anmeldeinformationen](../protect/derived-credentials.md) sind Zertifikate auf Smartcards, die zur Authentifizierung, Signierung und Verschlüsselung dienen. In Intune können Sie Profile mit diesen Anmeldeinformationen für Apps, E-Mail-Profile, Verbindungen mit VPNs, S/MIME und WLAN verwenden.

Dieses Features unterstützt folgende Betriebssysteme:

- Android Enterprise
- iOS/iPadOS

## <a name="device-features"></a>Gerätefunktionen

Mit [Gerätefunktionen](device-features-configure.md) können Sie Funktionen wie beispielsweise AirPrint, Benachrichtigungen und Nachrichten auf dem Sperrbildschirm auf iOS/iPadOS- und macOS-Geräten steuern.

Dieses Features unterstützt folgende Betriebssysteme:

- iOS/iPadOS
- macOS

## <a name="device-firmware-configuration-interface"></a>Schnittstelle zur Konfiguration der Gerätefirmware

Die [Schnittstelle zur Konfiguration der Gerätefirmware](device-firmware-configuration-interface-windows.md) (DFCI) ermöglicht es Administratoren, UEFI-Einstellungen (BIOS) mithilfe von Intune zu aktivieren oder zu deaktivieren. Verwenden Sie diese Einstellungen, um die Sicherheit auf der Ebene der Firmware zu erhöhen, die in der Regel resilient gegen böswillige Angriffe ist.

Dieses Features unterstützt folgende Betriebssysteme:

- Windows 10 1809 und höher auf unterstützter Firmware

## <a name="device-restrictions"></a>Geräteeinschränkungen

Mit [Geräteeinschränkungen](device-restrictions-configure.md) werden Einstellungen für Sicherheit, Hardware, Datenfreigabe und viele andere Einstellungen auf dem Gerät gesteuert. Sie können beispielsweise ein Geräteeinschränkungsprofil erstellen, das verhindert, dass Benutzer von iOS/iPadOS-Geräten auf die Kamera des Geräts zugreifen. 

Dieses Features unterstützt folgende Betriebssysteme:

- Android-Geräteadministrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 10 und höher
- Windows 10 Team

## <a name="domain-join"></a>Domänenbeitritt

Der [Domänenbeitritt](domain-join-configure.md) konfiguriert Informationen für die lokale Active Directory-Domäne. Diese Informationen werden für in Hybrid-Azure AD eingebundene Geräte bereitgestellt, wenn sie mit Windows Autopilot und Intune bereitgestellt werden. Dieses Profil teilt Geräten mit, welcher Domäne und Organisationseinheit sie beitreten sollen.

Dieses Features unterstützt folgende Betriebssysteme:

- Windows 10 und höher

## <a name="edition-upgrade"></a>Upgrade der Edition

Mit [Windows 10-Editionsupgrades](edition-upgrade-configure-windows-10.md) können Sie Geräte, auf denen einige Windows 10-Versionen ausgeführt werden, automatisch auf eine neuere Edition upgraden.

Dieses Features unterstützt folgende Betriebssysteme:

- Windows 10 und höher

## <a name="education"></a>Education

Mit den [Education settings - Windows 10](education-settings-configure.md) (Education-Einstellungen: Windows 10) können Sie Optionen für die [Take a Test-Windows-App](https://docs.microsoft.com/education/windows/take-tests-in-windows-10) konfigurieren. Wenn Sie diese Optionen konfigurieren, können keine anderen Apps auf dem Gerät ausgeführt werden, bis der Test abgeschlossen ist.

In den [Einstellungen für Bildungseinrichtungen (iOS/iPadOS)](../fundamentals/education-settings-configure-ios-shared.md) wird die iOS/iPadOS-Classroom-App so konfiguriert, dass der Unterricht strukturiert und Geräte von Schülern/Kursteilnehmern im Kursraum gesteuert werden können. Sie können iPad-Geräte so konfigurieren, dass mehrere Schüler/Kursteilnehmer gemeinsam ein Gerät verwenden können.

## <a name="email"></a>E-Mail

Mit [E-Mail-Einstellungen](email-settings-configure.md) können Sie Exchange ActiveSync-E-Mail-Einstellungen auf den Geräten erstellen, zuweisen und überwachen. E-Mail-Profile helfen bei der Einheitlichkeit, beim Reduzieren der Anzahl von Supportanfragen und ermöglichen Endbenutzern den Zugriff auf Unternehmens-E-Mails auf ihren persönlichen Geräten, ohne dass ihrerseits eine Konfiguration erforderlich wäre. 

Dieses Features unterstützt folgende Betriebssysteme:

- Android-Geräteadministrator
- Android Enterprise
- iOS/iPadOS
- Windows Phone 8.1
- Windows 10 und höher

## <a name="endpoint-protection"></a>Endpoint Protection

[Endpoint Protection](../protect/endpoint-protection-configure.md) konfiguriert BitLocker- und Microsoft Defender-Einstellungen für Windows 10-Geräte. Außerdem werden auf macOS-Geräten die Firewall, das Gateway und andere Ressourcen konfiguriert.

Informationen zur Integration von Microsoft Defender Advanced Threat Protection in Microsoft Intune finden Sie unter [Konfigurieren von Endpunkten mithilfe von Tools für die mobile Geräteverwaltung (MDM)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-mdm).

Dieses Features unterstützt folgende Betriebssysteme:

- macOS
- Windows 10 und höher

## <a name="esim-cellular---public-preview"></a>eSIM-Mobiltelefone: Public Preview

Mit [eSIM-Mobilfunkprofilen](esim-device-configuration.md) können Administratoren Tarife für Mobilfunkdaten auf Ihren verwalteten Geräten für den Zugriff auf das Internet und auf Daten konfigurieren. Sobald Sie Aktivierungscodes von Ihrem Mobilfunkanbieter erhalten haben, verwenden Sie Intune, um diese Codes zu importieren und dann Ihren auf eSIM ausgelegten Geräten zuzuweisen.

Dieses Features unterstützt folgende Betriebssysteme:

- Windows 10 Fall Creators Update und höher

## <a name="extensions"></a>-Erweiterungen

[Kernel-Erweiterungen](kernel-extensions-overview-macos.md) ermöglichen es Administratoren, Funktionen oder Programme auf Kernel-Ebene auf macOS-Geräten hinzuzufügen. Konfigurieren Sie diese Einstellungen, um allen Erweiterungen eines bestimmten Entwicklers oder Partners zu vertrauen oder bestimmte Kernelerweiterungen zuzulassen.

Dieses Features unterstützt folgende Betriebssysteme:

- macOS

## <a name="identity-protection"></a>Schutz der Identität

[Identity Protection](../protect/identity-protection-configure.md) steuert die Windows Hello for Business-Funktionen auf Windows 10- und Windows 10 Mobile-Geräten. Konfigurieren Sie diese Einstellungen, um Windows Hello for Business für Benutzer und Geräte zur Verfügung zu stellen und die Anforderungen für Geräte-PINs und Gesten festzulegen.  

Dieses Features unterstützt folgende Betriebssysteme:  

- Windows 10 und höher
- Windows Holographic for Business  

## <a name="kiosk"></a>Kiosk

Im Profil für [Kioskeinstellungen](kiosk-settings.md) kann ein Gerät so konfiguriert werden, dass auf diesem eine oder mehrere Apps ausgeführt werden. In Ihrem Kiosk können Sie auch andere Features wie ein Startmenü und einen Webbrowser anpassen.

Dieses Features unterstützt folgende Betriebssysteme:

- Windows 10 und höher

Kioskeinstellungen sind auch als Geräteeinschränkungen für [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices) und [iOS/iPadOS](device-restrictions-ios.md#kiosk) verfügbar.

## <a name="microsoft-defender-atp"></a>Microsoft Defender ATP

[Microsoft Defender ATP (Advanced Threat Protection)](../protect/advanced-threat-protection.md) integriert mit Intune, um Geräte zu überwachen und zu schützen. Sie können Risikostufen festlegen und festlegen, was geschieht, wenn Geräte die Risikostufe überschreiten. In Kombination mit bedingtem Zugriff können Sie somit bösartigen Aktivitäten in Ihrer Organisation vorbeugen.

Dieses Features unterstützt folgende Betriebssysteme:

- Windows 10 und höher

## <a name="oemconfig"></a>OEMConfig

[OEMConfig](android-oem-configuration-overview.md) ist ein Standard, der es Originalgeräteherstellern (OEMs) und EMM-Anbietern (Enterprise Mobility Management) ermöglicht, OEM-spezifische Funktionen auf standardisierte Weise auf Android Enterprise-Geräten zu erstellen und zu unterstützen. Mit „OEMConfig“ kann ein Originalgerätehersteller ein Schema erstellen, das OEM-spezifische Verwaltungsfunktionen definiert, und es in eine App einbetten, die in Google Play hochgeladen wird. Intune liest das Schema aus der App und ermöglicht Intune-Administratoren die Konfiguration der Einstellungen im Schema.

Dieses Features unterstützt folgende Betriebssysteme:

- Android Enterprise (OEMConfig)

## <a name="powershell-scripts"></a>PowerShell-Skripts

[PowerShell-Skripts auf Windows 10-Geräten](../apps/intune-management-extension.md) verwenden die Intune-Verwaltungserweiterung, um Ihre PowerShell-Skripts in Intune hochzuladen und diese Skripte dann auf Ihren Geräten auszuführen. Beachten Sie auch, was für die Verwendung der Erweiterung erforderlich ist, wie sie in Intune hinzufügt wird und weitere wichtige Informationen.

Dieses Features unterstützt folgende Betriebssysteme:

- Windows 10 und höher
- Windows Holographic for Business

## <a name="preference-file"></a>Einstellungsdatei

[Einstellungsdateien](preference-file-settings-macos.md) auf macOS-Geräten enthalten Informationen über Apps. Sie können Einstellungsdateien beispielsweise verwenden, um Webbrowsereinstellungen zu steuern oder Apps anzupassen.

Dieses Features unterstützt folgende Betriebssysteme:

- macOS

## <a name="shared-multi-user-device"></a>Von mehreren Benutzern gemeinsam verwendetes Gerät

[Windows 10](shared-user-device-settings-windows.md) und [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md) umfassen Einstellungen zur Verwaltung von Geräten mit mehreren Benutzern, auch bekannt als freigegebene Geräte oder freigegebene PCs. Wenn sich ein Benutzer bei dem Gerät anmeldet, wählen Sie aus, ob der Benutzer die Optionen des Energiesparmodus ändern oder Dateien auf dem Gerät speichern kann. Ein weiteres Beispiel ist das Erstellen einer Richtlinie, die inaktive Anmeldeinformationen von Windows HoloLens-Geräten löscht, um Speicherplatz zu sparen.

Diese Einstellungen für von mehreren Benutzern gemeinsam verwendete Geräte ermöglichen es einem Administrator, einige der Gerätefunktionen zu steuern und diese freigegebenen Geräte mit Intune zu verwalten.

Dieses Features unterstützt folgende Betriebssysteme:

- Windows 10 und höher
- Windows Holographic for Business

## <a name="update-policies"></a>Updaterichtlinien

Im Artikel [Hinzufügen von iOS-Softwareupdaterichtlinien in Intune](../protect/software-updates-ios.md) erfahren Sie, wie Sie iOS/iPadOS-Richtlinien erstellen und zuweisen, um Softwareupdates auf Ihren iOS/iPadOS-Geräten zu installieren. Außerdem können Sie den Installationsstatus überprüfen.

Informationen zu Updaterichtlinien für Windows-Geräte finden Sie unter [Übermittlungsoptimierung](delivery-optimization-windows.md). 

Dieses Features unterstützt folgende Betriebssysteme:

- iOS/iPadOS

## <a name="vpn"></a>VPN

Mit [VPN-Einstellungen](vpn-settings-configure.md) können Sie Benutzern und Geräten in Ihrer Organisation VPN-Profile zuweisen, damit diese einfach eine sichere Verbindung mit dem Netzwerk herstellen können. 

Virtuelle private Netzwerke (Virtual Private Networks, VPNs) ermöglichen Benutzern einen sicheren Remotezugriff auf Ihr Unternehmensnetzwerk. Mit einem VPN-Verbindungsprofil stellen Geräte eine Verbindung mit dem VPN-Server her. 

Dieses Features unterstützt folgende Betriebssysteme: 

- Android-Geräteadministrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows Phone 8.1
- Windows 8.1
- Windows 10 und höher

## <a name="wi-fi"></a>WLAN

Mit [WLAN-Einstellungen](wi-fi-settings-configure.md) können Sie Benutzern und Geräten WLAN-Einstellungen zuweisen. Wenn Sie ein WLAN-Profil zuweisen, erhalten Benutzer Zugriff auf Ihr Unternehmens-WLAN, ohne es selbst konfigurieren zu müssen. 

Dieses Features unterstützt folgende Betriebssysteme: 

- Android-Geräteadministrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 8.1 (nur Import)
- Windows 10 und höher

## <a name="zebra-mobility-extensions-mx"></a>Zebra Mobility Extensions (MX)

Mit [Zebra Mobility Extensions (MX)](android-zebra-mx-overview.md) können Administratoren Zebra-Geräte in Intune verwenden und verwalten. Sie erstellen StageNow-Profile mit Ihren Einstellungen und verwenden dann Intune, um diese Profile Ihren Zebra-Geräten zuzuweisen und bereitzustellen. Unter [StageNow-Protokolle und häufige Probleme](android-zebra-mx-logs-troubleshoot.md) finden Sie weitere Informationen zur Problembehebungen bei Profilen und zu möglichen Problemen bei der Verwendung von StageNow.

Dieses Features unterstützt folgende Betriebssysteme:

- Android-Geräteadministrator (Mobility-Erweiterungen)

## <a name="manage-and-troubleshoot"></a>Verwaltung und Problembehandlung

[Verwalten Sie Ihre Profile](device-profile-monitor.md), um den Status von Geräten und die zugewiesenen Profile zu überprüfen. Lösen Sie Konflikte leichter, indem Sie sich die Einstellungen ansehen, die Konflikte verursachen, und die Profile, die diese Einstellungen enthalten. Unter [Häufige Probleme und Auflösungen](device-profile-troubleshoot.md) werden wichtige Informationen für Administratoren zusammengefasst, die mit Profilen arbeiten. Dort wird u. a. beschrieben, wie Sie ein Profil löschen können und wann Benachrichtigungen an Geräte geschickt werden.

## <a name="next-steps"></a>Nächste Schritte

Wählen Sie Ihre Plattform aus, und legen Sie los.
