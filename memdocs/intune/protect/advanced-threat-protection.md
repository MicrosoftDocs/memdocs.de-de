---
title: Verwenden von Microsoft Defender ATP in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Verwenden Sie Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) mit Intune, einschließlich Einrichtung und Konfiguration, Onboarding Ihrer Intune-Geräte mit ATP, und verwenden Sie dann eine ATP-Geräterisikobewertung mit Ihren Richtlinien für Intune-Gerätecompliance und bedingten Zugriff zum Schutz von Netzwerkressourcen.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: edc3bb23097a26753a9e54b0b520e6fc22be3a69
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2020
ms.locfileid: "80085197"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>Erzwingen der Konformität für Microsoft Defender ATP mit bedingtem Zugriff in Intune

Sie können Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) als Mobile Threat Defense-Lösung mit Microsoft Intune integrieren. Mit der Integration tragen Sie dazu bei, Sicherheitsverletzungen zu verhindern und deren Auswirkungen innerhalb einer Organisation zu begrenzen. Microsoft Defender ATP funktioniert mit Geräten, auf denen Windows 10 oder höher ausgeführt wird.

Um erfolgreich zu sein, verwenden Sie die folgenden Konfigurationen gemeinsam:

- **Richten Sie eine Dienst-zu-Dienst-Verbindung zwischen Intune und Microsoft Defender ATP ein**. Diese Verbindung ermöglicht Microsoft Defender ATP das Sammeln von Daten zu Computerrisiken von Windows 10-Geräten, die Sie mit Intune verwalten.
- **Verwenden Sie ein Gerätekonfigurationsprofil für das Onboarding von Geräten mit Microsoft Defender ATP**. Sie führen das Onboarding von Geräten durch, um sie für die Kommunikation mit Microsoft Defender ATP zu konfigurieren und Daten bereitzustellen, mit deren Hilfe Sie ihre Risikostufe bewerten können.
- **Verwenden Sie eine Gerätekonformitätsrichtlinie, um die Risikostufe festzulegen, die Sie zulassen möchten**. Risikostufen werden von Microsoft Defender ATP gemeldet. Geräte, die die zulässige Risikostufe überschreiten, werden als nicht konform eingestuft.
- **Verwenden Sie eine Richtlinie für bedingten Zugriff**, um den Zugriff von Benutzern auf Unternehmensressourcen mit nicht konformen Geräten zu blockieren.

Wenn Sie Intune mit Microsoft Defender ATP integrieren, können Sie die Bedrohungs- und Sicherheitsrisikenverwaltung von ATP (Thread & Vulnerability Management, TVM) nutzen und [Intune verwenden, um mittels TVM identifizierte Schwachstellen von Endpunkten zu beheben](atp-manage-vulnerabilities.md).

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>Beispiel für die Verwendung von Microsoft Defender ATP mit Intune

Im folgenden Beispiel wird erläutert, wie diese Lösungen zusammenarbeiten, um Ihre Organisation zu schützen. In diesem Beispiel sind Microsoft Defender ATP und Intune bereits integriert.

Stellen Sie sich vor, dass eine Person eine Word-Anlage mit eingebettetem bösartigem Code an einen Benutzer in Ihrer Organisation sendet.

- Der Benutzer öffnet die Anlage und aktiviert den Inhalt.
- Ein Angriff mit erhöhten Rechten beginnt, und ein Angreifer an einem Remotecomputer verfügt über Administratorrechte für das Gerät des Opfers.
- Der Angreifer greift dann remote auf die anderen Geräte des Benutzers zu. Diese Sicherheitsverletzung kann sich auf die gesamte Organisation auswirken.

Microsoft Defender ATP kann Sicherheitsereignisse wie dieses Szenario auflösen.

