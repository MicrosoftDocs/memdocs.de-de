---
title: Verschlüsselungsbericht für verschlüsselte Berichte in Microsoft Intune
titleSuffix: Microsoft Intune
description: Rufen Sie einen Bericht zum Verschlüsselungsstatus Ihres iOS/iPadOS- oder Windows-Geräts ab, und greifen Sie über das Microsoft Intune-Portal auf die FileVault- und BitLocker-Wiederherstellungsschlüssel zu.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: d14ee52decf1b6ef9b2566b3233a385c1331bcc5
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910977"
---
# <a name="monitor-device-encryption-with-intune"></a>Überwachen der Geräteverschlüsselung mit Intune

Der Microsoft Intune-Verschlüsselungsbericht enthält Details zum Verschlüsselungsstatus Ihrer verwalteten Geräte sowie Optionen zum Verwalten von Wiederherstellungsschlüsseln für Geräte. Welche Wiederherstellungsschlüsseloptionen verfügbar sind, hängt vom Typ des Geräts ab, das aufgerufen wird.

Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an, um den Bericht zu finden. Wählen Sie **Geräte** > **Überwachen** aus. Wählen Sie dann unter *Konfiguration* **Verschlüsselungsbericht** aus.

## <a name="view-encryption-details"></a>Abrufen von Verschlüsselungsdetails

Der Verschlüsselungsbericht enthält allgemeine Informationen zu allen unterstützten und von Ihnen verwalteten Geräten. In den folgenden Abschnitten finden Sie Details zu den Informationen, die im Intune-Bericht enthalten sind.

### <a name="prerequisites"></a>Voraussetzungen

Der Verschlüsselungsbericht unterstützt die Berichterstellung auf Geräten, auf denen die folgenden Betriebssystemversionen ausgeführt werden:

- macOS 10.13 oder höher
- Windows, Version 1607 oder höher

### <a name="report-details"></a>Berichtdetails

