---
title: 'Überwachen der Gerätekonformitätsrichtlinien in Microsoft Intune: Azure | Microsoft-Dokumentation'
description: Verwenden Sie das Dashboard für die Gerätekonformität, um die Konformität der Geräte insgesamt zu überwachen, Berichte anzuzeigen sowie die Gerätekonformität pro Richtlinie und pro Einstellung anzuzeigen.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/18/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6a2dbd43ff5a8048286693dbfb417d6bb720a877
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79353033"
---
# <a name="monitor-intune-device-compliance-policies"></a>Überwachen von Intune-Richtlinien zur Gerätekompatibilität

Konformitätsberichte erleichtern das Überprüfen der Gerätekonformität und das Beheben von Problemen mit der Konformität in Ihrem Unternehmen. Diese Berichte verschaffen Ihnen folgende Informationen:

- Der gesamte Konformitätszustand der Geräte
- Der Konformitätszustand einer individuellen Einstellung
- Der Konformitätszustand einer individuellen Richtlinie
- Detailinformationen zu einzelnen Geräten, um spezifische Einstellungen und Richtlinien anzuzeigen, die das Gerät betreffen.

## <a name="open-the-compliance-dashboard"></a>Öffnen des Konformitätsdashboards

Öffnen Sie das **Intune-Gerätekonformitätsdashboard**:

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Übersicht** > **Konformitätsstatus** (Registerkarte) aus.

> [!IMPORTANT]
> Geräte müssen in Intune registriert werden, um Gerätekompatibilitätsrichtlinien empfangen zu können.

## <a name="dashboard-overview"></a>Dashboard-Übersicht

Wenn das Dashboard geöffnet wird, erhalten Sie eine Übersicht mit allen Konformitätsberichten. In den Berichten finden Sie folgende Informationen:

- Gerätekonformität im Überblick
- Richtlinienspezifische Gerätekompatibilität
- Einstellungsspezifische Gerätekompatibilität
- Status des Bedrohungs-Agents
- Geräteschutzstatus

![Bild vom Dashboard, das das Gerätekonformitätsdashboard und verschiedene Berichte anzeigt](./media/compliance-policy-monitor/idc-1.png)

Wenn Sie sich diese Berichterstattung genauer ansehen, sehen Sie auch spezifische Konformitätsrichtlinien und -Einstellungen, die für ein spezifisches Gerät gelten, einschließlich des Konformitätszustands für jede Einstellung.

### <a name="device-compliance-status"></a>Gerätekonformitätsstatus

Das Diagramm **Gerätekonformitätszustand** veranschaulicht die Konformitätszustände für alle in Intune registrierten Geräte. Die Gerätekonformitätszustände werden in zwei verschiedenen Datenbanken gespeichert: Intune und Azure Active Directory.

> [!IMPORTANT]
> Intune folgt bei allen Konformitätsauswertungen auf dem Gerät dem Zeitplan für das Einchecken von Geräten. [Weitere Informationen zum Zeitplan für das Einchecken von Geräten](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)

Beschreibungen der verschiedenen Zustände der Gerätekonformitätsrichtlinie:

- **Konform**: Das Gerät hat mindestens eine Einstellung einer Gerätekonformitätsrichtlinie erfolgreich angewendet.

- **In Toleranzperiode**: Mindestens eine Einstellung der Gerätekompatibilitätsrichtlinie gilt für das Gerät. Jedoch hat der Benutzer die Richtlinien noch nicht angewandt. Das bedeutet, dass das Gerät nicht konform ist, sich jedoch in der vom Administrator festgelegten Toleranzperiode befindet.

  - Erfahren Sie mehr über [Aktionen für nicht konforme Geräte](actions-for-noncompliance.md).

- **Nicht ausgewertet**: Ein anfänglicher Zustand für neu registrierte Geräte. Für diesen Zustand können auch folgende Gründe vorliegen:

  - Geräte, denen keine Konformitätsrichtlinie zugewiesen wurde und die keinen Auslöser für die Überprüfung auf Konformität besitzen
  - Geräte, die seit der letzten Aktualisierung der Konformitätsrichtlinie nicht eingecheckt wurden
  - Geräte, die keinem bestimmten Benutzer zugeordnet sind, z. B.:
    - Über das Programm zur Geräteregistrierung von Apple erworbene iOS/iPadOS-Geräte ohne Benutzeraffinität
    - Dedizierte Android Kiosk- oder Android Enterprise-Geräte
  - Geräte, die bei einem Geräteregistrierungs-Manager-Konto registriert sind

- **Nicht konform**: Das Gerät konnte keine Einstellungen einer Gerätekompatibilitätsrichtlinie anwenden. Oder der Benutzer hat die Richtlinien nicht eingehalten.

- **Gerät nicht synchronisiert**: Das Gerät konnte den Status der Gerätekonformitätsrichtlinie nicht melden. Mögliche Ursachen:

  - **Unbekannt**: Das Gerät ist offline oder konnte aus einem anderen Grund nicht mit Intune oder Azure AD kommunizieren.

  - **Fehler**: Das Gerät konnte nicht mit Intune und Azure AD kommunizieren und hat eine Fehlermeldung mit der Ursache erhalten.

