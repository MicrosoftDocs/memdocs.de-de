---
title: Konformitätseinstellungen für iOS-/iPadOS-Geräte in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Dieser Artikel enthält eine Liste aller Einstellungen, die Sie zum Festlegen von Konformität für Ihre iOS-/iPadOS-Geräte in Microsoft Intune verwenden können. Sie können eine E-Mail anfordern, Geräte des Typs „mit Jailbreak“ oder „rooted“ überprüfen, das zulässige minimale und maximale Betriebssystem festlegen, Kennwortbeschränkungen einrichten, einschließlich Kennwortlänge und Geräteinaktivität, Apps einschränken und mehr.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 3cfb8222-d05b-49e3-ae6f-36ce1a16c61d
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 536ad36120a8fb5dc4ad0d16b8f265e56260d461
ms.sourcegitcommit: 56bb5419c41c2e150ffed0564350123135ea4592
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/02/2020
ms.locfileid: "82729255"
---
# <a name="iosipados-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>iOS-/iPadOS-Einstellungen, um Geräte mit Intune als konform oder nicht konform zu kennzeichnen

In diesem Artikel werden die verschiedenen Konformitätseinstellungen aufgeführt und beschrieben, die Sie in Intune für iOS-/iPadOS-Geräte konfigurieren können. Im Rahmen Ihrer MDM-Lösung (Mobile Device Management, Verwaltung mobiler Geräte) verwenden Sie diese Einstellungen, um Geräte des Typs „rooted“ (mit Jailbreak) als nicht konform zu markieren, eine zulässige Bedrohungsstufe festzulegen, den Ablauf von Kennwörtern einzurichten und vieles mehr.

Diese Funktion gilt für:

- iOS
- iPadOS

