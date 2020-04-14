---
title: Überprüfen von Erfolg oder Fehler bei Sicherheitsbaselines in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Überprüfen Sie Fehler-, Konflikt- und Erfolgsstatus bei der Bereitstellung von Sicherheitsbaselines für Benutzer und Geräte bei der Verwaltung mobiler Geräte für Microsoft Intune. Erfahren Sie, wie Sie Probleme mithilfe von Clientprotokollen und den Berichtsfunktionen in Intune behandeln.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: shpate
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 53187f7795eee07a62a83c1fb17a289451b32ee2
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551667"
---
# <a name="monitor-security-baseline-and-profiles-in-microsoft-intune"></a>Überwachen der Sicherheitsbaseline und von Profilen in Microsoft Intune

Intune umfasst mehrere Optionen zum Überwachen Ihrer Sicherheitsbaselines. Sie können das Sicherheitsbaselineprofil überwachen, das für Ihre Benutzer und Geräte gilt. Sie können auch die tatsächliche Baseline überwachen, und alle Geräte, die den empfohlenen Werten entsprechen (oder nicht).

Dieser Artikel führt Sie durch beide Überwachungsoptionen.

Im Artikel [Erstellen einer Windows 10-Sicherheitsbaseline in Intune](security-baselines.md) finden Sie weitere Details zum Sicherheitsbaselinefeature in Microsoft Intune.

## <a name="monitor-the-baseline-and-your-devices"></a>Überwachen der Baseline und Ihrer Geräte

Wenn Sie eine Baseline überwachen, erhalten Sie basierend auf den Empfehlungen von Microsoft Einblicke in den Sicherheitsstatus Ihrer Geräte. Diese können Sie im Bereich „Übersicht“ der Sicherheitsbaseline in der Intune-Konsole abrufen.  Im Anschluss an die Zuweisung einer Baseline dauert es 24 Stunden, bis die Daten angezeigt werden. Änderungen, die danach vorgenommen werden, werden innerhalb von sechs Stunden angezeigt.

Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an, um Überwachungsdaten für die Baseline und die Geräte anzuzeigen. Wählen Sie als Nächstes **Endpunktsicherheit** > **Sicherheitsbaselines** und dann eine Baseline aus, und sehen Sie sich den Bereich **Übersicht** an.

Der Bereich **Übersicht** umfasst zwei Methoden zum Überwachen von Statusangaben:

- **Geräteansicht:** eine Zusammenfassung der Anzahl der Geräte, die sich in den einzelnen Statuskategorien der Baseline befinden
- **Per-category** (Kategoriebasierte Ansicht): Ansicht der einzelnen Kategorien in der Baseline, auf der auch der Anteil der Geräte (in Prozent) für die einzelnen Statusgruppen der Baselinekategorien angegeben sind

Jedem Gerät ist einer der folgenden Statuswerte zugewiesen (diese werden sowohl in der *Geräteansicht* als auch in den einzelnen *kategoriebasierten* Ansichten verwendet):

- **Matches baseline** (Übereinstimmung mit Baseline): alle Einstellungen in der Baseline stimmen mit den empfohlenen Einstellungen überein
- **Stimmt nicht mit Baseline überein**: Bei mindestens einer Einstellung in der Baseline wurden in der ursprünglichen Baseline die Standardwerte geändert. Die Standardwerte in den einzelnen Sicherheitsbaselines sind die empfohlenen Werte für diese Baseline.

  > [!NOTE]
  > Wenn Sie ein Baselineprofil erstellen oder bearbeiten, führen alle Änderungen an einem Standardwert oder einer Konfigurationseinstellung zum Status *Stimmt nicht mit Baseline überein*. Wenden Sie sich an den Microsoft-Support, um herauszufinden, welche Einstellungen geändert wurden. 

- **Falsch konfiguriert**: Mindestens eine Einstellung wurde nicht richtig konfiguriert. Dieser Status bedeutet, dass die Einstellung sich im Status „Konflikt“, „Fehler“ oder „Ausstehend“ befindet.
- **Nicht anwendbar**: Mindestens eine Einstellung ist nicht anwendbar und wird nicht verwendet.

### <a name="device-view"></a>Geräteansicht

Der Bereich „Übersicht“ umfasst eine diagrammbasierte Zusammenfassung der Anzahl der Geräte mit einem bestimmten Baselinestatus; **Status der Sicherheitsbaseline für zugewiesene Windows 10-Geräte**.