> [!IMPORTANT]
> In Intune registrierte Geräte, für die keine Gerätekonformitätsrichtlinien festgelegt sind, werden in diesem Bericht der Kategorie **Konform** zugeordnet.

#### <a name="drill-down-for-more-details"></a>Ausführen eines Drilldowns für weitere Details

Wählen Sie einen Zustand im Diagramm **Gerätekonformitätszustand** aus. Wählen Sie beispielsweise den Zustand **Nicht konform** aus:

![Auswahl des Zustands „Nicht konform“](./media/compliance-policy-monitor/select-not-compliant-status.png)

Durch diese Aktion wird das Fenster **Gerätekonformität** geöffnet, in dem Geräte in einem Diagramm zum **Gerätezustand** angezeigt werden. Dieses Diagramm zeigt weitere Details zu den Geräten mit diesem Zustand an, einschließlich Betriebssystemplattform, letztes Check-In-Datum und mehr.
![Bild vom Dashboard mit weiteren Details zum Gerät mit diesem spezifischen Zustand](./media/compliance-policy-monitor/drill-down-details.png)

Wenn Sie alle Geräte im Besitz eines spezifischen Benutzers anzeigen möchten, können Sie außerdem das Berichtsdiagramm filtern, indem Sie die E-Mail-Adresse des Benutzers eingeben:

#### <a name="filter-and-columns"></a>Filter und Spalten

![Schaltflächen „Filtern“ und „Spalten“ zum Ändern der Ergebnisse im Diagramm](./media/compliance-policy-monitor/filter-columns.png)

Wenn Sie auf die Schaltfläche **Filtern** klicken, wird das Filterflyout mit weiteren Optionen geöffnet, einschließlich des **Konformitätszustands**, Geräten mit **Jailbreak** und mehr. **Wenden Sie den Filter an**, um die Ergebnisse zu aktualisieren.

Verwenden Sie die Eigenschaft **Spalten**, um Spalten in die Diagrammausgabe hinzuzufügen oder daraus zu entfernen. Beispielsweise kann ein **Benutzerprinzipalname** die auf dem Gerät registrierte E-Mail-Adresse anzeigen. **Wenden Sie die Spalten an**, um die Ergebnisse zu aktualisieren.

#### <a name="device-details"></a>Gerätedetails

Wählen Sie ein spezifisches Gerät im Diagramm **Gerätedetails** aus, und klicken Sie dann auf **Gerätekonformität**:

![Auswählen eines spezifischen Geräts und anschließendes Klicken auf „Gerätekonformität“, um die angewendeten Gerätekonformitätsrichtlinien anzuzeigen](./media/compliance-policy-monitor/see-policies-applied-specific-device.png)

Intune zeigt weitere Details zu angewendeten Einstellungen der Gerätekonformitätsrichtlinien für das Gerät an. Wenn Sie eine spezifische Richtlinie auswählen, werden alle Einstellungen in der Richtlinie angezeigt.

### <a name="devices-without-compliance"></a>Nicht konforme Geräte

Auf der Seite *Konformitätszustand* können Sie neben dem Diagramm *Richtlinienkonformität* die Kachel **Geräte ohne Konformitätsrichtlinie** auswählen, um Informationen zu Geräten anzuzeigen, denen keine Konformitätsrichtlinien zugewiesen sind:

![Anzeigen von Geräten ohne Konformitätsrichtlinien](./media/compliance-policy-monitor/devices-without-policies.png)

Wenn Sie die Kachel auswählen, werden alle Geräte ohne Konformitätsrichtlinien angezeigt. Außerdem wird der Benutzer des Geräts, der Richtlinienbereitstellungszustand und das Gerätemodell angezeigt.

#### <a name="what-you-need-to-know"></a>Was Sie wissen müssen

