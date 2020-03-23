---
title: Intune-Einstellungen für Sicherheitsbaselines in Microsoft Defender Advanced Threat Protection
titleSuffix: Microsoft Intune
description: Von Intune unterstützte Einstellungen für Sicherheitsbaselines zur Verwaltung von Microsoft Defender Advanced Threat Protection
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/05/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7ebea853ac536b182a9cfe35e8b291aea3a776f0
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79351200"
---
# <a name="microsoft-defender-advanced-threat-protection-baseline-settings-for-intune"></a>Microsoft Defender Advanced Threat Protection-Baselineeinstellungen für Intune

Zeigen Sie die Baselineeinstellungen für Microsoft Defender Advanced Threat Protection (früher Windows Defender Advanced Threat Protection) an, die von Microsoft Intune unterstützt werden. Die Standardeinstellungen der ATP-Baseline (Advanced Threat Protection) entsprechen der für ATP empfohlenen Konfiguration und stimmen möglicherweise nicht mit den Standardeinstellungen anderer Sicherheitsbaselines überein.  

Die Microsoft Defender Advanced Threat Protection-Baseline ist verfügbar, wenn Ihre Umgebung den Anforderungen zur Verwendung von [Microsoft Defender Advanced Threat Protection](advanced-threat-protection.md#prerequisites) entspricht. 

Diese Baseline wurde für physische Geräte optimiert und wird zurzeit nicht für die Verwendung auf virtuellen Computern (VMs) oder VDI-Endpunkten empfohlen. Bestimmte Baselineeinstellungen können sich auf interaktive Remotesitzungen in virtualisierten Umgebungen auswirken. Weitere Informationen finden Sie unter [Increase compliance to the Microsoft Defender ATP security baseline (Erhöhung der Compliance für die Microsoft Defender ATP-Sicherheitsbaseline)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline).

## <a name="application-guard"></a>Application Guard  
Weitere Informationen finden Sie in der Windows-Dokumentation unter [WindowsDefenderApplicationGuard CSP](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp).  

Während der Verwendung von Microsoft Edge schützt Microsoft Defender Application Guard Ihre Umgebung vor Websites, die von Ihrer Organisation nicht als vertrauenswürdig definiert wurden. Wenn Benutzer Websites besuchen, die nicht in Ihrer isolierten Netzwerkgrenze aufgelistet sind, werden die Websites in einer virtuellen Hyper-V-Browsersitzung geöffnet. Vertrauenswürdige Websites werden durch eine Netzwerkgrenze definiert.  

- **Application Guard** - *Settings/AllowWindowsDefenderApplicationGuard*  
  Wählen Sie *Ja* aus, um dieses Feature zu aktivieren. Dadurch werden nicht vertrauenswürdige Websites in einem virtualisierten Hyper-V-Browsercontainer geöffnet. Wenn *Nicht konfiguriert* festgelegt wurde, wird jede beliebige Website (vertrauenswürdig oder nicht vertrauenswürdig) auf dem Gerät (und nicht in einem virtualisierten Container) geöffnet.  

  **Standardeinstellung:** Ja
 
  - **External content on enterprise sites** (Externer Inhalt auf Unternehmenswebsites) - *Settings/BlockNonEnterpriseContent*  
    Wählen Sie *Ja* aus, um Inhalte von nicht genehmigten Websites zu blockieren, sodass sie nicht geladen werden können. Wenn *Nicht konfiguriert* festgelegt wurde, können Websites, bei denen es sich nicht um Unternehmenswebsites handelt, auf dem Gerät geöffnet werden. 
 
    **Standardeinstellung:** Ja

  - **Clipboard behavior** (Verhalten der Zwischenablage) - *Settings/ClipboardSettings*  
    Legen Sie zulässige Aktionen für das Kopieren und Einfügen zwischen dem lokalen Computer und dem virtuellen Browser von Application Guard fest.  Zu den Optionen gehören:
    - Nicht konfiguriert  
    - Kopieren und Einfügen zwischen PC und Browser blockieren: Hierbei wird beides blockiert. Daten können zwischen dem Computer und dem virtuellen Browser nicht übertragen werden.  
    - Kopieren und Einfügen nur von Browser zu PC zulassen: Daten können nicht vom PC in den virtuellen Browser übertragen werden.
    - Kopieren und Einfügen nur von PC zu Browser zulassen: Daten können nicht vom virtuellen Browser auf den Host-PC übertragen werden.
    - Kopieren und Einfügen zwischen PC und Browser zulassen: Kein Blockieren von Inhalten  

    **Standardeinstellung:** Kopieren und Einfügen zwischen PC und Browser blockieren  

- **Richtlinie zur Windows-Netzwerkisolation – Unternehmensnetzwerk-Domänennamen**  
  Weitere Informationen finden Sie in der Windows-Dokumentation unter [Policy CSP – NetworkIsolation (Richtlinien-Konfigurationsdienstanbieter – NetworkIsolation)](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-networkisolation).
  
  Geben Sie eine Liste von Enterprise-Ressourcen als Domänen, IP-Adressbereiche und Netzwerkgrenzen an, die in der Cloud gehostet werden, die Application Guard als Unternehmensstandorte behandelt.  

  **Standard**: securitycenter.windows.com

## <a name="application-reputation"></a>Anwendungszuverlässigkeit  

Weitere Informationen finden Sie unter [Policy CSP - SmartScreen (Richtlinien-Konfigurationsdienstanbieter: SmartScreen)](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-smartscreen) in Ihrer Windows-Dokumentation.

- **Ausführen nicht überprüfter Dateien blockieren**  
    Hindern Sie Benutzer am Ausführen von nicht überprüften Dateien. Wenn *Nicht konfiguriert* festgelegt wurde, können Mitarbeiter SmartScreen-Warnungen ignorieren und schädliche Dateien ausführen. Legen Sie *Ja* fest, damit Mitarbeiter SmartScreen-Warnungen nicht ignorieren und schädliche Dateien nicht ausführen können.  
  
    **Standardeinstellung:** Ja

- **SmartScreen für Apps und Dateien anfordern**  
  Legen Sie *Ja* fest, um SmartScreen für Windows zu aktivieren.  

  **Standardeinstellung:** Ja

## <a name="attack-surface-reduction"></a>Verringerung der Angriffsfläche  

- **Office apps launch child process type** (Untergeordnete Prozesse in Office-Apps starten)  
  [Regel zur Verringerung der Angriffsfläche](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) – Wenn *Blockieren* festgelegt wurde, ist das Erstellen von untergeordneten Prozessen mit Office-Apps nicht gestattet. Office-Apps umfassen Word, Excel, PowerPoint, OneNote und Access. Die Erstellung eines untergeordneten Prozesses ist ein typisches Verhalten für eine Schadsoftware – besonders für makrobasierte Angriffe, mit denen versucht wird, Office-Apps zum Starten oder Herunterladen schädlicher ausführbarer Dateien zu verwenden.  

  **Standardeinstellung:** Blockieren

- **Ausführungstyp für heruntergeladene Nutzlast für Skript**  
  [Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection) – Geben Sie eine Erkennungsstufe für potenziell unerwünschte Anwendungen an, die heruntergeladen werden oder bei denen eine Installation versucht wird.  

  **Standardeinstellung:** Blockieren 

- **Diebstahl von Anmeldeinformationen verhindern**  
  Legen Sie die Einstellung *Aktivieren* auf [Schützen abgeleiteter Domänenanmeldeinformationen mit Credential Guard](https://docs.microsoft.com/windows/security/identity-protection/credential-guard/credential-guard) fest. Microsoft Defender Credential Guard nutzt auf Virtualisierung basierende Sicherheitsverfahren, um Geheimnisse zu isolieren, sodass nur privilegierte Systemsoftware auf diese Daten zugreifen kann. Nicht autorisierter Zugriff auf diese geheimen Schlüssel kann zum Diebstahl von Anmeldeinformationen führen, z. B. durch einen Pass-the-Hash- oder einen Pass-the-Ticket-Angriff. Microsoft Defender Credential Guard verhindert diese Angriffe durch den Schutz von NTLM-Kennworthashes, Kerberos Ticket-Granting Tickets und Anmeldeinformationen, die von Anwendungen als Domänenanmeldeinformationen gespeichert werden.  

  **Standardeinstellung:** Aktivieren Sie

- **Ausführung von E-Mail-Inhalt**  
  [Regel zur Verringerung der Angriffsfläche](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) – Wenn *Blockieren* festgelegt wurde, verhindert diese Regel die Ausführung oder das Starten der folgenden Dateitypen aus einer E-Mail, die in Microsoft Outlook oder einem webbasierten E-Mail-Dienst (z.B. Gmail.com oder Outlook.com) angezeigt wird:  

  - Ausführbare Dateien (z. B. .EXE, DLL oder SCR)  
  - Skriptdateien (z.B. PS PowerShell, VBS VisualBasic oder JS JavaScript)  
  - Skriptarchivdateien  

  **Standardeinstellung:** Blockieren

- **Adobe Reader launch in a child process** (Adobe Reader in einem untergeordneten Prozess starten)  
  [Regel zur Verringerung der Angriffsfläche](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) – Wenn *Aktivieren* festgelegt wurde, verhindert diese Regel, dass Adobe Reader einen untergeordneten Prozess erstellt. Über Social Engineering oder Exploits kann Schadsoftware zusätzliche Payloads herunterladen und starten sowie Adobe Reader unterbrechen.  

  **Standardeinstellung:** Aktivieren Sie

- **Verborgener Makrocode von Skripts**  
  [Regel zur Verringerung der Angriffsfläche](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) – Schadsoftware und andere Bedrohungen versuchen möglicherweise, ihren schädlichen Code in einigen Skriptdateien zu verbergen oder auszublenden. Mit dieser Regel wird verhindert, dass verborgen scheinende Skripts ausgeführt werden.  
    
  **Standardeinstellung:** Blockieren

- **Nicht vertrauenswürdiger USB-Prozess**  
  [Regel zur Verringerung der Angriffsfläche](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) – Wenn *Blockieren* festgelegt wurde, können unsignierte oder nicht vertrauenswürdige ausführbare Dateien von USB-Wechseldatenträgern und SD-Karten nicht ausgeführt werden.

  Ausführbare Dateien umfassen:
  - Ausführbare Dateien (z. B. .EXE, DLL oder SCR)
  - Skriptdateien (z.B. PS PowerShell, VBS VisualBasic oder JS JavaScript)  

  **Standardeinstellung:** Blockieren

- **Injection für andere Prozesse in Office-Apps**  
  [Regel zur Verringerung der Angriffsfläche](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) – Wenn *Blockieren* festgelegt wurde, können Office-Apps, darunter Word, Excel, PowerPoint und OneNote, keinen Code in andere Prozesse einfügen. Das Einfügen von Code wird normalerweise von Schadsoftware zur Ausführung von schädlichem Code verwendet, mit dem versucht wird, die Aktivität vor Antivirusprogrammen zu verbergen.  

  **Standardeinstellung:** Blockieren

- **Win32-Import aus Office-Makrocode gestatten**  
  [Regel zur Verringerung der Angriffsfläche](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) – Wenn *Blockieren* festgelegt wurde, versucht diese Regel, Office-Dateien mit Makrocode zu blockieren, die Win32-DLLs importieren können. Office-Dateien umfassen Word, Excel, PowerPoint und OneNote. Schadsoftware kann Makrocode in Office-Dateien verwenden, um Win32-DLLs zu importieren und zu laden, mit denen dann API-Aufrufe ausgeführt werden, um eine weitere Infektion des gesamten Systems zu ermöglichen.  

  **Standardeinstellung:** Blockieren

- **Office communication apps launch in a child process** (Office-Kommunikations-Apps in einem untergeordneten Prozess starten)  
  [Regel zur Verringerung der Angriffsfläche](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) – Wenn *Aktivieren* festgelegt wurde, verhindert diese Regel, dass Outlook untergeordnete Prozesse erstellt. Durch Blockieren der Erstellung eines untergeordneten Prozesses schützt diese Regel vor Social Engineering-Angriffen und verhindert, dass Exploit-Code ein Sicherheitsrisiko in Outlook ausnutzt.  

  **Standardeinstellung:** Aktivieren Sie

- **Inhaltserstellung oder Start von ausführbaren Office-App-Dateien**  
  [Regel zur Verringerung der Angriffsfläche](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) – Wenn *Blockieren* festgelegt wurde, können Office-Apps keine ausführbaren Inhalte erstellen. Office-Apps umfassen Word, Excel, PowerPoint, OneNote und Access.  

  Diese Regel zielt auf typische Verhalten von verdächtigen und schädlichen Add-Ons und Skripts (Erweiterungen) ab, die ausführbare Dateien erstellen oder starten. Dies ist ein typisches Verfahren von Schadsoftware. Die Verwendung von Erweiterungen durch Office-Apps wird blockiert. Typischerweise verwenden diese Erweiterungen den Windows Scripting Host (WSH-Dateien), um Skripts auszuführen, die bestimmte Aufgaben automatisieren oder von Benutzern erstellte Add-On-Features bieten.

  **Standardeinstellung:** Blockieren

## <a name="bitlocker"></a>BitLocker  

Weitere Informationen finden Sie in der Windows-Dokumentation unter [Einstellungen für BitLocker-Gruppenrichtlinien](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings).  

- **Geräte verschlüsseln**  
  Wählen Sie *Ja* aus, um die BitLocker-Geräteverschlüsselung zu aktivieren. Je nach Gerätehardware und Windows-Version werden Gerätebenutzer möglicherweise aufgefordert zu bestätigen, dass es auf dem Gerät keine Drittanbieterverschlüsselung gibt. Wenn die Windows-Verschlüsselung aktiviert wird, während eine Drittanbieterverschlüsselung aktiv ist, wird das Gerät instabil.  

   **Standardeinstellung:** Ja

- **Richtlinie für BitLocker-Verschlüsselung von Wechseldatenträgern**  
  Die Werte für diese Richtlinie bestimmen die Stärke der Verschlüsselung, die BitLocker für die Verschlüsselung von Wechseldatenträgern verwendet. Unternehmen steuern die Verschlüsselungsstufe für erhöhte Sicherheit (AES-256 ist sicherer als AES-128). Wenn Sie *Ja* auswählen, um diese Einstellung zu aktivieren, können Sie einen Verschlüsselungsalgorithmus und die Verschlüsselungsstärke für Schlüssel bei Festplattenlaufwerken, Betriebssystemlaufwerken und Wechseldatenträgern individuell konfigurieren. Für Festplatten- und Betriebssystemlaufwerke wird die Verwendung des XTS-AES-Algorithmus empfohlen. Für Wechseldatenträger sollten Sie AES-CBC 128-Bit oder AES-CBC 256-Bit verwenden, wenn es in anderen Geräten verwendet wird, auf denen nicht Windows 10, Version 1511 oder höher ausgeführt wird. Das Ändern der Verschlüsselungsmethode hat keine Auswirkungen, wenn das Laufwerk bereits verschlüsselt ist oder die Verschlüsselung gerade ausgeführt wird. In diesen Fällen wird diese Richtlinieneinstellung ignoriert. 

  Konfigurieren Sie bei der Richtlinie für BitLocker-Verschlüsselung von Wechseldatenträgern die folgenden Einstellungen:

  - **Verschlüsselung für Schreibzugriff anfordern**  
    **Standardeinstellung:** Ja

  - **Verschlüsselungsmethode**  
    **Standardeinstellung:** AES-CBC, 128 Bit

- **Speicherkarte verschlüsseln (nur Mobilgeräte):** Wenn *Ja* aktiviert wird, wird die Speicherkarte des mobilen Geräts verschlüsselt.  

   **Standardeinstellung:** Ja

- **Richtlinie für BitLocker-Verschlüsselung von Festplattenlaufwerken**  
  Die Werte für diese Richtlinie bestimmen die Stärke der Verschlüsselung, die BitLocker für die Verschlüsselung von Festplattenlaufwerken verwendet. Unternehmen können die Verschlüsselungsstufe für erhöhte Sicherheit steuern (AES-256 ist sicherer als AES-128). Wenn Sie diese Einstellung aktivieren, können Sie einen Verschlüsselungsalgorithmus konfigurieren und für Festplattenlaufwerke, Betriebssystemlaufwerke und Wechseldatenträger die Verschlüsselungsstärke für Schlüssel individuell konfigurieren. Für Festplatten- und Betriebssystemlaufwerke wird die Verwendung des XTS-AES-Algorithmus empfohlen. Für Wechseldatenträger sollten Sie AES-CBC 128-Bit oder AES-CBC 256-Bit verwenden, wenn es in anderen Geräten verwendet wird, auf denen nicht Windows 10, Version 1511 oder höher ausgeführt wird. Das Ändern der Verschlüsselungsmethode hat keine Auswirkungen, wenn das Laufwerk bereits verschlüsselt ist oder die Verschlüsselung gerade ausgeführt wird. In diesen Fällen wird diese Richtlinieneinstellung ignoriert.

  Konfigurieren Sie bei der Richtlinie für BitLocker-Verschlüsselung von Festplattenlaufwerken die folgenden Einstellungen:

  - **Verschlüsselung für Schreibzugriff anfordern**  
    **Standardeinstellung:** Ja

  - **Verschlüsselungsmethode**  
    **Standardeinstellung:** XTS-AES, 128 Bit

- **Richtlinie für BitLocker-Verschlüsselung von Systemlaufwerken**  
  Die Werte für diese Richtlinie bestimmen die Stärke der Verschlüsselung, die BitLocker für die Verschlüsselung des Systemlaufwerks verwendet. Unternehmen sollten die Verschlüsselungsstufe für erhöhte Sicherheit steuern (AES-256 ist sicherer als AES-128). Wenn Sie diese Einstellung aktivieren, können Sie einen Verschlüsselungsalgorithmus konfigurieren und für Festplattenlaufwerke, Betriebssystemlaufwerke und Wechseldatenträger die Verschlüsselungsstärke für Schlüssel individuell konfigurieren. Für Festplatten- und Betriebssystemlaufwerke wird die Verwendung des XTS-AES-Algorithmus empfohlen. Für Wechseldatenträger sollten Sie AES-CBC 128-Bit oder AES-CBC 256-Bit verwenden, wenn es in anderen Geräten verwendet wird, auf denen nicht Windows 10, Version 1511 oder höher ausgeführt wird. Das Ändern der Verschlüsselungsmethode hat keine Auswirkungen, wenn das Laufwerk bereits verschlüsselt ist oder die Verschlüsselung gerade ausgeführt wird. In diesen Fällen wird diese Richtlinieneinstellung ignoriert.  

  Konfigurieren Sie bei der Richtlinie für BitLocker-Verschlüsselung von Systemlaufwerken die folgenden Einstellungen:  

  - **Verschlüsselungsmethode**  
    **Standardeinstellung:** XTS-AES, 128 Bit

## <a name="device-control"></a>Gerätesteuerung  

- **Bei einer vollständigen Überprüfung Wechseldatenträger überprüfen**  
  [Defender/AllowFullScanRemovableDriveScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning): Wenn *Ja* festgelegt wurde, überprüft Defender während einer vollständigen Überprüfung bei Wechseldatenträgern z.B. USB-Speichersticks auf Schadsoftware und unerwünschte Software. Defender Antivirus überprüft alle Dateien auf USB-Geräten, bevor Dateien darauf ausgeführt werden können.

  Zugehörige Einstellung in dieser Liste: *Defender/AllowFullScanOnMappedNetworkDrives*  

  **Standardeinstellung:** Ja

- **Aufzählung externer Geräte, die mit Kernel-DMA-Schutz nicht kompatibel sind**  
   Lesen Sie dazu *DmaGuard/DeviceEnumerationPolicy* in [Policy CSP – DmaGuard](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy).

  Diese Richtlinie bietet zusätzliche Sicherheit für externe DMA-fähige Geräte. Sie ermöglicht eine bessere Kontrolle über die Aufzählung von externen DMA-fähigen Geräten, die mit DMA Gerätespeicherisolation und Sandboxing nicht kompatibel sind.

  Diese Richtlinie gilt nur, wenn der Kernel-DMA-Schutz unterstützt wird und durch die Systemfirmware aktiviert wurde. Kernel-DMA-Schutz ist eine Plattformfunktion, die nicht durch Richtlinien oder den Benutzer eines Geräts gesteuert werden kann. Er muss zum Zeitpunkt der Herstellung vom System unterstützt werden. 

  Um zu überprüfen, ob das System Kernel-DMA-Schutz unterstützt, führen Sie MSINFO32.exe auf dem System aus, und überprüfen Sie das Feld *Kernel-DMA-Schutz* auf der Übersichtsseite.  

  Zu den Optionen gehören: 
  - *Gerätestandard* – Nach der Anmeldung oder Entsperrung des Bildschirms dürfen Geräte mit für DMA-Neuzuordnung kompatiblen Treibern jederzeit aufgezählt werden. Geräte mit für DMA-Neuzuordnung inkompatiblen Treibern werden erst aufgezählt, nachdem der Benutzer den Bildschirm entsperrt hat.
  - *Alle zulassen* – Alle externen DMA-fähigen PCIe-Geräte werden jederzeit aufgezählt.
  - *Alle blockieren* – Geräte mit für DMA-Neuzuordnung kompatiblen Treibern dürfen jederzeit aufgezählt werden. Geräte mit für DMA-Neuzuordnung inkompatiblen Treibern dürfen DMA niemals starten und ausführen.

  **Standardeinstellung:** Gerätestandard

- **Hardware device installation by device identifiers** (Installation von Hardwaregeräten anhand der Geräte-ID)  
  [DeviceInstallation/PreventInstallationOfMatchingDeviceIDs](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-preventinstallationofmatchingdeviceids) – Bei dieser Richtlinie geben Sie eine Liste von Plug &amp; Play-Hardware-IDs und kompatiblen IDs für Geräte an, bei denen Windows an der Installation gehindert wird. Diese Richtlinieneinstellung hat Vorrang gegenüber jeder anderen Richtlinieneinstellung, die die Installation eines Geräts ermöglicht. Wenn Sie diese Richtlinieneinstellung aktivieren (*Block hardware device installation* – Hardwaregeräteinstallation blockieren – festlegen), wird Windows an der Installation gehindert, wenn die zugehörige Hardware-ID oder kompatible ID in der von Ihnen erstellten Liste enthalten ist. Wenn Sie diese Richtlinieneinstellung auf einem Remotedesktopserver aktivieren, wirkt sich die Richtlinie auf die Umleitung der angegebenen Geräte von einem Remotedesktopclient an den Remotedesktopserver aus. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren (*Allow hardware device installation* – Hardwaregeräteinstallation zulassen – festlegen), können Geräte installiert und aktualisiert werden, sofern andere Richtlinieneinstellungen dies zulassen.  

  **Standardeinstellung:** Block hardware device installation (Hardwaregeräteinstallation blockieren)  

  Wenn *Block hardware device installation* ausgewählt wurde, stehen die folgenden Einstellungen zur Verfügung.
  - **Zugehörige Hardwaregeräte entfernen** (Übereinstimmende Hardwaregeräte entfernen)  
    Diese Einstellung ist nur verfügbar, wenn die Option *Hardware device installation by device identifiers* (Installation von Hardwaregeräten anhand der Geräte-ID) auf *Block hardware device installation* (Hardwaregeräteinstallation blockieren) festgelegt ist.  

    **Standardeinstellung:** Ja

  - **Hardware device identifiers that are blocked** (Blockierte Bezeichner von Hardwaregeräten)  
    Diese Einstellung ist nur verfügbar, wenn die Option *Hardware device installation by device identifiers* (Installation von Hardwaregeräten anhand der Geräte-ID) auf *Block hardware device installation* (Hardwaregeräteinstallation blockieren) festgelegt ist. Um diese Einstellung zu konfigurieren, erweitern Sie die Option, wählen Sie **+ Hinzufügen** aus, und geben Sie die Hardware-Geräte-ID an, die Sie blockieren möchten.  

    **Standardeinstellung:** PCI\CC_0C0A

- **Block direct memory access** (Direkten Speicherzugriff blockieren)  
  [DataProtection/AllowDirectMemoryAccess](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess) – Verwenden Sie diese Richtlinieneinstellung, um den direkten Speicherzugriff (Direct Memory Access, DMA) für alle Hot-Plug-PCI-Downstreamports auf einem Gerät so lange zu verhindern, bis sich ein Benutzer bei Windows anmeldet. Sobald sich ein Benutzer anmeldet, werden die mit den Hot-Plug-PCI-Anschlüssen verbundenen PCI-Geräte von Windows aufgezählt. Jedes Mal, wenn der Benutzer den Computer sperrt, wird DMA an Hot-Plug-PCI-Anschlüssen ohne untergeordnete Geräte blockiert, bis sich der Benutzer erneut anmeldet. Geräte, die vor dem Entsperren des Computers bereits aufgezählt wurden, sind weiterhin funktionsfähig, bis sie entfernt werden oder das System neu gestartet bzw. in den Ruhezustand versetzt wird. 

  Die Richtlinieneinstellung wird nur erzwungen, wenn BitLocker oder die Geräteverschlüsselung aktiviert ist.  

  **Standardeinstellung:** Ja


- **Hardware device installation by device identifiers** (Installation von Hardwaregeräten anhand der Setupklassen)  
  [DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-allowinstallationofmatchingdevicesetupclasses) – Mit dieser Richtlinie können Sie eine Liste von GUIDs für Gerätesetupklassen angeben, bei denen Windows an der Installation gehindert wird. Diese Richtlinieneinstellung hat Vorrang gegenüber jeder anderen Richtlinieneinstellung, die die Installation eines Geräts ermöglicht. Wenn Sie diese Richtlinieneinstellung aktivieren (auf *Block hardware device installation* festlegen), können Gerätetreiber nicht installiert oder aktualisiert werden, deren GUIDs für Gerätesetupklassen in der von Ihnen erstellten Liste enthalten sind. Wenn Sie diese Richtlinieneinstellung auf einem Remotedesktopserver aktivieren, wirkt sich dies auf die Umleitung der angegebenen Geräte von einem Remotedesktopclient an den Remotedesktopserver aus. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren (auf *Allow hardware device installation* festlegen), können Geräte installiert und aktualisiert werden, sofern andere Richtlinieneinstellungen dies zulassen.  

  **Standardeinstellung:** Block hardware device installation (Hardwaregeräteinstallation blockieren)

  Wenn *Block hardware device installation* ausgewählt wurde, stehen die folgenden Einstellungen zur Verfügung.  

  - **Zugehörige Hardwaregeräte entfernen** (Übereinstimmende Hardwaregeräte entfernen)  
    Diese Einstellung ist nur verfügbar, wenn *Hardware device installation by setup classes (Hardwaregeräteinstallation nach Setup-Klasse)* auf *Block hardware device installation (Hardwaregeräteinstallation blockieren)* eingestellt ist.  
 
    **Standardeinstellung:** Ja  

  - **Hardware device identifiers that are blocked** (Blockierte Bezeichner von Hardwaregeräten)  
    Diese Einstellung ist nur verfügbar, wenn „Hardware device installation by setup classes“ auf „Block hardware device installation“ eingestellt ist. Um diese Einstellung zu konfigurieren, erweitern Sie die Option, wählen Sie **+ Hinzufügen** aus, und geben Sie die Hardware-Geräte-ID an, die Sie blockieren möchten.  
 
    **Standardeinstellung:** {d48179be-ec20-11d1-b6b8-00c04fa372a7}

## <a name="endpoint-detection-and-response"></a>Endpunkterkennung und Reaktion  
Weitere Informationen finden Sie in der Windows-Dokumentation unter [WindowsAdvancedThreatProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp).  

- **Häufigkeit von Telemetrieberichten erhöhen** - *Configuration/TelemetryReportingFrequency*

  Hiermit wird die Häufigkeit von Microsoft Defender Advanced Threat Protection-Telemetrieberichten erhöht.  

  **Standardeinstellung:** Ja

- **Beispielfreigabe für alle Dateien** - *Configuration/SampleSharing* 

  Hiermit wird der Konfigurationsparameter für die Microsoft Defender Advanced Threat Protection-Beispielfreigabe zurückgegeben oder festgelegt.  

  **Standardeinstellung:** Ja

## <a name="exploit-protection"></a>Exploit-Schutz  

- **Exploit-Schutz-XML**  
  Weitere Informationen finden Sie in der Windows-Dokumentation unter [Importieren, Exportieren und Bereitstellen von Exploit-Schutz-Konfigurationen](/windows/security/threat-protection/microsoft-defender-atp/import-export-exploit-protection-emet-xml).  

  Ermöglicht dem IT-Administrator, eine Konfiguration vorzunehmen, die für alle Geräte in der Organisation die gewünschten Optionen zur Risikominderung für System und Anwendungen abbildet. Die Konfiguration wird in einer XML-Datei vorgenommen. 

  Durch den Exploit-Schutz können Geräte vor Schadsoftware geschützt werden, die Exploits für die Verbreitung und den Befall von Systemen verwendet. Sie können die App „Windows-Sicherheit“ oder PowerShell verwenden, um Lösungen zur Entschärfung (Konfigurationen) zu erstellen. Diese Konfiguration können Sie anschließend als XML-Datei exportieren und für die Computer in Ihrem Netzwerk freigeben, sodass diese über dieselben Einstellungen zur Entschärfung verfügen.
 
  Sie können außerdem eine vorhandene XML-Konfigurationsdatei aus EMET in eine XML-Konfigurationsdatei für den Exploit-Schutz konvertieren und importieren.

- **Block exploit protection override** (Blockieren von Exploit-Schutz außer Kraft setzen)  
  [WindowsDefenderSecurityCenter/DisallowExploitProtectionOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disallowexploitprotectionoverride) – Legen Sie *Ja* fest, um zu verhindern, dass Benutzer im Microsoft Defender Security Center Änderungen am Bereich mit den Exploit-Schutzeinstellungen vornehmen. Wenn Sie diese Einstellung deaktivieren oder nicht konfigurieren, können lokale Benutzer Änderungen im Einstellungsbereich für Exploit-Schutz vornehmen.  
  **Standardeinstellung:** Ja  

## <a name="microsoft-defender-antivirus"></a>Microsoft Defender Antivirus  

Weitere Informationen finden Sie unter [Policy CSP - Defender (Richtlinien-Konfigurationsdienstanbieter: Defender)](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender) in Ihrer Windows-Dokumentation.

- **Scan scripts loaded in Microsoft web browsers** (In Microsoft-Webbrowsern geladene Skripts überprüfen)  
  [Defender/AllowScriptScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning) – Legen Sie die Einstellung auf *Ja* fest, um Microsoft Defender-Skriptüberprüfungsfunktionen zuzulassen.  

  **Standardeinstellung:** Ja

- **Eingehende E-Mail überprüfen**  
  [Defender/AllowEmailScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning) – Legen Sie die Einstellung auf *Ja* fest, um Microsoft Defender das Überprüfen von E-Mails zu ermöglichen.  

  **Standardeinstellung:** Ja

- **Zustimmung für die Übermittlung von Beispielen in Windows Defender**  
  [Defender/SubmitSamplesConsent](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)– Überprüft in Microsoft Defender die Benutzerzustimmungsebene zum Senden von Daten. Wenn die erforderliche Zustimmung bereits erteilt wurde, sendet Microsoft Defender die Daten. Wenn nicht (und wenn der Benutzer angegeben hat, nie zu fragen), wird die Benutzeroberfläche gestartet, um den Benutzer zur Einwilligung aufzufordern (sofern *Schutz über die Cloud* auf *Ja* festgelegt wurde), bevor Daten gesendet werden.  

  **Standardeinstellung:** Sichere Beispiele automatisch senden

- **Netzwerkinspektionssystem (NIS)**  
  [Defender/EnableNetworkProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection) – Blockieren Sie schädlichen Datenverkehr, der durch Signaturen im Netzwerkinspektionssystem (NIS) erkannt wurde.  
 
  **Standardeinstellung:** Ja

- **Signature update interval (in hours)** (Intervall für das Aktualisieren von Signaturen (in Stunden))  
  [Defender/SignatureUpdateInterval](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval) – Geben Sie in Stunden an, wie oft das Gerät auf neue Updates von Defender-Signaturen überprüfen soll.  
 
  **Standardeinstellung:** 4

- **Niedrige CPU-Priorität für geplante Überprüfungen konfigurieren**  
  [Defender/EnableLowCPUPriority](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority) – Wenn *Ja* festgelegt wurde, wird die CPU-Priorität für Überprüfungen auf „niedrig“ festgelegt. Wurde *Nicht konfiguriert* festgelegt, werden keine Änderungen an der CPU-Priorität für geplante Überprüfungen vorgenommen.  

    **Standardeinstellung:** Ja

- **Defender block on access protection** (Defender-Zugriffsschutz blockieren)  
  [Defender/AllowOnAccessProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection) – Wenn die Einstellung auf *Ja* festgelegt wurde, wird der Microsoft Defender-Zugriffsschutz aktiviert.  

  **Standardeinstellung:** Ja

- **Type of system scan to perform** (Art der durchzuführenden Systemüberprüfung)  
  [Defender/ScanParameter](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-scanparameter) – Defender-Überprüfungstyp.  

  **Standardeinstellung:** Schnellüberprüfung

- **Alle Downloads überprüfen**  
  [Defender/AllowIOAVProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowioavprotection) – Wenn *Ja* festgelegt wurde, überprüft Defender alle heruntergeladenen Dateien und Anlagen.  

  **Standardeinstellung:** Ja

- **Tage bis zum Löschen von in Quarantäne befindlicher Schadsoftware**  
  [Defender/DaysToRetainCleanedMalware](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware) – Geben Sie an, wie viele Tage in Quarantäne befindliche Elemente im System beibehalten werden sollen, bevor sie automatisch gelöscht werden. Wenn „0“ festgelegt wurde, werden diese Elemente nie gelöscht.  

  **Standardeinstellung:** 0

- **Scheduled scan start time** (Startzeit für die geplante Überprüfung)  
  [Defender/ScheduleScanTime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescantime) – Planen Sie eine Uhrzeit, zu der Defender Geräte überprüfen soll. 
  
  Zugehörige Option in dieser Liste: *Defender/ScheduleScanDay*   

  **Standardeinstellung:** 2 Uhr

- **Schutz über die Cloud**  
  [Defender/AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection) – Wenn die Einstellung auf *Ja* festgelegt wurde, sendet Microsoft Defender Informationen zu entdeckten Problemen an Microsoft. Microsoft analysiert diese Informationen, erfährt mehr über die Probleme, die Sie und andere Kunden betreffen, und bietet verbesserte Lösungen an.

  Wenn für diese Richtlinie *Ja* festgelegt wurde, können Sie es Benutzern mithilfe von *Defender sample submission consent type* (Zustimmungstyp für die Übermittlung von Beispielen in Windows Defender) ermöglichen, das Senden von Informationen von ihrem Gerät zu steuern.  

  **Standardeinstellung:** Ja

- **Potenziell unerwünschte App-Aktion in Defender**  
  [Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection) – Microsoft Defender Antivirus kann *potenziell unerwünschte Anwendungen* (Potentially Unwanted Applications, PUAs) identifizieren und verhindern, dass sie heruntergeladen und auf Endpunkten in ihrem Netzwerk installiert werden. 
 
  - Wenn *Blockieren* festgelegt wurde, blockiert Microsoft Defender PUAs und listet sie zusammen mit anderen Bedrohungen im Verlauf auf.
  - Wenn *Überwachen* festgelegt wurde, erkennt Microsoft Defender PUAs, blockiert sie aber nicht. Informationen zu den Anwendungen, gegen die Microsoft Defender Maßnahmen ergriffen hätte, können gefunden werden, indem nach Ereignissen gesucht wird, die von Microsoft Defender in der Ereignisanzeige erstellt wurden.  
  - Wenn *Gerätestandard* festgelegt wurde, ist PUA deaktiviert.  
 
  **Standardeinstellung:** Blockieren

- **Defender: Erweitertes Timeout für Cloud**  
  [Defender/CloudExtendedTimeout](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout) – Geben Sie die maximale zusätzliche Zeit an, während der Microsoft Defender Antivirus eine Datei beim Warten auf ein Ergebnis aus der Cloud blockieren soll. Die Basiszeitspanne, während der Microsoft Defender wartet, ist 10 Sekunden. Zusätzliche Zeit, die Sie hier angeben (bis zu 50 Sekunden), wird zu diesen 10 Sekunden hinzugefügt. In den meisten Fällen dauert die Überprüfung kürzer als der Maximalwert. Das Erweitern des Zeitraums ermöglicht es der Cloud, verdächtige Dateien gründlich zu überprüfen.  

  Der erweiterte Zeitwert lautet standardmäßig „0“ (deaktiviert). Intune empfiehlt, dass Sie diese Einstellung aktivieren und mindestens 20 zusätzliche Sekunden angeben.  
 
  **Standardeinstellung:** 0

- **Archivdateien überprüfen**  
  [Defender/AllowArchiveScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning) – Legen Sie die Einstellung auf *Ja* fest, damit Microsoft Defender Archivdateien überprüft.  

  **Standardeinstellung:** Ja

- **Defender system scan schedule** (Defender-Zeitplan für Systemüberprüfung)  
  [Defender/ScheduleScanDay](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday) – Legen Sie fest, an welchem Tag Defender Geräte überprüfen soll. 
 
  Zugehörige Option in dieser Liste: *Defender/ScheduleScanTime*

  **Standardeinstellung:** Benutzerdefiniert

- **Verhaltensüberwachung**  
  [Defender/AllowBehaviorMonitoring](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring) – Legen Sie die Einstellung auf *Ja* fest, um die Microsoft Defender-Verhaltensüberwachungsfunktionen zu aktivieren. Eingebettet in Windows 10 sammeln und verarbeiten die Sensoren der Microsoft Defender-Verhaltensüberwachung Signale zum Verhalten des Betriebssystems und senden diese Sensordaten an Ihre private, isolierte Cloudinstanz von Microsoft Defender ATP.  

  **Standardeinstellung:** Ja

- **Über Netzwerkordner geöffnete Dateien überprüfen**  
  [Defender/AllowScanningNetworkFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles) – Legen Sie die Einstellung auf *Ja* fest, damit Microsoft Defender Dateien im Netzwerk überprüft. Der Benutzer kann erkannte Schadsoftware nicht aus schreibgeschützten Dateien entfernen.  

  **Standardeinstellung:** Ja

- **Defender-Cloud-Block-Level**  
  [Defender/CloudBlockLevel](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel) – Bestimmen Sie mit dieser Richtlinie, wie aggressiv Microsoft Defender Antivirus beim Blockieren und Überprüfen verdächtiger Dateien sein soll. Zu den Optionen gehören:

  - „Hoch“ – Unbekannte Dateien aggressiv blockieren und gleichzeitig die Clientleistung optimieren (größere Wahrscheinlichkeit falsch positiver Ergebnisse)
  - „Hoher Zuwachs“ – Unbekannte Dateien aggressiv blockieren und zusätzliche Schutzmaßnahmen anwenden (beeinträchtigt möglicherweise die Clientleistung)
  - Keine Toleranz – Alle unbekannten ausführbaren Dateien blockieren

  **Standardeinstellung:** Nicht konfiguriert

- **Echtzeitüberwachung**  
  [Defender/AllowRealtimeMonitoring](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring) – Legen Sie die Einstellung auf *Ja* fest, um Microsoft Defender-Echtzeitüberwachung zuzulassen.  

  **Standardeinstellung:** Ja

- **CPU-Nutzungslimit während einer Überprüfung**  
  [Defender/AvgCPULoadFactor](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-avgcpuloadfactor) – Geben Sie die maximale durchschnittliche CPU-Auslastung (in %) an, die Microsoft Defender während einer Überprüfung nutzen kann.  

  **Standardeinstellung:** 50

- **Bei einer vollständigen Überprüfung zugeordnete Netzlaufwerke überprüfen**  
  [Defender/AllowFullScanOnMappedNetworkDrives](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives) – Legen Sie die Einstellung auf *Ja* fest, damit Microsoft Defender Dateien im Netzwerk überprüft. Der Benutzer kann erkannte Schadsoftware nicht aus schreibgeschützten Dateien entfernen.

  Zugehörige Einstellung in dieser Liste: *Defender/AllowScanningNetworkFiles*

  **Standardeinstellung:** Ja

- **Endbenutzerzugriff auf Defender blockieren**  
  [Defender/AllowUserUIAccess](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess) – Legen Sie die Einstellung auf *Ja* fest, damit der Zugriff von Endbenutzern auf die Benutzeroberfläche von Microsoft Defender auf ihrem Gerät blockiert wird.  

  **Standardeinstellung:** Ja

- **Quick scan start time** (Startzeit der Schnellüberprüfung)  
  [Defender/ScheduleQuickScanTime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime) – Planen Sie eine Uhrzeit, zu der Defender eine Schnellüberprüfung durchführen soll.  

  **Standardeinstellung:** 2 Uhr

## <a name="microsoft-defender-firewall"></a>Microsoft Defender Firewall
Weitere Informationen finden Sie in der Windows-Dokumentation unter [Firewall CSP](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp).

- **Leerlaufzeit für Sicherheitszuordnung vor Löschvorgang** - *MdmStore/Global/SaIdleTime*   
  Sicherheitszuordnungen werden gelöscht, nachdem der Netzwerkdatenverkehr während dieser Anzahl von Sekunden nicht angezeigt wurde.  
  **Standardeinstellung:** 300

- **File Transfer Protocol** - *MdmStore/Global/DisableStatefulFtp*   
  Blockiert das zustandsbehaftete Dateiübertragungsprotokoll (File Transfer Protocol, FTP).  
  **Standardeinstellung:** Ja

- **Paketwarteschlangen** - *MdmStore/Global/EnablePacketQueue*    
  Geben Sie an, wie die Skalierung für die Software auf der Empfangsseite für den verschlüsselten Empfang und die Weiterleitung im Klartext für das IPsec-Tunnelgatewayszenario aktiviert werden soll. Auf diese Weise wird die Paketreihenfolge beibehalten.  
  **Standardeinstellung:** Gerätestandard

- **Firewallprofil-Domäne** - *FirewallRules/FirewallRuleName/Profile*  
  Gibt die Profile an, zu denen die Regel gehört: „Domäne“, „Privat“ oder „Öffentlich“. Dieser Wert stellt das Profil für Netzwerke dar, die mit Domänen verbunden sind.  

  Verfügbare Einstellungen:  
  - **Unicastantworten auf Multicastbroadcasts erforderlich**  
    **Standardeinstellung:** Ja

  - **Autorisierte Anwendungsregeln aus Gruppenrichtlinie zusammengeführt**  
    **Standardeinstellung:** Ja

  - **Eingehende Benachrichtigungen blockiert**  
    **Standardeinstellung:** Ja

  - **Globale Portregeln aus Gruppenrichtlinie zusammengeführt**  
    **Standardeinstellung:** Ja

  - **Geschützter Modus blockiert**  
    **Standardeinstellung:** Ja

  - **Firewall aktiviert**  
    **Standardeinstellung:** Zulässig

  - **Verbindungssicherheitsregeln aus Gruppenrichtlinie nicht zusammengeführt**  
    **Standardeinstellung:** Ja

  - **Richtlinienregeln aus Gruppenrichtlinie nicht zusammengeführt**  
    **Standardeinstellung:** Ja

- **Firewallprofil öffentlich** - *FirewallRules/FirewallRuleName/Profiles*  
  Gibt die Profile an, zu denen die Regel gehört: „Domäne“, „Privat“ oder „Öffentlich“. Dieser Wert stellt das Profil für öffentliche Netzwerke dar. Diese Netzwerke werden von den Administratoren des Serverhosts als „öffentlich“ klassifiziert. Die Klassifizierung erfolgt, wenn sich der Host zum ersten Mal mit dem Netzwerk verbindet. In der Regel sind diese Netzwerke an Flughäfen, in Cafés und an anderen öffentlichen Orten zu finden, an denen die Peers im Netzwerk oder der Netzwerkadministrator nicht vertrauenswürdig sind.  

  Verfügbare Einstellungen:

  - **Eingehende Verbindungen blockiert**  
    **Standardeinstellung:** Ja 

  - **Unicastantworten auf Multicastbroadcasts erforderlich**  
    **Standardeinstellung:** Ja  

  - **Geschützter Modus erforderlich**  
    **Standardeinstellung:** Ja 
 
  - **Ausgehende Verbindungen erforderlich**  
    **Standardeinstellung:** Ja  

  - **Autorisierte Anwendungsregeln aus Gruppenrichtlinie zusammengeführt**  
    **Standardeinstellung:** Ja  

  - **Eingehende Benachrichtigungen blockiert**  
    **Standardeinstellung:** Ja  

  - **Globale Portregeln aus Gruppenrichtlinie zusammengeführt**  
    **Standardeinstellung:** Ja

  - **Geschützter Modus blockiert**  
    **Standardeinstellung:** Ja

  - **Firewall aktiviert**  
    **Standardeinstellung:** Zulässig  

  - **Verbindungssicherheitsregeln aus Gruppenrichtlinie nicht zusammengeführt**  
    **Standardeinstellung:** Ja  

  - **Eingehender Datenverkehr erforderlich**  
    **Standardeinstellung:** Ja

  - **Richtlinienregeln aus Gruppenrichtlinie nicht zusammengeführt**  
    **Standardeinstellung:** Ja  

- **Firewallprofil privat** - *FirewallRules/FirewallRuleName/Profiles*  
  Gibt die Profile an, zu denen die Regel gehört: „Domäne“, „Privat“ oder „Öffentlich“. Dieser Wert stellt das Profil für private Netzwerke dar.  

  Verfügbare Einstellungen: 

  - **Eingehende Verbindungen blockiert**  
    **Standardeinstellung:** Ja

  - **Unicastantworten auf Multicastbroadcasts erforderlich**  
    **Standardeinstellung:** Ja

  - **Geschützter Modus erforderlich**  
    **Standardeinstellung:** Ja

  - **Ausgehende Verbindungen erforderlich**  
    **Standardeinstellung:** Ja

  - **Eingehende Benachrichtigungen blockiert**  
    **Standardeinstellung:** Ja

  - **Globale Portregeln aus Gruppenrichtlinie zusammengeführt**  
    **Standardeinstellung:** Ja

  - **Geschützter Modus blockiert**  
    **Standardeinstellung:** Ja  

  - **Firewall aktiviert**  
    **Standardeinstellung:** Zulässig

  - **Autorisierte Anwendungsregeln aus Gruppenrichtlinie nicht zusammengeführt**  
    **Standardeinstellung:** Ja

  - **Verbindungssicherheitsregeln aus Gruppenrichtlinie nicht zusammengeführt**  
    **Standardeinstellung:** Ja

  - **Eingehender Datenverkehr erforderlich**  
    **Standardeinstellung:** Ja

  - **Richtlinienregeln aus Gruppenrichtlinie nicht zusammengeführt**  
    **Standardeinstellung:** Ja  

- **Firewallmethode „Codierung vorinstallierter Schlüssel“**  
  **Standardeinstellung:** UTF8

- **Überprüfung der Zertifikatssperrliste**  
  **Standardeinstellung:** Gerätestandard

## <a name="web--network-protection"></a>Web- und Netzwerkzugriffsschutz  

- **Netzwerkschutztyp**  
  [Defender/EnableNetworkProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection) – Diese Richtlinie ermöglicht es Ihnen, den Netzwerkschutz in Microsoft Defender Exploit Guard zu aktivieren oder zu deaktivieren. Der Netzwerkschutz ist ein Feature von Microsoft Defender Exploit Guard, das Arbeitnehmer beim Verwenden von Apps vor dem Zugriff auf Phishingwebsites, Websites mit Exploits und schädliche Inhalte im Internet schützt. Dabei wird auch verhindert, dass Browser von Drittanbietern Verbindungen zu gefährlichen Websites herstellen.  

  Wenn *Aktivieren* oder *Überwachungsmodus* festgelegt wurde, können Benutzer den Netzwerkschutz nicht deaktivieren, und Sie können über das Microsoft Defender Security Center Informationen zu Verbindungsversuchen anzeigen.  
 
  - *Aktivieren* verhindert, dass Benutzer und Apps eine Verbindung mit gefährlichen Domänen herstellen.  
  - *Überwachungsmodus* verhindert nicht, dass Benutzer und Apps eine Verbindung mit gefährlichen Domänen herstellen.  

  Wenn *Benutzerdefiniert* festgelegt wurde, wird nicht verhindert, dass Benutzer und Apps eine Verbindung mit gefährlichen Domänen herstellen. Außerdem stehen im Microsoft Defender Security Center keine Informationen zu Verbindungen zur Verfügung.  

  **Standardeinstellung:** Überwachungsmodus

- **SmartScreen für Microsoft Edge anfordern**  
  [Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen) – Microsoft Edge verwendet Microsoft Defender SmartScreen (aktiviert), um Benutzer standardmäßig vor potenziellen Phishing-Angriffen und Schadsoftware zu schützen. Diese Richtlinie ist standardmäßig aktiviert (auf *Ja* festgelegt). Wenn sie aktiviert wurde, wird verhindert, dass Benutzer Microsoft Defender SmartScreen deaktivieren.  Wenn die effektive Richtlinie für ein Gerät gleich „Nicht konfiguriert“ lautet, können Benutzer Microsoft Defender SmartScreen deaktivieren, wodurch das Gerät ungeschützt bleibt.  

  **Standardeinstellung:** Ja
  
- **Zugriff auf schädliche Websites blockieren**  
  [Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride) – Standardmäßig ermöglicht Microsoft Edge Benutzern, die Warnungen von Microsoft Defender SmartScreen zu potenziell schädlichen Websites zu umgehen (zu ignorieren) und trotzdem auf die betreffende Website zuzugreifen. Wenn diese Richtlinie aktiviert (auf *Ja* festgelegt) wurde, verhindert Microsoft Edge, dass Benutzer Warnungen umgehen und zur Website wechseln.  

  **Standardeinstellung:** Ja

- **Block unverified file download** (Herunterladen nicht überprüfter Dateien blockieren)  
  [Browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles) – Standardmäßig ermöglicht Microsoft Edge Benutzern, die Warnungen von Microsoft Defender SmartScreen zu potenziell schädlichen Dateien zu umgehen (zu ignorieren) und nicht geprüfte Dateien trotzdem herunterzuladen. Wenn diese Richtlinie aktiviert (auf *Ja* festgelegt) wurde, werden Benutzer daran gehindert, die Warnungen zu umgehen, und sie können keine nicht überprüften Dateien herunterladen.  

  **Standardeinstellung:** Ja

## <a name="windows-hello-for-business"></a>Windows Hello for Business  

Weitere Informationen finden Sie in der Windows-Dokumentation unter [PassportForWork CSP](https://docs.microsoft.com/windows/client-management/mdm/passportforwork-csp).

- **Konfigurieren von Windows Hello for Business** - *TenantId/Policies/UsePassportForWork*    
  Windows Hello for Business ist eine alternative Methode zum Anmelden bei Windows durch Ersetzen von Kennwörtern, Smartcards und virtuellen Smartcards.  


  > [!IMPORTANT]
  > Die Optionen für diese Einstellung erfüllen nicht ihren eigentlichen Zweck. Die Option *Ja* aktiviert Windows Hello nicht, sondern wird als *Nicht konfiguriert* verarbeitet. Wenn diese Einstellung auf *Nicht konfiguriert* festgelegt ist, wird Windows Hello auf Geräten aktiviert, die diese Baseline empfangen.
  >
  > Die folgenden Beschreibungen wurden diesem gegensätzlichen Verhalten entsprechend überarbeitet. Dieser Fehler soll in einem späteren Update dieser Sicherheitsbaseline behoben werden.

  - Wenn diese Option auf *Nicht konfiguriert* festgelegt ist, wird Windows Hello aktiviert, und das Gerät stellt Windows Hello for Business bereit.
  - Wenn diese Einstellung auf *Ja* festgelegt ist, hat die Baseline keinerlei Einfluss auf die Richtlinieneinstellung des Geräts. Wenn Windows Hello for Business also auf einem Gerät deaktiviert ist, bleibt dies so. Ebenfalls bleibt der Dienst aktiviert, wenn er zuvor bereits aktiviert wurde.
  <!-- expected behavior 
  - When set to *Yes*, you  enable this policy and the device provisions Windows Hello for Business.  
  - When set to *Not configured*, the baseline does not affect the policy setting of the device. This means that if Windows Hello for Business is disabled on a device, it remains disabled. If its enabled, it remains enabled. 
  -->

  Sie können Windows Hello for Business nicht über diese Baseline deaktivieren. Sie können Windows Hello for Business bei der Konfiguration der [Windows-Registrierung](windows-hello.md) oder als Bestandteil eines Gerätekonfigurationsprofils zum [Identitätsschutz](identity-protection-configure.md) deaktivieren.  

Windows Hello for Business ist eine alternative Methode zum Anmelden bei Windows durch Ersetzen von Kennwörtern, Smartcards und virtuellen Smartcards.  

  Wenn Sie diese Richtlinieneinstellung aktivieren oder nicht konfigurieren, stellt das Gerät Windows Hello for Business bereit. Wenn Sie diese Richtlinieneinstellung deaktivieren, stellt das Gerät Windows Hello for Business für keinen Benutzer bereit.

  Intune unterstützt nicht das Deaktivieren von Windows Hello. Stattdessen können Sie eine Richtlinie konfigurieren, um Windows Hello for Business zu aktivieren („Ja“) oder um Windows Hello nicht direkt zu konfigurieren („nicht konfiguriert“). Wenn „nicht konfiguriert“ festgelegt wurde, kann ein Gerät die Konfiguration über eine andere Richtlinie empfangen, wodurch dieses Feature möglicherweise aktiviert oder deaktiviert wird.  

  **Standardeinstellung:** Ja  

- **Kleinbuchstaben in PIN vorschreiben** - *TenantId/Policies/PINComplexity/LowercaseLetters*  
  **Standardeinstellung:** Zulässig  

- **Sonderzeichen in PIN vorschreiben** - *TenantId/Policies/PINComplexity/SpecialCharacters*  
  **Standardeinstellung:** Zulässig  

- **Großbuchstaben in PIN vorschreiben** - *TenantId/Policies/PINComplexity/UppercaseLetters*   
  **Standardeinstellung:** Zulässig  