![Überprüfen des Status der Geräte](./media/security-baselines-monitor/overview.png)

Wenn ein Gerät verschiedene Statusangaben aus unterschiedlichen Baselinekategorien aufweist, wird dem Gerät ein einzelner Status zugewiesen. Dieser Status wird entsprechend der folgenden Reihenfolge bestimmt: **Falsch konfiguriert**, **Does not match baseline** (Keine Übereinstimmung mit Baseline), **Not applicable** (Nicht verfügbar), **Matches baseline** (Übereinstimmung mit Baseline).

Wenn also für ein Gerät einmal die Einstellung *Falsch konfiguriert* und einmal (oder mehrmals) die Einstellung *Does not match baseline* (Keine Übereinstimmung mit Baseline) festgelegt ist, wird dem Gerät der Status *Falsch konfiguriert* zugewiesen.

Sie können auf das Diagramm klicken, um einen Drillthrough auszuführen und eine Liste der Geräte mit den verschiedenen Statusangaben anzuzeigen. Anschließen können Sie einzelne Geräte aus der Liste auswählen, um Details zu diesen abzurufen. Beispiel:

- Klicken Sie auf **Gerätekonfiguration**, und wählen Sie dann das Profil mit einem Fehlerstatus aus:

  ![Anzeigen des Status eines Profils](./media/security-baselines-monitor/device-configuration-profile-list.png)

- Wählen Sie das „Fehler“-Profil aus. Eine Liste aller Einstellungen im Profil und deren Status werden angezeigt. Jetzt können Sie scrollen, um die Einstellung zu finden, die den Fehler verursacht:

  ![Anzeigen der Einstellung, die den Fehler verursacht hat](./media/security-baselines-monitor/profile-with-error-status.png)

Verwenden Sie diese Berichterstellung, um alle Einstellungen in einem Profil anzuzeigen, die ein Problem verursachen. Außerdem erhalten Sie weitere Informationen zu Richtlinien und Profilen, die auf den Geräten bereitgestellt werden.

> [!NOTE]
> Wenn eine Eigenschaft in der Baseline auf **Nicht konfiguriert** festgelegt ist, wird die Einstellung ignoriert, und keine Einschränkungen werden erzwungen. Die Eigenschaft wird nicht in Berichten angezeigt.

### <a name="per-category-view"></a>Kategorieansichten

Der Bereich „Übersicht“ umfasst ein kategoriebasiertes Diagramm für die Baseline; **Kategoriebasierter Status der Sicherheitsbaseline**.  Diese Ansicht enthält die einzelnen Baselinekategorien und den Anteil der Geräte (in Prozent), die diesen Kategorien zugeordnet werden können.

![Kategoriebasierte Statusansicht](./media/security-baselines-monitor/monitor-baseline-per-category.png)

Der Status für **Matches baseline** (Übereinstimmung mit Baseline) wird erst angezeigt, wenn 100 % der Geräte diesen Kategoriestatus aufweisen.

Sie können die Ansicht für die einzelnen Kategorien nach Spalten sortieren, indem Sie im oberen Bereich der Spalte auf die Pfeile nach unten bzw. nach oben klicken.

## <a name="monitor-the-profile"></a>Überwachen des Profils

Das Überwachen des Profils bietet Ihnen einen Einblick in den Bereitstellungsstatus Ihrer Geräte, aber nicht in den Sicherheitsstatus gemäß der Baselineempfehlungen.

1. Wählen Sie in Intune **Sicherheitsbaselines**, dann eine Baseline und dann **Erstellte Profile** aus.

2. Wählen Sie ein Profil aus. In **Übersicht** zeigt die Abbildung, wie vielen Geräten und Benutzern dieses Profil zugewiesen ist:

   ![Anzeige der Anzahl der Geräte und Benutzer, die dem Sicherheitsbaselineprofil zugewiesen sind](./media/security-baselines-monitor/existing-profile-overview.png)

3. Unter **Verwalten** > **Eigenschaften** wird eine Liste aller Einstellungen in der Baseline angezeigt. Sie können auch jede dieser Einstellungen ändern:

   ![Anzeigen und Aktualisieren von Einstellungen im Sicherheitsbaselineprofil](./media/security-baselines-monitor/manage-settings.png)

4. Unter **Überwachung** sehen Sie den Bereitstellungsstatus des Profils auf einzelnen Geräten, den Status für jeden Benutzer und den Status für jede Einstellung in der Baseline:

   ![Anzeigen der verschiedenen Überwachungsoptionen für ein Sicherheitsbaselineprofil](./media/security-baselines-monitor/monitor-status-options.png)