- In unserem Beispiel erkennt Microsoft Defender ATP, dass das Gerät nicht ordnungsgemäßen Code ausgeführt hat, seine Prozessrechte erhöht wurden, dass es bösartigen Code eingeschleust und eine verdächtige Remoteshell aufgerufen hat.
- Basierend auf diesen Aktionen des Geräts [klassifiziert Microsoft Defender ATP das Gerät als hochriskant](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity) und legt einen detaillierten Bericht über verdächtige Aktivitäten im Microsoft Defender Security Center-Portal ab.

Da Sie über eine Intune-Gerätekonformitätsrichtlinie verfügen, um Geräte mit der Risikostufe *Mittel* oder *Hoch* als nicht konform zu klassifizieren, wird das gefährdete Gerät als nicht konform klassifiziert. Diese Klassifizierung ermöglicht Ihrer Richtlinie für bedingten Zugriff, den Zugriff von diesem Gerät auf Ihre Unternehmensressourcen zu blockieren.

## <a name="prerequisites"></a>Voraussetzungen

Um Microsoft Defender ATP mit Intune zu verwenden, stellen Sie sicher, dass Sie Folgendes konfiguriert haben und verwenden können:

- Lizenzierter Mandant für Enterprise Mobility + Security E3 und Windows E5 (oder Microsoft 365 Enterprise E5)
- Microsoft Intune-Umgebung mit [Intune-verwalteten](../enrollment/windows-enroll.md) Windows 10-Geräten, die auch mit Azure AD verknüpft sind
- [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) und Zugriff auf das Microsoft Defender Security Center (ATP-Portal)

> [!NOTE]
> Microsoft Defender ATP wird für Intune-App-Schutzrichtlinien für iOS/iPadOS und Android nicht unterstützt.

## <a name="enable-microsoft-defender-atp-in-intune"></a>Aktivieren von Microsoft Defender ATP in Intune

Der erste Schritt ist das Einrichten einer Dienst-zu-Dienst-Verbindung zwischen Intune und Microsoft Defender ATP. Dies erfordert Administratorzugriff auf Microsoft Defender Security Center und Intune.

### <a name="to-enable-defender-atp"></a>Aktivieren von Defender ATP

Sie müssen Defender ATP nur einmal pro Mandant aktivieren.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Endpunktsicherheit** > **Microsoft Defender ATP** aus und dann **Microsoft Defender Security Center öffnen**.

   ![Wählen Sie die Option zum Öffnen von Microsoft Defender Security Center aus.](./media/advanced-threat-protection/atp-device-compliance-open-microsoft-defender.png)

4. In **Microsoft Defender Security Center**:
    1. Wählen Sie **Einstellungen** > **Erweiterte Features** aus.
    2. Wählen Sie für **Microsoft Intune-Verbindung** die Option **Ein** aus:

        ![Aktivieren der Verbindung mit Intune](./media/advanced-threat-protection/atp-security-center-intune-toggle.png)

    3. Wählen Sie **Voreinstellungen speichern** aus.

4. Kehren Sie im Microsoft Endpoint Manager Admin Center zu **Microsoft Defender ATP** zurück. Legen Sie unter **Einstellungen für MDM-Konformitätsrichtlinie** **Windows-Geräte mit Version 10.0.15063 und höher mit Microsoft Defender ATP verbinden** auf **Ein** fest.

5. Wählen Sie **Speichern** aus.