- Es ist wichtig, Geräte ohne Konformitätsrichtlinie mit der Sicherheitseinstellung **Markieren Sie Geräte ohne zugewiesene Konformitätsrichtlinie als** zu identifizieren. Sie können diesen dann mindestens eine Konformitätsrichtlinie zuweisen.

  Die Sicherheitseinstellung kann im Intune-Portal konfiguriert werden. Gehen Sie zu **Geräte** > **Konformitätsrichtlinien** > **Einstellungen für Konformitätsrichtlinien**. Legen Sie dann **Markieren Sie Geräte ohne zugewiesene Konformitätsrichtlinie als** auf **Konform** oder **Nicht konform** fest.

  Erfahren Sie mehr über diese [Sicherheitsverbesserung im Intune-Dienst](https://blogs.technet.microsoft.com/intunesupport/2018/02/09/updated-upcoming-security-enhancements-in-the-intune-service/).

- Benutzer, denen eine beliebige Konformitätsrichtlinie zugewiesen ist, werden unabhängig von der Geräteplattform nicht im Bericht angezeigt. Wenn Sie beispielsweise eine Windows-Konformitätsrichtlinie einem Benutzer mit einem Android-Gerät zugewiesen haben, wird das Gerät nicht im Bericht angezeigt. Das Android-Gerät wird von Intune jedoch als nicht konform angesehen. Es wird empfohlen, Richtlinien für jede Geräteplattform zu erstellen und diese für alle Benutzer bereitzustellen, um Probleme zu vermeiden.

### <a name="per-policy-device-compliance"></a>Richtlinienspezifische Gerätekompatibilität

Im Diagramm **Richtlinienkonformität** werden Ihnen die Richtlinien und die Anzahl konformer und nicht konformer Geräte angezeigt.

![Anzeigen einer Liste von Richtlinien und der Anzahl konformer und nicht konformer Geräte für die jeweilige Richtlinie](./media/compliance-policy-monitor/idc-8.png)

### <a name="setting-compliance"></a>Einstellungskonformität

Im Diagramm **Einstellungskonformität** werden alle Einstellungen von allen Konformitätsrichtlinien, die Plattform, auf der die Richtlinieneinstellungen angewandt werden, und die Anzahl nicht konformer Geräte angezeigt.

![Eine Liste mit allen Einstellungen in den verschiedenen Richtlinien](./media/compliance-policy-monitor/idc-10.png)

## <a name="view-compliance-reports"></a>Anzeigen von Konformitätsberichten

Zusätzlich zur Verwendung der Diagramme auf der Registerkarte *Konformitätsstatus* können Sie zu **Berichte** > **Gerätekonformität** wechseln.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Klicken Sie erst auf **Geräte** > **Überwachen** und anschließend unter **Konformität** auf den Bericht, den Sie abrufen möchten. Unter anderem haben Sie Zugriff auf die folgenden Konformitätsberichte:

   - Gerätekonformität
   - Nicht konforme Geräte
   - Geräte ohne Konformitätsrichtlinie
   - Einstellungskonformität
   - Richtlinienkonformität
   - Windows-Integritätsnachweisbericht
   - Status des Bedrohungs-Agents

Weitere Informationen zu Berichten finden Sie unter [Intune-Berichte](../fundamentals/reports.md).

## <a name="view-status-of-device-policies"></a>Anzeigen des Status von Geräterichtlinien

Sie können die unterschiedlichen Status Ihrer Richtlinien nach Plattform überprüfen. Sie besitzen z.B. eine macOS-Konformitätsrichtlinie, und Sie möchten die Geräte anzeigen, die von dieser Richtlinie betroffen sind, und wissen, ob Konflikte oder Fehler vorhanden sind.

Dieses Feature ist im Gerätestatusbericht enthalten:

1. Wählen Sie **Geräte** > **Konformitätrichtlinien** > **Richtlinien** aus. Ihnen wird eine Liste mit Richtlinien angezeigt, einschließlich der Plattform (falls die Richtlinie zugewiesen ist) usw.
2. Wählen Sie eine Richtlinie aus, und klicken Sie dann auf **Übersicht**. In dieser Ansicht enthält die Richtlinienzuweisung die folgenden Status:

    - **Erfolgreich**: Die Richtlinie wurde angewendet.
    - **Fehler**: Die Richtlinie kann nicht angewendet werden. Diese Meldung wird in der Regel mit einem Fehlercode angezeigt, der auf eine Erklärung verweist.
    - **Konflikt:** Zwei Einstellungen werden auf dasselbe Gerät angewendet, und Intune kann den Konflikt nicht lösen. Ein Administrator sollte das überprüfen.
    - **Ausstehend:** Das Gerät hat sich noch nicht bei Intune eingecheckt, damit die Richtlinie angewendet werden kann.
    - **Nicht zutreffend**: Die Richtlinie kann nicht auf das Gerät angewendet werden. Beispielsweise aktualisiert die Richtlinie eine Einstellung für iOS 11.1, das Gerät verwendet jedoch iOS 10.

3. Um die Details auf dem Gerät mithilfe der Richtlinie anzuzeigen, wählen Sie einen Status aus, z.B. **Succeeded** (erfolgreich). Im nächsten Fenster werden die spezifischen Gerätedetails, einschließlich des Gerätenamens und des Bereitstellungsstatus, aufgeführt.

## <a name="how-intune-resolves-policy-conflicts"></a>Wie Intune-Richtlinienkonflikte löst

Richtlinienkonflikte können auftreten, wenn mehrere Intune-Richtlinien auf ein Gerät angewendet werden. Wenn sich Richtlinieneinstellungen überschneiden, löst Intune Konflikte nach den folgenden Regeln:

- Wenn die in Konflikt stehenden Einstellungen zu einer Intune-Konfigurationsrichtlinie und einer Kompatibilitätsrichtlinie gehören, haben die Einstellungen in der Kompatibilitätsrichtlinie Vorrang vor den Einstellungen in der Konfigurationsrichtlinie. Dies geschieht auch, wenn die Einstellungen in der Konfigurationsrichtlinie sicherer sind.

- Wenn Sie mehrere Kompatibilitätsrichtlinien bereitgestellt haben, verwendet Intune die sichersten dieser Richtlinien.

## <a name="next-steps"></a>Nächste Schritte

[Konformitätsrichtlinien – Übersicht](device-compliance-get-started.md)