## <a name="view-endpoint-security-configurations-per-device"></a>Anzeigen der Endpunktsicherheitskonfigurationen pro Gerät

Sie können Details zu den Sicherheitskonfigurationen anzeigen, die für ein bestimmtes Gerät gelten. Dadurch können Sie gegebenenfalls Einstellungen identifizieren, die fehlerhaft konfiguriert wurden.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Navigieren Sie zu **Geräte**  >  **Alle Geräte**, und wählen Sie das Gerät aus, das Sie anzeigen möchten.

3. Klicken Sie in der Kategorie *Überwachen* auf **Endpoint security configuration** (Endpunktsicherheitskonfiguration), um die Liste der Sicherheitskonfigurationen anzuzeigen, die für das Gerät gelten.

4. Sie können auf eine Endpunktsicherheitskonfiguration klicken, um sie aufzuklappen und weitere Informationen zur Bewertung dieser Sicherheitskonfiguration auf dem Gerät anzuzeigen.

## <a name="troubleshoot-using-per-setting-status"></a>Problembehandlung bei der Verwendung von Status pro Einstellung

Sie haben eine Sicherheitsbaseline bereitgestellt, aber der Bereitstellungsstatus zeigt einen Fehler an. Die folgenden Schritte bieten Ihnen eine Anleitung zur Problembehandlung.

1. Wählen Sie in Intune **Sicherheitsbaselines**, dann eine Baseline und dann **Erstellte Profile** aus.

2. Wählen Sie ein Profil unter **Überwachung** > **Status pro Einstellung** aus.

3. Die Tabelle enthält alle Einstellungen und den Status jeder Einstellung. Wählen Sie die Spalte **Fehler** oder **Konflikt** aus, um die Einstellung anzuzeigen, die Ursache des Fehlers ist.

### <a name="mdm-diagnostic-information"></a>MDM-Diagnoseinformationen

Jetzt kennen Sie die problematische Einstellung. Der nächste Schritt ist, herauszufinden, warum diese Einstellung einen Fehler oder Konflikt verursacht.

Auf Windows 10-Geräten ist ein integrierter MDM-Diagnoseinformationsbericht verfügbar. Dieser Bericht enthält Standardwerte, aktuelle Werte, listet die Richtlinie auf, zeigt an, ob sie für das Gerät oder den Benutzer bereitgestellt wird, und vieles mehr. Verwenden Sie diesen Bericht, um zu ermitteln, warum die Einstellung einen Konflikt oder Fehler verursacht hat.

1. Navigieren Sie auf dem Gerät zu **Einstellungen** > **Konten** > **Zugriff auf Geschäfts-, Schul- oder Unikonto**.

2. Wählen Sie das Konto und dann **Informationen** > **Erweiterter Diagnosebericht** > **Bericht erstellen** aus.

3. Wählen Sie **Exportieren** aus, und öffnen Sie die generierte Datei.

4. Suchen Sie in den verschiedenen Abschnitten des Berichts nach der Fehler- oder Konflikteinstellung.

  Schauen Sie z.B. in den Abschnitt **Registrierte Konfigurationsquellen und Zielressourcen** oder **Nicht verwaltete Richtlinien**. So können Sie erfahren, warum der Fehler oder Konflikt verursacht wird.

[Diagnostizieren von MDM-Fehlern in Windows 10](https://docs.microsoft.com/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10) enthält weitere Informationen zu diesen integrierten Bericht.

> [!TIP]
>
> - Einige Einstellungen werden auch in der GUID aufgelistet. Sie können für diese GUID in der lokalen Registrierung (Regedit) nach festgelegten Werten suchen.
> - Die Protokolle der Ereignisanzeige können auch einige Fehlerinformationen zu der problematischen Einstellung enthalten (**Ereignisanzeige** > **Anwendungs- und Dienstprotokolle** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostics-Provider** > **Admin** ).

## <a name="next-steps"></a>Nächste Schritte

- [Informationen zu Sicherheitsbaselines](security-baselines.md)
- [Vermeiden von Konflikten](security-baselines.md#avoid-conflicts)
- [Überwachen von Geräteprofilen](../configuration/device-profile-monitor.md) 
- [Häufige Probleme und Lösungen](../configuration/device-profile-troubleshoot.md)
- [Richtlinien und Profile zur Problembehandlung in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)