Als Intune-Administrator verwenden Sie diese Konformitätseinstellungen, um die Ressourcen Ihrer Organisation zu schützen. Weitere Informationen zu Konformitätsrichtlinien und ihren Aufgaben finden Sie unter [Erste Schritte bei der Gerätekonformität](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen einer Konformitätsrichtlinie](create-compliance-policy.md#create-the-policy) Wählen Sie als **Plattform** die Option **iOS/iPadOS** aus.

## <a name="email"></a>E-Mail

- **E-Mail kann auf dem Gerät nicht eingerichtet werden**  
  - **Nicht konfiguriert** (*Standardeinstellung*): Diese Einstellung wird nicht für die Konformitätsprüfung ausgewertet.
  - **Anfordern:** Ein verwaltetes E-Mail-Konto ist erforderlich. Wenn der Benutzer bereits über ein E-Mail-Konto auf dem Gerät verfügt, muss dieses E-Mail-Konto entfernt werden, damit Intune ordnungsgemäß ein Konto einrichten kann. Wenn auf dem Gerät kein E-Mail-Konto vorhanden ist, sollte sich der Benutzer an den IT-Administrator wenden, damit dieser ein verwaltetes E-Mail-Konto konfiguriert.

  Das Gerät wird in den folgenden Situationen als nicht kompatibel betrachtet:  
  - Das E-Mail-Profil ist einer anderen Benutzergruppe zugewiesen als der Benutzergruppe, die der Kompatibilitätsrichtlinie unterliegt.
  - Der Benutzer hat bereits ein E-Mail-Konto auf dem Gerät eingerichtet, das dem Intune-E-Mail-Profil entspricht, das auf dem Gerät bereitgestellt wurde. Intune kann das vom Benutzer konfigurierte Profil nicht überschreiben und es nicht verwalten. Zum Sicherstellen der Kompatibilität muss der Endbenutzer die vorhandenen E-Mail-Einstellungen entfernen. Anschließend kann Intune das verwaltete E-Mail-Profil installieren.  

Weitere Informationen zu E-Mail-Profilen finden Sie unter [Konfigurieren des Zugriffs auf Organisations-E-Mail mithilfe von E-Mail-Profilen in Microsoft Intune](../configuration/email-settings-configure.md).

## <a name="device-health"></a>Geräteintegrität

- **Geräte mit Jailbreak**  
  *Unterstützt für iOS 8.0 und höher*

  - **Nicht konfiguriert** (*Standardeinstellung*): Diese Einstellung wird nicht für die Konformitätsprüfung ausgewertet.
  - **Blockieren**: Geräte mit Jailbreak oder entfernten Nutzungsbeschränkungen werden als nicht konform gekennzeichnet.  

- **Anfordern, dass das Gerät höchstens der angegebenen Gerätebedrohungsstufe entspricht**  
  *Unterstützt für iOS 8.0 und höher*

  Verwenden Sie diese Einstellung, um die Risikobewertung als Konformitätsbedingung zu verwenden. Wählen Sie die zulässige Bedrohungsstufe aus:
  - **Nicht konfiguriert** (*Standardeinstellung*): Diese Einstellung wird nicht für die Konformitätsprüfung ausgewertet.
  - **Gesichert**: Diese Option ist die sicherste und bedeutet, dass auf dem Gerät keine Bedrohungen vorhanden sein können. Wenn auf dem Gerät Bedrohungen jeglicher Stufen erkannt werden, wird es als nicht konform bewertet.
  - **Niedrig**: Das Gerät wird als konform bewertet, wenn nur Bedrohungen auf niedrigen Stufen vorliegen. Jegliche Bedrohung einer höheren Stufe bewirkt, dass das Gerät in den Status „Nicht konform“ eingestuft wird.
  - **Mittel**: Das Gerät wird als konform bewertet, wenn auf dem Gerät Bedrohungen auf niedriger oder mittlerer Stufe gefunden werden. Wenn auf dem Gerät Bedrohungen hoher Stufen erkannt werden, wird es als nicht konform bewertet.
  - **Hoch**: Dies ist die am wenigsten sichere Option, die alle Bedrohungsebenen zulässt. Es ist möglicherweise hilfreich, diese Lösung nur zu Berichtszwecken zu verwenden.

## <a name="device-properties"></a>Geräteeigenschaften

### <a name="operating-system-version"></a>Version des Betriebssystems  

- **Minimales Release des Betriebssystems**  
  *Unterstützt für iOS 8.0 und höher*

  Wenn ein Gerät die Anforderung an die Mindestversion des Betriebssystems nicht erfüllt, wird es als nicht konform gemeldet. Ein Link zur Vorgehensweise zum Upgrade wird angezeigt. Der Endbenutzer kann sein Gerät aktualisieren. Danach kann er auf Organisationsressourcen zugreifen.

- **Maximales Release des Betriebssystems**  
  *Unterstützt für iOS 8.0 und höher*

  Wird auf einem Gerät eine neuere Betriebssystemversion als in der Regel verwendet, wird der Zugriff auf Organisationsressourcen gesperrt. Der Endbenutzer wird aufgefordert, sich an den zuständigen IT-Administrator zu wenden. Das Gerät kann solange nicht auf Organisationsressourcen zugreifen, bis die Regel geändert und die betreffende Betriebssystemversion zugelassen wird.

- **Mindestbuildversion des Betriebssystems**  
  *Unterstützt für iOS 8.0 und höher*

  Wenn Apple Sicherheitsupdates veröffentlicht, wird in der Regel die Nummer des Builds aktualisiert, nicht die Betriebssystemversion. Verwenden Sie diese Funktion, um eine zulässige minimale Buildnummer am Gerät einzugeben.

- **Höchste Buildversion des Betriebssystems*  
  *Unterstützt für iOS 8.0 und höher*

  Wenn Apple Sicherheitsupdates veröffentlicht, wird in der Regel die Nummer des Builds aktualisiert, nicht die Betriebssystemversion. Verwenden Sie diese Funktion, um eine zulässige maximale Buildnummer am Gerät einzugeben.

## <a name="system-security"></a>Systemsicherheit

### <a name="password"></a>Kennwort

> [!NOTE]
> Nachdem eine Konformitäts- oder Konfigurationsrichtlinie auf ein iOS-/iPadOS-Gerät angewendet wurde, werden Benutzer alle 15 Minuten dazu aufgefordert, einen Passcode festzulegen. Benutzer erhalten kontinuierlich eine Aufforderung, bis sie eine Kennung festgelegt haben. Sobald für das iOS-/iPadOS-Gerät ein Passcode festgelegt wurde, wird der Verschlüsselungsprozess automatisch gestartet. Das Gerät bleibt verschlüsselt, bis der Passcode deaktiviert ist.

- **Anfordern eines Kennworts zum Entsperren mobiler Geräte**  
  - **Nicht konfiguriert** (*Standardeinstellung*): Diese Einstellung wird nicht für die Konformitätsprüfung ausgewertet.  
  - **Erforderlich**: Benutzer müssen ein Kennwort eingeben, bevor sie auf ihr Gerät zugreifen können. iOS-/iPadOS-Geräte mit Kennwort sind verschlüsselt.

- **Einfache Kennwörter**  
  *Unterstützt für iOS 8.0 und höher*

  - **Nicht konfiguriert** (*Standardeinstellung*): Benutzer können einfache Kennwörter wie **1234** oder **1111** erstellen.
  - **Blockieren**: Benutzer können kein einfaches Kennwort wie **1234** oder **1111** erstellen.

- **Minimale Kennwortlänge**  
  *Unterstützt für iOS 8.0 und höher*

  Geben Sie die Mindestanzahl an Ziffern oder Zeichen ein, die das Kennwort enthalten muss.

- **Erforderlicher Kennworttyp**  
  *Unterstützt für iOS 8.0 und höher*

  Wählen Sie aus, ob ein Kennwort nur aus **numerischen** Zeichen bestehen oder eine Kombination aus Zahlen und anderen Zeichen verwendet werden soll (**alphanumerisch**).

- **Anzahl der nicht alphanumerischen Zeichen im Kennwort**  
  Geben Sie die Mindestanzahl von Sonderzeichen (`&`, `#`, `%`, `!` usw.) ein, die im Kennwort enthalten sein müssen.

  Wenn Sie eine höhere Anzahl festlegen, muss der Benutzer ein komplexeres Kennwort erstellen.

- **Maximaler Zeitraum der Bildschirmsperre (in Minuten) bis zur Anforderung eines Kennworts**  
  *Unterstützt für iOS 8.0 und höher*

  Geben Sie an, wie lange der Bildschirm gesperrt bleiben soll, bevor ein Benutzer ein Kennwort für den Zugriff auf das Gerät eingeben muss. Zu den Optionen gehören der Standardwert *Nicht konfiguriert*, *Sofort* sowie von *1 Minute* bis *4 Stunden*.

- **Maximaler Zeitraum der Inaktivität (in Minuten) bis zur Bildschirmsperrung**  
  Geben Sie die Leerlaufzeit ein, bevor das Gerät seinen Bildschirm sperrt. Zu den Optionen gehören standardmäßig *nicht konfiguriert*, *sofort*und *1 Minute* bis *15 Minuten*.

- **Kennwortablauf (Tage)**  
  *Unterstützt für iOS 8.0 und höher*

  Wählen Sie die Anzahl der Tage aus, nach der das Kennwort abläuft und ein neues erstellt werden muss.

- **Anzahl vorheriger Kennwörter, deren Wiederverwendung verhindert wird**  
  *Unterstützt für iOS 8.0 und höher*

  Geben Sie die Anzahl der zuvor verwendeten Kennwörter ein, die nicht erneut verwendet werden können.

### <a name="device-security"></a>Gerätesicherheit

- **Eingeschränkte Apps**  
  Sie können Apps einschränken, indem Sie ihre Bündel-IDs der Richtlinie hinzufügen. Wenn die App auf einem Gerät installiert wird, wird das Gerät als nicht konform gekennzeichnet.

  - **App-Name**: Geben Sie einen benutzerfreundlichen Namen ein, damit Sie die Bündel-ID einfacher identifizieren können.
  - **App-Bündel-ID**: Geben Sie die eindeutige Bündel-ID ein, die vom App-Anbieter zugewiesen wurde. Informationen zum Ermitteln der Bündel-ID finden Sie unter [Ermitteln der Bündel-ID für eine iOS-/iPadOS-App](https://support.microsoft.com/help/4294074/how-to-find-the-bundle-id-for-an-ios-app) (öffnet eine andere Microsoft-Website).  

## <a name="next-steps"></a>Nächste Schritte

- [Hinzufügen von Aktionen für nicht kompatible Geräte](actions-for-noncompliance.md) und [Verwenden von Bereichsmarkierungen zum Filtern von Richtlinien](../fundamentals/scope-tags.md).
- [Überwachen Ihrer Konformitätsrichtlinien](compliance-policy-monitor.md).
- Siehe die [Einstellungen für Kompatibilitätsrichtlinien für macOS](compliance-policy-create-mac-os.md)-Geräte.