Im Bereich „Verschlüsselungsbericht“ werden alle von Ihnen verwalteten Geräte einschließlich entsprechender allgemeiner Details aufgelistet. Sie können ein Gerät aus der Liste auswählen, um einen Drilldown auszuführen und weitere Details im Bereich [Geräteverschlüsselungsstatus](#device-encryption-status) anzuzeigen.

- **Gerätename:** der Name des Geräts.
- **Betriebssystem:** die Geräteplattform, z. B. Windows oder macOS.
- **Betriebssystemversion:** die Version von Windows oder macOS auf dem Gerät.
- **TPM-Version** *(gilt nur für Windows 10):* die Version des TPM-Chips (Trusted Platform Module) auf dem Windows 10 Gerät.
- **Verschlüsselungsbereitschaft:** eine Auswertung der Bereitschaft der Geräte zur Unterstützung einer anwendbaren Verschlüsselungstechnologie wie der BitLocker-oder FileVault-Verschlüsselung. Die Geräte können die folgenden Status aufweisen:
  - **Bereit:** Das Gerät kann mithilfe einer MDM-Richtlinie (Mobile Device Management) verschlüsselt werden. Dazu muss es die folgenden Anforderungen erfüllen:

    **Für macOS-Geräte:**
    - macOS, Version 10.13 oder höher

    **Für Windows 10-Geräte:**
    - Version 1709 oder höher von *Business*, *Enterprise* oder *Education* oder Version 1809 oder höher von *Pro*
    - Das Gerät muss über einen TPM-Chip verfügen.

    Weitere Informationen finden Sie in der Windows-Dokumentation unter [BitLocker configuration service provider (CSP) (BitLocker-Konfigurationsdienstanbieter (Configuration Service Provider, CSP))](/windows/client-management/mdm/bitlocker-csp).

  - **Nicht bereit:** Das Gerät kann nicht vollständig verschlüsselt werden, unterstützt jedoch die Verschlüsselung. Das Windows-Gerät könnte beispielsweise von einem Benutzer manuell verschlüsselt werden oder über eine Gruppenrichtlinie, die so festgelegt werden kann, dass die Verschlüsselung ohne ein TPM zulässig ist.
  - **Nicht zutreffend**: Es stehen nicht genügend Informationen zur Verfügung, um dieses Gerät zu klassifizieren.

- **Verschlüsselungsstatus:** Gibt an, ob das Betriebssystemlaufwerk verschlüsselt ist

- **Benutzerprinzipalname:** Der primäre Benutzer des Geräts.

### <a name="device-encryption-status"></a>Geräteverschlüsselungsstatus

Wenn Sie im Verschlüsselungsbericht ein Gerät auswählen, zeigt Intune den Bereich **Geräteverschlüsselungsstatus** an. In diesem Bereich finden Sie die folgenden Details:

- **Gerätename:** Der Name des Geräts, das Sie sich ansehen

- **Verschlüsselungsbereitschaft:** eine Auswertung der Bereitschaft der Geräte zur Unterstützung der Verschlüsselung über eine MDM-Richtlinie.

  Beispiel: Wenn ein Windows 10-Gerät als *Nicht bereit* eingestuft wird, kann es trotzdem sein, dass die Verschlüsselung unterstützt wird. Das Windows 10-Gerät kann nur als *Bereit* eingestuft werden, wenn es über einen TPM-Chip verfügt. Es nicht erforderlich, dass der TPM-Chip die Verschlüsselung unterstützt. (Weitere Informationen finden Sie im vorherigen Abschnitt unter *Verschlüsselungsbereitschaft*.)

- **Verschlüsselungsstatus:** Gibt an, ob das Betriebssystemlaufwerk verschlüsselt ist Es kann bis zu 24 Stunden dauern, bis Intune den Verschlüsselungsstatus eines Geräts oder die Änderung dieses Status meldet. Dieser Zeitraum schließt die Zeit zum Verschlüsseln des Betriebssystems und die Zeit für die Rückmeldung des Geräts an Intune ein.

  Um die Meldung des FileVault-Verschlüsselungsstatus vor dem normalen Einchecken des Geräts zu beschleunigen, müssen die Benutzer ihre Geräte nach Abschluss der Verschlüsselung synchronisieren.

- **Profile:** eine Liste von *Gerätekonfigurationsprofilen*, die für dieses Gerät gelten und mit den folgenden Werten konfiguriert werden:

  - macOS:
    - Profiltyp = *Endpoint Protection*
    - „Einstellungen“ > „FileVault“ > „FileVault“ = *Aktivieren*

  - Windows 10:
    - Profiltyp = *Endpoint Protection*
    - Einstellungen > Windows-Verschlüsselung > Geräte verschlüsseln = *Erforderlich*

  Sie können die Profilliste verwenden, um einzelne Richtlinien für eine Überprüfung auszuwählen, sollte die *Profilstatuszusammenfassung* auf Probleme hindeuten.

- **Profilstatuszusammenfassung:** Eine Zusammenfassung der Profile, die für das Gerät gelten Die Zusammenfassung stellt die am wenigsten vorteilhafte Bedingung aller anwendbaren Profile dar. Wenn beispielsweise ein Profil von mehreren anwendbaren Profilen einen Fehler auslöst, zeigt die *Profilstatuszusammenfassung* *Fehler* an.

  Um weitere Details eines Status anzuzeigen, wechseln Sie zu **Intune** > **Gerätekonfiguration** > **Profile**, und wählen Sie das Profil aus. Wählen Sie optional **Gerätestatus** und anschließend ein Gerät aus.

- **Statusdetails:** Erweiterte Details zum Verschlüsselungsstatus eines Geräts.

  > [!IMPORTANT]
  > Für Windows 10-Geräte zeigt Intune *Statusdetails* für Geräte an, die mindestens das *Windows 10-Update vom 10. April 2019* ausführen.

  Dieses Feld zeigt Informationen zu jedem anwendbaren Fehler an, der erkannt werden kann. Mithilfe dieser Informationen verstehen Sie, warum ein Gerät möglicherweise nicht für die Verschlüsselung bereit ist.

  Im Folgenden sehen Sie Beispiele für Statusdetails, die Intune melden kann:

  **macOS**:
  - Der Wiederherstellungsschlüssel wurde noch nicht abgerufen und gespeichert. Höchstwahrscheinlich wurde das Gerät nicht entsperrt, oder es wurde nicht angemeldet.

    *Zu berücksichtigen: Dieses Ergebnis stellt nicht notwendigerweise einen Fehlerzustand dar, sondern einen temporären Zustand, der durch die zeitliche Steuerung auf dem Gerät verursacht werden kann, wenn die Hinterlegung von Wiederherstellungsschlüsseln eingerichtet werden muss, bevor die Verschlüsselungsanforderung an das Gerät gesendet wird. Dieser Status kann auch darauf hindeuten, dass das Gerät weiterhin gesperrt ist oder in letzter Zeit nicht bei Intune angemeldet wurde. Außerdem ist es möglich, dass ein Benutzer einen Wiederherstellungsschlüssel für ein Gerät erhält, das noch nicht verschlüsselt ist, da die FileVault-Verschlüsselung erst gestartet wird, nachdem das Gerät zum Laden an den Strom angeschlossen wurde.*

  - Der Benutzer verzögert die Verschlüsselung oder führt derzeit den Verschlüsselungsprozess aus.

    *Zu berücksichtigen: Der Benutzer hat sich nach dem Empfang der Verschlüsselungsanforderung noch nicht abgemeldet. Dies ist erforderlich, damit das Gerät von FileVault verschlüsselt werden kann. Es kann aber auch sein, dass der Benutzer das Gerät manuell entschlüsselt hat. Intune kann nicht verhindern, dass ein Benutzer sein Gerät entschlüsselt.*

  - Das Gerät ist bereits verschlüsselt. Der Gerätebenutzer muss das Gerät entschlüsseln, um weitere Schritte ausführen zu können.

    *Zu berücksichtigen: Intune kann FileVault nicht auf einem Gerät einrichten, das bereits verschlüsselt ist. Nachdem ein Gerät jedoch eine Richtlinie zum Aktivieren von FileVault erhält, kann ein Benutzer seinen [persönlichen Wiederherstellungsschlüssel hochladen, um Intune zu aktivieren und dann die Verschlüsselung auf dem Gerät zu verwalten](../protect/encrypt-devices-filevault.md#assume-management-of-filevault-on-previously-encrypted-devices). Alternativ (aber nicht empfohlen, da das Gerät dabei für eine Weile nicht verschlüsselt ist) kann der Benutzer sein Gerät vorher manuell entschlüsseln, damit es dann von der Intune-Richtlinie verschlüsselt werden kann.*

  - Für FileVault muss der Benutzer sein Verwaltungsprofil in macOS Catalina und höher genehmigen.

    *Zu berücksichtigen: Ab macOS, Version 10.15 (Catalina) können durch den Benutzer genehmigte Registrierungseinstellungen dazu führen, dass der Benutzer die FileVault-Verschlüsselung manuell genehmigen muss. Weitere Informationen finden Sie unter [Durch den Benutzer genehmigte Registrierung](../enrollment/macos-enroll.md) in der Intune-Dokumentation.*

  - Unbekannt

    *Zu berücksichtigen: Eine mögliche Ursache für einen unbekannten Status ist, dass das Gerät gesperrt ist und Intune den Hinterlegungs-oder Verschlüsselungsvorgang nicht starten kann. Sobald das Gerät entsperrt wird, kann der Vorgang fortgesetzt werden.*

  **Windows 10:**
  - Die BitLocker-Richtlinie erfordert eine Benutzereinwilligung, damit der BitLocker-Laufwerkverschlüsselungsassistent gestartet werden kann, um mit der Verschlüsselung des Betriebssystemvolumes zu beginnen. Der Benutzer hat jedoch nicht eingewilligt.

  - Die Verschlüsselungsmethode des Betriebssystemvolume stimmt nicht mit der BitLocker-Richtlinie überein.

  - Die BitLocker-Richtlinie erfordert eine TPM-Schutzvorrichtung, damit das Betriebssystemvolume geschützt wird; es wird jedoch kein TPM verwendet.

  - Die BitLocker-Richtlinie erfordert eine reine TPM-Schutzvorrichtung für das Betriebssystemvolume, aber es wird kein TPM-Schutz verwendet.

  - Die BitLocker-Richtlinie erfordert einen TPM+PIN-Schutz für das Betriebssystemvolume, aber es wird keine TPM+PIN-Schutzvorrichtung verwendet.

  - Die BitLocker-Richtlinie erfordert einen TPM+Systemstartschlüssel-Schutz für das Betriebssystemvolume, aber es wird keine TPM+Systemstartschlüssel-Schutzvorrichtung verwendet.

  - Die BitLocker-Richtlinie erfordert einen TPM+PIN+Systemstartschlüssel-Schutz für das Betriebssystemvolume, aber es wird keine TPM+PIN+Systemstartschlüssel-Schutzvorrichtung verwendet.

  - Das Betriebssystemvolume ist nicht geschützt.

  - Die Sicherung des Wiederherstellungsschlüssel ist fehlgeschlagen.

  - Ein Festplattenlaufwerk ist nicht geschützt.

  - Die Verschlüsselungsmethode des Festplattenlaufwerks stimmt nicht mit der BitLocker-Richtlinie überein.

  - Wenn Laufwerke verschlüsselt werden sollen, erfordert die BitLocker-Richtlinie entweder eine Anmeldung des Benutzers als Administrator, oder die Richtlinie „AllowStandardUserEncryption“ muss auf 1 festgelegt werden, wenn das Gerät mit Azure AD verknüpft ist.

  - Die Windows-Wiederherstellungsumgebung (Windows Recovery Environment, WinRE) ist nicht konfiguriert.

  - Für BitLocker steht kein TPM zur Verfügung – entweder, weil keines vorhanden ist, es in der Registrierung nicht mehr zur Verfügung steht, oder weil sich das Betriebssystem auf einem Laufwerk befindet, das entfernt werden kann.

  - Das TMP ist nicht bereit für BitLocker.

  - Das Netzwerk ist nicht verfügbar. Dies ist aber eine Voraussetzung zur Sicherung des Wiederherstellungsschlüssels.

## <a name="export-report-details"></a>Exportieren von Berichtsdetails

Wenn Sie den Bereich „Verschlüsselungsbericht“ anzeigen, können Sie auf **Exportieren** klicken, um die Berichtsdetails in einer *CSV*-Datei herunterzuladen. Dieser Bericht enthält allgemeine Informationen zum Bereich *Verschlüsselungsbericht* und Details zum *Geräteverschlüsselungsstatus* der einzelnen Geräte, die Sie verwalten.

![Exportieren von Details](./media/encryption-monitor/export.png)

Dieser Bericht kann bei der Identifizierung von Problemen von Gerätegruppen verwendet werden. Beispielsweise können Sie den Bericht verwenden, um eine Liste der macOS-Geräte zu erstellen, für die *der Benutzer bereits FileVault aktiviert hat*. So können die Geräte ermittelt werden, die manuell entschlüsselt werden müssen, damit Intune deren FileVault-Einstellungen verwalten kann.

## <a name="manage-recovery-keys"></a>Verwalten von Wiederherstellungsschlüsseln

Ausführliche Informationen zum Verwalten von Wiederherstellungsschlüsseln finden Sie in den folgenden Intune-Dokumentationen:

macOS FileVault:
- [Abrufen persönlicher Wiederherstellungsschlüssel](../protect/encrypt-devices-filevault.md#retrieve-a-personal-recovery-key)
- [Rotieren von Wiederherstellungsschlüsseln](../protect/encrypt-devices-filevault.md#rotate-recovery-keys)
- [Wiederherstellen von Wiederherstellungsschlüsseln](../protect/encrypt-devices-filevault.md#recover-recovery-keys)

Windows 10 BitLocker:
- [Rotieren von BitLocker-Wiederherstellungsschlüsseln](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys)

## <a name="next-steps"></a>Nächste Schritte

[Verwalten der BitLocker-Richtlinie](../protect/encrypt-devices.md)

[Verwalten der FileVault-Richtlinie](encrypt-devices-filevault.md)