> [!TIP]
> Wenn Sie eine neue Anwendung in Intune Mobile Threat Defense integrieren und die Verbindung mit Intune aktivieren, erstellt Intune eine klassische Richtlinie für den bedingten Zugriff in Azure Active Directory. Jede MTD-App, die Sie integrieren (einschließlich [Defender ATP](advanced-threat-protection.md) oder jedes unserer zusätzlichen [MTD-Partner](mobile-threat-defense.md#mobile-threat-defense-partners)), erstellt eine neue klassische Richtlinie für bedingten Zugriff. Diese Richtlinien können ignoriert werden, dürfen jedoch nicht bearbeitet, gelöscht oder deaktiviert werden.
>
> Wenn die klassische Richtlinie gelöscht wird, müssen Sie die zur Erstellung dieser Richtlinie verantwortliche Verbindung mit Intune löschen und anschließend erneut einrichten. Auf diese Weise wird die klassische Richtlinie neu erstellt. Es wird keine Unterstützung für die Migration klassischer Richtlinien für MTD-Apps zum neuen Richtlinientyp für bedingten Zugriff bereitgestellt.
>
> Klassische bedingte Zugriffsrichtlinien für MTD-Apps:
>
> - Sie werden von Intune MTD verwendet und verlangen, dass Geräte in Azure AD registriert werden, damit sie eine Geräte-ID erhalten, bevor Kommunikation mit MTD-Partnern erfolgt. Die ID ist erforderlich, damit Geräte ihren Status erfolgreich an Intune melden können.
> - Sie haben keine Auswirkung auf andere Cloud-Apps oder Ressourcen.
> - Die Zugriffsrichtlinien unterscheiden sich von Richtlinien für bedingten Zugriff, die Sie möglicherweise erstellen, damit sie Ihnen bei der Verwaltung von MTD helfen.
> - Standardmäßig interagieren sie nicht mit anderen Richtlinien für den bedingten Zugriff, die Sie für die Auswertung verwenden.
>
> Wenn Sie klassische Richtlinien für den bedingten Zugriff in [Azure](https://portal.azure.com/#home) anzeigen möchten, wechseln Sie zu **Azure Active Directory** > **Bedingter Zugriff** > **Klassische Richtlinien**.

## <a name="onboard-devices-by-using-a-configuration-profile"></a>Onboarding von Geräten mithilfe eines Konfigurationsprofils durchführen

Nachdem Sie die Dienst-zu-Dienst-Verbindung zwischen Intune und Microsoft Defender ATP hergestellt haben, führen Sie das Onboarding Ihrer von Intune verwalteten Geräte in ATP durch, damit Daten über Ihre Risikostufe gesammelt und verwendet werden können. Verwenden Sie zum Onboarding der Geräte ein Gerätekonfigurationsprofil für Microsoft Defender ATP.

Wenn Sie die Verbindung mit Microsoft Defender ATP hergestellt haben, empfängt Intune ein Microsoft Defender ATP-Onboardingkonfigurationspaket von Microsoft Defender ATP. Dieses Paket wird auf Geräten mit dem Gerätekonfigurationsprofil bereitgestellt. Das Konfigurationspaket konfiguriert Geräte zur Kommunikation mit [Microsoft Defender ATP-Diensten](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection), um Dateien zu überprüfen, Bedrohungen zu erkennen und das Risiko an Microsoft Defender ATP zu melden. Nachdem Sie ein Gerät über das Konfigurationspaket integriert haben, müssen Sie dies nicht erneut tun. Sie können das Onboarding von Geräten auch mit einer [Gruppenrichtlinie oder Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints) durchführen.

### <a name="create-the-device-configuration-profile"></a>Erstellen des Gerätekonfigurationsprofils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Geben Sie einen **Namen** und eine **Beschreibung** ein.
4. Wählen Sie unter **Plattform** die Option **Windows 10 und höher** aus.
5. Wählen Sie für **Profiltyp** die Option **Microsoft Defender ATP (Windows 10 Desktop)** aus.
6. Konfigurieren Sie die Einstellungen:

   - **Pakettyp für die Microsoft Defender ATP-Clientkonfiguration**: Wählen Sie **Onboarding** aus, um das Konfigurationspaket zum Profil hinzuzufügen. Klicken Sie auf **Offboard** (Integration aufheben), um das Konfigurationspaket aus dem Profil zu entfernen.
  
     > [!NOTE]
     > Wenn Sie eine ordnungsgemäße Verbindung mit Microsoft Defender ATP hergestellt haben, führt Intune automatisch ein **Onboarding** für das Konfigurationsprofil für Sie durch, und die Einstellung **Pakettyp für die Microsoft Defender ATP-Clientkonfiguration** ist nicht verfügbar.
  
   - **Beispielfreigabe für alle Dateien**: Durch das **Aktivieren** dieser Option werden Stichproben erfasst und mit Microsoft Defender ATP geteilt. Wenn Sie z. B. eine verdächtige Datei sehen, können Sie sie zur gründlichen Analyse an Microsoft Defender ATP senden. Wenn **Nicht konfiguriert** festgelegt ist, werden keine Stichproben mit Microsoft Defender ATP geteilt.
   - **Häufigkeit von Telemetrieberichten erhöhen**: Bei Geräten mit hohem Risiko werden durch das **Aktivieren** dieser Option häufiger Telemetriedaten an den Microsoft Defender ATP-Dienst gemeldet.

     [Onboarding von Windows 10-Computern mit Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-sccm) enthält nähere Informationen zu diesen Microsoft Defender ATP-Einstellungen.

7. Wählen Sie **OK** und **Erstellen** aus, um Ihre Änderungen zu speichern, die das Profil erstellt.
8. [Weisen Sie das Gerätekonfigurationsprofil Geräten zu, die Sie mit Microsoft Defender ATP bewerten möchten.](../configuration/device-profile-assign.md)

## <a name="create-and-assign-the-compliance-policy"></a>Erstellen und Zuweisen der Konformitätsrichtlinie

Die Konformitätsrichtlinie bestimmt die Risikostufe, die Sie für ein Gerät als akzeptabel einstufen.

Wenn Sie mit dem Erstellen von Kompatibilitätsrichtlinien nicht vertraut sind, lesen Sie den Abschnitt [Erstellen der Richtlinie](../protect/create-compliance-policy.md#create-the-policy) im Artikel *Erstellen einer Konformitätsrichtlinie in Microsoft Intune*. Die folgenden Informationen beziehen sich speziell auf die Konfiguration von Defender ATP im Rahmen einer Konformitätsrichtlinie.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Konformitätsrichtlinien** > **Richtlinien** > **Richtlinie erstellen** aus.

3. Wählen Sie für **Plattform** *Windows 10 und höher* aus, und wählen Sie dann **Erstellen** aus, um das Konfigurationsfenster **Richtlinie erstellen** zu öffnen.

4. Geben Sie auf der Registerkarte **Grundlagen** einen **Namen** an, um die Richtlinie später identifizieren zu können. Sie können auch eine **Beschreibung** angeben.
  
5. Erweitern Sie auf der Registerkarte **Konformitätseinstellungen** die Gruppe **Microsoft Defender ATP**, und legen Sie für **Anfordern, dass das Gerät höchstens das angegebene Computerrisiko aufweist** die bevorzugte Stufe fest.

   Bedrohungsstufenklassifizierungen werden [von Microsoft Defender ATP bestimmt](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue).

   - **Löschen**: Diese Stufe ist die sicherste Einstellung. Solange auf einem Gerät Bedrohungen vorhanden sind, ist kein Zugriff auf Unternehmensressourcen möglich. Wenn Bedrohungen gefunden werden, wird das Gerät als nicht kompatibel bewertet. (Microsoft Defender ATP verwendet den Wert *Sicher*.)
   - **Niedrig:** Das Gerät ist konform, wenn nur Bedrohungen auf niedriger Stufe vorliegen. Geräte mit mittleren oder hohen Bedrohungsstufen sind nicht konform.
   - **Mittel**: Das Gerät ist konform, wenn auf dem Gerät Bedrohungen niedriger oder mittlerer Stufe gefunden werden. Wenn auf dem Gerät Bedrohungen hoher Stufen erkannt werden, wird es als nicht kompatibel bewertet.
   - **Hoch**: Dies ist die unsicherste Stufe, die alle Bedrohungsstufen zulässt. Also werden Geräte mit hohen, mittleren oder niedrigen Bedrohungsstufen als konform angesehen.

6. Vervollständigen Sie die Konfiguration der Richtlinie einschließlich der Zuweisung der Richtlinie zu den entsprechenden Gruppen.

## <a name="create-a-conditional-access-policy"></a>Erstellen einer Richtlinie für bedingten Zugriff

Die Richtlinie für bedingten Zugriff blockiert den Zugriff auf Ressourcen für Geräte, die die von Ihnen in der Konformitätsrichtlinie festgelegte Bedrohungsstufe überschreiten. Sie können den Zugriff des Geräts auf Unternehmensressourcen wie SharePoint oder Exchange Online blockieren.

> [!TIP]
> Der bedingte Zugriff ist eine Technologie von Azure Active Directory (Azure AD). Bei dem Knoten für bedingten Zugriff, auf den über das Microsoft Endpoint Manager Admin Center zugegriffen wird, handelt es sich um denselben Knoten, auf den aus *Azure AD* zugegriffen wird.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Endpunktsicherheit** > **Bedingter Zugriff** > **Neue Richtlinie** aus.

3. Geben Sie einen **Namen** für die Richtlinie ein, und wählen Sie **Benutzer und Gruppen** aus. Fügen Sie mit den Optionen „Einschließen“ oder „Ausschließen“ Ihre Gruppen für die Richtlinie hinzu, und wählen Sie **Fertig** aus.

4. Wählen Sie **Cloud-Apps** und die zu schützenden Apps aus. Wählen Sie z.B. **Apps auswählen** und **Office 365 SharePoint Online** sowie **Office 365 Exchange Online** aus.

   Wählen Sie **Fertig** aus, um die Änderungen zu speichern.

5. Wählen Sie **Bedingungen** > **Client-Apps** aus, um die Richtlinie auf Apps und Browser anzuwenden. Wählen Sie z.B. **Ja** aus, und aktivieren Sie dann **Browser** sowie **Mobile Apps und Desktopclients**.

   Wählen Sie **Fertig** aus, um die Änderungen zu speichern.

6. Wählen Sie **Gewähren** aus, um den bedingten Zugriff basierend auf der Gerätekonformität anzuwenden. Wählen Sie z.B. **Zugriff gewähren** > **Markieren des Geräts als kompatibel erforderlich** aus.

    Wählen Sie **OK** aus, um die Änderungen zu speichern.

7. Wählen Sie **Richtlinie aktivieren** und dann **Erstellen** zum Speichern der Änderungen aus.

## <a name="monitor-device-compliance"></a>Überwachen der Gerätekonformität

Überwachen Sie als Nächstes den Status von Geräten, auf die die Microsoft Defender ATP-Konformitätsrichtlinie angewandt wird.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Überwachen** > **Richtlinienkonformität** aus.

3. Suchen Sie Ihre Microsoft Defender ATP-Richtlinie in der Liste, und sehen Sie, welche Geräte konform bzw. nicht konform sind.

Sie können für nicht konforme Geräte am gleichen Speicherort auch die Option für einen *operational report* (Betriebsbericht) verwenden:

1. Klicken Sie auf **Geräte** > **Überwachen** > **Noncompliant devices** (Nicht konforme Geräte).

Weitere Informationen zu Berichten finden Sie unter [Intune-Berichte](../fundamentals/reports.md).

## <a name="view-onboarding-status"></a>Anzeigen des Onboardingstatus

Um den Onboardingstatus aller von Intune verwalteten Windows 10-Geräte anzuzeigen, wechseln Sie zu **Gerätekompatibilität** > **Microsoft Defender ATP**. Auf dieser Seite können Sie auch die Erstellung eines Gerätekonfigurationsprofils für das Onboarding mehrerer Geräte in Microsoft Defender ATP initiieren.

## <a name="next-steps"></a>Nächste Schritte

[Microsoft Defender ATP – bedingter Zugriff](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)

[Microsoft Defender ATP – Risikodashboard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)

[Verwenden von Intune zum Korrigieren von mit Microsoft Defender ATP identifizierten Sicherheitsrisiken](atp-manage-vulnerabilities.md).

[Erste Schritte mit den Gerätekonformitätsrichtlinien in Intune](device-compliance-get-started.md)
